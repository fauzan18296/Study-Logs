# 📊 Evaluasi Model Machine Learning

## Mengapa Akurasi Saja Tidak Cukup?

Banyak pemula menganggap bahwa model Machine Learning yang memiliki akurasi tinggi pasti lebih baik.

Padahal, **akurasi hanyalah salah satu metrik evaluasi** dan dalam beberapa kasus bisa sangat menyesatkan.

> [!IMPORTANT]
> Model yang baik bukanlah model dengan angka akurasi terbesar, melainkan model yang mampu memberikan prediksi yang baik pada data baru (unseen data) dan sesuai dengan tujuan bisnis atau masalah yang ingin diselesaikan.

---

# 🎯 Apa yang Menentukan Model Machine Learning Bagus?

## 1. Generalization

Kemampuan model untuk bekerja pada data yang belum pernah dilihat sebelumnya.

Contoh:

| Model | Train Accuracy | Test Accuracy |
|---------|---------|---------|
| A | 99% | 70% |
| B | 92% | 89% |

Model **B** biasanya lebih baik karena mampu melakukan generalisasi dengan lebih baik.

---

## 2. Overfitting dan Underfitting

### Overfitting

Model terlalu menghafal data training.

Ciri-ciri:

- Train Accuracy sangat tinggi
- Test Accuracy jauh lebih rendah

Contoh:

| Train | Test |
|---------|---------|
| 99% | 70% |

---

### Underfitting

Model terlalu sederhana sehingga gagal menangkap pola data.

Ciri-ciri:

| Train | Test |
|---------|---------|
| 60% | 58% |

---

### Model Ideal

| Train | Test |
|---------|---------|
| 92% | 89% |

Performa tinggi dan selisihnya kecil.

---

# 📌 Confusion Matrix

Confusion Matrix digunakan untuk melihat jenis kesalahan yang dilakukan model.

Misalkan kita memiliki model deteksi spam.

| | Prediksi Positif | Prediksi Negatif |
|----------|----------|----------|
| Aktual Positif | TP | FN |
| Aktual Negatif | FP | TN |

Keterangan:

| Singkatan | Nama | Arti |
|------------|------------|------------|
| TP | True Positive | Positif yang berhasil terdeteksi |
| TN | True Negative | Negatif yang berhasil terdeteksi |
| FP | False Positive | Negatif tetapi diprediksi positif |
| FN | False Negative | Positif tetapi diprediksi negatif |

---

## Contoh Confusion Matrix

| | Prediksi Spam | Prediksi Bukan Spam |
|----------|----------|----------|
| Spam Asli | 80 | 20 |
| Bukan Spam Asli | 10 | 90 |

Maka:

- TP = 80
- FN = 20
- FP = 10
- TN = 90

---

# 🎯 Accuracy

Accuracy menunjukkan proporsi prediksi yang benar dari seluruh data.

```math
Accuracy = \frac{TP + TN}{TP + TN + FP + FN}
```

Contoh:

```math
Accuracy = \frac{80 + 90}{80 + 90 + 10 + 20}
```

```math
Accuracy = \frac{170}{200}
```

```math
Accuracy = 85\%
```

Interpretasi:

> Model memberikan prediksi yang benar pada 85% data.

---

# 🎯 Precision

Precision menjawab pertanyaan:

> Dari semua data yang diprediksi positif, berapa yang benar-benar positif?

Rumus:

```math
Precision = \frac{TP}{TP + FP}
```

Contoh:

```math
Precision = \frac{80}{80 + 10}
```

```math
Precision = \frac{80}{90}
```

```math
Precision = 88.9\%
```

Interpretasi:

> Ketika model mengatakan "spam", 88.9% prediksi tersebut memang spam.

---

## Kapan Precision Penting?

Contoh kasus:

- Deteksi spam
- Deteksi fraud
- Sistem rekomendasi

Karena kita ingin meminimalkan **False Positive (FP)**.

---

# 🎯 Recall

Recall menjawab pertanyaan:

> Dari semua data positif yang sebenarnya ada, berapa yang berhasil ditemukan model?

Rumus:

```math
Recall = \frac{TP}{TP + FN}
```

Contoh:

```math
Recall = \frac{80}{80 + 20}
```

```math
Recall = \frac{80}{100}
```

```math
Recall = 80\%
```

Interpretasi:

> Model berhasil menemukan 80% dari seluruh spam yang ada.

---

## Kapan Recall Penting?

Contoh kasus:

- Diagnosa kanker
- Deteksi penyakit
- Sistem alarm kebakaran

Karena kita ingin meminimalkan **False Negative (FN)**.

---

# ⚖️ Precision vs Recall

## Model A

- 10 pasien diprediksi sakit
- Semua benar

Hasil:

```text
Precision = 100%
Recall = 10%
```

Model sangat konservatif.

---

## Model B

- 90 pasien diprediksi sakit
- 70 benar
- 20 salah

Hasil:

```text
Precision ≈ 78%
Recall = 70%
```

Model lebih agresif.

---

> Tidak ada yang selalu lebih baik.
>
> Pilihan tergantung tujuan bisnis dan konsekuensi kesalahan.

---

# 🎯 F1 Score

F1 Score digunakan ketika Precision dan Recall sama-sama penting.

Rumus:

```math
F1 = 2 \times \frac{Precision \times Recall}{Precision + Recall}
```

Contoh:

```math
F1 = 2 \times \frac{0.889 \times 0.80}{0.889 + 0.80}
```

```math
F1 \approx 84.2\%
```

---

# ⚠️ Mengapa Accuracy Bisa Menipu?

Misalkan dataset:

| Kelas | Jumlah |
|---------|---------|
| Sehat | 990 |
| Sakit | 10 |

Model selalu menebak:

```text
Sehat
```

Confusion Matrix:

| | Prediksi Sakit | Prediksi Sehat |
|----------|----------|----------|
| Sakit | 0 | 10 |
| Sehat | 0 | 990 |

Maka:

- TP = 0
- FN = 10
- FP = 0
- TN = 990

---

## Accuracy

```math
Accuracy = \frac{990}{1000}
```

```math
Accuracy = 99\%
```

Kelihatannya luar biasa.

Namun:

```math
Precision = 0
```

```math
Recall = 0
```

Model tidak pernah menemukan pasien yang sakit.

---

> [!WARNING]
> Akurasi tinggi tidak selalu berarti model bagus.

---

# 🧠 Cara Berpikir Saat Mengevaluasi Model

Jangan langsung bertanya:

> "Akurasinya berapa?"

Lebih baik tanyakan:

1. Berapa TP, FP, TN, dan FN?
2. Berapa Precision?
3. Berapa Recall?
4. Berapa F1 Score?
5. Apakah dataset seimbang?
6. Apa konsekuensi dari FP dan FN?

---

# 📌 Ringkasan Cepat

| Metric | Fokus Utama | Semakin Besar Semakin Baik? |
|----------|----------|----------|
| Accuracy | Prediksi benar secara keseluruhan | ✅ |
| Precision | Mengurangi False Positive | ✅ |
| Recall | Mengurangi False Negative | ✅ |
| F1 Score | Keseimbangan Precision dan Recall | ✅ |

---

# 🚀 Kesimpulan

> Model Machine Learning yang baik bukanlah model dengan akurasi terbesar.

Model yang baik adalah model yang:

- Memiliki performa baik pada data baru.
- Tidak overfitting.
- Tidak underfitting.
- Menggunakan metrik yang sesuai dengan masalah.
- Memiliki Precision, Recall, dan F1 Score yang masuk akal.
- Memahami konsekuensi dari False Positive dan False Negative.

Dengan kata lain:

> **Confusion Matrix adalah sumber utama evaluasi model, sedangkan Accuracy, Precision, Recall, dan F1 Score hanyalah cara berbeda untuk membaca informasi yang ada di dalamnya.**
