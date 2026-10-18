# 📊 Panduan EDA, Distribusi Data, dan Deteksi Outlier

> **Tujuan catatan:** memahami data sebelum modeling, membaca distribusi dengan beberapa metode, mendeteksi kandidat outlier, memilih penanganan yang masuk akal, dan menuliskan kesimpulan EDA yang dapat dipertanggungjawabkan.
>
> **Prinsip utama:** EDA bukan sekadar menjalankan fungsi atau membuat grafik. EDA adalah proses mengumpulkan bukti untuk memahami data dan mengambil keputusan yang tepat.

---

## 🧭 Daftar Isi

1. [Peta Besar EDA](#-1-peta-besar-eda)
2. [Mengapa EDA Awal Penting?](#-2-mengapa-eda-awal-penting)
3. [Memahami Fungsi EDA Awal](#-3-memahami-fungsi-eda-awal)
4. [Memahami `describe()`](#-4-memahami-describe)
5. [Apa Itu Distribusi Data?](#-5-apa-itu-distribusi-data)
6. [Metode Analisis Distribusi](#-6-metode-analisis-distribusi)
7. [Memahami Outlier](#-7-memahami-outlier)
8. [Metode Deteksi Outlier](#-8-metode-deteksi-outlier)
9. [Perbandingan Metode Outlier](#-9-perbandingan-metode-outlier)
10. [Cara Menangani Outlier](#-10-cara-menangani-outlier)
11. [Apakah `describe()` Tetap Dibutuhkan?](#-11-apakah-describe-tetap-dibutuhkan)
12. [Alur EDA dari Awal sampai Akhir](#-12-alur-eda-dari-awal-sampai-akhir)
13. [EDA dan Machine Learning](#-13-eda-dan-machine-learning)
14. [Template Kode EDA](#-14-template-kode-eda)
15. [Template Narasi Laporan](#-15-template-narasi-laporan)
16. [Checklist EDA](#-16-checklist-eda)
17. [Latihan Pemahaman](#-17-latihan-pemahaman)
18. [Ringkasan Prinsip](#-18-ringkasan-prinsip)

---

## 🗺️ 1. Peta Besar EDA

EDA (*Exploratory Data Analysis*) adalah proses memeriksa, meringkas, dan memvisualisasikan data untuk memahami kualitas, pola, hubungan, dan potensi masalah sebelum analisis lanjutan atau modeling.

Secara umum, EDA mencakup:

| Tahap | Pertanyaan utama | Contoh alat |
|---|---|---|
| Memahami struktur | Seberapa besar data? Apa tipe setiap kolom? | `shape`, `head()`, `info()` |
| Memahami kualitas | Apakah ada nilai hilang, duplikasi, atau nilai tidak valid? | `isna()`, `duplicated()`, `unique()` |
| Memahami statistik | Di mana pusat dan seberapa besar penyebaran data? | `describe()`, mean, median, std |
| Memahami distribusi | Bagaimana nilai tersebar dan apa bentuknya? | Histogram, KDE, ECDF |
| Mendeteksi kandidat anomali | Nilai mana yang tidak biasa? | Boxplot, IQR, Z-score, MAD, Isolation Forest, LOF |
| Memahami hubungan | Apakah fitur saling berhubungan? | Scatter plot, korelasi, analisis per kelompok |
| Mengambil keputusan | Apakah data perlu diperbaiki, ditransformasi, atau dipertahankan? | Investigasi konteks dan evaluasi |

### Analogi: pemeriksaan dokter

Bayangkan kamu adalah dokter yang menerima pasien. Sebelum menentukan pengobatan, kamu perlu memeriksa kondisi dasar, melihat gejala, melakukan tes, lalu menafsirkan hasilnya.

EDA juga demikian:

- `shape` dan `info()` seperti pemeriksaan awal.
- `describe()` seperti ringkasan hasil pengukuran.
- Grafik distribusi seperti melihat pola gejala.
- Deteksi outlier seperti menemukan hasil pemeriksaan yang tidak biasa.
- Investigasi sumber data seperti mencari penyebabnya.
- Penanganan data seperti menentukan tindakan berdasarkan bukti.

**Jangan langsung “memberi obat” dengan menghapus data hanya karena suatu nilai terlihat aneh.**

---

## 🔎 2. Mengapa EDA Awal Penting?

Sebelum membangun model, kita perlu memahami apa yang sebenarnya ada di dalam dataset.

Misalnya, tugas kita adalah memprediksi apakah pelanggan akan berhenti berlangganan (*churn*). Sebelum modeling, kita perlu mengetahui:

- Berapa banyak baris dan fitur?
- Apakah target tersedia?
- Apakah tipe data sudah benar?
- Apakah ada missing value?
- Apakah terdapat duplikasi?
- Apakah distribusi fitur masuk akal?
- Apakah terdapat nilai ekstrem?
- Apakah suatu kolom hanya berfungsi sebagai identitas?
- Apakah ada potensi *data leakage*?

EDA awal membantu menghindari keputusan yang dibuat berdasarkan asumsi tanpa bukti.

> **Catatan:** tidak semua fungsi harus dijalankan secara mekanis pada setiap dataset. Pilih pemeriksaan berdasarkan struktur data, tujuan analisis, dan risiko yang relevan. Namun, pemeriksaan dasar biasanya menjadi titik awal yang baik.

---

## 🧰 3. Memahami Fungsi EDA Awal

### 3.1 `df.shape` — ukuran dataset

```python
print(df.shape)
```

Misalnya, hasilnya:

```text
(1000, 12)
```

Artinya terdapat 1.000 baris dan 12 kolom.

- Baris biasanya mewakili observasi.
- Kolom biasanya mewakili variabel atau fitur.

**Pertanyaan analisis:**

- Apakah jumlah observasi cukup untuk tujuan analisis?
- Apakah ada kolom yang tidak dibutuhkan?
- Apakah jumlah baris sesuai dengan ekspektasi sumber data?

**Analogi:** menghitung berapa orang yang datang ke sebuah kelas dan berapa informasi yang dicatat untuk setiap orang.

### 3.2 `df.head()` — melihat contoh isi data

```python
print(df.head())
```

Secara default, fungsi ini menampilkan lima baris pertama.

**Tujuan:**

- Memahami bentuk data sebenarnya.
- Memeriksa nama kolom.
- Melihat apakah ada nilai yang tampak tidak konsisten.
- Menemukan indikasi format yang tidak sesuai.

`head()` hanya menunjukkan sebagian kecil data. Jangan menyimpulkan seluruh dataset berdasarkan lima baris pertama saja.

### 3.3 `df.info()` — memeriksa struktur dan tipe data

```python
df.info()
```

Fungsi ini memberikan informasi tentang:

- Nama kolom.
- Jumlah nilai non-null.
- Tipe data.
- Penggunaan memori.

Contoh masalah: `Age` bertipe `object`, padahal seharusnya numerik. Kemungkinan isinya berupa angka yang tersimpan sebagai teks atau terdapat nilai seperti `"unknown"`.

**Pertanyaan analisis:** apakah tipe data sesuai dengan makna variabel?

### 3.4 `df.describe()` — ringkasan statistik

```python
print(df.describe())
```

Secara default, `describe()` merangkum kolom numerik. Untuk kolom kategorikal:

```python
print(df.describe(include="object"))
```

Fungsi ini membantu memeriksa pusat data, penyebaran, rentang, dan kuartil. Namun, `describe()` tidak menjelaskan seluruh bentuk distribusi dan tidak dapat menentukan apakah suatu nilai ekstrem merupakan kesalahan.

### 3.5 Missing value

```python
print(df.isna().sum())
```

Menghitung jumlah nilai yang hilang pada setiap kolom.

Persentase missing value:

```python
missing_pct = df.isna().mean() * 100
print(missing_pct.sort_values(ascending=False))
```

**Pertanyaan analisis:**

- Berapa banyak nilai yang hilang?
- Berapa persentasenya?
- Apakah nilai hilang terjadi secara acak atau memiliki pola?
- Apakah nilai tersebut dapat dipulihkan dari sumber lain?
- Apakah imputasi, indikator missing, atau penghapusan dapat dibenarkan?

Tidak ada ambang universal bahwa kolom dengan missing value lebih dari persentase tertentu harus otomatis dihapus. Keputusan bergantung pada nilai informasinya, mekanisme missing, dan tujuan analisis.

### 3.6 Duplikasi

```python
print(df.duplicated().sum())
```

Menghitung baris yang duplikat berdasarkan seluruh kolom secara default.

**Penting:** baris yang tampak sama belum tentu duplikasi yang salah. Dalam data transaksi, dua transaksi yang kebetulan memiliki nilai sama dapat menjadi kejadian yang berbeda. Periksa definisi satu observasi dan kunci unik terlebih dahulu.

### 3.7 Nilai unik dan kategori

```python
print(df["Status"].value_counts(dropna=False))
print(df["Status"].unique())
```

Berguna untuk memeriksa kategori yang tidak konsisten, salah ketik, kategori langka, atau nilai yang tidak diharapkan.

### 3.8 Contoh kode EDA awal

```python
import pandas as pd
import numpy as np

df = pd.read_csv("customer.csv")

print("Shape:", df.shape)
print(df.head())
df.info()

print("\nStatistik numerik:")
print(df.describe())

print("\nStatistik kategorikal:")
print(df.describe(include="object"))

print("\nMissing value:")
print(df.isna().sum())

print("\nPersentase missing:")
print((df.isna().mean() * 100).sort_values(ascending=False))

print("\nDuplikasi baris:", df.duplicated().sum())
```

---

## 🧮 4. Memahami `describe()`

Misalkan data pendapatan bulanan (juta rupiah) adalah:

```python
income = [2, 3, 3, 4, 4, 5, 5, 6, 8, 20]
```

Ringkasan statistik menjelaskan aspek yang berbeda.

| Statistik | Makna | Cara membaca |
|---|---|---|
| `count` | Jumlah nilai yang tersedia | Berapa observasi valid? |
| `mean` | Rata-rata | Jumlah seluruh nilai dibagi jumlah observasi |
| `std` | Simpangan baku sampel di Pandas | Seberapa tersebar nilai terhadap rata-rata? |
| `min` | Nilai terkecil | Apakah nilai minimum masuk akal? |
| `25%` | Kuartil pertama, Q1 | Batas seperempat bagian bawah |
| `50%` | Median, Q2 | Titik tengah data terurut |
| `75%` | Kuartil ketiga, Q3 | Batas tiga perempat bagian bawah |
| `max` | Nilai terbesar | Apakah nilai maksimum masuk akal? |

### 4.1 Mean dan median

Mean:

$$
\bar{x} = \frac{1}{n}\sum_{i=1}^{n}x_i
$$

Median adalah nilai tengah setelah data diurutkan. Jika jumlah observasi genap, median biasanya merupakan rata-rata dua nilai tengah.

Pada contoh pendapatan di atas, mean adalah 6 juta dan median 4,5 juta.

Nilai 20 menarik mean ke atas. Median lebih tahan terhadap pengaruh nilai ekstrem.

**Analogi nilai ujian:** lima siswa memperoleh 60, 65, 70, 75, dan 100.

- Mean = 74.
- Median = 70.

Jika nilai 100 ternyata salah input menjadi 500, mean berubah drastis sedangkan median tetap 70.

**Cara menafsirkan:**

- Mean jauh di atas median: petunjuk potensial distribusi menceng ke kanan.
- Mean jauh di bawah median: petunjuk potensial distribusi menceng ke kiri.
- Mean dekat median: bisa konsisten dengan distribusi simetris, tetapi tidak membuktikan simetri.

### 4.2 Simpangan baku (`std`)

Simpangan baku mengukur penyebaran nilai terhadap rata-rata.

$$
s = \sqrt{\frac{\sum_{i=1}^{n}(x_i-\bar{x})^2}{n-1}}
$$

Dalam Pandas, `Series.std()` secara default menggunakan `ddof=1`, yaitu simpangan baku sampel.

- `std` kecil: nilai relatif terkumpul di sekitar mean.
- `std` besar: nilai lebih tersebar terhadap mean.

`std` yang besar bukan bukti otomatis adanya outlier. Distribusi yang lebar juga dapat memiliki simpangan baku besar.

### 4.3 Kuartil dan IQR

- Q1: persentil ke-25.
- Q2: median atau persentil ke-50.
- Q3: persentil ke-75.

IQR (*Interquartile Range*) mengukur rentang 50% data tengah:

$$
IQR = Q_3 - Q_1
$$

IQR relatif tahan terhadap nilai ekstrem dibandingkan range atau simpangan baku.

**Catatan:** metode interpolasi kuartil dapat berbeda antarperangkat lunak. Gunakan hasil kuartil dari implementasi yang benar-benar dipakai saat menghitung batas IQR.

---

## 📈 5. Apa Itu Distribusi Data?

Distribusi data menjelaskan bagaimana nilai suatu variabel tersebar: nilai yang sering muncul, pusat, variasi, kemencengan, ekor, dan kemungkinan beberapa kelompok.

Misalnya, rata-rata tinggi badan mahasiswa adalah 168 cm. Informasi itu saja belum menjelaskan apakah kebanyakan mahasiswa berada dekat 168 cm, apakah ada kelompok berbeda, atau apakah terdapat nilai yang tidak masuk akal.

### Empat karakteristik utama distribusi

#### A. Bentuk (*shape*)

Distribusi bisa simetris, menceng ke kiri, menceng ke kanan, atau memiliki beberapa puncak.

#### B. Penyebaran (*spread*)

Apakah nilai terkumpul rapat atau tersebar jauh? Ukurannya antara lain range, IQR, dan standar deviasi.

Range:

$$
\text{Range} = x_{\max} - x_{\min}
$$

#### C. Kemencengan (*skewness*)

Skewness menggambarkan ketidaksimetrian distribusi.

- Skewness positif: ekor relatif memanjang ke kanan.
- Skewness negatif: ekor relatif memanjang ke kiri.
- Skewness dekat nol: tidak menunjukkan kemencengan yang kuat, tetapi tidak menjamin distribusi normal.

#### D. Puncak (*modality*)

- Unimodal: satu puncak utama.
- Bimodal: dua puncak utama.
- Multimodal: lebih dari dua puncak utama.

Beberapa puncak dapat mengindikasikan populasi atau kelompok berbeda, tetapi dapat juga muncul akibat ukuran sampel, noise, atau pilihan parameter visualisasi.

> **Penting:** distribusi tidak harus mengikuti kurva lonceng. Pendapatan, durasi, harga rumah, jumlah transaksi, dan probabilitas dapat memiliki bentuk yang berbeda.

---

## 📊 6. Metode Analisis Distribusi

Tidak ada satu metode yang menjawab semua pertanyaan. Gabungkan statistik numerik dan visualisasi.

### 6.1 Histogram

**Pertanyaan:** bagaimana frekuensi nilai tersebar?

Histogram membagi nilai numerik ke dalam interval (*bins*) dan menunjukkan jumlah observasi di setiap interval.

```python
import matplotlib.pyplot as plt

df["Income"].hist(bins=20)
plt.xlabel("Pendapatan")
plt.ylabel("Frekuensi")
plt.title("Distribusi Pendapatan")
plt.show()
```

**Cara menganalisis:**

1. Cari rentang dengan frekuensi tertinggi.
2. Perhatikan apakah ada ekor panjang ke salah satu sisi.
3. Amati celah atau beberapa puncak.
4. Ubah jumlah `bins` jika grafik terlalu kasar atau terlalu terpecah.
5. Cocokkan bentuk grafik dengan mean, median, kuartil, dan nilai ekstrem.

**Analogi:** mengelompokkan mahasiswa berdasarkan tinggi badan ke interval 150–159 cm, 160–169 cm, dan seterusnya.

**Keterbatasan:** bentuk histogram bergantung pada lebar dan batas bin. Puncak kecil tidak otomatis menunjukkan kelompok yang benar-benar berbeda.

### 6.2 KDE (*Kernel Density Estimation*)

**Pertanyaan:** bagaimana estimasi kepadatan data berubah secara halus?

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.kdeplot(data=df, x="Income")
plt.title("KDE Pendapatan")
plt.show()
```

**Cara menganalisis:**

- Puncak kurva menunjukkan area dengan kepadatan relatif tinggi.
- Ekor panjang dapat menunjukkan kemencengan.
- Beberapa puncak dapat mengisyaratkan kelompok berbeda.

**Analogi:** histogram seperti memasukkan orang ke kotak-kotak tinggi badan; KDE seperti melihat kerumunan tersebut sebagai permukaan halus.

**Keterbatasan:** KDE adalah estimasi, bukan distribusi sebenarnya yang diketahui secara pasti. Parameter *bandwidth* dapat mengubah kehalusan dan jumlah puncak yang terlihat. KDE juga perlu ditafsirkan hati-hati pada data diskret atau data yang memiliki batas alami.

### 6.3 Boxplot

**Pertanyaan:** di mana pusat, rentang tengah, dan kandidat outlier?

```python
sns.boxplot(data=df, x="Income")
plt.title("Boxplot Pendapatan")
plt.show()
```

Boxplot memperlihatkan median, Q1, Q3, IQR, whisker, dan titik di luar whisker.

Dengan aturan boxplot standar, whisker biasanya menjangkau nilai terjauh yang masih berada di dalam batas:

$$
L = Q_1 - 1.5(IQR)
$$

$$
U = Q_3 + 1.5(IQR)
$$

**Cara menganalisis:**

- Garis di dalam kotak: median.
- Batas bawah dan atas kotak: Q1 dan Q3.
- Kotak panjang: IQR besar.
- Median tidak berada di tengah kotak: kemungkinan ketidaksimetrian.
- Titik di luar whisker: kandidat outlier menurut aturan tersebut.

**Analogi:** mengurutkan nilai ujian siswa dan melihat rentang 50% siswa yang berada di bagian tengah distribusi.

**Keterbatasan:** boxplot ringkas, tetapi tidak menunjukkan seluruh detail bentuk distribusi atau banyaknya puncak.

### 6.4 Mean, median, dan skewness

```python
s = df["Income"].dropna()

print("Mean:", s.mean())
print("Median:", s.median())
print("Skewness:", s.skew())
```

Skewness sampel dapat membantu mengukur kemencengan. Nilai positif mengindikasikan kemencengan ke kanan, sedangkan nilai negatif mengindikasikan kemencengan ke kiri.

**Cara menganalisis:**

- Bandingkan mean dengan median.
- Periksa tanda dan besar skewness.
- Cocokkan dengan histogram dan KDE.
- Jangan menentukan bentuk distribusi hanya dari satu angka.

### 6.5 ECDF (*Empirical Cumulative Distribution Function*)

**Pertanyaan:** berapa proporsi observasi yang nilainya kurang dari atau sama dengan suatu batas?

```python
sns.ecdfplot(data=df, x="Income")
plt.title("ECDF Pendapatan")
plt.show()
```

ECDF menunjukkan proporsi kumulatif observasi hingga suatu nilai.

Secara matematis:

$$
F_n(x) = \frac{1}{n}\sum_{i=1}^{n} I(X_i \leq x)
$$

Di sini, \(I(X_i \leq x)\) bernilai 1 jika observasi memenuhi kondisi dan 0 jika tidak.

**Contoh:** jika ECDF bernilai 0,8 pada pendapatan Rp8 juta, sekitar 80% observasi memiliki pendapatan kurang dari atau sama dengan Rp8 juta.

**Analogi:** menjawab pertanyaan, “Berapa persen pelanggan berpendapatan maksimal Rp8 juta?”

**Kelebihan:** tidak perlu memilih lebar bin seperti histogram.

### 6.6 Cara menggabungkan metode distribusi

Misalnya:

- `describe()` menunjukkan mean lebih tinggi daripada median.
- Histogram memperlihatkan ekor kanan yang panjang.
- KDE menunjukkan kepadatan utama dan ekor kanan.
- Boxplot menunjukkan beberapa titik di luar whisker.

**Kesimpulan sementara:** distribusi mungkin menceng ke kanan dan memiliki kandidat outlier.

**Belum boleh disimpulkan:** semua kandidat outlier adalah kesalahan data atau harus dihapus.

---

## 🚩 7. Memahami Outlier

Outlier adalah observasi yang berbeda secara mencolok dari sebagian besar data berdasarkan suatu kriteria statistik, pola, atau model tertentu.

Contoh nilai transaksi (juta rupiah):

```python
transactions = [2, 3, 3, 4, 4, 5, 6, 7, 8, 100]
```

Nilai 100 jauh lebih besar dari sebagian besar nilai lainnya. Namun, ada beberapa kemungkinan:

1. Kesalahan input: seharusnya 10, tetapi tercatat 100.
2. Transaksi valid: pelanggan besar melakukan pembelian 100.
3. Peristiwa langka: terjadi promosi atau transaksi khusus.
4. Proses berbeda: transaksi perusahaan dan ritel tercampur.

### Deteksi bukan penanganan

- **Deteksi:** menandai nilai yang tidak biasa berdasarkan aturan.
- **Investigasi:** mencari penyebab dan memeriksa sumber.
- **Keputusan:** memilih tindakan berdasarkan bukti dan tujuan analisis.

**Analogi detektif:** menemukan sidik jari yang berbeda bukan berarti sidik jari tersebut harus dihapus. Ia harus diperiksa karena bisa jadi justru merupakan bukti penting.

---

## 🧪 8. Metode Deteksi Outlier

### 8.1 IQR (*Interquartile Range*)

IQR menggunakan kuartil dan tidak mengharuskan data berdistribusi normal.

$$
IQR = Q_3 - Q_1
$$

Batas bawah dan atas:

$$
L = Q_1 - 1.5(IQR)
$$

$$
U = Q_3 + 1.5(IQR)
$$

Nilai di bawah \(L\) atau di atas \(U\) ditandai sebagai kandidat outlier.

**Contoh:**

```python
values = [2, 3, 3, 4, 4, 5, 6, 7, 8, 100]
s = pd.Series(values)

q1 = s.quantile(0.25)
q3 = s.quantile(0.75)
iqr = q3 - q1

lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

mask = (s < lower) | (s > upper)

print("Q1:", q1)
print("Q3:", q3)
print("IQR:", iqr)
print("Batas bawah:", lower)
print("Batas atas:", upper)
print("Kandidat:", s[mask].tolist())
```

Untuk ilustrasi manual dengan metode median dari separuh data, Q1 = 3 dan Q3 = 7 sehingga IQR = 4 dan batas atas = 13. Implementasi kuartil berbasis interpolasi dapat menghasilkan nilai sedikit berbeda. Gunakan hasil aktual dari kode yang kamu jalankan.

**Kapan cocok?**

- Pemeriksaan awal fitur numerik.
- Data tidak harus normal.
- Membutuhkan aturan sederhana yang mudah dijelaskan.

**Keterbatasan:** IQR tidak mengetahui konteks bisnis. Nilai besar yang sah tetap dapat ditandai.

### 8.2 Z-score

Z-score mengukur jarak nilai dari rata-rata dalam satuan simpangan baku.

$$
z_i = \frac{x_i - \mu}{\sigma}
$$

Keterangan:

- \(x_i\): nilai observasi.
- \(\mu\): rata-rata.
- \(\sigma\): simpangan baku populasi atau estimasi simpangan baku yang digunakan.

Contoh: rata-rata tinggi 170 cm, simpangan baku 5 cm, dan nilai 185 cm:

$$
z = \frac{185-170}{5} = 3
$$

Nilai tersebut berada tiga simpangan baku di atas rata-rata.

Aturan praktis yang sering dipakai adalah \(|z| > 3\), tetapi ini bukan aturan universal.

```python
s = df["Height"]

mean = s.mean()
std = s.std()

if std > 0:
    z_scores = (s - mean) / std
    mask = z_scores.abs() > 3
    print(df.loc[mask, ["Height"]])
else:
    print("Standar deviasi nol; Z-score tidak dapat digunakan.")
```

**Kapan cocok?** Ketika distribusi cukup mendekati normal dan jarak dari rata-rata relevan.

**Keterbatasan:**

- Mean dan standar deviasi sensitif terhadap outlier.
- Data yang sangat menceng dapat menghasilkan interpretasi yang menyesatkan.
- Observasi di luar tiga simpangan baku tidak otomatis merupakan kesalahan.

### 8.3 MAD (*Median Absolute Deviation*)

MAD mengukur median penyimpangan absolut dari median dan relatif tahan terhadap nilai ekstrem.

$$
MAD = \operatorname{median}(|x_i-\tilde{x}|)
$$

Robust Z-score yang umum digunakan:

$$
z_{\text{robust}} =
\frac{0.6745(x_i-\tilde{x})}{MAD}
$$

Nilai dengan:

$$
|z_{\text{robust}}| > 3.5
$$

kadang ditandai sebagai kandidat outlier. Ambang tersebut merupakan pedoman, bukan hukum universal.

```python
s = df["Transaction"].dropna()

median = s.median()
mad = (s - median).abs().median()

if mad > 0:
    robust_z = 0.6745 * (s - median) / mad
    mask = robust_z.abs() > 3.5
    print(s[mask])
else:
    print("MAD = 0; periksa distribusi dan gunakan metode alternatif.")
```

**Kapan cocok?** Saat data menceng atau nilai ekstrem dapat mengganggu mean dan standar deviasi.

**Keterbatasan:** jika banyak nilai identik, MAD bisa bernilai nol sehingga rumus di atas tidak dapat langsung dipakai.

### 8.4 Metode visual

Gunakan visualisasi untuk membantu investigasi:

- Histogram: apakah nilai ekstrem berada di ekor?
- Boxplot: nilai mana di luar whisker?
- Scatter plot: apakah observasi menyimpang dari pola hubungan dua fitur?

```python
fig, axes = plt.subplots(1, 2, figsize=(12, 4))

sns.histplot(df["Transaction"], ax=axes[0])
axes[0].set_title("Distribusi transaksi")

sns.boxplot(x=df["Transaction"], ax=axes[1])
axes[1].set_title("Kandidat outlier")

plt.tight_layout()
plt.show()
```

Jika nilai ekstrem sangat besar, grafik berskala linear dapat membuat sebagian besar data tampak menumpuk dekat nol. Skala log dapat membantu jika sesuai, tetapi interpretasi harus tetap mempertimbangkan konteks.

### 8.5 Isolation Forest

Isolation Forest merupakan metode berbasis pohon yang mencoba mengisolasi observasi. Observasi yang lebih mudah diisolasi cenderung diberi skor anomali lebih tinggi.

```python
from sklearn.ensemble import IsolationForest

features = ["Age", "Income", "MonthlySpend"]
X = df[features].dropna()

model = IsolationForest(
    contamination=0.02,
    random_state=42
)

labels = model.fit_predict(X)

# -1 = kandidat anomali, 1 = kandidat normal
anomaly_mask = labels == -1

print("Jumlah kandidat:", anomaly_mask.sum())
print(X.loc[anomaly_mask])
```

**Catatan:** `contamination=0.02` digunakan dalam penentuan ambang dengan perkiraan proporsi pencilan sebesar 2%. Ini bukan bukti bahwa 2% data benar-benar salah.

Metode ini tidak memahami konteks bisnis. Periksa kandidat yang dihasilkan sebelum mengambil keputusan.

### 8.6 Local Outlier Factor (LOF)

LOF membandingkan kepadatan lokal suatu observasi dengan kepadatan tetangganya. Observasi yang jauh lebih jarang dibandingkan lingkungan lokalnya dapat ditandai sebagai anomali.

Contoh:

```python
from sklearn.neighbors import LocalOutlierFactor

features = ["Age", "Income", "MonthlySpend"]
X = df[features].dropna()

lof = LocalOutlierFactor(
    n_neighbors=20,
    contamination=0.02
)

labels = lof.fit_predict(X)

# -1 = kandidat anomali, 1 = kandidat normal
anomaly_mask = labels == -1

print("Jumlah kandidat:", anomaly_mask.sum())
print(X.loc[anomaly_mask])
```

**Kapan cocok?** Saat anomali bersifat lokal, misalnya sebuah titik yang tampak normal secara global tetapi tidak biasa di lingkungan tetangganya.

**Keterbatasan:**

- Skala fitur dapat memengaruhi hasil.
- Jumlah tetangga perlu dipilih sesuai struktur data.
- Struktur kelompok yang berbeda dapat memengaruhi kepadatan.
- Skor atau label anomali bukan bukti kesalahan.

Untuk fitur dengan skala yang berbeda jauh, pertimbangkan preprocessing yang sesuai dan lakukan fit terhadap transformasi hanya pada data latih jika digunakan dalam pipeline prediksi.

---

## ⚖️ 9. Perbandingan Metode Outlier

| Metode | Dasar | Kelebihan | Keterbatasan |
|---|---|---|---|
| IQR | Kuartil dan rentang tengah | Sederhana, relatif robust | Dapat menandai nilai ekstrem yang valid |
| Z-score | Mean dan standar deviasi | Mudah diinterpretasikan pada data mendekati normal | Sensitif terhadap pencilan dan kemencengan |
| MAD | Median dan deviasi absolut | Robust terhadap nilai ekstrem | Dapat bernilai nol |
| Histogram / boxplot | Pola visual | Mudah untuk pemeriksaan awal | Dipengaruhi pilihan visualisasi |
| Isolation Forest | Kemudahan isolasi | Dapat memeriksa banyak fitur | Hasil dipengaruhi parameter dan struktur data |
| LOF | Kepadatan lokal | Bisa menangkap anomali lokal | Sensitif terhadap skala dan jumlah tetangga |

> **Jangan memilih metode karena mendeteksi outlier paling banyak.** Pilih berdasarkan karakteristik data, tujuan analisis, dan konsekuensi kesalahan keputusan.

---

## 🛠️ 10. Cara Menangani Outlier

Deteksi dan penanganan adalah dua tahap berbeda.

Misalnya, dari 1.000 transaksi ditemukan 20 kandidat outlier. Jumlah itu tidak berarti 20 baris harus dihapus.

Sebelum memilih tindakan, tanyakan:

1. Apakah nilai valid menurut domain atau bisnis?
2. Apakah nilai merupakan kesalahan pencatatan, kejadian langka, atau kelompok berbeda?
3. Apa konsekuensi jika nilai dipertahankan atau diubah?
4. Apakah keputusan tersebut sesuai dengan tujuan model?

### 10.1 Mempertahankan data

Gunakan jika nilai ekstrem terbukti valid dan penting bagi masalah.

**Contoh:** pendapatan pelanggan perusahaan memang jauh lebih tinggi daripada pelanggan ritel. Menghapusnya dapat membuat model kurang memahami pelanggan bernilai tinggi.

### 10.2 Memperbaiki kesalahan data

Gunakan jika ada bukti kuat bahwa nilai salah, misalnya satuan atau format input tidak sesuai dokumentasi.

Perbaiki dari sumber tepercaya jika memungkinkan. Jangan menebak nilai benar hanya karena nilainya ekstrem.

### 10.3 Transformasi

Transformasi logaritmik dapat mengurangi kemencengan dan mengecilkan rentang nilai besar.

```python
df["Income_log"] = np.log1p(df["Income"])
```

Untuk `log1p(x)`, nilai harus lebih besar dari -1. Transformasi ini cocok untuk pendapatan nonnegatif, tetapi tidak otomatis sesuai untuk semua variabel.

**Penting:** transformasi tidak menghapus observasi ekstrem. Transformasi mengubah skala nilai.

### 10.4 Capping atau winsorization

Capping membatasi nilai di luar ambang tertentu.

```python
lower = df["Income"].quantile(0.01)
upper = df["Income"].quantile(0.99)

df["Income_capped"] = df["Income"].clip(
    lower=lower,
    upper=upper
)
```

Dalam contoh ini, nilai di bawah persentil pertama atau di atas persentil ke-99 dibatasi.

**Konsekuensi:** beberapa nilai berbeda menjadi sama dengan batasnya, sehingga informasi tentang besarnya nilai ekstrem berkurang.

Jika digunakan untuk modeling, pelajari batas dari data latih saja, lalu terapkan batas yang sama ke data validasi dan uji.

### 10.5 Menghapus observasi

Penghapusan layak dipertimbangkan jika ada bukti bahwa observasi tidak valid dan tidak dapat diperbaiki, atau memang tidak memenuhi kriteria populasi penelitian.

Contoh: usia tercatat 250 tahun karena kesalahan input yang terkonfirmasi.

Jangan menghapus baris hanya karena melewati batas IQR atau Z-score.

### 10.6 Simulasi keputusan

Data transaksi: Rp2 juta, Rp3 juta, Rp4 juta, Rp5 juta, dan Rp500 juta.

Jika Rp500 juta ditandai sebagai outlier oleh IQR, langkah pertama yang paling masuk akal adalah memeriksa sumber, satuan, dan konteks transaksi.

- Jika kesalahan input terkonfirmasi, perbaiki berdasarkan sumber yang benar.
- Jika transaksi valid, pertimbangkan mempertahankannya.
- Jika valid tetapi sangat memengaruhi model, uji pendekatan alternatif seperti transformasi atau capping hanya jika dapat dibenarkan oleh tujuan analisis.

---

## 🧾 11. Apakah `describe()` Tetap Dibutuhkan?

**Ya, jika ringkasan numeriknya membantu menjawab pertanyaan analisis. Namun, tidak semua metode membutuhkan `describe()` secara langsung.**

| Metode | Peran `describe()` | Apa yang tetap harus diperiksa? |
|---|---|---|
| Histogram | Memberi konteks pusat, rentang, dan kuartil | Bentuk, ekor, celah, puncak |
| KDE | Membantu menafsirkan pusat dan rentang | Bentuk kurva, puncak, bandwidth |
| Boxplot | Sangat relevan untuk kuartil dan median | Whisker dan titik di luarnya |
| ECDF | Opsional sebagai ringkasan tambahan | Proporsi pada nilai atau ambang tertentu |
| IQR | Kuartil diperlukan | Batas bawah/atas dan kandidat |
| Z-score | Mean dan standar deviasi diperlukan | Nilai Z-score dan kesesuaian asumsi |
| MAD | Median diperlukan; `describe()` tidak memberi MAD langsung | Nilai MAD dan apakah MAD nol |
| Isolation Forest | Tidak wajib | Skor, parameter, kandidat, konteks multivariat |
| LOF | Tidak wajib | Kepadatan lokal, skala, jumlah tetangga |

### Mengapa `describe()` tidak cukup?

`describe()` standar menjelaskan setiap kolom secara terpisah (*univariate summary*). Ia tidak menunjukkan seluruh bentuk distribusi atau hubungan antarfitur.

Contoh: usia 25 tahun dan pendapatan Rp50 juta mungkin masing-masing masuk rentang yang wajar. Namun, apakah kombinasi keduanya tidak biasa bergantung pada pola populasi. Analisis multivariat diperlukan untuk menyelidikinya.

### Contoh analisis terpadu

Misalkan hasil `describe()` untuk `Income`:

| Statistik | Nilai |
|---|---:|
| `count` | 1.000 |
| `mean` | 8 |
| `std` | 12 |
| `min` | 1 |
| `25%` | 3 |
| `50%` | 4 |
| `75%` | 7 |
| `max` | 100 |

Angka merupakan ilustrasi pendapatan dalam juta rupiah.

**Langkah interpretasi:**

1. Mean lebih tinggi daripada median: ada indikasi nilai besar menarik rata-rata ke atas.
2. `std` besar relatif terhadap mean: penyebaran cukup besar, tetapi ini bukan bukti tunggal outlier.
3. IQR = 7 − 3 = 4.
4. Batas atas IQR = 7 + 1.5 × 4 = 13.
5. Nilai di atas 13 menjadi kandidat outlier menurut aturan IQR.
6. Histogram dan KDE membantu memeriksa bentuk distribusi.
7. Boxplot membantu melihat kandidat secara visual.
8. Sumber dan konteks data perlu diperiksa sebelum penanganan.

**Kesimpulan yang benar:** hasil statistik memberi petunjuk untuk penyelidikan lebih lanjut. Hasil tersebut tidak cukup untuk menyatakan semua nilai di atas 13 salah.

---

## 🔄 12. Alur EDA dari Awal sampai Akhir

### Langkah 1 — Pahami struktur dan kualitas

Periksa `shape`, `head()`, `info()`, tipe data, missing value, duplikasi, dan nilai unik.

### Langkah 2 — Tentukan unit observasi dan tujuan

Pastikan satu baris mewakili apa: pelanggan, transaksi, hari, atau kejadian. Tentukan target jika melakukan supervised learning.

### Langkah 3 — Periksa statistik ringkas

Gunakan `describe()` untuk melihat count, mean, std, kuartil, min, dan max. Cari petunjuk yang layak diperiksa lebih lanjut.

### Langkah 4 — Visualisasikan distribusi

Gunakan histogram, KDE, boxplot, atau ECDF sesuai pertanyaan. Cocokkan temuan visual dengan statistik.

### Langkah 5 — Deteksi kandidat outlier

Pilih IQR, Z-score, MAD, atau metode multivariat berdasarkan karakteristik data. Catat metode dan ambang yang digunakan.

### Langkah 6 — Investigasi konteks

Periksa nilai aktual, sumber data, satuan, proses bisnis, dan hubungan dengan fitur lain. Pisahkan kesalahan data dari observasi langka yang valid.

### Langkah 7 — Tentukan penanganan

Pilih mempertahankan, memperbaiki, mentransformasi, membatasi, atau menghapus berdasarkan bukti.

### Langkah 8 — Evaluasi dampak

Bandingkan statistik, grafik, jumlah observasi, dan dampak terhadap model. Dokumentasikan alasan keputusan.

---

## 🤖 13. EDA dan Machine Learning

EDA membantu menentukan langkah preprocessing, tetapi ada perbedaan antara pemeriksaan awal dan proses yang mempelajari parameter dari data.

### Contoh temuan dan tindak lanjut

| Temuan | Interpretasi awal | Langkah berikutnya |
|---|---|---|
| `Age` bertipe `object` | Tipe data mungkin tidak sesuai | Periksa nilai unik dan konversi dengan aman |
| 8% `Income` hilang | Ada informasi yang tidak tersedia | Investigasi pola missing dan strategi imputasi |
| `Income` menceng ke kanan | Rentang nilai memanjang ke kanan | Periksa nilai ekstrem dan pertimbangkan transformasi jika relevan |
| Nilai ekstrem pada `MonthlySpend` | Bisa anomali atau transaksi valid | Validasi dengan konteks bisnis |
| `CustomerID` unik | Kemungkinan identitas | Evaluasi apakah memiliki informasi prediktif yang sah |
| Duplikasi pelanggan | Bisa kesalahan atau banyak transaksi sah | Periksa unit observasi dan kunci unik |

### Mencegah data leakage

EDA awal dapat dilakukan untuk memahami struktur dataset. Namun, parameter preprocessing yang dipelajari dari data—misalnya median imputasi, batas winsorization, standardisasi, atau seleksi fitur berdasarkan target—sebaiknya dipelajari dari data latih saja.

Alur yang umum:

1. Periksa struktur dan kualitas data.
2. Tentukan target, unit observasi, dan potensi *data leakage*.
3. Pisahkan data latih dan data uji dengan strategi yang sesuai.
4. Pelajari parameter preprocessing dari data latih.
5. Terapkan parameter yang sama ke data validasi/uji tanpa menghitung ulang dari data uji.
6. Evaluasi hasil model.

Jika batas statistik atau seleksi fitur berdasarkan target dihitung dari seluruh dataset sebelum split, informasi dari data uji dapat memengaruhi proses pelatihan sehingga evaluasi tampak terlalu optimistis.

**Pengecualian:** memperbaiki kesalahan yang jelas berdasarkan aturan eksternal yang sudah diketahui, seperti konversi satuan yang terdokumentasi, berbeda dari mempelajari ambang statistik dari seluruh dataset.

### Apakah outlier selalu buruk untuk model?

Tidak. Dampaknya tergantung algoritma dan tujuan.

- Model berbasis jarak dapat sensitif terhadap skala dan observasi ekstrem.
- Regresi linear dengan kuadrat galat dapat sangat dipengaruhi beberapa observasi.
- Model pohon dan ensemble pohon sering tidak membutuhkan distribusi normal, tetapi tetap dapat terpengaruh oleh pencilan atau kualitas data.
- Outlier yang valid dapat mengandung informasi penting tentang kejadian langka yang justru ingin diprediksi.

Jangan menganggap satu algoritma sepenuhnya kebal terhadap outlier. Evaluasi pada data validasi dan pertimbangkan tujuan model.

---

## 💻 14. Template Kode EDA

Template berikut merupakan titik awal untuk fitur numerik. Sesuaikan nama kolom dan pemeriksaan dengan datasetmu.

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

# 1. Baca data
df = pd.read_csv("customer.csv")

# 2. Struktur data
print("Shape:", df.shape)
print(df.head())
df.info()

# 3. Kualitas data
print("\nMissing value:")
print(df.isna().sum())

print("\nDuplikasi:", df.duplicated().sum())

# 4. Ringkasan numerik
print("\nDescribe:")
print(df.describe())

# Pilih satu fitur numerik
col = "Income"
s = df[col].dropna()

# 5. Statistik tambahan
print("\nMean:", s.mean())
print("Median:", s.median())
print("Skewness:", s.skew())

# 6. Visualisasi distribusi
fig, axes = plt.subplots(1, 3, figsize=(15, 4))

sns.histplot(s, bins=20, kde=True, ax=axes[0])
axes[0].set_title("Histogram + KDE")

sns.boxplot(x=s, ax=axes[1])
axes[1].set_title("Boxplot")

sns.ecdfplot(x=s, ax=axes[2])
axes[2].set_title("ECDF")

plt.tight_layout()
plt.show()

# 7. Kandidat outlier dengan IQR
q1 = s.quantile(0.25)
q3 = s.quantile(0.75)
iqr = q3 - q1

lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

outlier_mask = (s < lower) | (s > upper)

print("\nQ1:", q1)
print("Q3:", q3)
print("IQR:", iqr)
print("Batas bawah:", lower)
print("Batas atas:", upper)
print("Jumlah kandidat:", outlier_mask.sum())
print("Nilai kandidat:")
print(s[outlier_mask])
```

**Catatan praktik:**

- Pastikan kolom yang dipilih benar-benar numerik.
- `dropna()` pada contoh ini hanya mengabaikan nilai hilang saat menganalisis satu fitur; ini tidak berarti missing value seluruh dataset telah ditangani.
- Jika banyak nilai identik atau IQR = 0, evaluasi apakah aturan IQR masih informatif.
- Untuk data yang sangat besar, visualisasi dan deteksi multivariat mungkin memerlukan strategi sampling atau preprocessing yang sesuai.
- Jangan langsung menghapus kandidat yang ditemukan kode.

---

## 📝 15. Template Narasi Laporan

Gunakan pola **temuan → interpretasi → verifikasi → keputusan**.

### A. Distribusi

> Fitur `[nama fitur]` memiliki mean sebesar `[nilai]` dan median sebesar `[nilai]`. Perbedaan ini memberikan indikasi awal mengenai kemungkinan kemencengan distribusi. Histogram dan KDE digunakan untuk memeriksa bentuk distribusi, sedangkan statistik ringkas digunakan sebagai konteks numerik. Interpretasi akhir dibuat berdasarkan gabungan bukti, bukan satu statistik saja.

### B. Deteksi outlier

> Kandidat outlier pada fitur `[nama fitur]` diidentifikasi menggunakan metode `[nama metode]` dengan ambang `[ambang]`. Sebanyak `[jumlah]` observasi ditandai. Hasil ini menunjukkan penyimpangan menurut aturan yang digunakan, bukan bukti otomatis bahwa observasi salah.

### C. Investigasi dan penanganan

> Kandidat outlier diperiksa berdasarkan `[sumber/konteks/domain]`. Setelah investigasi, observasi `[dipertahankan/diperbaiki/ditransformasi/dibatasi/dihapus]` karena `[alasan berbasis bukti]`. Dampak keputusan dievaluasi melalui `[statistik/grafik/performa model]`.

### D. Contoh narasi terpadu

> Fitur `Income` memiliki mean lebih tinggi daripada median, sehingga terdapat indikasi distribusi menceng ke kanan. Histogram digunakan untuk memeriksa bentuk distribusi, sedangkan boxplot dan aturan IQR digunakan untuk mengidentifikasi kandidat outlier. Observasi yang melewati batas IQR kemudian diperiksa berdasarkan konteks dan sumber data. Penanganan ditentukan setelah diketahui apakah nilai tersebut merupakan kesalahan pencatatan atau observasi valid.

Hindari laporan seperti:

> Data memiliki outlier karena nilai maksimum jauh dari rata-rata. Oleh sebab itu, outlier dihapus.

Laporan tersebut melompat dari pengamatan ke keputusan tanpa investigasi.

---

## ✅ 16. Checklist EDA

### A. Memahami dataset

- [ ] Periksa `shape`, `head()`, `info()`, dan tipe data.
- [ ] Periksa missing value, duplikasi, dan nilai unik.
- [ ] Identifikasi target dan makna setiap fitur.
- [ ] Pastikan definisi satu observasi jelas.

### B. Memahami distribusi

- [ ] Periksa `describe()` dan statistik numerik.
- [ ] Buat histogram dan KDE bila relevan.
- [ ] Bandingkan mean dan median.
- [ ] Periksa skewness tanpa menganggapnya sebagai bukti tunggal.
- [ ] Gunakan boxplot atau ECDF untuk perspektif tambahan.

### C. Menyelidiki outlier

- [ ] Tentukan fitur numerik yang perlu diperiksa.
- [ ] Pilih IQR, Z-score, MAD, atau metode multivariat sesuai konteks.
- [ ] Catat ambang dan jumlah kandidat.
- [ ] Periksa nilai aktual dan sumbernya.
- [ ] Bedakan kesalahan data dari kejadian langka yang valid.

### D. Menentukan penanganan

- [ ] Tentukan alasan untuk mempertahankan, memperbaiki, mentransformasi, membatasi, atau menghapus.
- [ ] Catat jumlah observasi yang terdampak.
- [ ] Hindari *data leakage* saat mempelajari parameter preprocessing.
- [ ] Evaluasi dampak keputusan terhadap distribusi dan performa model.

---

## 🧠 17. Latihan Pemahaman

Gunakan data durasi penggunaan aplikasi (menit):

```python
duration = [10, 12, 12, 13, 14, 15, 16, 18, 20, 120]
```

### Pertanyaan 1

Jika mean jauh lebih tinggi daripada median, apa dugaan awal yang masuk akal?

- A. Distribusi pasti normal.
- B. Distribusi mungkin menceng ke kanan.
- C. Semua data pasti salah.

**Jawaban:** B. Nilai 120 dapat menarik mean ke atas, tetapi bentuk distribusi tetap perlu diperiksa.

### Pertanyaan 2

Jika IQR menandai nilai 120 sebagai outlier, apa yang diketahui?

- A. Nilai 120 pasti kesalahan input.
- B. Nilai 120 adalah kandidat outlier menurut aturan IQR.
- C. Nilai 120 harus langsung dihapus.

**Jawaban:** B. Deteksi statistik memberi sinyal untuk investigasi, bukan keputusan penghapusan.

### Pertanyaan 3

Jika durasi 120 menit terkonfirmasi sebagai sesi pengguna yang benar-benar terjadi, apa tindakan yang masuk akal?

- A. Selalu hapus.
- B. Selalu lakukan capping pada persentil ke-95.
- C. Pertimbangkan mempertahankannya dan evaluasi pengaruhnya terhadap tujuan model.

**Jawaban:** C. Data valid perlu dinilai berdasarkan tujuan analisis dan dampaknya terhadap model.

### Pertanyaan 4

Mengapa histogram dan `describe()` sebaiknya dibaca bersama?

**Jawaban:** `describe()` memberi ringkasan numerik seperti mean, median, kuartil, dan rentang. Histogram memperlihatkan bentuk sebaran yang tidak bisa dijelaskan oleh ringkasan tersebut saja. Keduanya saling melengkapi.

### Pertanyaan 5

Mengapa Z-score tidak selalu ideal untuk distribusi yang sangat menceng?

**Jawaban:** Z-score bergantung pada mean dan standar deviasi yang dapat dipengaruhi nilai ekstrem. Pada distribusi yang sangat menceng, jarak dari mean dalam satuan standar deviasi dapat menjadi kurang representatif.

---

## 🎯 18. Ringkasan Prinsip

1. **EDA adalah proses berpikir berbasis bukti**, bukan sekadar menjalankan fungsi.
2. `shape`, `info()`, `head()`, `describe()`, missing value, dan duplikasi menjawab pertanyaan yang berbeda.
3. `describe()` memberikan ringkasan numerik, tetapi tidak menggantikan visualisasi.
4. Histogram, KDE, boxplot, dan ECDF memiliki fungsi yang saling melengkapi.
5. IQR, Z-score, MAD, Isolation Forest, dan LOF mendeteksi kandidat berdasarkan kriteria berbeda.
6. Outlier bukan sinonim kesalahan data.
7. Investigasi konteks harus dilakukan sebelum memutuskan penanganan.
8. Mempertahankan, memperbaiki, mentransformasi, melakukan capping, dan menghapus adalah pilihan yang bergantung pada bukti dan tujuan.
9. Untuk modeling, pelajari parameter preprocessing dari data latih dan terapkan parameter yang sama ke data validasi/uji.
10. Tulis kesimpulan dengan pola **temuan → interpretasi → verifikasi → keputusan**.

> **Pola pikir seorang analis:** jangan hanya bertanya “Metode apa yang harus saya gunakan?” Tanyakan juga “Pertanyaan apa yang ingin saya jawab, bukti apa yang saya miliki, apa yang belum saya ketahui, dan apa konsekuensi keputusan saya?”

---

## 📐 Catatan Format Rumus untuk GitHub

GitHub mendukung matematika dalam Markdown menggunakan delimiter LaTeX berikut.

Rumus dalam baris:

```markdown
Nilai Z-score dihitung dengan $z = \frac{x-\mu}{\sigma}$.
```

Rumus pada baris tersendiri:

```markdown
$$
IQR = Q_3 - Q_1
$$
```

Contoh rumus:

```markdown
$$
L = Q_1 - 1.5(IQR)
$$

$$
U = Q_3 + 1.5(IQR)
$$

$$
z_i = \frac{x_i-\mu}{\sigma}
$$
```

**Catatan:** gunakan `$$ ... $$` untuk rumus display pada README atau file `.md` GitHub. Jangan mengandalkan fenced code block berlabel `math` seperti ```` ```math ```` untuk merender rumus; blok kode menampilkan teks mentah, bukan matematika yang dirender.
