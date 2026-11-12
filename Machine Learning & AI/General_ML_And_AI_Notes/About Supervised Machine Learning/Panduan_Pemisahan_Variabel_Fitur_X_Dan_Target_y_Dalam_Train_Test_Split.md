# Panduan Pemisahan Variabel Fitur (X) dan Target (y) dalam Train-Test Split

Saat melakukan *train-test split* dalam machine learning, data harus dipisahkan menjadi dua komponen utama: **Fitur (X)** dan **Target (y)**. Prinsip dasarnya adalah menentukan apa yang ingin diprediksi (y) dan apa saja faktor pendukungnya (X).

---

## 📌 Konsep Dasar Pemisahan Data

### 🎯 1. Variabel Target (y)
* **Definisi:** Kolom atau label data yang **ingin diprediksi** nilainya oleh model.
* **Cara Mengambil:** Pilih kolom target tersebut secara langsung dari DataFrame.
* **Rumus Singkat:** `y = df['nama_kolom_target']`

### 📊 2. Variabel Fitur (X)
* **Definisi:** Seluruh kolom yang digunakan sebagai **faktor/modal untuk memprediksi** target.
* **Cara Mengambil:** **Buang (drop) kolom target** dari DataFrame asli, sehingga hanya menyisakan kolom fitur pendukung.
* **Rumus Singkat:** `X = df.drop(columns=['nama_kolom_target'])`

---

## 💻 Implementasi Kode (Python & Scikit-Learn)

Berikut adalah contoh implementasi standar menggunakan library `pandas` dan `scikit-learn`:

```python
import pandas as pd
from sklearn.model_selection import train_test_split

# 1. Menentukan Target (y) dan Fitur (X)
y = df['kolom_target']                  # Mengambil target saja
X = df.drop(columns=['kolom_target'])  # Mengambil fitur (target di-drop)

# 2. Melakukan Train-Test Split (Contoh: 80% Train, 20% Test)
X_train, X_test, y_train, y_test = train_test_split(
    X, 
    y, 
    test_size=0.2, 
    random_state=42
)

# 3. Verifikasi Ukuran Data
print(f"Ukuran X_train: {X_train.shape} | Ukuran y_train: {y_train.shape}")
print(f"Ukuran X_test:  {X_test.shape} | Ukuran y_test:  {y_test.shape}")
```

---

## 💡 Ringkasan Analogi

| Komponen | Status Kolom Target | Fungsi | Contoh (Prediksi Harga Rumah) |
| :--- | :--- | :--- | :--- |
| **Variabel X** | **Di-drop** (Dibuang) | Informasi pendukung / Kunci jawaban soal | Luas bangunan, jumlah kamar, lokasi |
| **Variabel y** | **Dipilih** (Dipertahankan) | Nilai yang dicari / Soal ujian model | Harga rumah |
