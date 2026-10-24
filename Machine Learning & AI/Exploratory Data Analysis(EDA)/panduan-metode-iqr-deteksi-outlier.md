# Panduan Metode IQR untuk Mendeteksi Outlier

> **Nama file:** `panduan-metode-iqr-deteksi-outlier.md`  
> **Topik:** Data Profiling & Exploratory Data Analysis (EDA)

---

## 📌 1. Apa Itu IQR?

**Interquartile Range (IQR)** adalah ukuran sebaran data yang menunjukkan rentang 50% data di bagian tengah distribusi. IQR digunakan dalam metode IQR untuk membantu menandai nilai yang berpotensi menjadi *outlier*.

IQR dihitung dari selisih kuartil ketiga (`Q3`) dan kuartil pertama (`Q1`).

```math
IQR = Q_3 - Q_1
```

- **Q1 (kuartil pertama):** persentil ke-25 (`25%` pada `describe()`).
- **Q2 (median):** persentil ke-50 (`50%` pada `describe()`).
- **Q3 (kuartil ketiga):** persentil ke-75 (`75%` pada `describe()`).

> [!NOTE]
> `Q1` dan `Q3` bukanlah batas outlier. Keduanya dipakai untuk menghitung IQR, yang kemudian digunakan untuk menentukan batas bawah dan batas atas.

---

## 🧮 2. Rumus Batas Outlier

### Batas bawah (*Lower Fence*)

```math
\\text{Lower Fence} = Q_1 - 1.5 \\times IQR
```

### Batas atas (*Upper Fence*)

```math
\\text{Upper Fence} = Q_3 + 1.5 \\times IQR
```

Faktor `1.5` merupakan aturan praktis yang umum digunakan pada metode IQR untuk menandai nilai yang jauh dari rentang tengah data.

### Kriteria klasifikasi

| Kondisi nilai data | Interpretasi menurut IQR |
|---|---|
| Nilai `< Lower Fence` | Outlier bawah |
| Nilai `> Upper Fence` | Outlier atas |
| Nilai berada di antara kedua batas, termasuk tepat pada batas | Bukan outlier menurut aturan IQR |

**Penting:** outlier bawah dan outlier atas diperiksa secara terpisah. Sebuah dataset bisa memiliki salah satunya saja, keduanya, atau tidak satu pun.

---

## 🔎 3. Contoh Membaca `describe()`

Misalkan hasil `df["kolom"].describe()` adalah:

| Statistik | Nilai |
|---|---:|
| `min` | 10 |
| `25%` (`Q1`) | 20 |
| `50%` (median) | 30 |
| `75%` (`Q3`) | 40 |
| `max` | 65 |

### Langkah 1 — Hitung IQR

```math
IQR = Q_3 - Q_1 = 40 - 20 = 20
```

### Langkah 2 — Hitung batas bawah

```math
\\text{Lower Fence} = 20 - (1.5 \\times 20) = -10
```

### Langkah 3 — Hitung batas atas

```math
\\text{Upper Fence} = 40 + (1.5 \\times 20) = 70
```

### Langkah 4 — Bandingkan `min` dan `max` dengan batas

- `min = 10`, sedangkan `Lower Fence = -10`. Karena `10 > -10`, tidak ada indikasi outlier bawah dari nilai minimum tersebut.
- `max = 65`, sedangkan `Upper Fence = 70`. Karena `65 < 70`, tidak ada indikasi outlier atas dari nilai maksimum tersebut.

**Kesimpulan:** berdasarkan `min` dan `max` pada contoh ini, tidak ditemukan outlier menurut aturan IQR.

> [!TIP]
> Untuk memeriksa apakah ada outlier, bandingkan nilai minimum dan maksimum dengan kedua *fence*. Jangan membandingkan `min` hanya dengan `Q1` atau `max` hanya dengan `Q3`.

---

## ⚠️ 4. Kesalahan Interpretasi yang Perlu Dihindari

| Pernyataan | Benar atau salah? | Penjelasan |
|---|---|---|
| Jika `min < Q1`, berarti `min` adalah outlier. | ❌ Salah | Nilai minimum biasanya bisa lebih kecil daripada Q1. Periksa apakah `min < Lower Fence`. |
| Jika `min >= Q1`, berarti tidak ada outlier bawah. | ❌ Salah | Pemeriksaan tetap berdasarkan Lower Fence, bukan Q1. |
| Jika `max > Q3`, berarti `max` adalah outlier. | ❌ Salah | Nilai maksimum biasanya bisa lebih besar daripada Q3. Periksa apakah `max > Upper Fence`. |
| Jika `max <= Q3`, berarti tidak ada outlier atas. | ❌ Salah | Pemeriksaan tetap berdasarkan Upper Fence, bukan Q3. |
| Jika semua nilai berada di antara kedua fence, tidak ada outlier menurut aturan IQR. | ✅ Benar | Inilah kriteria yang digunakan metode IQR. |

### Inti pemahaman

- `Q1` dan `Q3` adalah **kuartil**, bukan batas outlier.
- `Lower Fence` dan `Upper Fence` adalah **batas untuk menandai outlier**.
- Nilai di luar salah satu fence ditandai sebagai outlier menurut aturan IQR.

---

## ↔️ 5. Contoh: Hanya Ada Outlier Atas

Misalkan:

- `Lower Fence = 10`
- `Upper Fence = 50`
- `min = 15`
- `max = 80`

Interpretasi:

- **Outlier bawah:** tidak ada, karena `15 > 10`.
- **Outlier atas:** ada, karena `80 > 50`.

Jadi, tidak wajib ada outlier bawah dan atas secara bersamaan.

---

## 🧠 6. Latihan Pemahaman

Diketahui:

- `Q1 = 20`
- `Q3 = 40`
- `Lower Fence = -10`
- `Upper Fence = 70`
- `min = 5`
- `max = 75`

Kesimpulan mana yang paling tepat?

1. Tidak ada outlier karena nilai minimum lebih besar daripada Q1.
2. Hanya ada outlier bawah karena nilai minimum lebih kecil daripada Q1.
3. Ada outlier atas, tetapi tidak ada outlier bawah.
4. Ada outlier bawah dan outlier atas.

<details>
<summary><strong>Lihat jawaban dan penjelasan</strong></summary>

**Jawaban: 3. Ada outlier atas, tetapi tidak ada outlier bawah.**

- Nilai minimum `5` lebih besar daripada Lower Fence `-10`, sehingga bukan outlier bawah.
- Nilai maksimum `75` lebih besar daripada Upper Fence `70`, sehingga merupakan outlier atas.

</details>

---

## 🧪 7. Contoh Implementasi dengan Pandas

```python
Q1 = df["kolom"].quantile(0.25)
Q3 = df["kolom"].quantile(0.75)

IQR = Q3 - Q1

lower_fence = Q1 - 1.5 * IQR
upper_fence = Q3 + 1.5 * IQR

outlier_mask = (
    (df["kolom"] < lower_fence) |
    (df["kolom"] > upper_fence)
)

outliers = df.loc[outlier_mask, "kolom"]

print("Q1:", Q1)
print("Q3:", Q3)
print("IQR:", IQR)
print("Lower Fence:", lower_fence)
print("Upper Fence:", upper_fence)
print("Jumlah outlier:", outlier_mask.sum())
print(outliers)
```

**Catatan:** sesuaikan `"kolom"` dengan nama kolom numerik yang sedang dianalisis. Jika kolom memiliki nilai kosong (`NaN`), periksa juga penanganan nilai kosong pada tahap profiling.

---

## 🎯 8. Outlier Tidak Selalu Berarti Data Salah

IQR menandai nilai yang berada di luar batas statistik. Namun, **nilai yang ditandai sebagai outlier tidak otomatis harus dihapus**.

Selidiki konteksnya terlebih dahulu:

- **Kesalahan pencatatan atau pengukuran:** perbaiki jika nilai yang benar dapat diketahui; jika tidak, tentukan penanganannya dengan alasan yang jelas.
- **Nilai ekstrem tetapi valid:** pertahankan jika memang mencerminkan kejadian nyata.
- **Nilai yang penting untuk prediksi:** pertimbangkan dampaknya terhadap model sebelum menghapus atau mengubahnya.

IQR adalah metode deteksi awal, bukan keputusan otomatis untuk menghapus data.

---

## ✅ Ringkasan

1. Hitung `IQR = Q3 - Q1`.
2. Hitung `Lower Fence = Q1 - 1.5 × IQR`.
3. Hitung `Upper Fence = Q3 + 1.5 × IQR`.
4. Nilai di bawah Lower Fence ditandai sebagai outlier bawah.
5. Nilai di atas Upper Fence ditandai sebagai outlier atas.
6. Jangan menentukan outlier hanya dengan membandingkan `min` terhadap Q1 atau `max` terhadap Q3.
7. Selidiki konteks data sebelum memutuskan untuk menghapus atau mengubah outlier.
