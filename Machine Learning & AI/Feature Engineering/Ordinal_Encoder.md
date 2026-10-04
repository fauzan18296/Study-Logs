# 📌 OrdinalEncoder: Perbedaan `unknown_value=-1` dan `unknown_value=np.nan`

Saat menggunakan **OrdinalEncoder**, terkadang muncul kategori baru saat proses `transform()` yang belum pernah dilihat saat `fit()`.

Contoh:

```python
from sklearn.preprocessing import OrdinalEncoder

encoder = OrdinalEncoder(
    handle_unknown="use_encoded_value",
    unknown_value=-1
)
```

Data saat `fit()`:

```text
Merah → 0
Biru  → 1
Hijau → 2
```

Saat `transform()`:

```text
Kuning
```

Karena `"Kuning"` belum pernah muncul saat `fit()`, maka encoder akan menggunakan nilai yang ditentukan pada `unknown_value`.

---

# 🔹 Opsi 1: Menggunakan `unknown_value=-1`

```python
OrdinalEncoder(
    handle_unknown="use_encoded_value",
    unknown_value=-1
)
```

Hasil:

```text
Merah  → 0
Biru   → 1
Hijau  → 2
Kuning → -1
```

## ✅ Kelebihan

* Tetap bertipe **integer**.
* Lebih hemat memori dibanding float.
* Sederhana dan mudah dipahami.
* Cocok untuk banyak model berbasis tree:

  * Decision Tree
  * Random Forest
  * XGBoost
  * LightGBM

## ⚠️ Kekurangan

Model dapat menganggap `-1` sebagai nilai numerik yang valid.

```text
-1 < 0 < 1 < 2
```

Padahal secara konsep:

```text
Kuning (Unknown)
≠
Kategori yang lebih kecil dari Merah
```

Dengan kata lain, `-1` adalah **angka sungguhan**, bukan penanda missing value.

---

# 🔹 Opsi 2: Menggunakan `unknown_value=np.nan`

```python
import numpy as np

OrdinalEncoder(
    handle_unknown="use_encoded_value",
    unknown_value=np.nan,
    dtype=float
)
```

Hasil:

```text
Merah  → 0.0
Biru   → 1.0
Hijau  → 2.0
Kuning → NaN
```

## ✅ Kelebihan

Lebih merepresentasikan kondisi sebenarnya:

```text
"Saya tidak tahu kategori ini"
```

daripada:

```text
"Kategori ini bernilai -1"
```

Secara statistik dan semantik, `NaN` lebih cocok untuk menandai:

* Missing Value
* Unknown Category
* Data Tidak Tersedia

---

## ⚠️ Kekurangan

Tidak semua algoritma bisa menangani `NaN`.

Contoh:

❌ Logistic Regression

❌ SVM

❌ KNN

Biasanya perlu preprocessing tambahan:

```python
from sklearn.impute import SimpleImputer
```

---

# 🤔 Kenapa `np.nan` Harus Bertipe Float?

Karena `NaN` merupakan bagian dari standar **IEEE Floating Point**.

Contoh:

```python
import numpy as np

x = np.array([1, 2, np.nan])

print(x.dtype)
```

Output:

```text
float64
```

Jika menggunakan integer:

```python
np.array([1, 2, np.nan], dtype=int)
```

akan menghasilkan error.

Karena tipe integer tidak memiliki representasi khusus untuk `NaN`.

---

# 🔍 Perbedaan Konseptual Penting

## `-1` adalah Nilai

```python
-1 == -1
```

Output:

```python
True
```

Artinya:

```text
-1 adalah angka yang valid
```

---

## `NaN` Bukan Nilai

```python
import numpy as np

np.nan == np.nan
```

Output:

```python
False
```

Artinya:

```text
NaN bukan nilai sebenarnya

NaN = informasi tidak diketahui
```

Inilah alasan banyak library data science memperlakukan `NaN` secara khusus.

---

# 📊 Ringkasan Perbandingan

| Aspek                                 | `-1`           | `np.nan`       |
| ------------------------------------- | -------------- | -------------- |
| Tipe Data                             | Integer        | Float          |
| Hemat Memori                          | ✅ Ya           | ❌ Tidak        |
| Merepresentasikan Missing Value       | ❌ Tidak        | ✅ Ya           |
| Dianggap Nilai Numerik oleh Model     | ✅ Ya           | ❌ Tidak        |
| Perlu `dtype=float`                   | ❌ Tidak        | ✅ Ya           |
| Cocok untuk Tree-Based Model          | ✅ Sangat Cocok | ✅ Bisa         |
| Cocok untuk Menandai Unknown Category | ⚠️ Cukup       | ✅ Sangat Cocok |

---

# 🎯 Kapan Menggunakan `-1`?

Gunakan jika:

* Ingin output tetap integer.
* Tidak ingin ada missing value.
* Menggunakan model berbasis tree.
* Mengutamakan kesederhanaan pipeline.

```python
OrdinalEncoder(
    handle_unknown="use_encoded_value",
    unknown_value=-1
)
```

---

# 🎯 Kapan Menggunakan `np.nan`?

Gunakan jika:

* Ingin membedakan secara jelas antara kategori valid dan kategori tidak dikenal.
* Akan melakukan imputasi setelah encoding.
* Menggunakan pipeline yang memang mendukung missing value.

```python
OrdinalEncoder(
    handle_unknown="use_encoded_value",
    unknown_value=np.nan,
    dtype=float
)
```

---

# 💡 Intuisi Sederhana

Bayangkan ada kategori warna:

```text
Merah
Biru
Hijau
```

Lalu muncul:

```text
Kuning
```

### Jika menggunakan `-1`

```text
Merah  = 0
Biru   = 1
Hijau  = 2
Kuning = -1
```

Artinya:

> "Saya memberi nomor khusus untuk kategori yang tidak dikenal."

---

### Jika menggunakan `np.nan`

```text
Merah  = 0
Biru   = 1
Hijau  = 2
Kuning = NaN
```

Artinya:

> "Saya tidak tahu kategori ini."

Perbedaan inilah yang menjadi alasan utama memilih antara `-1` dan `np.nan`.
