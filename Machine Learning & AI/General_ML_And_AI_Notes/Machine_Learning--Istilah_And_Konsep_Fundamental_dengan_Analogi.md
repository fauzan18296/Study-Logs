# 🤖 Machine Learning — Istilah & Konsep Fundamental

> 📚 Catatan ringkas untuk memahami istilah-istilah penting dalam **Machine Learning**, mulai dari data hingga MLOps.
>
> 💡 Setiap analogi di bawah ini adalah alat bantu memahami konsep, bukan definisi teknis yang harus dianggap identik sepenuhnya.

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

> 🧠 **Analogi:** Jika dataset adalah daftar seluruh peserta lomba, satu sample adalah satu peserta beserta informasi miliknya.

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

> 🧠 **Analogi:** Feature seperti petunjuk yang diberikan kepada detektif. Umur dan gaji adalah informasi yang bisa digunakan untuk memperkirakan apakah seseorang akan membeli produk.

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

> 🧠 **Analogi:** Jika feature adalah petunjuk dalam soal, target adalah jawaban yang ingin dipelajari model dari contoh-contoh sebelumnya.

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

> 🧠 **Analogi:** Class seperti pilihan kotak untuk memilah surat: setiap email dimasukkan ke kategori “Spam” atau “Bukan Spam”.

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

> 🧠 **Analogi:** Seperti formulir pendaftaran yang kolom nomor teleponnya kosong. Sebelum memakai formulir itu, kita perlu memutuskan apakah akan meminta data kembali, menghapus catatan, atau mengisi nilai pengganti yang masuk akal.

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

> 🧠 **Analogi:** Di antara orang-orang yang biasanya berjalan 10–18 menit ke kantor, seseorang yang membutuhkan 500 menit terlihat sangat berbeda. Namun, kita harus memeriksa penyebabnya—mungkin salah catat, mungkin juga memang ada kejadian khusus.

> ⚠️ Outlier tidak selalu berarti data salah. Bisa saja merupakan kejadian nyata yang memang jarang terjadi.

---

## Encoding

**Encoding** adalah proses mengubah data kategorikal menjadi representasi numerik agar dapat diproses oleh algoritma tertentu.

Contoh:

```text
Ya    → 1
Tidak → 0
```

> 🧠 **Analogi:** Encoding seperti memberi kode angka pada label warna agar mesin dapat memprosesnya. Kode itu harus dipilih hati-hati: angka 1 dan 0 tidak selalu berarti bahwa satu kategori “lebih besar” daripada kategori lain.

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

> 🧠 **Analogi:** Bayangkan membandingkan umur dalam satuan tahun dengan gaji dalam rupiah. Angka gaji jauh lebih besar hanya karena satuannya, bukan otomatis karena fiturnya lebih penting. Scaling membantu menyamakan skala, terutama untuk algoritma yang sensitif terhadapnya.

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

> 🧠 **Analogi:** Feature engineering seperti mengolah bahan mentah menjadi informasi yang lebih berguna. Daripada memberi model harga satuan dan jumlah barang saja, kita bisa membuat fitur total harga jika memang relevan.

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

> 🧠 **Analogi:** Feature selection seperti memilih petunjuk paling relevan untuk menyelesaikan misteri. Membawa semua informasi, termasuk yang tidak berguna atau berulang, bisa membuat proses lebih rumit.

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

> 🧠 **Analogi:** Training seperti mengajari siswa menggunakan banyak contoh soal beserta jawabannya. Model menyesuaikan diri agar dapat memprediksi jawaban untuk contoh baru.

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

> 🧠 **Analogi:** Regression seperti memperkirakan waktu perjalanan atau harga rumah. Hasilnya berupa angka yang bisa berada pada rentang nilai, bukan sekadar memilih kategori.

---

## Classification

Digunakan untuk memprediksi **kategori/class**.

Contoh:

```text
Email → Spam / Not Spam
```

> 🧠 **Analogi:** Classification seperti memilah surat ke kotak berlabel “Spam” dan “Bukan Spam”. Model memilih kelas yang paling sesuai berdasarkan pola yang dipelajarinya.

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

> 🧠 **Analogi:** Unsupervised learning seperti mengelompokkan buku di perpustakaan tanpa label kategori yang sudah disediakan. Kita mencari kemiripan atau struktur yang muncul dari data itu sendiri.

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

> 🧠 **Analogi:** Reinforcement learning seperti melatih robot bermain game. Tindakan yang menghasilkan reward positif cenderung dipelajari, sedangkan tindakan yang menghasilkan hasil buruk mendorong strategi berbeda.

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

> 🧠 **Analogi:** Algorithm adalah resep atau metode memasak, sedangkan model adalah hasil belajar dari bahan dan contoh yang digunakan. Resep yang sama bisa menghasilkan model berbeda jika data training-nya berbeda.

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

> 🧠 **Analogi:** Inference seperti memakai pengetahuan siswa setelah belajar untuk menjawab soal ujian baru. Proses ini menggunakan model yang sudah dilatih, bukan mengajarinya dari awal.

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

Cocok digunakan ketika distribusi class relatif seimbang dan kesalahan pada tiap kelas memiliki konsekuensi yang sebanding.

> 🧠 **Analogi:** Accuracy seperti nilai total ujian: jika 90 dari 100 jawaban benar, nilainya 90%. Namun, nilai total saja tidak menunjukkan jenis soal mana yang sering salah.

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

> 🧠 **Analogi:** Petugas keamanan yang menandai seseorang sebagai pelanggar harus cukup akurat. Precision mengukur, dari semua orang yang ditandai, berapa banyak yang benar-benar pelanggar.

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

> 🧠 **Analogi:** Tim pencarian bertugas menemukan semua orang yang hilang. Recall mengukur berapa banyak orang yang benar-benar dicari berhasil ditemukan, termasuk mereka yang mungkin terlewat.

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

> 🧠 **Analogi:** Bayangkan dua tugas: menemukan sebanyak mungkin kasus dan memastikan temuan itu benar. F1 merangkum keseimbangan keduanya; nilai yang sangat rendah pada salah satu sisi akan menekan skor gabungan.

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

> 🧠 **Analogi:** MAE seperti menghitung rata-rata jarak meleset dari tebakan harga rumah. Jika prediksi rata-rata meleset Rp20 juta, MAE menunjukkan besar kesalahan rata-rata dalam satuan harga.

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

> 🧠 **Analogi:** Jika dua prediksi meleset 2 dan 20 unit, MSE memberi bobot yang jauh lebih besar pada kesalahan 20 karena error dikuadratkan. Ini berguna ketika kesalahan besar ingin dihukum lebih berat.

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

Semakin kecil → semakin baik. RMSE menggunakan satuan yang sama dengan target, sehingga sering lebih mudah ditafsirkan daripada MSE.

> 🧠 **Analogi:** RMSE seperti ukuran rata-rata kesalahan yang lebih menonjolkan tebakan yang meleset jauh, tetapi hasil akhirnya kembali ke satuan asli, misalnya rupiah.

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

> 🧠 **Analogi:** Seperti siswa yang baru membaca sedikit materi dan belum mampu menjawab soal latihan maupun ujian. Model belum menangkap pola penting.

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

> 🧠 **Analogi:** Seperti siswa yang menghafal jawaban latihan sampai sangat lancar, tetapi bingung ketika soal sedikit diubah. Model terlalu menyesuaikan diri pada data training.

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

### 🧠 Analogi Hyperparameter

Hyperparameter seperti pengaturan cara belajar sebelum latihan dimulai: berapa banyak pohon yang dibuat, seberapa dalam pohon boleh tumbuh, atau seberapa besar langkah pembaruan. Pengaturan ini memengaruhi proses belajar, tetapi bukan jawaban yang langsung dipelajari sebagai parameter.

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

> 🧠 **Analogi:** Parameter seperti nilai yang dipelajari siswa selama latihan—model menyesuaikannya berdasarkan data.

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

> 🧠 **Analogi:** Bayangkan lima set soal latihan. Siswa berlatih dengan empat set lalu diuji pada set yang tersisa. Proses diulang sampai setiap set pernah menjadi bahan evaluasi. Ini membantu melihat apakah hasil model bergantung pada satu pembagian data saja.


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

> 🧠 **Analogi:** Bias tinggi seperti memakai aturan yang terlalu sederhana untuk semua kasus; variance tinggi seperti membuat aturan yang berubah drastis setiap kali contoh latihan berubah. Kita mencari keseimbangan agar aturan tetap cukup fleksibel, tetapi tidak terlalu sensitif.

Tujuannya adalah menemukan **tingkat kompleksitas yang memberikan generalisasi terbaik**.

---

# 10. 🚀 Istilah Dunia Kerja Machine Learning

## EDA — Exploratory Data Analysis

Proses mengeksplorasi dan memahami dataset sebelum modeling.

> 🧠 **Analogi:** EDA seperti memeriksa bahan sebelum memasak: melihat apakah ada bahan yang busuk, jumlahnya cukup, atau ada sesuatu yang tidak biasa. Tanpa pemeriksaan, kesalahan pada data bisa terbawa ke model.

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

> 🧠 **Analogi:** Pipeline seperti jalur produksi pabrik. Setiap produk melewati langkah yang sama dengan urutan yang konsisten, sehingga proses lebih mudah diulang dan mengurangi risiko langkah terlewat.

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

> 🧠 **Analogi:** Deployment seperti membuka restoran setelah resep diuji di dapur. Model tidak lagi hanya eksperimen di notebook, tetapi disediakan agar aplikasi atau pengguna bisa memakainya.

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

> 🧠 **Analogi:** Batch prediction seperti memproses satu tumpukan besar formulir pada akhir hari, bukan memproses setiap formulir tepat saat diterima.

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

> 🧠 **Analogi:** Real-time prediction seperti kasir yang memeriksa harga barang saat pelanggan memindai barang, lalu langsung memberikan hasil.

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

> 🧠 **Analogi:** Monitoring seperti memeriksa mesin setelah pabrik beroperasi. Mesin yang dulu berjalan baik tetap perlu diawasi karena beban, bahan, atau kondisi lingkungan dapat berubah.

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

> 🧠 **Analogi:** Model dilatih menggunakan pelanggan yang kebanyakan berusia 18–40 tahun, tetapi sekarang lebih banyak menerima pelanggan berusia 60–80 tahun. “Bahan masukan” yang diterima model telah berubah, walaupun penurunan performa belum tentu langsung terjadi.

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

> 🧠 **Analogi:** Dulu pelanggan membeli produk karena diskon, tetapi sekarang mereka lebih dipengaruhi biaya pengiriman. Hubungan antara petunjuk dan perilaku pembelian berubah, sehingga pola lama model mungkin tidak lagi cukup berguna.

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

> 🧠 **Analogi:** Experiment tracking seperti buku catatan laboratorium. Kita mencatat bahan, pengaturan, dan hasil setiap percobaan agar dapat membandingkan hasil serta mengulang eksperimen yang berhasil.

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

> 🧠 **Analogi:** MLOps seperti mengelola layanan restoran secara menyeluruh: bukan hanya membuat resep, tetapi juga memastikan pasokan bahan, proses dapur, pelayanan, pemeriksaan kualitas, dan perbaikan berkelanjutan berjalan baik.

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
