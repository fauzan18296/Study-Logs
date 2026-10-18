# Panduan EDA: Memahami Distribusi Data, Mendeteksi Outlier, dan Menentukan Penanganannya

> **Tujuan catatan**
>
> Catatan ini membantu memahami EDA (*Exploratory Data Analysis*) secara
> konseptual: apa yang diperiksa, mengapa metode digunakan, bagaimana
> membaca hasil, bagaimana metode saling melengkapi, dan bagaimana
> mengambil keputusan tanpa menghapus informasi secara sembarangan.

------------------------------------------------------------------------

## Daftar Isi

1.  [Peta Besar EDA](#1-peta-besar-eda)
2.  [Mengapa EDA Awal Penting?](#2-mengapa-eda-awal-penting)
3.  [Memahami `shape`, `info()`, `describe()`, dan Pemeriksaan
    Dasar](#3-memahami-shape-info-describe-dan-pemeriksaan-dasar)
4.  [Memahami Distribusi Data](#4-memahami-distribusi-data)
5.  [Metode Analisis Distribusi](#5-metode-analisis-distribusi)
6.  [Membaca `describe()` dengan
    Benar](#6-membaca-describe-dengan-benar)
7.  [Memahami Outlier](#7-memahami-outlier)
8.  [Metode Deteksi Outlier](#8-metode-deteksi-outlier)
9.  [Perbandingan Metode Deteksi](#9-perbandingan-metode-deteksi)
10. [Cara Menangani Outlier](#10-cara-menangani-outlier)
11. [Bagaimana `describe()` Melengkapi Metode
    Lain](#11-bagaimana-describe-melengkapi-metode-lain)
12. [Workflow EDA yang Sistematis](#12-workflow-eda-yang-sistematis)
13. [EDA, Preprocessing, dan Data
    Leakage](#13-eda-preprocessing-dan-data-leakage)
14. [Template Kode EDA](#14-template-kode-eda)
15. [Template Narasi Laporan](#15-template-narasi-laporan)
16. [Kesalahan Umum](#16-kesalahan-umum)
17. [Checklist Praktis](#17-checklist-praktis)
18. [Latihan Pemahaman](#18-latihan-pemahaman)
19. [Ringkasan Inti](#19-ringkasan-inti)

------------------------------------------------------------------------

## 1. Peta Besar EDA

**EDA adalah proses menyelidiki data untuk memahami struktur, kualitas,
distribusi, pola, hubungan, dan potensi masalah sebelum menarik
kesimpulan atau membangun model.**

EDA bukan sekadar membuat grafik sebanyak-banyaknya. EDA adalah proses
mengumpulkan bukti untuk menjawab pertanyaan tentang data.

Bayangkan seorang dokter memeriksa pasien. Dokter tidak langsung
memberikan obat hanya karena melihat satu gejala. Ia memeriksa kondisi
dasar, mengumpulkan bukti, mencari penyebab, lalu memilih tindakan.
Analis data sebaiknya berpikir dengan cara serupa.

### Empat tahap berpikir

1.  **Amati:** apa yang ada di dalam dataset?
2.  **Analisis:** pola apa yang tampak?
3.  **Verifikasi:** apakah pola tersebut benar, masuk akal, dan relevan
    dengan konteks?
4.  **Putuskan:** apakah data perlu dipertahankan, diperbaiki,
    ditransformasi, dibatasi, atau dihapus?

> **Prinsip utama:** deteksi statistik bukan bukti otomatis bahwa data
> salah. Temuan EDA adalah petunjuk yang perlu ditafsirkan berdasarkan
> konteks.

------------------------------------------------------------------------

## 2. Mengapa EDA Awal Penting?

Sebelum menganalisis distribusi atau membangun model, kita perlu tahu
seperti apa dataset yang sedang dihadapi.

Misalnya, kamu menerima dataset pelanggan untuk memprediksi *customer
churn* (pelanggan berhenti berlangganan). Sebelum modeling, kamu perlu
mengetahui:

-   Berapa banyak baris dan kolom?
-   Apa arti setiap baris?
-   Apakah tipe data sesuai?
-   Apakah ada nilai hilang atau duplikasi?
-   Apakah ada nilai yang tidak masuk akal?
-   Bagaimana distribusi fitur numerik?
-   Apakah terdapat kolom identitas, target, atau potensi kebocoran
    target?

### Analogi

EDA awal seperti pemeriksaan dasar sebelum melakukan pemeriksaan yang
lebih spesifik. `shape`, `info()`, `describe()`, dan pemeriksaan missing
value menjawab pertanyaan yang berbeda. Tidak satu pun cukup untuk
memahami seluruh dataset.

------------------------------------------------------------------------

## 3. Memahami `shape`, `info()`, `describe()`, dan Pemeriksaan Dasar

### 3.1 `df.shape` --- ukuran dataset

``` python
print(df.shape)
```

Contoh hasil:

``` text
(1000, 12)
```

Artinya terdapat 1.000 baris dan 12 kolom.

**Tujuan:** mengetahui skala dataset dan jumlah variabel.

**Pertanyaan analisis:** - Apakah jumlah observasi sesuai dengan
ekspektasi? - Apakah jumlah kolom sesuai dokumentasi? - Apakah jumlah
baris berubah setelah proses filter atau penggabungan data?

**Analogi:** menghitung berapa orang yang hadir dan berapa karakteristik
yang dicatat untuk setiap orang.

**Batasan:** `shape` tidak menjelaskan apakah data berkualitas,
distribusinya masuk akal, atau apakah ada outlier.

### 3.2 `df.info()` --- struktur dan tipe data

``` python
df.info()
```

`info()` umumnya menampilkan: - nama kolom; - jumlah nilai non-null; -
tipe data; - penggunaan memori.

Contoh masalah: kolom `Age` bertipe `object`, padahal seharusnya
numerik. Ini dapat terjadi karena nilai angka tersimpan sebagai teks
atau kolom berisi nilai seperti `"unknown"`.

**Pertanyaan analisis:** - Apakah tipe data sesuai dengan makna kolom? -
Apakah jumlah non-null lebih kecil daripada jumlah baris? - Apakah kolom
kategorikal, numerik, tanggal, dan boolean teridentifikasi dengan benar?

**Analogi:** memeriksa label dan jenis isi setiap kotak sebelum
menggunakannya.

**Batasan:** tipe `object` tidak selalu berarti salah; kolom tersebut
bisa memang berisi teks. Konteks kolom tetap diperlukan.

### 3.3 `df.describe()` --- ringkasan statistik

``` python
df.describe()
```

Secara default, `describe()` merangkum kolom numerik. Untuk kolom
kategorikal:

``` python
df.describe(include="object")
```

Untuk merangkum berbagai tipe kolom:

``` python
df.describe(include="all")
```

Statistik numerik yang umum:

  -----------------------------------------------------------------------
  Statistik               Makna                   Pertanyaan yang dijawab
  ----------------------- ----------------------- -----------------------
  `count`                 Jumlah nilai non-null   Berapa nilai tersedia?

  `mean`                  Rata-rata               Di mana pusat
                                                  berdasarkan rata-rata?

  `std`                   Simpangan baku          Seberapa besar variasi
                                                  relatif terhadap mean?

  `min`                   Nilai minimum           Apa nilai terkecil?
                                                  Apakah masuk akal?

  `25%`                   Kuartil pertama (Q1)    Di mana batas
                                                  seperempat data
                                                  terbawah?

  `50%`                   Median (Q2)             Di mana titik tengah
                                                  data terurut?

  `75%`                   Kuartil ketiga (Q3)     Di mana batas tiga
                                                  perempat data terbawah?

  `max`                   Nilai maksimum          Apa nilai terbesar?
                                                  Apakah masuk akal?
  -----------------------------------------------------------------------

**Penting:** `describe()` memberikan ringkasan, bukan penjelasan lengkap
tentang distribusi. Dua dataset bisa memiliki mean dan standar deviasi
serupa tetapi bentuk distribusinya berbeda.

### 3.4 Missing value

``` python
print(df.isna().sum())
```

Persentase missing value:

``` python
missing_pct = df.isna().mean().mul(100)
print(missing_pct.sort_values(ascending=False))
```

**Analisis:** - Kolom mana yang memiliki nilai hilang? - Berapa jumlah
dan persentasenya? - Apakah kehilangan data terjadi secara acak atau
berkaitan dengan kelompok tertentu? - Apakah nilai kosong benar-benar
berarti tidak diketahui, atau memiliki makna khusus?

Jangan langsung menghapus kolom hanya karena persentase missing value
tinggi. Pertimbangkan kegunaan fitur, penyebab data hilang, ukuran
sampel, dan kemungkinan informasi yang hilang.

### 3.5 Duplikasi

``` python
print("Jumlah baris duplikat:", df.duplicated().sum())
```

Duplikasi berdasarkan kolom tertentu:

``` python
print(df.duplicated(subset=["CustomerID"]).sum())
```

**Analisis:** baris identik belum tentu merupakan duplikasi yang salah.
Dalam dataset transaksi, seorang pelanggan dapat melakukan banyak
transaksi. Pahami terlebih dahulu apa yang seharusnya unik: pelanggan,
transaksi, sesi, atau kejadian lainnya.

### 3.6 Melihat contoh data dan nilai unik

``` python
print(df.head())
print(df.sample(min(5, len(df)), random_state=42))
print(df["SomeColumn"].value_counts(dropna=False))
```

Gunakan `head()` dan `sample()` untuk melihat contoh aktual. Gunakan
`value_counts()` untuk memahami frekuensi kategori atau nilai yang
berulang.

### 3.7 Mengapa pemeriksaan dasar saling melengkapi?

  -----------------------------------------------------------------------
  Pemeriksaan             Fokus                   Tidak dapat menjawab
                                                  sendiri
  ----------------------- ----------------------- -----------------------
  `shape`                 Ukuran                  Kualitas atau bentuk
                                                  distribusi

  `info()`                Struktur dan tipe       Makna nilai ekstrem

  `describe()`            Ringkasan statistik     Seluruh bentuk
                                                  distribusi

  `isna().sum()`          Missing value           Penyebab missing value

  `duplicated()`          Duplikasi               Apakah duplikasi salah
                                                  menurut konteks

  `head()` / `sample()`   Contoh baris            Pola keseluruhan
                                                  dataset

  `value_counts()`        Frekuensi nilai         Hubungan multivariat
                                                  yang kompleks
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 4. Memahami Distribusi Data

**Distribusi** menjelaskan bagaimana nilai suatu variabel tersebar:
nilai yang sering muncul, pusat data, lebar penyebaran, kemencengan, dan
jumlah puncak.

Bayangkan tinggi badan 1.000 mahasiswa. Rata-rata tinggi saja tidak
memberi tahu apakah sebagian besar mahasiswa berkumpul di sekitar
rata-rata, apakah terdapat dua kelompok, atau apakah beberapa nilai
tidak masuk akal.

### Empat karakteristik utama

#### 4.1 Bentuk (*shape*)

Distribusi dapat simetris, menceng ke kiri, menceng ke kanan, atau
memiliki bentuk lain.

#### 4.2 Pusat (*center*)

Pusat data dapat dilihat melalui mean, median, dan modus. Mean sensitif
terhadap nilai ekstrem; median biasanya lebih tahan.

#### 4.3 Penyebaran (*spread*)

Penyebaran dapat dipahami melalui range, IQR, dan standar deviasi.

#### 4.4 Puncak (*modality*)

-   **Unimodal:** satu puncak utama.
-   **Bimodal:** dua puncak.
-   **Multimodal:** beberapa puncak.

Beberapa puncak dapat mengindikasikan kelompok berbeda, tetapi tidak
otomatis membuktikan adanya beberapa populasi. Pilihan bin histogram
atau bandwidth KDE dapat memengaruhi bentuk yang terlihat.

### Skewness (kemencengan)

-   **Skewness positif:** ekor cenderung lebih panjang ke kanan.
-   **Skewness negatif:** ekor cenderung lebih panjang ke kiri.
-   **Skewness dekat nol:** tidak menunjukkan kemencengan yang kuat,
    tetapi bukan jaminan distribusi simetris.

Mean lebih tinggi daripada median sering menjadi petunjuk *right-skew*,
sedangkan mean lebih rendah daripada median sering menjadi petunjuk
*left-skew*. Ini bukan aturan yang selalu berlaku.

------------------------------------------------------------------------

## 5. Metode Analisis Distribusi

Tidak ada satu metode yang menjawab semua pertanyaan. Gunakan beberapa
metode yang saling melengkapi.

### 5.1 Histogram

**Pertanyaan:** bagaimana frekuensi nilai tersebar dalam interval?

``` python
import matplotlib.pyplot as plt

df["Income"].hist(bins=20)
plt.xlabel("Income")
plt.ylabel("Frequency")
plt.title("Distribution of Income")
plt.show()
```

**Cara analisis:** 1. Cari rentang dengan frekuensi tertinggi. 2.
Periksa apakah distribusi simetris atau menceng. 3. Cari ekor panjang,
celah, dan beberapa puncak. 4. Coba jumlah `bins` yang berbeda jika
grafik terlalu kasar atau terlalu terpecah. 5. Cocokkan bentuk grafik
dengan statistik ringkasan.

**Analogi:** mengelompokkan mahasiswa menurut rentang tinggi badan dan
menghitung jumlah orang dalam setiap rentang.

**Keterbatasan:** bentuk histogram bergantung pada jumlah dan batas bin.
Puncak kecil belum tentu merupakan kelompok nyata.

### 5.2 KDE (*Kernel Density Estimation*)

**Pertanyaan:** bagaimana perkiraan kepadatan data berubah secara halus?

``` python
import seaborn as sns
import matplotlib.pyplot as plt

sns.kdeplot(data=df, x="Income")
plt.title("KDE of Income")
plt.show()
```

**Cara analisis:** - Puncak menunjukkan wilayah dengan kepadatan relatif
tinggi. - Ekor panjang dapat mengindikasikan kemencengan. - Beberapa
puncak bisa mengisyaratkan beberapa kelompok. - Periksa bandwidth karena
penghalusan dapat menyembunyikan atau menciptakan kesan puncak.

**Analogi:** histogram seperti mengelompokkan orang ke dalam kotak,
sedangkan KDE menggambarkan kerumunan dengan kurva halus.

**Keterbatasan:** KDE adalah estimasi, bukan distribusi sebenarnya yang
diketahui secara pasti. Pada data diskret, data sangat sedikit, atau
data berbatas, interpretasinya memerlukan kehati-hatian.

### 5.3 Boxplot

**Pertanyaan:** di mana pusat data, rentang tengah, dan kandidat nilai
ekstrem?

``` python
sns.boxplot(data=df, x="Income")
plt.show()
```

Komponen utama: - Garis di dalam kotak: median. - Batas kotak: Q1 dan
Q3. - Tinggi/lebar kotak: IQR. - Whisker: rentang yang ditentukan oleh
aturan boxplot. - Titik di luar whisker: kandidat outlier menurut aturan
tersebut.

Whisker standar boxplot biasanya menjangkau nilai terjauh yang masih
berada di dalam batas Q1 − 1,5 × IQR dan Q3 + 1,5 × IQR, bukan selalu
nilai minimum dan maksimum.

**Analogi:** mengurutkan nilai ujian lalu menandai rentang yang mencakup
separuh data bagian tengah.

**Keterbatasan:** boxplot tidak memperlihatkan detail distribusi atau
jumlah puncak dengan baik. Titik di luar whisker bukan otomatis
kesalahan data.

### 5.4 Mean, median, dan skewness

``` python
s = df["Income"].dropna()

print("Mean:", s.mean())
print("Median:", s.median())
print("Skewness:", s.skew())
```

**Cara analisis:** - Mean jauh di atas median: kemungkinan ekor kanan
lebih panjang. - Mean jauh di bawah median: kemungkinan ekor kiri lebih
panjang. - Mean dekat median: bisa saja relatif simetris, tetapi
konfirmasi dengan grafik.

Skewness mengukur kemencengan distribusi, tetapi nilainya harus
ditafsirkan berdasarkan ukuran sampel dan karakteristik data. Jangan
memakai satu ambang universal sebagai aturan mutlak.

**Analogi:** beberapa pelanggan berpendapatan sangat tinggi dapat
menarik rata-rata ke atas, meskipun mayoritas pelanggan berpendapatan
sedang.

### 5.5 ECDF (*Empirical Cumulative Distribution Function*)

**Pertanyaan:** berapa proporsi observasi yang nilainya kurang dari atau
sama dengan ambang tertentu?

``` python
sns.ecdfplot(data=df, x="Income")
plt.title("ECDF of Income")
plt.show()
```

Jika kurva mencapai 0,8 pada pendapatan Rp8 juta, sekitar 80% observasi
memiliki pendapatan tidak lebih dari Rp8 juta.

**Analogi:** menghitung persentase pelanggan yang memiliki pendapatan
maksimal Rp8 juta.

**Kelebihan:** tidak memerlukan pemilihan bin histogram dan langsung
menunjukkan proporsi kumulatif.

### 5.6 Menggabungkan bukti distribusi

Misalnya: - mean lebih tinggi daripada median; - histogram menunjukkan
ekor kanan panjang; - KDE menunjukkan kepadatan tinggi di nilai rendah
dan ekor ke kanan; - boxplot menandai beberapa titik di luar whisker.

Kesimpulan sementara: distribusi kemungkinan menceng ke kanan dan
memiliki kandidat outlier.

**Belum boleh disimpulkan bahwa semua kandidat outlier merupakan
kesalahan.** Konteks dan sumber data tetap harus diperiksa.

------------------------------------------------------------------------

## 6. Membaca `describe()` dengan Benar

Misalkan ringkasan fitur `Income` (dalam juta rupiah) adalah:

  Statistik     Nilai
  ----------- -------
  `count`       1.000
  `mean`            8
  `std`            12
  `min`             1
  `25%`             3
  `50%`             4
  `75%`             7
  `max`           100

### Interpretasi bertahap

**1. `count`:** ada 1.000 nilai non-null. Bandingkan dengan jumlah baris
dataset untuk memahami apakah terdapat missing value pada kolom ini.

**2. `min` dan `max`:** nilai terkecil adalah 1 dan terbesar 100. Apakah
nilai maksimum masuk akal menurut domain? Belum dapat diputuskan hanya
dari rentang.

**3. Mean dan median:** mean = 8, median = 4. Perbedaan ini memberi
petunjuk bahwa nilai besar mungkin menarik rata-rata ke atas.

**4. `std`:** standar deviasi = 12, lebih besar daripada mean. Ini
menunjukkan penyebaran yang besar relatif terhadap skala mean, tetapi
tidak membuktikan outlier.

**5. Kuartil:** Q1 = 3 dan Q3 = 7. Separuh data bagian tengah berada
antara Rp3 juta dan Rp7 juta.

IQR:

``` math
IQR = Q_3 - Q_1
```

``` math
IQR = 7 - 3 = 4
```

Batas atas IQR:

``` math
U = Q_3 + 1.5(IQR)
```

``` math
U = 7 + 1.5(4) = 13
```

Nilai di atas 13 menjadi kandidat outlier berdasarkan aturan IQR.

**Catatan:** hasil kuartil dapat sedikit berbeda tergantung metode
perhitungan kuartil dan implementasi perangkat lunak.

### Analogi mean dan median

Nilai ujian lima siswa: 60, 65, 70, 75, 100.

-   Mean = 74.
-   Median = 70.

Jika nilai 100 ternyata salah input dan tercatat 500, mean berubah
drastis, tetapi median tetap 70. Ini menunjukkan mengapa mean lebih
sensitif terhadap nilai ekstrem.

### Apa yang tidak dapat disimpulkan dari `describe()`?

-   Nilai maksimum jauh dari median tidak otomatis berarti salah.
-   Mean lebih tinggi daripada median tidak membuktikan skewness
    sendirian.
-   Standar deviasi besar tidak otomatis berarti ada outlier.
-   Kuartil tidak menjelaskan mengapa suatu nilai muncul.
-   Ringkasan per kolom tidak menjelaskan hubungan antarfitur.

------------------------------------------------------------------------

## 7. Memahami Outlier

**Outlier** adalah observasi yang berbeda secara mencolok dari sebagian
besar data berdasarkan suatu kriteria statistik, pola, atau model.

Contoh transaksi (juta rupiah):

``` text
[2, 3, 3, 4, 4, 5, 6, 7, 8, 100]
```

Nilai 100 terlihat jauh lebih besar, tetapi beberapa kemungkinan
penyebabnya adalah:

1.  Kesalahan input, misalnya seharusnya 10.
2.  Transaksi besar yang benar-benar terjadi.
3.  Peristiwa langka, misalnya promosi besar.
4.  Campuran populasi berbeda, misalnya transaksi perusahaan dan ritel.

### Deteksi tidak sama dengan penanganan

-   **Deteksi:** menandai observasi yang tidak biasa.
-   **Investigasi:** memeriksa sumber, konteks, dan penyebabnya.
-   **Penanganan:** memilih tindakan berdasarkan bukti dan tujuan
    analisis.

### Analogi detektif

Detektif menemukan sidik jari yang berbeda. Menemukannya bukan bukti
bahwa sidik jari itu salah atau tidak relevan. Sidik jari tersebut perlu
diselidiki sebelum diputuskan apakah penting.

------------------------------------------------------------------------

## 8. Metode Deteksi Outlier

### 8.1 IQR (*Interquartile Range*)

IQR mengukur rentang antara kuartil ketiga dan kuartil pertama. Metode
ini umum digunakan untuk deteksi univariat dan tidak mengharuskan data
normal.

Rumus:

``` math
IQR = Q_3 - Q_1
```

``` math
L = Q_1 - 1.5(IQR)
```

``` math
U = Q_3 + 1.5(IQR)
```

Nilai di bawah L atau di atas U ditandai sebagai kandidat outlier.

#### Contoh

Data:

``` text
[2, 3, 3, 4, 4, 5, 6, 7, 8, 100]
```

Dengan metode kuartil median dari separuh data untuk ilustrasi ini: - Q1
= 3 - Q3 = 7 - IQR = 4 - Batas bawah = −3 - Batas atas = 13

Karena 100 \> 13, nilai 100 adalah kandidat outlier menurut aturan IQR.

**Catatan:** perangkat lunak dapat memakai konvensi kuartil berbeda,
sehingga hasil Q1 dan Q3 bisa berbeda.

#### Implementasi

``` python
s = df["Transaction"].dropna()

q1 = s.quantile(0.25)
q3 = s.quantile(0.75)
iqr = q3 - q1

lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

outlier_mask = (s < lower) | (s > upper)

print("Batas bawah:", lower)
print("Batas atas:", upper)
print("Jumlah kandidat:", outlier_mask.sum())
print(s[outlier_mask])
```

**Kelebihan:** sederhana, relatif tahan terhadap nilai ekstrem, dan
mudah dijelaskan.

**Keterbatasan:** tidak memahami konteks bisnis dan bisa menandai nilai
ekstrem yang valid, terutama pada distribusi yang sangat menceng.

### 8.2 Z-score

Z-score mengukur jarak observasi dari mean dalam satuan standar deviasi.

``` math
z = \frac{x - \mu}{\sigma}
```

Keterangan: - x = nilai observasi; - μ = mean; - σ = standar deviasi.

Contoh: mean tinggi badan = 170 cm, standar deviasi = 5 cm, dan tinggi
seseorang = 185 cm.

``` math
z = \frac{185 - 170}{5} = 3
```

Nilai tersebut berada tiga standar deviasi di atas mean.

Aturan praktis yang umum digunakan adalah menandai `|z| > 3`, tetapi
ambang ini bukan hukum universal.

``` python
s = df["Height"].dropna()

mean = s.mean()
std = s.std()

if std > 0:
    z_scores = (s - mean) / std
    outlier_mask = z_scores.abs() > 3
    print(s[outlier_mask])
else:
    print("Standar deviasi nol; Z-score tidak dapat digunakan.")
```

**Cocok ketika:** distribusi cukup mendekati normal dan jarak dari mean
dalam satuan standar deviasi relevan.

**Keterbatasan:** - mean dan standar deviasi sensitif terhadap
outlier; - distribusi menceng dapat menghasilkan interpretasi
menyesatkan; - data normal pun dapat memiliki observasi di luar tiga
standar deviasi.

### 8.3 MAD (*Median Absolute Deviation*)

MAD menggunakan median dan penyimpangan absolut dari median sehingga
lebih tahan terhadap nilai ekstrem daripada Z-score klasik.

``` math
MAD = \operatorname{median}(|x_i - \tilde{x}|)
```

Di sini, `x̃` adalah median.

Robust Z-score yang umum digunakan:

``` math
z_{\text{robust}} = \frac{0.6745(x_i - \tilde{x})}{MAD}
```

Nilai absolut robust Z-score di atas sekitar 3,5 kadang digunakan
sebagai penanda kandidat outlier. Ambang ini tetap merupakan pedoman,
bukan kepastian.

``` python
s = df["Transaction"].dropna()

median = s.median()
mad = (s - median).abs().median()

if mad > 0:
    robust_z = 0.6745 * (s - median) / mad
    outlier_mask = robust_z.abs() > 3.5
    print(s[outlier_mask])
else:
    print("MAD = 0; periksa distribusi dan gunakan pendekatan lain.")
```

**Kelebihan:** lebih robust terhadap nilai ekstrem.

**Keterbatasan:** jika sebagian besar data identik, MAD bisa bernilai
nol sehingga rumus tidak dapat langsung digunakan.

### 8.4 Metode visual

Gunakan histogram, boxplot, dan scatter plot sebagai alat investigasi.

-   Histogram: apakah nilai ekstrem berada pada ekor distribusi?
-   Boxplot: nilai mana yang berada di luar whisker?
-   Scatter plot: apakah observasi menyimpang dari hubungan dua
    variabel?

``` python
import matplotlib.pyplot as plt
import seaborn as sns

fig, axes = plt.subplots(1, 2, figsize=(12, 4))

sns.histplot(df["Transaction"].dropna(), ax=axes[0])
axes[0].set_title("Distribusi transaksi")

sns.boxplot(x=df["Transaction"].dropna(), ax=axes[1])
axes[1].set_title("Kandidat outlier")

plt.tight_layout()
plt.show()
```

Jika nilai ekstrem sangat besar, skala linear dapat membuat data lain
terlihat menumpuk dekat nol. Skala logaritmik bisa membantu untuk nilai
positif, tetapi interpretasi harus tetap sesuai konteks.

### 8.5 Isolation Forest

Isolation Forest adalah metode berbasis pohon yang mengisolasi
observasi. Observasi yang lebih mudah diisolasi cenderung memperoleh
skor anomali lebih tinggi.

Contoh:

``` python
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

`contamination=0.02` membantu menentukan ambang dengan asumsi proporsi
pencilan sekitar 2%. Ini **bukan bukti** bahwa tepat 2% data salah.

Perlu diperhatikan: - pilih fitur yang relevan; - perhatikan skala dan
representasi fitur; - lakukan imputasi yang sesuai sebelum metode yang
tidak menerima missing value; - interpretasikan hasil sebagai kandidat
anomali, bukan keputusan penghapusan.

### 8.6 Local Outlier Factor (LOF)

LOF membandingkan kepadatan lokal observasi dengan kepadatan
tetangganya. Observasi yang jauh lebih jarang di sekitar tetangganya
dapat ditandai sebagai anomali lokal.

Contoh:

``` python
from sklearn.neighbors import LocalOutlierFactor

features = ["Age", "Income", "MonthlySpend"]
X = df[features].dropna()

lof = LocalOutlierFactor(
    n_neighbors=20,
    contamination=0.02
)

labels = lof.fit_predict(X)

anomaly_mask = labels == -1

print("Jumlah kandidat:", anomaly_mask.sum())
print(X.loc[anomaly_mask])
```

**Kelebihan:** dapat menangkap anomali lokal yang tidak terlihat jika
semua data dinilai menggunakan satu batas global.

**Keterbatasan:** sensitif terhadap skala fitur, jumlah tetangga,
struktur kelompok, dan parameter. `n_neighbors=20` hanyalah contoh yang
perlu dievaluasi.

### 8.7 Mengapa `describe()` tidak cukup untuk anomali multivariat?

`describe()` merangkum setiap kolom secara terpisah. Namun, sebuah
observasi bisa tampak normal pada setiap fitur individual tetapi aneh
ketika fitur-fitur tersebut digabungkan.

Misalnya, kombinasi usia 20 tahun dan pendapatan sangat tinggi mungkin
jarang dalam satu populasi, meskipun masing-masing nilai masih berada
dalam rentang yang mungkin.

Untuk kasus seperti ini, gunakan scatter plot, analisis kelompok, atau
metode multivariat seperti Isolation Forest dan LOF.

------------------------------------------------------------------------

## 9. Perbandingan Metode Deteksi

  -------------------------------------------------------------------------
  Metode            Dasar             Kelebihan           Keterbatasan
  ----------------- ----------------- ------------------- -----------------
  IQR               Kuartil dan       Sederhana, relatif  Bisa menandai
                    rentang tengah    robust              nilai ekstrem
                                                          yang valid

  Z-score           Mean dan standar  Mudah               Sensitif terhadap
                    deviasi           diinterpretasikan   outlier dan
                                      untuk data          skewness
                                      mendekati normal    

  MAD               Median dan        Robust terhadap     Bisa gagal saat
                    deviasi absolut   nilai ekstrem       MAD = 0

  Histogram /       Pola visual       Mudah untuk         Dipengaruhi
  boxplot                             pemeriksaan awal    pilihan
                                                          visualisasi

  Isolation Forest  Kemudahan isolasi Menangani banyak    Skor bukan bukti
                                      fitur               kesalahan

  LOF               Kepadatan lokal   Menangkap anomali   Sensitif terhadap
                                      lokal               skala dan
                                                          parameter
  -------------------------------------------------------------------------

**Metode terbaik bukan metode yang menemukan outlier paling banyak.**
Metode terbaik adalah metode yang paling sesuai dengan struktur data,
tujuan analisis, dan konsekuensi kesalahan keputusan.

------------------------------------------------------------------------

## 10. Cara Menangani Outlier

Deteksi dan penanganan merupakan dua tahap berbeda. Misalnya, 20 dari
1.000 observasi ditandai sebagai kandidat outlier. Jumlah itu tidak
berarti 20 observasi harus dihapus.

Sebelum memilih tindakan, tanyakan: 1. Apakah nilainya valid menurut
domain? 2. Apakah ada bukti kesalahan pencatatan? 3. Apakah observasi
berasal dari proses atau populasi berbeda? 4. Apa dampak mempertahankan
atau mengubahnya terhadap analisis dan model?

### 10.1 Mempertahankan data

Gunakan ketika nilai ekstrem valid dan relevan dengan masalah.

Contoh: pelanggan perusahaan benar-benar memiliki pendapatan atau
transaksi besar. Menghapusnya dapat membuat model tidak memahami
pelanggan bernilai tinggi.

### 10.2 Memperbaiki kesalahan data

Gunakan jika terdapat bukti kesalahan dan nilai benar bisa diverifikasi
dari sumber yang dapat dipercaya.

Contoh: dokumentasi memastikan satuan harus dalam ribuan rupiah, tetapi
sebagian nilai tercatat dengan satuan berbeda.

Jangan menebak nilai yang benar hanya karena nilai itu ekstrem.

### 10.3 Transformasi

Transformasi log dapat mengurangi skewness dan memperkecil rentang nilai
besar.

``` python
df["Income_log"] = np.log1p(df["Income"])
```

`log1p(x)` menghitung logaritma natural dari `1 + x`. Untuk pendapatan
nonnegatif, transformasi ini dapat digunakan. Secara matematis, domain
realnya adalah `x > -1`.

Transformasi tidak menghapus observasi ekstrem; ia mengubah skala.
Pertimbangkan interpretasi fitur dan kebutuhan model.

### 10.4 Capping / winsorization

Capping membatasi nilai ke ambang tertentu.

``` python
lower = df["Income"].quantile(0.01)
upper = df["Income"].quantile(0.99)

df["Income_capped"] = df["Income"].clip(
    lower=lower,
    upper=upper
)
```

Contoh ini membatasi nilai di bawah persentil pertama dan di atas
persentil ke-99.

**Catatan:** persentil 1% dan 99% bukan aturan universal. Pilih ambang
berdasarkan konteks dan data latih jika parameter dipelajari dari data.

Konsekuensi: nilai berbeda bisa menjadi sama dengan batas, sehingga
informasi tentang besarnya nilai ekstrem berkurang.

### 10.5 Menghapus observasi

Pertimbangkan penghapusan jika ada bukti kuat bahwa observasi tidak
valid dan tidak dapat diperbaiki, atau memang tidak memenuhi definisi
populasi penelitian.

Contoh: usia tercatat 250 tahun karena kesalahan input yang sudah
dikonfirmasi.

Jangan menghapus hanya karena nilai melewati batas IQR atau Z-score.

### 10.6 Simulasi keputusan

Transaksi Rp500 juta ditandai oleh IQR. Langkah pertama yang masuk akal
adalah memeriksa sumber, satuan, dan konteks transaksi.

-   Menghapus langsung: terlalu cepat.
-   Mempertahankan langsung: juga belum tentu benar.
-   Memverifikasi dahulu: langkah awal yang paling kuat.

Setelah investigasi, pilih penanganan sesuai bukti.

------------------------------------------------------------------------

## 11. Bagaimana `describe()` Melengkapi Metode Lain?

`describe()` tetap berguna meskipun histogram, KDE, boxplot, ECDF, IQR,
Z-score, MAD, Isolation Forest, atau LOF sudah digunakan. Namun, tidak
semua metode memerlukan `describe()` secara langsung.

  -----------------------------------------------------------------------
  Metode                  Peran `describe()`      Fokus analisis utama
  ----------------------- ----------------------- -----------------------
  Histogram               Pendamping              Bentuk distribusi,
                                                  ekor, puncak, celah

  KDE                     Pendamping              Kepadatan, puncak,
                                                  ekor, bandwidth

  Boxplot                 Sangat berguna          Kuartil, median, IQR,
                                                  kandidat di luar
                                                  whisker

  ECDF                    Opsional                Proporsi di bawah/sama
                                                  dengan ambang

  IQR                     Sangat relevan          Q1, Q3, IQR, batas,
                                                  jumlah kandidat

  Z-score                 Mean dan std dibutuhkan Jarak dalam satuan
                                                  standar deviasi

  MAD                     Median dibutuhkan       MAD, robust Z-score,
                                                  kondisi MAD = 0

  Isolation Forest        Tidak wajib             Skor anomali, kombinasi
                                                  fitur, parameter

  LOF                     Tidak wajib             Kepadatan lokal,
                                                  tetangga, skala fitur
  -----------------------------------------------------------------------

### Pola analisis yang disarankan

1.  Gunakan `describe()` untuk melihat ringkasan numerik.
2.  Gunakan histogram dan KDE untuk memahami bentuk distribusi.
3.  Gunakan boxplot atau metode statistik untuk menandai kandidat
    outlier.
4.  Periksa nilai aktual dan konteksnya.
5.  Pilih penanganan yang dapat dijelaskan.
6.  Bandingkan kondisi sebelum dan sesudah tindakan.

**Jangan mengulang seluruh EDA tanpa tujuan.** Jalankan pemeriksaan yang
menjawab pertanyaan analisis dan gabungkan bukti yang relevan.

------------------------------------------------------------------------

## 12. Workflow EDA yang Sistematis

### Tahap A --- Memahami struktur dan kualitas

-   Periksa `shape`, `head()`, `sample()`, dan `info()`.
-   Periksa tipe data dan nilai unik.
-   Periksa missing value dan duplikasi.
-   Pahami unit observasi: pelanggan, transaksi, sesi, atau kejadian.

### Tahap B --- Memahami distribusi

-   Periksa `describe()`.
-   Gunakan histogram dan KDE bila relevan.
-   Bandingkan mean dan median.
-   Periksa skewness.
-   Gunakan boxplot dan ECDF untuk sudut pandang tambahan.

### Tahap C --- Menyelidiki outlier

-   Pilih fitur numerik yang relevan.
-   Gunakan IQR sebagai pemeriksaan awal atau metode lain yang sesuai.
-   Periksa kandidat outlier dan sumbernya.
-   Bedakan kesalahan data dari kejadian langka yang valid.
-   Pertimbangkan metode multivariat jika kombinasi fitur penting.

### Tahap D --- Menentukan penanganan

-   Pertahankan, perbaiki, transformasi, capping, atau hapus berdasarkan
    bukti.
-   Catat alasan dan jumlah observasi yang terdampak.
-   Hindari kebocoran data saat mempelajari parameter preprocessing.
-   Bandingkan dampak keputusan terhadap performa model.

### Tahap E --- Validasi ulang

-   Periksa statistik dan grafik setelah penanganan.
-   Pastikan tidak ada nilai yang rusak atau perubahan yang tidak
    diinginkan.
-   Evaluasi apakah tindakan tersebut masuk akal bagi tujuan analisis.
-   Dokumentasikan keputusan dan keterbatasannya.

------------------------------------------------------------------------

## 13. EDA, Preprocessing, dan Data Leakage

### EDA vs preprocessing

  -----------------------------------------------------------------------
  EDA                                 Data preprocessing
  ----------------------------------- -----------------------------------
  Mengeksplorasi dan memahami data    Mengubah data untuk analisis atau
                                      modeling

  Mengidentifikasi kandidat outlier   Melakukan capping, koreksi, atau
                                      tindakan lain yang dipilih

  Mengamati missing value             Melakukan imputasi atau penanganan
                                      missing value

  Menyelidiki distribusi              Melakukan transformasi jika
                                      diperlukan
  -----------------------------------------------------------------------

Keduanya bersifat iteratif: EDA → tindakan → pemeriksaan ulang. Deteksi
dan investigasi outlier termasuk eksplorasi; tindakan mengubah data
termasuk preprocessing.

### Menghindari data leakage

Jika tugasnya membangun model prediktif, pemisahan data dan
preprocessing harus dirancang dengan benar.

Workflow umum:

1.  Lakukan pemeriksaan awal untuk memahami struktur, kualitas, target,
    dan definisi observasi.
2.  Pisahkan data latih dan data uji menggunakan strategi yang sesuai.
3.  Pelajari parameter preprocessing dari data latih saja, misalnya
    median imputasi, batas capping, atau standardisasi.
4.  Terapkan parameter yang sama ke data validasi/uji tanpa menghitung
    ulang dari data tersebut.
5.  Evaluasi model pada data yang tidak digunakan untuk mempelajari
    parameter.

Jika ambang statistik atau seleksi fitur berbasis target dihitung
menggunakan seluruh dataset sebelum split, informasi dari data uji bisa
bocor ke proses pelatihan.

**Pengecualian praktis:** memperbaiki kesalahan berdasarkan aturan
eksternal yang sudah diketahui sebelumnya---misalnya konversi satuan
yang terdokumentasi---berbeda dari mempelajari ambang statistik dari
seluruh dataset.

------------------------------------------------------------------------

## 14. Template Kode EDA

Template berikut adalah titik awal. Sesuaikan nama kolom dan jenis
pemeriksaan dengan datasetmu.

``` python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

# Load data
df = pd.read_csv("data.csv")

# 1. Struktur dataset
print("Shape:", df.shape)
display(df.head())
df.info()

# 2. Ringkasan statistik
display(df.describe())
display(df.describe(include="object"))

# 3. Missing value
missing_count = df.isna().sum()
missing_pct = df.isna().mean().mul(100)

missing_summary = pd.DataFrame({
    "missing_count": missing_count,
    "missing_pct": missing_pct
}).sort_values("missing_pct", ascending=False)

display(missing_summary)

# 4. Duplikasi
print("Duplikat baris:", df.duplicated().sum())

# 5. Distribusi satu fitur numerik
col = "Income"
s = df[col].dropna()

print(s.describe())
print("Skewness:", s.skew())

fig, axes = plt.subplots(1, 3, figsize=(15, 4))

sns.histplot(s, bins=20, kde=True, ax=axes[0])
axes[0].set_title("Histogram + KDE")

sns.boxplot(x=s, ax=axes[1])
axes[1].set_title("Boxplot")

sns.ecdfplot(x=s, ax=axes[2])
axes[2].set_title("ECDF")

plt.tight_layout()
plt.show()

# 6. Deteksi kandidat outlier dengan IQR
q1 = s.quantile(0.25)
q3 = s.quantile(0.75)
iqr = q3 - q1

lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

outlier_mask = (s < lower) | (s > upper)

print("Q1:", q1)
print("Q3:", q3)
print("IQR:", iqr)
print("Batas bawah:", lower)
print("Batas atas:", upper)
print("Jumlah kandidat:", outlier_mask.sum())
display(s[outlier_mask])
```

**Catatan:** - `display()` tersedia di lingkungan seperti Jupyter
Notebook dan Colab. Dalam skrip Python biasa, gunakan `print()` atau
metode output lain. - Pastikan `Income` adalah kolom numerik yang sudah
diperiksa tipe datanya. - Kode ini mendeteksi kandidat outlier; tidak
otomatis menghapus atau mengubahnya. - Untuk modeling, parameter
preprocessing yang dipelajari dari data harus di-fit pada data latih
saja.

------------------------------------------------------------------------

## 15. Template Narasi Laporan

Gunakan pola **temuan → interpretasi → verifikasi → keputusan**.

### Contoh distribusi

> Fitur `Income` memiliki mean lebih tinggi daripada median, yang
> mengindikasikan kemungkinan distribusi menceng ke kanan. Histogram
> digunakan untuk memeriksa bentuk distribusi, sedangkan KDE membantu
> melihat estimasi kepadatan. Kesimpulan mengenai bentuk distribusi
> didasarkan pada kombinasi statistik dan visualisasi, bukan satu
> indikator saja.

### Contoh deteksi outlier

> Boxplot dan aturan IQR digunakan untuk mengidentifikasi kandidat
> outlier pada fitur `Income`. Observasi yang berada di luar batas IQR
> ditandai untuk pemeriksaan lanjutan. Penandaan ini tidak dianggap
> sebagai bukti bahwa data salah.

### Contoh penanganan

> Kandidat outlier diperiksa berdasarkan sumber dan konteks data.
> Observasi yang terbukti valid dipertahankan, sedangkan kesalahan yang
> dapat diverifikasi diperbaiki. Jika transformasi atau capping
> digunakan, alasan, parameter, dan dampaknya didokumentasikan serta
> dievaluasi kembali.

Hindari narasi seperti:

> Nilai maksimum jauh dari rata-rata, jadi semua outlier dihapus.

Pernyataan itu melompat dari temuan ke keputusan tanpa investigasi.

------------------------------------------------------------------------

## 16. Kesalahan Umum

1.  **Menganggap semua outlier adalah kesalahan.** Outlier bisa valid
    dan penting.
2.  **Menghapus nilai ekstrem hanya karena melewati batas IQR.** Batas
    IQR menandai kandidat, bukan memastikan kesalahan.
3.  **Mengandalkan `describe()` saja.** Ringkasan numerik tidak
    menunjukkan seluruh bentuk distribusi.
4.  **Mengandalkan grafik saja.** Visualisasi perlu didukung statistik
    dan konteks.
5.  **Menganggap mean ≈ median pasti berarti distribusi simetris.**
    Hubungan tersebut bukan jaminan simetri.
6.  **Menganggap `std` besar pasti berarti ada outlier.** Penyebaran
    yang besar dapat terjadi tanpa outlier yang jelas.
7.  **Menggunakan Z-score tanpa mempertimbangkan bentuk distribusi.**
    Z-score klasik sensitif terhadap outlier dan skewness.
8.  **Menggunakan Isolation Forest atau LOF tanpa memahami fitur dan
    parameter.** Keluaran model bukan label kebenaran.
9.  **Mempelajari ambang preprocessing dari seluruh data sebelum
    split.** Ini dapat menyebabkan data leakage.
10. **Tidak mendokumentasikan keputusan.** Analisis harus dapat
    ditelusuri dan dijelaskan.

------------------------------------------------------------------------

## 17. Checklist Praktis

### A. Memahami dataset

-   [ ] Periksa `shape`, `head()`, `info()`, dan tipe data.
-   [ ] Periksa missing value, duplikasi, dan nilai unik.
-   [ ] Identifikasi target dan makna setiap fitur.
-   [ ] Pahami unit observasi dan batasan data.

### B. Memahami distribusi

-   [ ] Periksa `describe()` dan statistik numerik.
-   [ ] Buat histogram dan KDE bila relevan.
-   [ ] Bandingkan mean dan median; periksa skewness.
-   [ ] Gunakan boxplot dan ECDF untuk sudut pandang tambahan.
-   [ ] Periksa apakah hasil visual konsisten dengan statistik.

### C. Menyelidiki outlier

-   [ ] Tentukan fitur numerik yang perlu diperiksa.
-   [ ] Pilih IQR, Z-score, MAD, atau metode multivariat sesuai konteks.
-   [ ] Periksa nilai aktual dan sumber data.
-   [ ] Bedakan kesalahan data dari kejadian langka yang valid.

### D. Memutuskan penanganan

-   [ ] Tentukan alasan untuk mempertahankan, memperbaiki,
    mentransformasi, membatasi, atau menghapus.
-   [ ] Catat alasan dan jumlah observasi yang terdampak.
-   [ ] Hindari data leakage saat mempelajari parameter preprocessing.
-   [ ] Evaluasi dampak keputusan terhadap analisis dan model.

### E. Validasi

-   [ ] Bandingkan ringkasan dan grafik sebelum/sesudah.
-   [ ] Pastikan tidak ada perubahan yang merusak makna data.
-   [ ] Dokumentasikan hasil, asumsi, dan keterbatasan.

------------------------------------------------------------------------

## 18. Latihan Pemahaman

Gunakan data durasi penggunaan aplikasi (menit):

``` text
[10, 12, 12, 13, 14, 15, 16, 18, 20, 120]
```

Coba jawab pertanyaan berikut sebelum membaca kunci jawaban.

### Pertanyaan 1

Jika mean jauh lebih tinggi daripada median, apa dugaan awal yang masuk
akal?

-   A. Distribusi pasti normal.
-   B. Distribusi mungkin menceng ke kanan.
-   C. Semua data pasti salah.

### Pertanyaan 2

Jika IQR menandai 120 sebagai kandidat outlier, apa yang sudah
diketahui?

-   A. Nilai 120 pasti salah input.
-   B. Nilai 120 adalah kandidat outlier menurut aturan IQR.
-   C. Nilai 120 harus dihapus.

### Pertanyaan 3

Jika 120 menit dikonfirmasi sebagai durasi sesi yang benar, apa tindakan
yang masuk akal?

-   A. Selalu hapus.
-   B. Selalu lakukan capping pada persentil ke-95.
-   C. Pertimbangkan untuk mempertahankannya dan evaluasi pengaruhnya
    terhadap tujuan model.

### Kunci dan alasan

1.  **B.** Nilai besar dapat menarik mean ke atas. Bentuk distribusi
    perlu diperiksa lebih lanjut.
2.  **B.** Deteksi statistik memberi sinyal untuk investigasi, bukan
    keputusan penghapusan.
3.  **C.** Data valid dinilai berdasarkan tujuan analisis dan dampaknya
    terhadap model.

------------------------------------------------------------------------

## 19. Ringkasan Inti

> **Alur berpikir seorang analis data:**
>
> 1.  **Pahami data:** `shape`, `info()`, `describe()`, missing value,
>     duplikasi, dan contoh baris.
> 2.  **Pahami distribusi:** histogram, KDE, mean, median, skewness,
>     boxplot, dan ECDF.
> 3.  **Deteksi kandidat outlier:** IQR, Z-score, MAD, atau metode
>     multivariat yang sesuai.
> 4.  **Investigasi:** cari tahu apakah nilai ekstrem merupakan
>     kesalahan, kejadian langka yang valid, atau bagian dari kelompok
>     berbeda.
> 5.  **Ambil tindakan:** pertahankan, perbaiki, transformasi, capping,
>     atau hapus berdasarkan bukti.
> 6.  **Validasi:** periksa kembali statistik, visualisasi, dan dampak
>     terhadap model.

### Lima prinsip yang harus diingat

-   `describe()` tetap berguna sebagai ringkasan numerik, tetapi tidak
    menggantikan visualisasi atau konteks.
-   Metode EDA saling melengkapi; masing-masing menjawab pertanyaan
    berbeda.
-   Outlier adalah kandidat observasi tidak biasa, bukan otomatis
    kesalahan.
-   Penanganan outlier harus memiliki alasan yang dapat dijelaskan.
-   EDA yang baik tidak hanya menghasilkan grafik dan angka, tetapi juga
    kesimpulan yang terukur, keterbatasan yang jelas, dan keputusan yang
    dapat dipertanggungjawabkan.

**Target belajarmu:** jangan hanya mampu menjalankan fungsi Pandas atau
Seaborn. Latih diri untuk menjelaskan *mengapa metode dipilih, apa bukti
yang dihasilkan, apa yang dapat disimpulkan, dan apa yang belum
diketahui*.
