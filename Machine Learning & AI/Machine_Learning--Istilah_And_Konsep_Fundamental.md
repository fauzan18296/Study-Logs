# 🤖 Machine Learning — Istilah & Konsep Fundamental

> 📚 Catatan ringkas untuk memahami istilah-istilah penting dalam **Machine Learning**, mulai dari data hingga MLOps.

---

## 📑 Daftar Isi

* [1. Data & Dataset](#1--data--dataset)
* [2. Data Preparation](#2--data-preparation)
* [3. Jenis Machine Learning](#3--jenis-machine-learning)
* [4. Model & Training](#4--model--training)
* [5. Evaluasi Model](#5--evaluasi-model)
* [6. Underfitting & Overfitting](#6--underfitting--overfitting)
* [7. Hyperparameter](#7--hyperparameter)
* [8. Cross Validation](#8--cross-validation)
* [9. Bias & Variance](#9--bias--variance)
* [10. Istilah Dunia Kerja ML](#10--istilah-dunia-kerja-machine-learning)
* [11. Learning Roadmap](#11--learning-roadmap)

---

# 1. 📊 Data & Dataset

## Dataset

**Dataset** adalah kumpulan data yang digunakan untuk melakukan analisis, training, dan evaluasi model Machine Learning.

Contoh:

| Umur |      Gaji | Membeli Produk |
| ---: | --------: | :------------: |
|   25 | 5.000.000 |       Ya       |
|   32 | 8.000.000 |      Tidak     |
|   28 | 6.000.000 |       Ya       |

---

## Sample / Observation

**Sample** atau **Observation** adalah satu observasi atau satu baris data.

Contoh:

```text
25 | 5.000.000 | Ya
```

Baris tersebut merupakan satu sample.

> 💡 Dalam konteks tertentu istilah **instance**, **sample**, dan **observation** dapat digunakan dengan makna yang hampir sama.

---

## Feature

**Feature (X)** adalah variabel input yang digunakan model untuk menghasilkan prediksi.

Pada dataset:

| Umur |      Gaji | Membeli |
| ---: | --------: | :-----: |
|   25 | 5.000.000 |    Ya   |

Maka:

```text
Feature:
- Umur
- Gaji
```

Secara umum:

```math
X = [x_1, x_2, ..., x_n]
```

---

## Target / Label

**Target** atau **Label (y)** adalah nilai yang ingin diprediksi oleh model.

Contoh:

```text
Feature → Umur, Gaji
Target  → Membeli Produk
```

Secara umum:

```math
y = Target
```

---

## Instance

**Instance** adalah satu objek/data individu yang digunakan dalam proses Machine Learning.

Contoh:

```text
Customer A
├── Umur
├── Gaji
└── Status Pembelian
```

---

## Class

**Class** adalah kategori atau kelas dalam masalah klasifikasi.

Contoh:

```text
Email
├── Spam
└── Not Spam
```

Maka:

```text
Class = Spam / Not Spam
```

---

# 2. 🧹 Data Preparation

Data mentah biasanya belum langsung siap digunakan untuk training.

Proses mempersiapkannya disebut **Data Preparation** atau **Data Preprocessing**.

---

## Missing Value

**Missing Value** adalah nilai yang hilang atau tidak tersedia.

Contoh:

| Umur |      Gaji |
| ---: | --------: |
|   25 | 5.000.000 |
|  NaN | 7.000.000 |
|   30 | 6.000.000 |

`NaN` merupakan missing value.

Beberapa pendekatan:

```text
Missing Value
     │
     ├── Hapus data
     │
     ├── Mean
     │
     ├── Median
     │
     └── Model-based Imputation
```

---

## Outlier

**Outlier** adalah observasi yang memiliki nilai sangat berbeda dari mayoritas data.

Contoh:

```text
10
12
14
15
18
500
```

`500` berpotensi menjadi outlier.

> ⚠️ Outlier tidak selalu berarti data salah. Bisa saja merupakan kejadian nyata yang memang jarang terjadi.

---

## Encoding

**Encoding** adalah proses mengubah data kategorikal menjadi representasi numerik agar dapat diproses oleh algoritma tertentu.

Contoh:

```text
Ya    → 1
Tidak → 0
```

Beberapa teknik:

* Label Encoding
* Ordinal Encoding
* One-Hot Encoding
* Target Encoding

---

## Scaling

**Scaling** adalah proses menyesuaikan skala numerik antar-feature.

Contoh:

```text
Umur  = 25
Gaji  = 50.000.000
```

Skala kedua feature sangat berbeda.

Beberapa algoritma sensitif terhadap perbedaan skala tersebut.

Metode populer:

* StandardScaler
* MinMaxScaler
* RobustScaler

### Standardization

```math
z = \frac{x-\mu}{\sigma}
```

Keterangan:

```text
x = nilai asli
μ = mean
σ = standard deviation
z = nilai setelah standardization
```

---

## Feature Engineering

**Feature Engineering (FE)** adalah proses membuat, mengubah, atau mentransformasikan feature agar informasi yang diberikan kepada model menjadi lebih berguna.

Contoh:

```text
Tanggal Lahir
      ↓
Feature Engineering
      ↓
Usia
```

Contoh lain:

```text
Harga
Jumlah Barang
      ↓
Total Harga
```

---

## Feature Selection

**Feature Selection** adalah proses memilih feature yang relevan untuk digunakan model.

Tujuan:

```text
Feature terlalu banyak
        ↓
Noise / Redundansi
        ↓
Feature Selection
        ↓
Feature lebih relevan
```

Manfaat:

* Mengurangi noise
* Mengurangi kompleksitas model
* Mempercepat training
* Berpotensi mengurangi overfitting
* Meningkatkan interpretabilitas

---

# 3. 🧠 Jenis Machine Learning

Secara umum Machine Learning dapat dibagi menjadi beberapa pendekatan.

---

## Supervised Learning

Model belajar dari data yang memiliki **target/label**.

```text
Feature + Label
      ↓
   Training
      ↓
    Model
      ↓
 Prediction
```

Contoh:

```text
Data:
Umur + Gaji → Membeli Produk

Model:
Umur + Gaji → Prediksi Membeli Produk
```

### Contoh Algoritma

* Linear Regression
* Logistic Regression
* Decision Tree
* Random Forest
* Support Vector Machine (SVM)
* XGBoost
* Neural Network

### Dua masalah utama

```text
Supervised Learning
       │
       ├── Regression
       │
       └── Classification
```

---

## Regression

Digunakan untuk memprediksi **nilai kontinu**.

Contoh:

```text
Prediksi:
- Harga rumah
- Suhu
- Pendapatan
- Harga saham
```

Output:

```text
250.000.000
32.5
7.850.000
```

---

## Classification

Digunakan untuk memprediksi **kategori/class**.

Contoh:

```text
Email → Spam / Not Spam
```

atau:

```text
Penyakit → Positif / Negatif
```

---

## Unsupervised Learning

Model belajar dari data yang **tidak memiliki target/label**.

```text
Data
 ↓
Algorithm
 ↓
Pattern / Structure
```

Contoh penggunaan:

```text
Customer
   ↓
Clustering
   ↓
Group 1
Group 2
Group 3
```

### Contoh Algoritma

* K-Means
* DBSCAN
* Hierarchical Clustering
* PCA

---

## Reinforcement Learning

Model belajar melalui interaksi dengan environment menggunakan konsep **reward** dan **penalty**.

```text
Agent
  ↓
Action
  ↓
Environment
  ↓
Reward
  ↓
Learning
```

Contoh:

* Game AI
* Robot
* Autonomous systems
* Optimasi keputusan

---

# 4. ⚙️ Model & Training

## Algorithm

**Algorithm** adalah metode atau prosedur yang digunakan untuk mempelajari pola dari data.

Contoh:

```text
Random Forest
XGBoost
K-Means
Neural Network
```

---

## Model

**Model** adalah hasil pembelajaran algoritma dari data.

Secara sederhana:

```text
Data
  +
Algorithm
  ↓
Training
  ↓
Model
```

Model kemudian digunakan untuk melakukan prediksi.

```text
Model + Data Baru
       ↓
    Prediction
```

---

## Training

**Training** adalah proses ketika model mempelajari pola dari training data.

```text
Training Data
      ↓
  Algorithm
      ↓
     Model
```

---

## Inference

**Inference** adalah proses menggunakan model yang sudah dilatih untuk menghasilkan prediksi pada data baru.

```text
Trained Model
      +
  New Data
      ↓
   Inference
      ↓
  Prediction
```

Contoh:

```text
Model harga rumah
        +
Rumah baru
        ↓
Prediksi harga
```

---

# 5. 📈 Evaluasi Model

Model tidak cukup hanya "bisa training".

Kita perlu mengetahui seberapa baik model bekerja menggunakan **Evaluation Metrics**.

---

## Accuracy

Accuracy mengukur proporsi prediksi yang benar dari seluruh prediksi.

```math
Accuracy = \frac{TP+TN}{TP+TN+FP+FN}
```

Cocok digunakan ketika distribusi class relatif seimbang.

> ⚠️ Accuracy bisa menyesatkan pada dataset yang sangat imbalanced.

---

## Confusion Matrix

Confusion Matrix digunakan untuk melihat hasil klasifikasi secara lebih detail.

|                     | Predicted Positive | Predicted Negative |
| ------------------- | -----------------: | -----------------: |
| **Actual Positive** |                 TP |                 FN |
| **Actual Negative** |                 FP |                 TN |

Keterangan:

```text
TP = True Positive
TN = True Negative
FP = False Positive
FN = False Negative
```

---

## Precision

Precision menjawab:

> "Dari semua yang diprediksi positif, berapa yang benar-benar positif?"

```math
Precision = \frac{TP}{TP+FP}
```

Precision penting ketika **False Positive mahal**.

Contoh:

```text
Spam Detection
```

Kita tidak ingin terlalu banyak email normal dianggap spam.

---

## Recall

Recall menjawab:

> "Dari semua data yang sebenarnya positif, berapa yang berhasil ditemukan?"

```math
Recall = \frac{TP}{TP+FN}
```

Recall penting ketika **False Negative mahal**.

Contoh:

```text
Deteksi penyakit
```

Kita ingin meminimalkan kasus positif yang terlewat.

---

## F1 Score

F1 Score merupakan harmonic mean antara Precision dan Recall.

```math
F1 = 2 \times
\frac{Precision \times Recall}
{Precision + Recall}
```

F1 berguna ketika kita ingin mempertimbangkan Precision dan Recall secara bersamaan.

---

## MAE

**Mean Absolute Error** digunakan pada masalah regression.

```math
MAE =
\frac{1}{n}
\sum_{i=1}^{n}
|y_i-\hat{y}_i|
```

Semakin kecil → semakin baik.

---

## MSE

**Mean Squared Error**:

```math
MSE =
\frac{1}{n}
\sum_{i=1}^{n}
(y_i-\hat{y}_i)^2
```

Error dikuadratkan sehingga kesalahan besar mendapatkan penalti lebih besar.

---

## RMSE

**Root Mean Squared Error**:

```math
RMSE =
\sqrt{
\frac{1}{n}
\sum_{i=1}^{n}
(y_i-\hat{y}_i)^2
}
```

Semakin kecil → semakin baik.

---

# 6. ⚖️ Underfitting & Overfitting

## Underfitting

Terjadi ketika model terlalu sederhana sehingga gagal menangkap pola penting dalam data.

```text
Training Performance → Buruk
Testing Performance  → Buruk
```

Secara sederhana:

```text
Model terlalu sederhana
        ↓
Tidak mampu mempelajari pola
        ↓
Underfitting
```

---

## Overfitting

Terjadi ketika model terlalu menyesuaikan diri terhadap training data sehingga performanya buruk pada data baru.

```text
Training Performance → Sangat baik
Testing Performance  → Buruk
```

Secara sederhana:

```text
Model terlalu kompleks
        ↓
Menghafal pola/noise training
        ↓
Overfitting
```

---

## Good Fit

Kondisi ketika model mampu mempelajari pola penting tanpa terlalu menghafal training data.

```text
Training Performance → Baik
Testing Performance  → Baik
```

---

## Perbandingan

| Kondisi      | Training      | Testing |
| ------------ | ------------- | ------- |
| Underfitting | ❌ Buruk       | ❌ Buruk |
| Good Fit     | ✅ Baik        | ✅ Baik  |
| Overfitting  | ✅ Sangat baik | ❌ Buruk |

---

# 7. 🎛️ Hyperparameter

**Hyperparameter** adalah konfigurasi model yang ditentukan sebelum atau selama proses training dan bukan dipelajari langsung sebagai parameter model dari data.

Contoh Random Forest:

```python
RandomForestClassifier(
    n_estimators=100,
    max_depth=10
)
```

Di sini:

```text
n_estimators → Hyperparameter
max_depth    → Hyperparameter
```

Contoh hyperparameter lainnya:

```text
Learning Rate
Batch Size
Number of Epochs
Maximum Depth
Number of Trees
Regularization Strength
```

---

## Parameter vs Hyperparameter

Ini penting untuk dibedakan.

### Parameter

Dipelajari oleh model dari data.

Contoh pada Linear Regression:

```math
y = w_1x_1 + w_2x_2 + b
```

`w₁`, `w₂`, dan `b` adalah parameter model.

### Hyperparameter

Ditentukan oleh kita atau proses tuning.

```text
Learning Rate
Max Depth
Number of Trees
```

---

# 8. 🔄 Cross Validation

**Cross Validation** adalah teknik untuk mengevaluasi kemampuan generalisasi model dengan menggunakan beberapa pembagian data.

Salah satu yang paling umum adalah **K-Fold Cross Validation**.

Misalnya:

```text
5-Fold Cross Validation
```

Data dibagi menjadi 5 bagian:

```text
Fold 1
Fold 2
Fold 3
Fold 4
Fold 5
```

Kemudian training dan validation dilakukan secara bergantian:

```text
Iteration 1:
Test → Fold 1
Train → Fold 2,3,4,5

Iteration 2:
Test → Fold 2
Train → Fold 1,3,4,5

Iteration 3:
Test → Fold 3
Train → Fold 1,2,4,5

...
```

Kemudian skor biasanya dirata-ratakan.

```math
CV_{score} =
\frac{1}{K}
\sum_{i=1}^{K} Score_i
```

### Tujuan

* Mendapatkan estimasi performa yang lebih stabil
* Mengurangi ketergantungan terhadap satu pembagian data
* Membantu hyperparameter tuning

---

# 9. ⚖️ Bias & Variance

## Bias

**Bias** adalah error yang muncul karena model membuat asumsi terlalu sederhana terhadap hubungan dalam data.

```text
Bias Tinggi
    ↓
Model terlalu sederhana
    ↓
Underfitting
```

---

## Variance

**Variance** menggambarkan seberapa sensitif model terhadap perubahan pada training data.

```text
Variance Tinggi
    ↓
Model terlalu sensitif
    ↓
Overfitting
```

---

## Bias-Variance Tradeoff

Secara konseptual:

```text
Model Complexity
       ↑
       │
Bias   ↓
       │
       │
       │
Variance ↑
       │
       └──────────────→
```

Tujuannya bukan sekadar membuat model paling kompleks.

Tujuannya adalah menemukan **tingkat kompleksitas yang memberikan generalisasi terbaik**.

---

# 10. 🚀 Istilah Dunia Kerja Machine Learning

## EDA — Exploratory Data Analysis

Proses mengeksplorasi dan memahami dataset sebelum modeling.

Biasanya meliputi:

```text
EDA
├── Struktur data
├── Missing Value
├── Distribusi
├── Outlier
├── Korelasi
└── Relationship antar-feature
```

---

## Pipeline

**Pipeline** adalah rangkaian proses yang menghubungkan preprocessing dan modeling dalam satu workflow.

Contoh:

```text
Raw Data
   ↓
Imputation
   ↓
Encoding
   ↓
Scaling
   ↓
Model
   ↓
Prediction
```

---

## Deployment

**Deployment** adalah proses membuat model yang sudah dilatih dapat digunakan di lingkungan nyata.

Contoh:

```text
Machine Learning Model
        ↓
      API
        ↓
     Backend
        ↓
Frontend / Application
```

---

## Batch Prediction

Prediksi dilakukan terhadap banyak data sekaligus.

Contoh:

```text
1.000.000 Customer
       ↓
Batch Prediction
       ↓
1.000.000 Predictions
```

---

## Real-Time Prediction

Prediksi dilakukan ketika request masuk.

```text
User Request
     ↓
    API
     ↓
  Model
     ↓
Prediction
     ↓
 Response
```

---

## Model Monitoring

Proses memantau model setelah deployment.

Hal yang dapat dipantau:

```text
├── Prediction Quality
├── Latency
├── Error Rate
├── Data Distribution
├── Data Drift
└── Model Drift
```

---

## Data Drift

Terjadi ketika distribusi data input berubah dibandingkan data yang digunakan ketika model dikembangkan.

Contoh:

```text
Training Data
Customer usia:
18–40 tahun

Production Data:
40–70 tahun
```

Distribusi input telah berubah.

---

## Model Drift

Model Drift mengacu pada penurunan relevansi/performa model karena hubungan antara input dan target berubah atau kondisi dunia nyata berubah.

Contoh:

```text
Model lama
    ↓
Perilaku customer berubah
    ↓
Prediction semakin buruk
    ↓
Model perlu dievaluasi/retraining
```

> 🔎 **Data Drift dan Model Drift tidak sama.** Data bisa berubah tanpa langsung menyebabkan performa model turun, dan performa model bisa turun karena perubahan hubungan antara feature dan target.

---

## Experiment Tracking

Proses mencatat eksperimen Machine Learning.

Contoh informasi:

```text
Experiment #01
├── Algorithm: Random Forest
├── max_depth: 10
├── n_estimators: 100
├── Accuracy: 0.91
└── F1: 0.89
```

Tujuannya agar eksperimen dapat dibandingkan dan direproduksi.

---

## MLOps

**MLOps (Machine Learning Operations)** adalah praktik untuk mengelola lifecycle Machine Learning secara sistematis.

Secara sederhana:

```text
Data
 ↓
Training
 ↓
Evaluation
 ↓
Deployment
 ↓
Monitoring
 ↓
Retraining
 ↓
Deployment
 ↓
...
```

MLOps menggabungkan konsep dari:

```text
Machine Learning
        +
Software Engineering
        +
DevOps
        +
Data Engineering
```

---

# 11. 🗺️ Learning Roadmap

Jika baru mulai belajar Machine Learning, tidak perlu menghafal semua istilah sekaligus.

Urutan yang lebih masuk akal:

```text
                    MACHINE LEARNING
                           │
                           ▼
                 ┌──────────────────┐
                 │ 1. DATA          │
                 │ Dataset          │
                 │ Feature          │
                 │ Target           │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ 2. PREPROCESSING │
                 │ Missing Value    │
                 │ Encoding         │
                 │ Scaling          │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ 3. MODELING      │
                 │ Regression       │
                 │ Classification   │
                 │ Clustering       │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ 4. EVALUATION    │
                 │ Accuracy         │
                 │ Precision        │
                 │ Recall           │
                 │ F1 / RMSE        │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ 5. OPTIMIZATION  │
                 │ Hyperparameter   │
                 │ Cross Validation │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ 6. GENERALIZATION│
                 │ Bias             │
                 │ Variance         │
                 │ Overfitting      │
                 │ Underfitting     │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ 7. PRODUCTION    │
                 │ Deployment       │
                 │ Monitoring       │
                 │ MLOps            │
                 └──────────────────┘
```

---

# 🧠 Ringkasan Konsep

| Konsep           | Inti Pertanyaan                            |
| ---------------- | ------------------------------------------ |
| Dataset          | Data apa yang kita miliki?                 |
| Feature          | Informasi apa yang diberikan ke model?     |
| Target           | Apa yang ingin diprediksi?                 |
| Preprocessing    | Bagaimana membuat data siap digunakan?     |
| Algorithm        | Metode apa yang digunakan untuk belajar?   |
| Model            | Apa yang dihasilkan setelah training?      |
| Training         | Bagaimana model belajar?                   |
| Inference        | Bagaimana model digunakan untuk data baru? |
| Evaluation       | Seberapa baik model bekerja?               |
| Overfitting      | Apakah model terlalu menghafal data?       |
| Underfitting     | Apakah model terlalu sederhana?            |
| Hyperparameter   | Bagaimana konfigurasi model?               |
| Cross Validation | Seberapa konsisten performa model?         |
| Deployment       | Bagaimana model digunakan di dunia nyata?  |
| Monitoring       | Apakah model tetap bekerja dengan baik?    |
| MLOps            | Bagaimana lifecycle ML dikelola?           |

---

# 🎯 Inti Besarnya

Machine Learning bukan hanya:

```text
Dataset
   ↓
Model
   ↓
Prediction
```

Workflow yang lebih realistis adalah:

```text
          ┌──────────────┐
          │     Data     │
          └──────┬───────┘
                 ↓
        Data Understanding
                 ↓
        Data Preprocessing
                 ↓
       Feature Engineering
                 ↓
        Model Development
                 ↓
         Model Evaluation
                 ↓
       Hyperparameter Tuning
                 ↓
            Deployment
                 ↓
           Monitoring
                 ↓
          Retraining
                 │
                 └──────────→ ♻️
```

> **Prinsip penting:** Model Machine Learning yang bagus bukan hanya model dengan algoritma paling canggih, tetapi model yang mampu **menggeneralisasi dengan baik terhadap data yang belum pernah dilihat** dan memberikan nilai nyata pada masalah yang ingin diselesaikan.
