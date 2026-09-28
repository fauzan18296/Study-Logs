# 📊 Memahami Distribusi Data

> Distribusi data bukan hanya tentang **berapa banyak data yang ada**, tetapi tentang **bagaimana data tersebut tersebar**.

---

# 🎯 Tujuan Mempelajari Distribusi

Saat melihat sebuah dataset, pertanyaan yang perlu diajukan bukan:

❌ "Ada berapa banyak datanya?"

Tetapi:

✅ "Di mana mayoritas data berada?"

✅ "Seberapa jauh data menyebar?"

✅ "Apakah ada nilai yang tidak biasa (outlier)?"

✅ "Apakah data simetris atau miring?"

---

# 🧠 Apa Itu Distribusi Data?

Distribusi menggambarkan:

* Lokasi mayoritas data
* Bentuk penyebaran data
* Kepadatan data
* Outlier
* Pola tertentu dalam data

Misalnya:

Dataset A

```text
70, 71, 72, 73, 74, 75, 76
```

Dataset B

```text
10, 20, 30, 75, 120, 150, 200
```

Kedua dataset memiliki:

```python
count = 7
```

Tetapi distribusinya sangat berbeda.

### Dataset A

* Data berkumpul di sekitar 70–76
* Penyebaran sempit

### Dataset B

* Data tersebar dari 10–200
* Penyebaran sangat lebar

---

# 1️⃣ Melihat Jumlah Data (Count)

```python
df["nilai"].count()
```

Contoh:

```text
1000
```

Artinya:

* Ada 1000 data yang tidak kosong (non-null)

⚠️ Penting:

`count()` **tidak menunjukkan distribusi**.

Ia hanya menunjukkan jumlah data yang tersedia.

---

# 2️⃣ Melihat Nilai Minimum dan Maksimum

```python
df["nilai"].min()
df["nilai"].max()
```

Contoh:

```text
min = 40
max = 100
```

---

## Range (Rentang Data)

```math
Range = Max - Min
```

Contoh:

```math
Range = 100 - 40
```

```math
Range = 60
```

Interpretasi:

* Range kecil → data lebih terkumpul
* Range besar → data lebih menyebar

---

# 3️⃣ Membandingkan Mean dan Median

## Mean (Rata-rata)

```python
df["nilai"].mean()
```

## Median (Nilai Tengah)

```python
df["nilai"].median()
```

---

## Contoh Data Simetris

```text
70, 72, 74, 76, 78
```

Hasil:

```text
Mean   = 74
Median = 74
```

Interpretasi:

* Distribusi relatif simetris

---

## Contoh Data Tidak Simetris

```text
10, 20, 30, 40, 500
```

Hasil:

```text
Mean   = 120
Median = 30
```

Interpretasi:

* Ada nilai ekstrem (outlier)
* Distribusi tidak seimbang

---

# 4️⃣ Membaca Quartile

Gunakan:

```python
df["nilai"].describe()
```

Contoh:

```text
count    1000
mean       75
std        10
min        40
25%        68
50%        75
75%        82
max       100
```

---

## Arti Quartile

### Q1 (25%)

```text
25% = 68
```

Artinya:

25% data berada di bawah atau sama dengan 68.

---

### Q2 (50%) = Median

```text
50% = 75
```

Artinya:

50% data berada di bawah atau sama dengan 75.

---

### Q3 (75%)

```text
75% = 82
```

Artinya:

75% data berada di bawah atau sama dengan 82.

---

# 5️⃣ Membaca Standar Deviasi (Std)

```python
df["nilai"].std()
```

Standar deviasi menunjukkan:

> Seberapa jauh data menyebar dari rata-ratanya.

---

## Contoh Penyebaran Sempit

```text
Mean = 75
Std  = 2
```

Interpretasi:

* Sebagian besar data dekat dengan rata-rata

---

## Contoh Penyebaran Lebar

```text
Mean = 75
Std  = 40
```

Interpretasi:

* Data sangat tersebar
* Variasi data tinggi

---

# 6️⃣ Histogram (Cara Terbaik Membaca Distribusi)

```python
df["nilai"].hist()
```

Histogram memperlihatkan bentuk distribusi secara visual.

---

## Distribusi Normal

```text
      *
    * * *
  * * * * *
 * * * * * *
  * * * * *
    * * *
      *
```

Karakteristik:

* Mayoritas data di tengah
* Simetris
* Bentuk seperti lonceng (Bell Curve)

---

## Right Skew (Miring ke Kanan)

```text
****
*****
******
****
***
**
*
```

Karakteristik:

* Mayoritas data kecil
* Sedikit data sangat besar

Contoh:

* Pendapatan
* Harga rumah
* Gaji

---

## Left Skew (Miring ke Kiri)

```text
*
**
***
****
******
*****
****
```

Karakteristik:

* Mayoritas data besar
* Sedikit data sangat kecil

---

# 7️⃣ Mencari Outlier

Gunakan:

```python
df.boxplot(column="nilai")
```

Contoh:

```text
10, 12, 13, 14, 15, 16, 300
```

Angka:

```text
300
```

Kemungkinan merupakan outlier.

---

# 📦 Ringkasan Alur Membaca Distribusi

Saat pertama kali mendapatkan dataset:

## Langkah 1

```python
df["kolom"].describe()
```

Lihat:

* Count
* Mean
* Std
* Min
* Max
* Quartile

---

## Langkah 2

```python
df["kolom"].hist()
```

Tanyakan:

* Data terkumpul di mana?
* Apakah simetris?
* Apakah miring kanan?
* Apakah miring kiri?
* Apakah ada beberapa puncak?
* Apakah ada outlier?

---

## Langkah 3

Bandingkan:

```python
mean
```

dengan

```python
median
```

Jika berbeda jauh:

* Distribusi kemungkinan tidak simetris
* Ada kemungkinan outlier

---

# 🎓 Mental Model yang Perlu Diingat

Distribusi data menjawab tiga pertanyaan utama:

```text
1. Di mana mayoritas data berada?
2. Seberapa jauh data menyebar?
3. Apakah ada pola atau nilai yang tidak biasa?
```

Jika hanya melihat:

```python
count()
```

kita hanya tahu:

```text
"Berapa banyak data?"
```

Jika melihat:

* Histogram
* Mean
* Median
* Quartile
* Standard Deviation
* Boxplot

kita mulai memahami:

```text
"Bagaimana data tersebut tersebar?"
```

Dan itulah inti dari membaca distribusi data dalam Data Analysis maupun Machine Learning.
