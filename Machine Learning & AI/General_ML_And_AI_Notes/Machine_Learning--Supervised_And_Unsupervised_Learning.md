# 🤖 Machine Learning: Supervised & Unsupervised Learning

> 📌 **Catatan Penting**
>
> Banyak pemula menganggap setiap algoritma Machine Learning hanya memiliki satu rumus matematika.
>
> Kenyataannya, sebagian besar algoritma dibangun dari kombinasi:
>
> * Aljabar
> * Aljabar Linear
> * Statistika
> * Probabilitas
> * Kalkulus
> * Optimisasi

---

# 🧠 Gambaran Besar Machine Learning

```text
Matematika Dasar
      ↓
Konsep Machine Learning
      ↓
Algoritma
      ↓
Model
      ↓
Prediksi
```

---

# 📚 1. Supervised Learning

## Apa itu Supervised Learning?

Supervised Learning adalah metode Machine Learning yang belajar dari data yang memiliki **label (target)**.

Contoh:

| Jam Belajar | Nilai |
| ----------- | ----- |
| 2           | 60    |
| 4           | 75    |
| 6           | 90    |

Model belajar hubungan:

```math
X \rightarrow y
```

Dimana:

* `X` = Feature / Input
* `y` = Target / Output

---

# 📈 A. Linear Regression

## Konsep

Digunakan untuk memprediksi nilai numerik.

Contoh:

* Harga rumah
* Pendapatan
* Suhu

Model mencari garis terbaik yang mewakili hubungan data.

### Persamaan Garis

```math
y = mx + b
```

Keterangan:

* `m` = slope (kemiringan)
* `b` = intercept (titik potong)

---

## Bentuk Machine Learning

```math
\hat{y}=w_1x_1+w_2x_2+\cdots+w_nx_n+b
```

Keterangan:

* `x` = fitur
* `w` = bobot (weight)
* `b` = bias
* `ŷ` = hasil prediksi

---

## Loss Function (MSE)

Mengukur seberapa besar kesalahan prediksi model.

```math
MSE=
\frac1n
\sum_{i=1}^{n}
(y_i-\hat y_i)^2
```

Semakin kecil MSE → semakin baik model.

---

## Gradient Descent

Digunakan untuk memperbarui bobot model.

```math
w=w-\alpha\frac{\partial J}{\partial w}
```

Keterangan:

* `α` = Learning Rate
* `J` = Cost Function

---

# 🎯 B. Logistic Regression

## Konsep

Digunakan untuk klasifikasi.

Contoh:

* Spam / Tidak Spam
* Lulus / Tidak Lulus
* Sakit / Tidak Sakit

---

## Fungsi Sigmoid

Mengubah nilai menjadi probabilitas.

```math
\sigma(z)=
\frac1{1+e^{-z}}
```

dimana:

```math
z=w^Tx+b
```

Output:

```math
0 \le P(y=1) \le 1
```

---

# 🌳 C. Decision Tree

## Konsep

Model membuat keputusan dengan serangkaian pertanyaan.

```text
Umur > 30 ?
│
├── Ya
└── Tidak
```

---

## Entropy

Mengukur ketidakpastian data.

```math
H(S)=
-\sum p_i \log_2(p_i)
```

Semakin kecil entropy → data semakin terpisah.

---

## Information Gain

Mengukur kualitas split.

```math
IG=
H(parent)-H(child)
```

---

# 🌲 D. Random Forest

## Konsep

Gabungan banyak Decision Tree.

```text
Tree 1
Tree 2
Tree 3
Tree 4
   ↓
 Voting
```

---

## Voting Klasifikasi

```math
\hat y=
mode(y_1,y_2,\ldots,y_n)
```

---

## Regresi

```math
\hat y=
\frac1n
\sum_{i=1}^{n}
y_i
```

---

# 📏 E. Support Vector Machine (SVM)

## Konsep

Mencari garis pemisah terbaik antar kelas.

---

## Hyperplane

```math
w^Tx+b=0
```

---

## Margin Maksimum

Tujuan SVM:

```math
\min
\frac12||w||^2
```

Semakin besar margin → semakin baik generalisasi.

---

# 👥 F. K-Nearest Neighbors (KNN)

## Konsep

Mencari tetangga terdekat.

```text
Data Baru
    ↓
Cari K Tetangga
    ↓
Voting
```

---

## Euclidean Distance

Mengukur jarak antar titik.

```math
d=
\sqrt{
(x_1-y_1)^2+
(x_2-y_2)^2+
\cdots+
(x_n-y_n)^2
}
```

---

# 🎲 G. Naive Bayes

## Konsep

Menggunakan probabilitas untuk melakukan prediksi.

---

## Bayes Theorem

```math
P(A|B)=
\frac{P(B|A)P(A)}
{P(B)}
```

---

## Dalam Machine Learning

```math
P(y|X)=
\frac{P(X|y)P(y)}
{P(X)}
```

---

# 📚 2. Unsupervised Learning

## Apa itu Unsupervised Learning?

Data tidak memiliki label.

Model mencari pola sendiri.

```math
X \rightarrow ?
```

---

# 🎯 A. K-Means Clustering

## Konsep

Mengelompokkan data berdasarkan kemiripan.

```text
Customer
   ↓
Cluster 1
Cluster 2
Cluster 3
```

---

## Centroid

Titik pusat cluster.

```math
\mu=
\frac1n
\sum_{i=1}^{n}x_i
```

---

## Objective Function

Meminimalkan jarak data ke centroid.

```math
J=
\sum_{i=1}^{k}
\sum_{x \in C_i}
||x-\mu_i||^2
```

---

# 🌳 B. Hierarchical Clustering

## Konsep

Membentuk struktur pohon (dendrogram).

```text
A
├── B
│   ├── C
│   └── D
```

---

## Single Linkage

```math
d(A,B)=
\min(d(x,y))
```

---

## Complete Linkage

```math
d(A,B)=
\max(d(x,y))
```

---

## Average Linkage

```math
d(A,B)=
\frac1{nm}
\sum d(x,y)
```

---

# 📍 C. DBSCAN

## Konsep

Mengelompokkan data berdasarkan kepadatan.

Parameter:

* eps
* min_samples

---

## Jarak Euclidean

```math
d(x,y)=
\sqrt{
\sum_{i=1}^{n}
(x_i-y_i)^2
}
```

---

# 📉 D. PCA (Principal Component Analysis)

## Konsep

Mengurangi jumlah fitur.

Contoh:

```text
100 Fitur
   ↓
10 Fitur
```

---

## Covariance

```math
Cov(X,Y)
=
\frac{
\sum
(X-\bar X)
(Y-\bar Y)
}
{n-1}
```

---

## Eigenvalue Problem

```math
Av=\lambda v
```

Keterangan:

* `A` = Matriks
* `v` = Eigenvector
* `λ` = Eigenvalue

---

# 🔔 E. Gaussian Mixture Model (GMM)

## Konsep

Menganggap data berasal dari beberapa distribusi Gaussian.

---

## Distribusi Gaussian

```math
f(x)=
\frac1{\sqrt{2\pi\sigma^2}}
e^{
-\frac{
(x-\mu)^2
}
{
2\sigma^2
}
}
```

---

# 🧮 Fondasi Matematika Machine Learning

| Bidang         | Digunakan Untuk           |
| -------------- | ------------------------- |
| Aljabar        | Persamaan dan fungsi      |
| Aljabar Linear | Vektor dan matriks        |
| Statistika     | Analisis data             |
| Probabilitas   | Ketidakpastian            |
| Kalkulus       | Turunan dan optimisasi    |
| Optimisasi     | Mencari parameter terbaik |
| Geometri       | Mengukur jarak            |
| Eigenvalue     | PCA dan Deep Learning     |

---

# 🚀 Roadmap Belajar yang Direkomendasikan

## Tahap 1 — Fondasi Matematika

1. Aljabar Dasar
2. Fungsi
3. Persamaan Linear
4. Vektor
5. Matriks

---

## Tahap 2 — Statistik

1. Mean
2. Median
3. Modus
4. Variance
5. Standard Deviation
6. Distribusi Data

---

## Tahap 3 — Probabilitas

1. Probabilitas Dasar
2. Conditional Probability
3. Bayes Theorem

---

## Tahap 4 — Kalkulus

1. Limit
2. Turunan
3. Gradient

---

## Tahap 5 — Machine Learning

1. Linear Regression
2. Logistic Regression
3. KNN
4. Decision Tree
5. Random Forest
6. SVM
7. K-Means
8. DBSCAN
9. PCA
10. Neural Network

---

# 🎯 Kesimpulan

Machine Learning bukan sekadar menghafal algoritma.

Yang paling penting adalah memahami fondasi matematika yang mendasarinya:

```text
Aljabar
   ↓
Statistika
   ↓
Probabilitas
   ↓
Kalkulus
   ↓
Optimisasi
   ↓
Machine Learning
```

Jika fondasi ini kuat, maka memahami algoritma baru akan menjadi jauh lebih mudah karena sebagian besar algoritma modern dibangun dari konsep matematika yang sama.
