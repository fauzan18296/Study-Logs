# 📊 Panduan Lengkap EDA & Outlier Handling
### Data Profiling • Distribution Analysis • Detection • Preprocessing • Machine Learning

> **Tujuan pembelajaran:** memahami cara mendeteksi, menganalisis, memvalidasi, dan menangani outlier berdasarkan karakteristik data, bukan sekadar menerapkan rumus secara otomatis.

---

## 📚 Daftar Isi

1. [Konsep Dasar Outlier](#1-konsep-dasar-outlier)
2. [Alur EDA dan Preprocessing](#2-alur-eda-dan-preprocessing)
3. [Data Profiling dan Statistik Deskriptif](#3-data-profiling-dan-statistik-deskriptif)
4. [Analisis Distribusi](#4-analisis-distribusi)
5. [Metode Outlier Detection](#5-metode-outlier-detection)
6. [Menentukan Persentil untuk Capping](#6-menentukan-persentil-untuk-capping)
7. [Metode Outlier Handling](#7-metode-outlier-handling)
8. [Memilih Metode Berdasarkan Jenis Data](#8-memilih-metode-berdasarkan-jenis-data)
9. [Implementasi Python](#9-implementasi-python)
10. [Preprocessing untuk Machine Learning](#10-preprocessing-untuk-machine-learning)
11. [Evaluasi Sebelum dan Sesudah Handling](#11-evaluasi-sebelum-dan-sesudah-handling)
12. [Checklist EDA dan Preprocessing](#12-checklist-eda-dan-preprocessing)
13. [Kesalahan Umum](#13-kesalahan-umum)
14. [Ringkasan](#14-ringkasan)

---

# 1. Konsep Dasar Outlier

## 1.1 Apa itu outlier?

Outlier adalah observasi yang berbeda secara signifikan dari pola umum data berdasarkan kriteria statistik, model, atau konteks tertentu.

Contoh fitur `Income`:

| Observasi | Income |
|---|---:|
| A | Rp3.000.000 |
| B | Rp3.500.000 |
| C | Rp4.000.000 |
| D | Rp4.500.000 |
| E | Rp50.000.000 |

Nilai Rp50.000.000 terlihat jauh lebih tinggi daripada observasi lainnya. Akan tetapi, nilai tersebut belum tentu merupakan kesalahan data.

Ada tiga kemungkinan utama:

1. **Kesalahan data:** salah memasukkan angka, satuan, atau desimal.
2. **Nilai ekstrem yang valid:** pendapatan tinggi yang benar-benar terjadi.
3. **Anomali:** observasi yang menyimpang dari pola dan memerlukan investigasi lebih lanjut.

## 1.2 Outlier detection vs. outlier handling

| Aspek | Detection | Handling |
|---|---|---|
| Tujuan | Menemukan kandidat outlier | Menentukan tindakan terhadap data |
| Pertanyaan | Nilai mana yang menyimpang? | Apa yang sebaiknya dilakukan? |
| Contoh | IQR, MAD, Isolation Forest | Capping, koreksi, transformasi |
| Hasil | Flag atau daftar observasi | Data yang dipertahankan atau ditransformasikan |

**Penting:** hasil deteksi tidak otomatis menjadi alasan untuk menghapus atau mengubah data.

## 1.3 Outlier univariat dan multivariat

### Univariat

Outlier dianalisis menggunakan satu fitur.

Contoh:
- Income sangat tinggi.
- Quantity negatif.
- TransactionAmount jauh di atas distribusi umum.

Metode yang relevan antara lain IQR, Z-score, MAD, dan percentile threshold.

### Multivariat

Outlier dinilai berdasarkan kombinasi beberapa fitur.

Contoh:

Sebuah transaksi mungkin memiliki nilai `Income` dan `Debt` yang masing-masing masih wajar. Namun, kombinasi pendapatan, utang, pengeluaran, dan karakteristik lainnya mungkin tidak biasa.

Metode yang dapat dipertimbangkan:
- Mahalanobis Distance.
- Isolation Forest.
- Local Outlier Factor.
- DBSCAN.
- One-Class SVM.
- PCA reconstruction error.

---

# 2. Alur EDA dan Preprocessing

```text
Data Collection
      |
      v
Data Profiling
      |
      v
Missing Value & Data Quality
      |
      v
EDA: Distribution Analysis
      |
      v
Outlier Detection
      |
      v
Validasi Konteks dan Domain
      |
      v
Pilih Outlier Handling
      |
      v
Evaluasi Distribusi Kembali
      |
      v
Feature Engineering & Modeling
```

Alur ini tidak selalu linear. Jika hasil pemeriksaan menunjukkan masalah pada data, kita dapat kembali ke tahap sebelumnya.

## 2.1 Data Profiling

Periksa:
- Jumlah baris dan kolom.
- Tipe data setiap fitur.
- Missing value.
- Duplikasi.
- Nilai minimum dan maksimum.
- Statistik deskriptif.
- Nilai unik dan kategori.
- Rentang nilai yang valid menurut domain.

## 2.2 EDA

Gunakan visualisasi dan statistik untuk memahami:
- Bentuk distribusi.
- Skewness.
- Variasi data.
- Nilai ekstrem.
- Hubungan antarf fitur.
- Perbedaan distribusi antarkelompok.
- Perubahan pola dari waktu ke waktu.

## 2.3 Validasi sebelum handling

Sebelum melakukan tindakan, tanyakan:

1. Apakah nilai tersebut benar-benar tidak valid?
2. Apakah nilai ekstrem memiliki makna bisnis?
3. Apakah nilai tersebut berasal dari populasi yang berbeda?
4. Apakah nilai tersebut memengaruhi tujuan analisis atau model?
5. Apa konsekuensi jika nilainya diubah atau dihapus?

---

# 3. Data Profiling dan Statistik Deskriptif

## 3.1 Fungsi `describe()`

`describe()` membantu memahami ringkasan statistik numerik.

```python
df.describe()
```

Untuk melihat kuantil yang lebih lengkap:

```python
df["Income"].describe(
    percentiles=[
        0.01,
        0.05,
        0.25,
        0.50,
        0.75,
        0.95,
        0.98,
        0.99
    ]
)
```

Interpretasi:

| Statistik | Kegunaan |
|---|---|
| `count` | Jumlah nilai yang tersedia |
| `mean` | Rata-rata |
| `std` | Standar deviasi |
| `min` | Nilai minimum |
| `25%` | Kuartil pertama (Q1) |
| `50%` | Median (Q2) |
| `75%` | Kuartil ketiga (Q3) |
| `max` | Nilai maksimum |

### Bagaimana `describe()` membantu analisis outlier?

Contoh:

- `max` sangat jauh di atas P99: periksa ekor atas.
- `min` negatif pada fitur yang seharusnya tidak negatif: periksa aturan domain.
- `mean` jauh lebih tinggi daripada median: mungkin ada skewness positif atau nilai ekstrem.
- `std` sangat besar: periksa variasi data dan kemungkinan nilai ekstrem.

Namun, semua indikator tersebut hanya petunjuk. Tidak satu pun membuktikan outlier secara otomatis.

---

# 4. Analisis Distribusi

## 4.1 Histogram

Histogram memperlihatkan frekuensi observasi dalam interval nilai.

```python
import matplotlib.pyplot as plt

df["Income"].hist(bins=40)

plt.title("Distribution of Income")
plt.xlabel("Income")
plt.ylabel("Frequency")
plt.show()
```

Gunakan histogram untuk memeriksa:
- Bentuk distribusi.
- Ekor panjang.
- Kelompok nilai yang berbeda.
- Nilai yang jarang muncul.
- Kemungkinan distribusi multimodal.

Jumlah `bins` memengaruhi tampilan. Terlalu sedikit bin dapat menyembunyikan pola, sedangkan terlalu banyak bin dapat membuat distribusi terlihat berisik.

## 4.2 KDE (Kernel Density Estimate)

KDE memperkirakan kepadatan distribusi sebagai kurva yang lebih halus.

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.histplot(
    data=df,
    x="Income",
    kde=True
)

plt.show()
```

KDE berguna untuk memahami:
- Puncak distribusi.
- Kemencengan.
- Bentuk ekor.
- Kemungkinan beberapa kelompok nilai.

KDE bukan alat yang membuktikan adanya outlier. Bentuk kurva juga dipengaruhi bandwidth.

## 4.3 Boxplot

```python
sns.boxplot(data=df, x="Income")
plt.show()
```

Boxplot menampilkan:
- Median.
- Q1 dan Q3.
- IQR.
- Whisker.
- Titik yang berada di luar whisker.

Whisker boxplot biasanya menggunakan aturan 1,5 × IQR, bukan otomatis mencapai nilai minimum dan maksimum seluruh dataset.

## 4.4 Skewness

Skewness menggambarkan kemencengan distribusi.

| Kondisi | Interpretasi |
|---|---|
| Mendekati 0 | Distribusi relatif simetris |
| Positif | Ekor cenderung lebih panjang ke kanan |
| Negatif | Ekor cenderung lebih panjang ke kiri |

```python
df["Income"].skew()
```

Skewness sensitif terhadap nilai ekstrem. Distribusi dengan skewness tinggi tidak otomatis memiliki data yang salah.

## 4.5 Q-Q plot

Q-Q plot membandingkan kuantil data dengan kuantil distribusi referensi, misalnya distribusi normal.

```python
import scipy.stats as stats
import matplotlib.pyplot as plt

stats.probplot(
    df["Income"].dropna(),
    dist="norm",
    plot=plt
)

plt.show()
```

Jika titik-titik menyimpang secara sistematis dari garis referensi, distribusi mungkin tidak mengikuti distribusi normal dengan baik.

## 4.6 ECDF

Empirical Cumulative Distribution Function menunjukkan proporsi observasi yang kurang dari atau sama dengan suatu nilai.

```python
sns.ecdfplot(data=df, x="Income")
plt.show()
```

ECDF berguna untuk memahami posisi persentil dan proporsi observasi di atas atau di bawah ambang tertentu.

## 4.7 Distribusi multimodal

Distribusi multimodal memiliki beberapa puncak.

Contohnya, data pengeluaran mungkin menggabungkan:
- Pelanggan individu.
- Pelanggan bisnis kecil.
- Pelanggan korporasi.

Sebelum melakukan capping global, periksa apakah kelompok tersebut memang memiliki karakteristik yang berbeda.

---

# 5. Metode Outlier Detection

## 5.1 IQR (Interquartile Range)

IQR mengukur rentang antara kuartil ketiga dan kuartil pertama.

```math
IQR = Q_3 - Q_1
```

Batas bawah:

```math
L = Q_1 - 1.5(IQR)
```

Batas atas:

```math
U = Q_3 + 1.5(IQR)
```

Kandidat outlier:

```math
x_i < L \quad \text{atau} \quad x_i > U
```

Contoh implementasi:

```python
q1 = df["Income"].quantile(0.25)
q3 = df["Income"].quantile(0.75)

iqr = q3 - q1

lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

mask = (
    (df["Income"] < lower) |
    (df["Income"] > upper)
)

print("Lower:", lower)
print("Upper:", upper)
print("Candidates:", mask.sum())
```

**Kelebihan:** tidak mensyaratkan distribusi normal.

**Keterbatasan:** pada distribusi berekor panjang, IQR dapat menandai banyak nilai valid.

## 5.2 Z-score

Z-score mengukur jarak nilai dari rata-rata dalam satuan standar deviasi.

```math
z_i = \frac{x_i-\mu}{\sigma}
```

Ambang yang sering digunakan:

```math
|z_i| > 3
```

```python
from scipy.stats import zscore

z = zscore(
    df["Income"],
    nan_policy="omit"
)

mask = abs(z) > 3
```

**Cocok:** data yang mendekati normal dan tidak terlalu terpengaruh oleh nilai ekstrem.

**Keterbatasan:** mean dan standar deviasi sensitif terhadap outlier.

## 5.3 Modified Z-score dengan MAD

MAD menggunakan median absolute deviation.

```math
MAD = \operatorname{median}(|x_i-\tilde{x}|)
```

Modified Z-score:

```math
M_i =
\frac{0.6745(x_i-\tilde{x})}{MAD}
```

Ambang umum:

```math
|M_i| > 3.5
```

Implementasi:

```python
import numpy as np

x = df["Income"]

median = x.median()
mad = (x - median).abs().median()

if mad > 0:
    modified_z = 0.6745 * (x - median) / mad
    mask = modified_z.abs() > 3.5
else:
    mask = pd.Series(False, index=x.index)
```

Jika MAD = 0, hasil tersebut tidak berarti seluruh nilai pasti normal. Perlu metode alternatif atau pemeriksaan khusus.

## 5.4 Percentile threshold

Ambang ditentukan berdasarkan kuantil.

```math
L = Q_{0.01}(X)
```

```math
U = Q_{0.99}(X)
```

```python
lower = df["Income"].quantile(0.01)
upper = df["Income"].quantile(0.99)

mask = (
    (df["Income"] < lower) |
    (df["Income"] > upper)
)
```

Persentil mengatur posisi ekor distribusi. Persentil tidak membuktikan bahwa observasi di ekor merupakan kesalahan.

## 5.5 Hampel Filter

Hampel Filter membandingkan suatu nilai dengan median lokal dan MAD dalam jendela tertentu.

Cocok untuk:
- Data sensor.
- Deret waktu.
- Pengukuran berurutan.

Perlu diperhatikan:
- Ukuran jendela.
- Pola lokal.
- Tren dan musiman.
- Kemungkinan lonjakan yang merupakan kejadian nyata.

## 5.6 Validasi berbasis domain

Contoh:
- Jumlah barang tidak boleh negatif.
- Persentase dengan definisi 0–100 tidak boleh di luar rentang itu.
- Tanggal lahir tidak boleh setelah tanggal transaksi.
- Nilai pengukuran tidak boleh melanggar batas fisik yang benar-benar berlaku.

Validasi domain sering kali lebih kuat daripada aturan statistik ketika batas yang benar sudah diketahui.

## 5.7 Mahalanobis Distance

Mengukur jarak multivariat dengan mempertimbangkan kovarians.

```math
D_M^2 = (x-\mu)^T\Sigma^{-1}(x-\mu)
```

Cocok untuk fitur numerik yang memiliki korelasi.

Keterbatasan:
- Estimasi kovarians sensitif terhadap outlier.
- Asumsi distribusi perlu diperiksa.
- Fitur dengan masalah skala atau multikolinearitas perlu diperhatikan.

## 5.8 Isolation Forest

Menggunakan pohon acak untuk mengisolasi observasi.

Cocok untuk data multivariat dengan banyak fitur.

Keterbatasan:
- Hasil bergantung pada parameter.
- Anomali tidak selalu merupakan kesalahan.
- Fitur dan representasi data memengaruhi hasil.

## 5.9 Local Outlier Factor (LOF)

Membandingkan kepadatan lokal observasi dengan kepadatan tetangganya.

Cocok untuk mendeteksi anomali lokal pada kelompok dengan kepadatan berbeda.

Keterbatasan:
- Sensitif terhadap jumlah tetangga.
- Scaling penting.
- Hasil dipengaruhi struktur lokal data.

## 5.10 DBSCAN

Mengelompokkan observasi berdasarkan kepadatan. Titik yang tidak masuk ke kelompok tertentu dapat dianggap noise.

Cocok untuk struktur kelompok nonlinier atau geografis.

Parameter utama:
- `eps`
- `min_samples`

Noise bukan otomatis kesalahan data.

## 5.11 One-Class SVM

Mempelajari wilayah yang dianggap normal.

Cocok ketika batas normal tidak sederhana dan data normal dapat dipelajari.

Keterbatasan:
- Sensitif terhadap scaling.
- Pemilihan parameter penting.
- Dapat mahal untuk dataset besar.

## 5.12 PCA reconstruction error

PCA mereduksi dimensi, kemudian kesalahan rekonstruksi dapat digunakan sebagai indikator penyimpangan.

```math
e_i = \|x_i-\hat{x}_i\|_2^2
```

Cocok untuk data numerik berdimensi tinggi ketika anomali menyimpang dari struktur utama data.

## 5.13 Metode berbasis konteks

| Metode | Tujuan |
|---|---|
| Residual analysis | Menemukan observasi yang jauh dari prediksi model |
| Control charts | Memantau penyimpangan proses |
| Seasonal decomposition | Mendeteksi penyimpangan dari tren dan musiman |
| Change-point detection | Mendeteksi perubahan pola statistik |
| Robust regression | Mengurangi pengaruh nilai ekstrem pada estimasi regresi |

---

# 6. Menentukan Persentil untuk Capping

## 6.1 Apa itu capping?

Capping membatasi nilai yang melewati ambang tanpa menghapus observasinya.

```math
x_{\text{capped}} =
\begin{cases}
L, & x < L\\
x, & L \le x \le U\\
U, & x > U
\end{cases}
```

Keterangan:
- L = batas bawah.
- U = batas atas.

## 6.2 Strategi persentil

| Strategi | Batas bawah | Batas atas | Karakteristik |
|---|---|---|---|
| P1–P99 | P1 | P99 | Relatif ringan |
| P2.5–P97.5 | P2.5 | P97.5 | Lebih agresif |
| P0.5–P99.5 | P0.5 | P99.5 | Lebih konservatif |
| P5–P95 | P5 | P95 | Agresif |
| Upper-only P95 | Nilai minimum asli | P95 | Hanya membatasi ekor atas |
| Upper-only P98 | Nilai minimum asli | P98 | Membatasi ekor atas secara lebih konservatif |
| Domain-based | Batas valid minimum | Batas valid maksimum | Berdasarkan aturan nyata |

Persentil-persentil tersebut adalah kandidat, bukan aturan universal.

## 6.3 Distribusi simetris

Pada distribusi simetris, capping di kedua sisi dapat dipertimbangkan jika nilai ekstrem pada kedua ekor memang perlu dibatasi.

P1–P99 membatasi sekitar 1% di setiap ekor.

Namun, distribusi simetris tidak otomatis membutuhkan capping. Jika nilai ekstrem valid dan penting, mempertahankan nilai asli mungkin lebih tepat.

## 6.4 Distribusi right-skewed

Pada distribusi dengan ekor kanan panjang, seperti pendapatan atau biaya transaksi, pertimbangkan apakah hanya ekor atas yang menjadi masalah.

| Batas atas | Proporsi teoritis di atas batas |
|---|---:|
| P95 | 5% |
| P98 | 2% |
| P99 | 1% |

Upper-only capping dapat dipertimbangkan ketika batas atas memang relevan, tetapi jangan menganggap seluruh nilai tinggi sebagai kesalahan.

## 6.5 Banyak nilai ekstrem

P5–P95 membatasi sekitar 5% pada setiap ekor, atau sekitar 10% observasi secara keseluruhan.

Strategi ini lebih agresif daripada P1–P99.

Namun, banyak nilai ekstrem bukan bukti bahwa capping agresif diperlukan. Jika nilai berasal dari transaksi valid, pembatasan dapat menghilangkan informasi penting.

## 6.6 Mengapa distribusi saja tidak cukup?

Distribusi membantu membentuk hipotesis tentang batas yang masuk akal, tetapi keputusan perlu mempertimbangkan:

1. Validitas nilai.
2. Domain bisnis.
3. Banyaknya observasi yang terdampak.
4. Perubahan statistik setelah handling.
5. Tujuan analisis.
6. Dampak terhadap model.

## 6.7 Contoh menghitung dampak capping

Misalnya terdapat 10.000 observasi tanpa nilai yang sama pada ambang.

| Strategi dua sisi | Perkiraan observasi terdampak |
|---|---:|
| P1–P99 | 200 |
| P2.5–P97.5 | 500 |
| P5–P95 | 1.000 |

Perkiraan ini berdasarkan posisi kuantil. Jumlah aktual dapat berbeda karena ties, interpolasi kuantil, dan implementasi persentil.

Capping mempertahankan baris, tetapi mengubah nilai pada bagian ekor.

## 6.8 Memeriksa kandidat persentil dengan Pandas

```python
col = df["TransactionAmount"].dropna()

print(
    col.describe(
        percentiles=[0.01, 0.05, 0.95, 0.98, 0.99]
    )
)

print("Skewness:", col.skew())

for p in [0.95, 0.98, 0.99]:
    upper = col.quantile(p)
    affected = (col > upper).sum()

    print({
        "percentile": f"P{int(p * 100)}",
        "upper_limit": upper,
        "affected_rows": affected,
        "affected_percent": (col > upper).mean() * 100
    })
```

Gunakan hasil tersebut untuk membandingkan kandidat. Jangan memilih batas hanya berdasarkan skewness.

---

# 7. Metode Outlier Handling

## 7.1 Keep / retain

Mempertahankan nilai asli.

Cocok ketika:
- Nilai ekstrem valid.
- Nilai tersebut penting secara bisnis.
- Analisis memang bertujuan mempelajari kejadian ekstrem.

## 7.2 Correct

Memperbaiki nilai ketika sumber kesalahan diketahui.

Contoh:
- Salah memasukkan satuan.
- Kesalahan desimal.
- Nilai yang dapat dipulihkan dari sumber terpercaya.

## 7.3 Capping / winsorization

Membatasi nilai di bawah atau di atas ambang.

```python
lower = df["Income"].quantile(0.01)
upper = df["Income"].quantile(0.99)

df["Income_capped"] = df["Income"].clip(
    lower=lower,
    upper=upper
)
```

Capping mengurangi rentang nilai ekstrem, tetapi dapat menghilangkan informasi pada ekor distribusi.

## 7.4 Trimming / deletion

Menghapus observasi tertentu.

```python
df_trimmed = df.loc[~mask].copy()
```

Gunakan hanya ketika ada alasan yang dapat dipertanggungjawabkan, misalnya observasi tidak valid atau tidak memenuhi kriteria penelitian.

Penghapusan dapat mengubah komposisi populasi.

## 7.5 Log transformation

Untuk fitur positif dengan distribusi sangat miring ke kanan:

```python
import numpy as np

df["Income_log"] = np.log1p(df["Income"])
```

`log1p(x)` menghitung logaritma natural dari `1 + x`.

Transformasi ini mengubah skala dan hubungan antar nilai. Transformasi ini bukan penghapusan outlier.

Nilai harus memenuhi domain log yang sesuai; `log1p` tidak dapat menangani nilai kurang dari atau sama dengan -1 dalam bilangan real.

## 7.6 Yeo–Johnson transformation

Transformasi ini dapat menangani nilai positif, nol, dan negatif.

```python
from sklearn.preprocessing import PowerTransformer

transformer = PowerTransformer(
    method="yeo-johnson"
)

X_transformed = transformer.fit_transform(X_train)
```

Parameter transformasi harus dipelajari dari data training dan digunakan kembali pada data lain.

## 7.7 Robust scaling

Menggunakan median dan IQR untuk melakukan scaling.

```math
x_{\text{scaled}} =
\frac{x-\operatorname{median}(X)}
{Q_3-Q_1}
```

```python
from sklearn.preprocessing import RobustScaler

scaler = RobustScaler()

X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

Robust scaling tidak menghapus outlier. Tujuannya mengurangi pengaruh nilai ekstrem pada parameter scaling.

Jika IQR nol, fitur memerlukan pemeriksaan atau penanganan khusus.

## 7.8 Robust imputation

Mengganti nilai yang terbukti tidak valid atau diperlakukan sebagai missing menggunakan estimasi yang sesuai.

Contohnya median:

```python
median_value = X_train["Income"].median()
```

Jangan mengganti nilai ekstrem yang valid dengan median hanya karena nilainya jauh dari mayoritas.

## 7.9 Binning

Mengubah nilai numerik menjadi kelompok interval.

```python
df["Income_group"] = pd.cut(
    df["Income"],
    bins=[0, 3_000_000, 7_000_000, 15_000_000, float("inf")],
    labels=["Low", "Medium", "High", "Very High"]
)
```

Binning dapat berguna untuk analisis kategori, tetapi mengurangi detail numerik. Batas interval perlu memiliki alasan yang jelas.

## 7.10 Group-wise handling

Menentukan batas per kelompok ketika kelompok tersebut memiliki karakteristik yang berbeda.

Contoh:
- Harga berdasarkan jenis properti.
- Pendapatan berdasarkan jabatan.
- Jumlah transaksi berdasarkan jenis pelanggan.

Pastikan kelompok tersebut memang relevan dan tersedia saat data baru diproses.

## 7.11 Model robust

Model tertentu lebih tahan terhadap pengaruh nilai ekstrem daripada model lainnya.

Contoh:
- Robust regression.
- Model berbasis pohon.
- Metode yang menggunakan loss function robust.

Model berbasis pohon tidak kebal terhadap outlier. Nilai ekstrem masih dapat memengaruhi split, struktur pohon, dan prediksi.

---

# 8. Memilih Metode Berdasarkan Jenis Data

| Jenis data | Metode analisis yang relevan |
|---|---|
| Numerik kontinu | Histogram, KDE, boxplot, IQR, MAD |
| Numerik diskrit | Frekuensi nilai, batas domain, IQR jika sesuai |
| Kategorikal | Frekuensi kategori langka, validasi label |
| Tanggal/waktu | Rentang valid, urutan waktu, pola musiman |
| Geografis | Batas wilayah, jarak, pola spasial |
| Multivariat numerik | Mahalanobis, Isolation Forest, LOF, PCA |
| Target regresi | Residual analysis setelah model awal, jika sesuai |

Kategori langka tidak otomatis merupakan outlier. Kategori tersebut mungkin sangat penting untuk analisis.

## 8.1 Contoh keputusan

| Situasi | Tindakan awal |
|---|---|
| Nilai negatif padahal secara domain mustahil | Validasi dan koreksi |
| Pendapatan tinggi yang valid | Pertahankan atau uji transformasi |
| Distribusi right-skewed | Periksa IQR, MAD, persentil, dan log transformation |
| Nilai melonjak pada sensor | Periksa konteks temporal dan Hampel Filter |
| Observasi aneh berdasarkan kombinasi fitur | Pertimbangkan metode multivariat |
| Banyak kelompok dengan rentang berbeda | Analisis per kelompok sebelum capping |
| Kesalahan pengukuran yang tidak dapat dipulihkan | Pertimbangkan missing atau eksklusi yang beralasan |

---

# 9. Implementasi Python

## 9.1 Pemeriksaan awal

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

col_name = "Income"
x = df[col_name]

print("Data type:", x.dtype)
print("Missing:", x.isna().sum())
print("Unique:", x.nunique())
print(x.describe())

print("Skewness:", x.skew())
print("Kurtosis:", x.kurtosis())
```

Kurtosis pada Pandas secara default menggunakan excess kurtosis. Nilai kurtosis bukan alat tunggal untuk memutuskan handling.

## 9.2 Visualisasi awal

```python
fig, axes = plt.subplots(1, 2, figsize=(12, 4))

sns.histplot(x=x.dropna(), kde=True, ax=axes[0])
axes[0].set_title("Distribution")

sns.boxplot(x=x, ax=axes[1])
axes[1].set_title("Boxplot")

plt.tight_layout()
plt.show()
```

## 9.3 Deteksi dengan IQR

```python
q1 = x.quantile(0.25)
q3 = x.quantile(0.75)

iqr = q3 - q1

lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

mask_iqr = x.notna() & (
    (x < lower) | (x > upper)
)

print("Lower:", lower)
print("Upper:", upper)
print("Count:", mask_iqr.sum())
print("Percentage:", mask_iqr.mean() * 100)
```

## 9.4 Memeriksa observasi kandidat

```python
candidates = df.loc[mask_iqr, [col_name]]

print(candidates.sort_values(col_name))
```

Jika dataset memiliki banyak kolom, jangan hanya melihat nilainya. Periksa kolom lain yang dapat menjelaskan observasi tersebut.

## 9.5 Capping dengan batas IQR

```python
df["Income_capped"] = x.clip(
    lower=lower,
    upper=upper
)
```

Ini hanya contoh penerapan. Batas IQR tidak otomatis merupakan pilihan terbaik untuk semua dataset.

## 9.6 Capping dengan persentil

```python
lower_p = x.quantile(0.01)
upper_p = x.quantile(0.99)

df["Income_p99_capped"] = x.clip(
    lower=lower_p,
    upper=upper_p
)
```

Untuk upper-only capping:

```python
upper_p95 = x.quantile(0.95)

df["Income_upper_capped"] = x.clip(
    upper=upper_p95
)
```

Tanpa argumen `lower`, `clip` mempertahankan nilai di bawah batas atas sesuai perilaku default Pandas.

## 9.7 Membandingkan statistik sebelum dan sesudah

```python
comparison = pd.DataFrame({
    "Original": x.describe(
        percentiles=[0.01, 0.25, 0.50, 0.75, 0.99]
    ),
    "Capped": df["Income_capped"].describe(
        percentiles=[0.01, 0.25, 0.50, 0.75, 0.99]
    )
})

print(comparison)
```

Periksa:
- Mean.
- Median.
- Standar deviasi.
- IQR.
- Minimum dan maksimum.
- Kuantil.
- Proporsi observasi yang terdampak.

## 9.8 Perbandingan visual

```python
fig, axes = plt.subplots(1, 2, figsize=(12, 4))

sns.histplot(
    x=df["Income"].dropna(),
    kde=True,
    ax=axes[0]
)
axes[0].set_title("Before Handling")

sns.histplot(
    x=df["Income_capped"].dropna(),
    kde=True,
    ax=axes[1]
)
axes[1].set_title("After Capping")

plt.tight_layout()
plt.show()
```

Tujuannya bukan membuat distribusi sesudah handling tampak lebih normal, tetapi memahami informasi yang berubah.

---

# 10. Preprocessing untuk Machine Learning

## 10.1 Hindari data leakage

Jangan menghitung persentil, median, scaler, atau parameter transformasi dari seluruh dataset sebelum pemisahan training dan test.

Alur yang disarankan:

```text
Dataset
   |
   v
Train-Test Split
   |
   +------> Training Data
   |            |
   |            v
   |      Fit Preprocessing
   |            |
   |            v
   |      Train Model
   |
   +------> Test Data
                |
                v
       Apply Training Parameters
                |
                v
        Evaluate Final Model
```

## 10.2 Contoh capping tanpa leakage

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)

lower = X_train["Income"].quantile(0.01)
upper = X_train["Income"].quantile(0.99)

X_train = X_train.copy()
X_test = X_test.copy()

X_train["Income"] = X_train["Income"].clip(
    lower=lower,
    upper=upper
)

X_test["Income"] = X_test["Income"].clip(
    lower=lower,
    upper=upper
)
```

Parameter batas berasal dari training set. Batas yang sama diterapkan pada test set.

Dalam proyek nyata, lebih baik mengemas preprocessing dalam transformer atau pipeline agar proses fitting dan transformasi konsisten.

## 10.3 Cross-validation

Jika menggunakan cross-validation, parameter preprocessing harus dipelajari hanya dari training fold pada setiap iterasi.

Jangan melakukan capping menggunakan seluruh data sebelum cross-validation karena informasi dari fold validasi dapat memengaruhi preprocessing.

## 10.4 Apakah model berbasis pohon membutuhkan capping?

Tidak selalu.

Decision Tree dan Random Forest biasanya tidak membutuhkan scaling seperti KNN atau SVM. Akan tetapi, nilai ekstrem masih dapat memengaruhi split dan perilaku model.

Untuk regresi, outlier pada target juga dapat memengaruhi loss dan estimasi. Jangan otomatis menghapus target ekstrem karena dapat mengubah pertanyaan yang ingin dijawab model.

---

# 11. Evaluasi Sebelum dan Sesudah Handling

Evaluasi bukan sekadar melihat apakah outlier berkurang.

## 11.1 Evaluasi statistik

Bandingkan:
- Mean dan median.
- Standar deviasi.
- IQR.
- Kuantil.
- Skewness.
- Minimum dan maksimum.
- Jumlah dan persentase observasi terdampak.

## 11.2 Evaluasi konteks

Periksa:
- Apakah nilai hasil transformasi masih masuk akal?
- Apakah kelompok penting berubah?
- Apakah kejadian langka yang valid ikut terpengaruh?
- Apakah hasil dapat dijelaskan kepada pengguna bisnis?

## 11.3 Evaluasi model

Untuk tugas prediksi, bandingkan kandidat pipeline pada pembagian data yang sama dan gunakan metrik yang relevan.

Contohnya:
- MAE.
- RMSE.
- R².
- Precision, recall, dan F1 untuk klasifikasi.
- Metrik yang mempertimbangkan biaya kesalahan bisnis.

Pilih strategi berdasarkan performa dan tujuan penggunaan, bukan hanya karena distribusi hasil preprocessing tampak lebih rapi.

---

# 12. Checklist EDA dan Preprocessing

## Data Profiling

- [ ] Memeriksa bentuk dataset.
- [ ] Memeriksa tipe data.
- [ ] Memeriksa missing value.
- [ ] Memeriksa duplikasi.
- [ ] Memeriksa nilai unik dan batas domain.
- [ ] Menggunakan `describe()`.

## Distribution Analysis

- [ ] Memeriksa histogram.
- [ ] Memeriksa KDE bila sesuai.
- [ ] Memeriksa boxplot.
- [ ] Memeriksa skewness.
- [ ] Memeriksa kuantil.
- [ ] Mempertimbangkan Q-Q plot jika normalitas relevan.
- [ ] Memeriksa kelompok atau tren waktu bila diperlukan.

## Outlier Detection

- [ ] Memilih metode yang sesuai.
- [ ] Mencatat batas yang digunakan.
- [ ] Menghitung jumlah kandidat.
- [ ] Menghitung persentase kandidat.
- [ ] Memeriksa observasi yang ditandai.
- [ ] Memvalidasi berdasarkan konteks.

## Outlier Handling

- [ ] Memutuskan keep, correct, cap, transform, impute, atau trim.
- [ ] Mendokumentasikan alasan.
- [ ] Memastikan metode sesuai tujuan analisis.
- [ ] Membandingkan distribusi sebelum dan sesudah.
- [ ] Memeriksa informasi yang hilang akibat transformasi.

## Machine Learning

- [ ] Memisahkan data sebelum mempelajari parameter preprocessing.
- [ ] Menghindari leakage pada cross-validation.
- [ ] Menerapkan parameter training pada validasi dan test.
- [ ] Membandingkan kandidat pipeline.
- [ ] Mengevaluasi dengan metrik yang relevan.

---

# 13. Kesalahan Umum

### ❌ Menganggap setiap titik di luar boxplot sebagai kesalahan

**Perbaikan:** anggap sebagai kandidat yang perlu diperiksa.

### ❌ Menggunakan P1–P99 untuk semua fitur

**Perbaikan:** pilih batas berdasarkan konteks, validitas data, dan dampak handling.

### ❌ Menganggap distribusi right-skewed harus di-cap pada P95

**Perbaikan:** pertimbangkan P95, P98, P99, transformasi, atau mempertahankan data. Tidak ada persentil universal.

### ❌ Menggunakan P5–P95 karena pencilan terlihat banyak

**Perbaikan:** cari penyebabnya. Banyak nilai ekstrem bisa menjadi karakteristik asli populasi.

### ❌ Menganggap robust scaling menghilangkan outlier

**Perbaikan:** robust scaling mengubah skala, bukan menghapus atau membatasi nilai ekstrem.

### ❌ Menghapus semua nilai ekstrem

**Perbaikan:** bedakan kesalahan, nilai valid, dan anomali yang perlu investigasi.

### ❌ Menghitung batas dari seluruh dataset sebelum split

**Perbaikan:** pelajari parameter preprocessing hanya dari training data.

### ❌ Memilih handling hanya karena membuat histogram lebih normal

**Perbaikan:** pertimbangkan kualitas data, tujuan analisis, interpretasi, dan hasil evaluasi.

---

# 14. Ringkasan

| Pertanyaan | Jawaban |
|---|---|
| Apa tujuan detection? | Menemukan kandidat observasi yang menyimpang |
| Apa tujuan handling? | Menentukan tindakan yang sesuai terhadap data |
| Metode univariat yang umum? | IQR, Z-score, MAD, persentil |
| Metode multivariat yang umum? | Mahalanobis, Isolation Forest, LOF, DBSCAN, One-Class SVM, PCA |
| Kapan memakai capping? | Ketika pembatasan nilai dapat dibenarkan dan bermanfaat |
| Mengapa persentil berbeda? | Karena tingkat pembatasan dan asumsi yang berbeda |
| Apakah skewness menentukan persentil? | Tidak, hanya membantu memahami distribusi |
| Apakah outlier harus dihapus? | Tidak |
| Apakah `describe()` tetap diperlukan? | Ya, untuk memahami statistik sebelum dan sesudah |
| Apakah semua model perlu capping? | Tidak |
| Bagaimana mencegah leakage? | Pelajari parameter preprocessing hanya dari training data |

## Prinsip utama

> **EDA membantu memahami data. Detection menandai kandidat. Validasi menentukan apakah nilai bermasalah. Handling menentukan tindakan yang dapat dipertanggungjawabkan. Evaluasi memastikan bahwa tindakan tersebut sesuai dengan tujuan analisis atau Machine Learning.**

Tidak ada satu metode outlier yang terbaik untuk semua data. Pilihan yang baik harus didukung oleh bukti statistik, konteks domain, dan evaluasi yang tepat.
