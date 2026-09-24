# 📊 Preprocessing DataFrame: Encoding, Scaling, dan Train-Test Split

> Panduan ringkas untuk memahami bagaimana DataFrame dipersiapkan sebelum dimasukkan ke algoritma Machine Learning.

---

## 🧭 Daftar Isi

* [1. Memahami X dan y](#1-memahami-x-dan-y)
* [2. Train-Test Split](#2-train-test-split)
* [3. StandardScaler](#3-standardscaler)
* [4. fit, transform, dan fit_transform](#4-fit-transform-dan-fit_transform)
* [5. Scaling pada DataFrame yang Sudah Di-Encode](#5-scaling-pada-dataframe-yang-sudah-di-encode)
* [6. Performance Index sebagai Target](#6-performance-index-sebagai-target)
* [7. Alur Lengkap](#7-alur-lengkap)
* [8. Contoh Kode Lengkap](#8-contoh-kode-lengkap)
* [9. Hal yang Perlu Diingat](#9-hal-yang-perlu-diingat)
* [10. Ringkasan Konsep](#10-ringkasan-konsep)

---

# 1. 🧩 Memahami `X` dan `y`

Misalkan dataset memiliki kolom:

```text
Hours Studied
Previous Scores
Sleep Hours
Extracurricular Activities
Performance Index
```

Jika **`Performance Index` adalah nilai yang ingin diprediksi**, maka:

* `X` → fitur/input
* `y` → target/output

Gunakan:

```python
X = df.drop("Performance Index", axis=1)
y = df["Performance Index"]
```

Secara konsep:

```text
X
│
├── Hours Studied
├── Previous Scores
├── Sleep Hours
└── Extracurricular Activities
          │
          ▼
       Model ML
          │
          ▼
y = Performance Index
```

### 🔑 Intinya

> **X = informasi yang digunakan model untuk melakukan prediksi.**

> **y = nilai yang ingin diprediksi oleh model.**

---

# 2. ✂️ Train-Test Split

Setelah `X` dan `y` dipisahkan, jangan langsung melakukan scaling pada seluruh dataset.

Pertama, pisahkan data menjadi:

* **Training data** → digunakan untuk belajar
* **Testing data** → digunakan untuk mengevaluasi model

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

Dengan `test_size=0.2`:

```text
80% → Training
20% → Testing
```

### Struktur Data

```text
Dataset
   │
   ├───────────────┐
   ▼               ▼
Training         Testing
   │               │
   ├── X_train     ├── X_test
   └── y_train     └── y_test
```

---

# 3. 📏 StandardScaler

`StandardScaler` digunakan untuk melakukan **standardization** pada fitur numerik.

Rumusnya:

$$
z = \frac{x - \mu}{\sigma}
$$

Keterangan:

| Simbol   | Arti                  |
| -------- | --------------------- |
| $x$      | Nilai asli            |
| $\mu$    | Mean / rata-rata      |
| $\sigma$ | Standard deviation    |
| $z$      | Nilai setelah scaling |

Tujuannya adalah membuat fitur memiliki skala yang lebih seragam.

### Contoh

Sebelum scaling:

```text
Age       → 18 - 60
Salary    → 3,000,000 - 20,000,000
```

Setelah standardization, nilainya dapat menjadi:

```text
Age       → -1.2, -0.4, 0.3, 1.5, ...
Salary    → -0.8, -0.2, 0.5, 1.3, ...
```

### ⚠️ Penting

Scaling **tidak berarti semua nilai menjadi antara 0 dan 1**.

`StandardScaler` menggunakan mean dan standard deviation sehingga nilai hasil scaling dapat berupa:

```text
-2.1
-1.0
 0.0
 0.8
 2.3
```

---

# 4. 🔄 `fit`, `transform`, dan `fit_transform`

Ketiga method ini memiliki fungsi yang berbeda.

## `fit()`

`fit()` berarti:

> **Belajar dari data.**

Pada `StandardScaler`, scaler akan mempelajari:

* mean
* standard deviation

Contoh:

```python
scaler.fit(X_train)
```

`fit()` belum mengubah data.

---

## `transform()`

`transform()` berarti:

> **Mengubah data menggunakan parameter yang sudah dipelajari.**

Contoh:

```python
X_train_scaled = scaler.transform(X_train)
```

Scaler menggunakan mean dan standard deviation yang sebelumnya diperoleh dari `fit()`.

---

## `fit_transform()`

`fit_transform()` berarti:

> **Belajar dari data + langsung mengubah data tersebut.**

Contoh:

```python
X_train_scaled = scaler.fit_transform(X_train)
```

Secara konsep:

```text
fit_transform()
      │
      ├── fit()
      │     ↓
      │  belajar mean & std
      │
      └── transform()
            ↓
        mengubah data
```

### Perbandingan

| Method            | Belajar Parameter | Mengubah Data |
| ----------------- | :---------------: | :-----------: |
| `fit()`           |         ✅         |       ❌       |
| `transform()`     |         ❌         |       ✅       |
| `fit_transform()` |         ✅         |       ✅       |

---

# 5. 📊 Scaling pada DataFrame yang Sudah Di-Encode

Misalnya CSV sudah di-encode:

```text
Age | Gender | StudyHours | Extracurricular | Performance Index
20  | 1      | 5          | 1                | 75
21  | 0      | 7          | 0                | 82
19  | 1      | 3          | 1                | 68
22  | 0      | 8          | 1                | 90
```

`Gender` dan `Extracurricular` sudah berubah menjadi angka.

Namun:

> **Encoding dan scaling adalah dua proses yang berbeda.**

## Encoding

Mengubah kategori menjadi representasi numerik.

```text
Yes → 1
No  → 0
```

## Scaling

Mengubah skala numerik menggunakan metode tertentu.

Contohnya `StandardScaler`:

$$
z = \frac{x-\mu}{\sigma}
$$

Sehingga:

```text
Encoding
   ↓
Kategori → Angka

Scaling
   ↓
Angka → Skala yang telah distandardisasi
```

### 🔑 Kesimpulan

Dataset yang **sudah di-encode belum tentu sudah siap untuk semua algoritma**.

Scaling masih dapat diperlukan tergantung algoritma yang digunakan.

---

# 6. 🎯 `Performance Index` sebagai Target

Jika `Performance Index` adalah nilai yang ingin diprediksi:

```python
X = df.drop("Performance Index", axis=1)
y = df["Performance Index"]
```

Maka:

```text
X → Features
y → Performance Index
```

Dalam workflow dasar regresi, kita melakukan scaling pada `X`, bukan memasukkan `Performance Index` ke dalam scaler yang sama.

Contoh:

```python
scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

Sedangkan:

```text
y_train
y_test
```

tetap digunakan sebagai target model.

### Alur

```text
Features (X)                    Target (y)
     │                               │
     ▼                               │
Train-Test Split                   │
     │                               │
     ▼                               ▼
X_train / X_test             y_train / y_test
     │                               │
     ▼                               │
StandardScaler                       │
     │                               │
     ▼                               │
X_train_scaled                       │
X_test_scaled                        │
     │                               │
     └──────────────┬────────────────┘
                    ▼
                  Model
```

---

# 7. 🔬 Alur Lengkap

Workflow preprocessing yang umum:

```text
                    DataFrame
                        │
                        ▼
                 Pisahkan X dan y
                        │
             ┌──────────┴──────────┐
             ▼                     ▼
             X                     y
         Features              Target
             │              Performance Index
             │
             ▼
       Train-Test Split
             │
       ┌─────┴─────┐
       ▼           ▼
    X_train       X_test
       │           │
       │           │
fit_transform   transform
       │           │
       ▼           ▼
X_train_scaled X_test_scaled
       │           │
       └─────┬─────┘
             ▼
          ML Model
             │
             ▼
         Prediction
             │
             ▼
      Performance Index
```

---

# 8. 💻 Contoh Kode Lengkap

Berikut contoh workflow sederhana menggunakan `LinearRegression`.

```python
import pandas as pd

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression


# ==========================================
# 1. Membaca dataset
# ==========================================

df = pd.read_csv("data.csv")


# ==========================================
# 2. Memisahkan features dan target
# ==========================================

X = df.drop("Performance Index", axis=1)
y = df["Performance Index"]


# ==========================================
# 3. Membagi data menjadi training dan testing
# ==========================================

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)


# ==========================================
# 4. Scaling features
# ==========================================

scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)


# ==========================================
# 5. Membuat model
# ==========================================

model = LinearRegression()


# ==========================================
# 6. Training model
# ==========================================

model.fit(X_train_scaled, y_train)


# ==========================================
# 7. Melakukan prediksi
# ==========================================

y_pred = model.predict(X_test_scaled)
```

---

# 9. ⚠️ Hal yang Perlu Diingat

## 9.1 Jangan `fit()` scaler pada data test

❌ Jangan:

```python
scaler.fit(X_test)
```

atau:

```python
X_test_scaled = scaler.fit_transform(X_test)
```

Karena scaler akan mempelajari parameter baru dari data test.

---

## 9.2 Gunakan scaler yang sama

✅ Yang benar:

```python
X_train_scaled = scaler.fit_transform(X_train)

X_test_scaled = scaler.transform(X_test)
```

Artinya:

```text
X_train
   │
   ▼
fit()
   │
   ▼
Mean + Standard Deviation
   │
   ▼
Scaler
   │
   ├──────────────→ X_train
   │                  │
   │                  ▼
   │              transform
   │
   └──────────────→ X_test
                      │
                      ▼
                  transform
```

Dengan demikian, `X_test` menggunakan aturan scaling yang **sama** dengan `X_train`.

---

## 9.3 Scaling tidak selalu wajib

Tidak semua algoritma membutuhkan scaling.

### 🟢 Umumnya sensitif terhadap scaling

Contohnya:

* K-Nearest Neighbors (KNN)
* K-Means
* Support Vector Machine (SVM)
* Logistic Regression
* Neural Network
* PCA

### 🔵 Umumnya tidak sensitif terhadap scaling

Contohnya algoritma berbasis decision tree:

* Decision Tree
* Random Forest
* XGBoost
* LightGBM
* CatBoost

Jadi:

> **Scaling bukan langkah wajib untuk setiap algoritma Machine Learning.**

Scaling dilakukan ketika karakteristik algoritmanya membuat skala fitur menjadi relevan.

---

# 10. 🧠 Ringkasan Konsep

## Workflow Utama

```text
CSV
 │
 ▼
Encoding
 │
 ▼
X dan y
 │
 ▼
Train-Test Split
 │
 ├─────────────┐
 ▼             ▼
X_train       X_test
 │             │
 ▼             ▼
fit_transform  transform
 │             │
 ▼             ▼
X_train_scaled X_test_scaled
 │             │
 └──────┬──────┘
        ▼
      Model
        │
        ▼
   Prediction
```

---

## 🔑 Tiga Method Penting

| Method            | Makna                                      |
| ----------------- | ------------------------------------------ |
| `fit()`           | Belajar parameter dari data                |
| `transform()`     | Menerapkan parameter yang sudah dipelajari |
| `fit_transform()` | Belajar + menerapkan parameter             |

---

## 🔑 Tiga Konsep yang Harus Dibedakan

### 1. Encoding ≠ Scaling

**Encoding:**

```text
Kategori → Angka
```

**Scaling:**

```text
Angka → Skala yang sesuai
```

---

### 2. `X` ≠ `y`

```text
X → Features / input
y → Target / output
```

Contoh:

```python
X = df.drop("Performance Index", axis=1)
y = df["Performance Index"]
```

---

### 3. Training ≠ Testing

```text
Training
→ digunakan untuk belajar

Testing
→ digunakan untuk mengevaluasi
```

Scaler juga harus mengikuti prinsip tersebut:

```text
X_train
   ↓
fit_transform()

X_test
   ↓
transform()
```

---

## 🎯 Inti yang Perlu Dipahami

> **Jangan menganggap scaling sebagai langkah wajib untuk semua dataset dan semua algoritma.**

> **Pertama tentukan `X` dan `y`, kemudian split data, lalu lakukan preprocessing berdasarkan kebutuhan algoritma.**

> **Jika menggunakan `StandardScaler`, parameter scaling dipelajari dari data training dan digunakan kembali untuk data testing maupun data baru.**
