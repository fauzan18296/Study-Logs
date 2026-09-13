# ‼️ Outlier: Deteksi dan Penanganan

Outlier adalah nilai yang jauh berbeda dari mayoritas data. Bisa berupa **error** (salah input, sensor rusak) atau **nilai ekstrem yang sah** (CEO di data gaji karyawan). Membedakan keduanya adalah setengah dari pekerjaan — jangan asal buang.

> **Dampak outlier:** menggeser mean & standar deviasi, merusak model sensitif skala (linear regression, KNN, neural network), tapi relatif aman untuk model berbasis pohon (random forest, XGBoost).

----

## 📐 Berikut beberapa cara untuk menangani dan mendeteksi outlier:

### 1.  Deteksi Visual: Boxplot & Histogram

Boxplot menampilkan outlier sebagai titik di luar whisker. Histogram menunjukkan ekor distribusi. Selalu mulai dari visual — angka saja bisa menipu.

**Code:**
```python
fig, ((axs0, axs1), (axs2, axs3)) = plt.subplots(2, 2, figsize=(10, 8))
sns.boxplot(x=df_detect_outlier["Price"], ax=axs0)
axs0.set_title("Boxplot Price")
sns.histplot(df_detect_outlier["Price"], bins=30, ax=axs1)
axs1.set_title("Histogram Price")

sns.boxplot(x=df_detect_outlier["Distance"], ax=axs2)
axs2.set_title("Boxplot Distance")
sns.histplot(df_detect_outlier["Distance"], bins=30, ax=axs3)
axs3.set_title("Histogram Distance")
plt.tight_layout()
plt.show()
```

**Output:**

![visual_boxplot](/Images/output_detect_outlier_boxplot.png)

---
#### 1.1 📖 Bagaimana cara baca visual boxplot?
---
- **Titik Bulat:** Outlier
- **Garis Tengah Dalam Kotak Biru:** Median
- **Kotak Biru:** Data utama biasanya q1-q3
- **Batas Garis:** Range data yang dianggap normal

----

### 2. Metode IQR (Interquartile Range)
Metode paling umum dan tahan terhadap distribusi tidak normal:

- IQR = Q3 - Q1
- Batas bawah = Q1 - 1.5 x IQR
- Batas atas = Q3 + 1.5 x IQR
- Nilai di luar batas = outlier

**Code:**
```python
Q1 = df_detect_outlier["Price"].quantile(0.25)
Q3 = df_detect_outlier["Price"].quantile(0.75)
IQR = Q3 - Q1
batas_bawah = Q1 - 1.5 * IQR
batas_atas = Q3 + 1.5 * IQR

outlier_mask = (df_detect_outlier["Price"] < batas_bawah) | (df_detect_outlier["Price"] > batas_atas)
print(f"Batas: [{batas_bawah:.1f}, {batas_atas:.1f}]")
print(f"Jumlah outlier: {outlier_mask.sum()}")
df_detect_outlier[outlier_mask]
```

**Output:**
```bash
Batas: [-437500.0, 2382500.0]
Jumlah outlier: 288
```
![output_IQR_Method](/Images/method_IQR_outlier.png)

---

#### 🖼️❔ 2.1 Apa konsep metode IQR pada kode diatas?
---

Konsep dasarnya adalah:

> "Mayoritas data berada di area tengah distribusi. Jika suatu nilai terlalu jauh dari area tengah tersebut, nilai itu dianggap outlier."

Metode IQR tidak melihat rata-rata (mean), tetapi melihat penyebaran 50% data di tengah.

Misalnya data:
```python
[10, 12, 13, 15, 16, 18, 20, 22, 100]
```

Secara intuitif:

- 10–22 terlihat sebagai kelompok utama
- 100 jauh sekali dari kelompok tersebut
IQR mencoba mengukur "seberapa lebar kelompok utama" lalu menentukan batas wajar di luar kelompok tersebut.

---
#### 🗝️❔ 2.2 Kenapa Metode IQR dianggap tahan terhadap distribusi tidak normal?
---
Asumsi yang perlu diuji:
> "Semua metode statistik membutuhkan distribusi normal."

Pada semua metode statistik tidak selalu membutuhkan distribusi normal.

IQR menggunakan: 
- Q1 (25%)
- Median (50%)
- Q3 (75%)

yang merupakan statistik berbasis urutan (ranking), bukan nilai absolut.

Misalnya:

##### **Mean**
Data:
```python 
[10, 12, 15, 18, 1000]
```
**Mean:**
```python
211
```
Nilai 1000 membuat mean berubah drastis.

##### **Median**
Data yang sama:
```python
[10, 12, 15, 18, 1000]
```

**Median:**
```python
15
```

Tidak banyak berubah.

Karena Q1 dan Q3 juga berbasis posisi data yang sudah diurutkan, outlier besar tidak terlalu memengaruhi hasilnya.

Itulah sebabnya IQR disebut **robust (tahan)** terhadap:

- distribusi miring (skewed)
- distribusi tidak normal
- outlier ekstrem

---
#### 🤔❔ 2.3  Mengapa ada Q1, Q3, IQR, batas bawah/atas, dan outlier mask?
---

Mari lihat fungsi masing-masing.

**Q1**
```python 
Q1 = df["Price"].quantile(0.25)
```

Menentukan titik di mana 25% data berada di bawahnya.

**Q3**

```python
Q3 = df["Price"].quantile(0.75)
```

Menentukan titik di mana 75% data berada di bawahnya.

**IQR**

```python
IQR = Q3 - Q1
```

Mengukur lebar area tengah.

Visualnya:
```
|----25%----|====50%====|----25%----|
            ^          ^
           Q1         Q3
```

Bagian tengah:
```
Q1 <---- IQR ----> Q3
```

**Batas bawah dan atas**

```python
batas_bawah = Q1 - 1.5 * IQR
batas_atas = Q3 + 1.5 * IQR
```

Digunakan untuk menentukan:

> "Seberapa jauh data boleh menyimpang dari kelompok utama."

Angka 1.5 bukan hukum alam.

Itu aturan praktis (rule of thumb) yang diperkenalkan oleh statistikawan John Tukey.

**Outlier Mask**

```python
outlier_mask = (
    (df["Price"] < batas_bawah) |
    (df["Price"] > batas_atas)
)
```

Menghasilkan:

```python
False
False
True
False
```

Mask hanyalah penanda:
```python
True  -> outlier
False -> bukan outlier
```

---
#### ⚙️❔ 2.4 Bagaimana cara kerja metode IQR ini?
---

Misalnya:

```python
Price:
10
12
15
18
20
22
25
28
100
```

##### **Langkah 1**

Hitung quartile

```python
Q1 = 13.5
Q3 = 26.5
```

##### **Langkah 2**

Hitung IQR

```python 
IQR = 26.5 - 13.5
IQR = 13
```

##### **Langkah 3**
Hitung batas

```python
Lower = 13.5 - (1.5 × 13)
      = -6

Upper = 26.5 + (1.5 × 13)
      = 46
```

##### **Langkah 4**

Periksa semua nilai

```python
10   -> valid
12   -> valid
15   -> valid
28   -> valid
100  -> outlier
```

Karena:

```python
100 > 46
```

---

### 3. Metode Z-Score

Cocok kalau distribusi mendekati normal: z = (x - mean) / std. Umumnya |z| > 3 dianggap outlier. Kelemahan: mean dan std sendiri terpengaruh outlier — untuk data sangat kotor, pakai IQR atau modified z-score (berbasis median).

**Code:**
```python
z = (df_detect_outlier["Distance"] - df_detect_outlier["Distance"].mean()) / df_detect_outlier["Distance"].std()
print(f"Outlier via z-score (|z| > 3): {(z.abs() > 3).sum()}")
df_detect_outlier[z.abs() > 3]
```

**Output:**
```bash
Outlier via z-score (|z| > 3): 113
```
![Method_Z-Score_Detect_Outlier](/Images/method_Z-Score_outlier.png)

---

## 📍 Prinsip Penting

1. Selalu **investigasi dulu**: outlier error atau sah?
2. Dokumentasikan setiap keputusan buang/ubah data.
3. Di konteks ML: deteksi batas outlier dari **train set saja**, terapkan ke test set.
4. Di beberapa kasus (fraud detection, anomaly detection) outlier justru sinyal, bukan noise.
