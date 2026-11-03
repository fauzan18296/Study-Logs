# 📚 Memahami `np.linspace()` dalam Simulasi Fisika

> Salah satu pertanyaan yang sering muncul saat belajar NumPy dan Fisika Komputasi adalah:
>
> **"Kenapa kita menggunakan `np.linspace(0, t, 100)` atau `np.linspace(0, t, 500)`?"**
>
> Apakah angka `100` atau `500` berasal dari rumus fisika?

Jawabannya:

> **Tidak.**
>
> Angka tersebut bukan bagian dari rumus fisika, melainkan jumlah titik sampel (*sample points*) yang digunakan komputer untuk merepresentasikan waktu yang sebenarnya kontinu.

---

# 🎯 Konsep Dasar

Misalkan kita memiliki kode:

```python
t = np.linspace(0, t_flight, 100)
```

Artinya:

| Bagian     | Arti                |
| ---------- | ------------------- |
| `0`        | Waktu awal          |
| `t_flight` | Waktu akhir         |
| `100`      | Jumlah titik sampel |

Komputer akan membuat 100 nilai waktu yang tersebar merata dari awal hingga akhir.

---

# 🔍 Contoh Sederhana

```python
import numpy as np

t = np.linspace(0, 10, 5)

print(t)
```

Output:

```python
[0. , 2.5, 5. , 7.5, 10.]
```

Visualisasi:

```text
0 ----- 2.5 ----- 5 ----- 7.5 ----- 10
```

Terdapat 5 titik yang tersebar merata.

---

# 🤔 Kenapa Tidak Menggunakan Satu Nilai Waktu Saja?

Misalnya:

```python
t = 2
```

Kemudian:

```python
y = v0*t - 0.5*g*t**2
```

Hasilnya:

```text
Posisi benda saat t = 2 detik
```

Kita hanya mengetahui satu posisi.

---

Sedangkan jika:

```python
t = np.linspace(0, 4, 100)
```

maka:

```python
t = [0, 0.04, 0.08, ..., 4]
```

Kemudian:

```python
y = v0*t - 0.5*g*t**2
```

NumPy akan menghitung:

```text
y(0)
y(0.04)
y(0.08)
...
y(4)
```

Sehingga diperoleh banyak titik yang dapat digambar menjadi grafik.

---

# 🚀 Hubungan dengan Gerak Parabola

Dalam gerak parabola kita memiliki persamaan:

```math
x = (v_0 \cos \alpha)t
```

dan

```math
y = (v_0 \sin \alpha)t - \frac{1}{2}gt^2
```

Jika kita memiliki banyak nilai waktu:

```python
t = np.linspace(0, t_flight, 100)
```

maka komputer akan menghitung:

```text
x(0), x(0.04), x(0.08), ...
```

dan

```text
y(0), y(0.04), y(0.08), ...
```

Lalu setiap pasangan:

```math
(x_i, y_i)
```

digunakan untuk menggambar lintasan parabola.

---

# 📈 Mengapa Kadang 100, 500, atau 1000?

## 10 Sampel

```python
t = np.linspace(0, 4, 10)
```

Visualisasi:

```text
•
   •
      •
         •
            •
```

Grafik terlihat kasar.

---

## 100 Sampel

```python
t = np.linspace(0, 4, 100)
```

Grafik sudah cukup halus.

---

## 1000 Sampel

```python
t = np.linspace(0, 4, 1000)
```

Grafik sangat halus.

---

# ⚠️ Kesalahan yang Sering Terjadi

Banyak orang mengira:

```python
np.linspace(0, t, 100)
```

dan

```python
np.linspace(0, t, 1000)
```

akan menghasilkan lintasan fisika yang berbeda.

Padahal:

> Fisika yang dihitung tetap sama.

Yang berubah hanyalah jumlah titik yang digunakan untuk menggambarkan lintasan.

---

# 📸 Analogi Resolusi Gambar

Bayangkan sebuah foto.

### Resolusi Rendah

```text
480p
```

### Resolusi Tinggi

```text
1080p
```

Objek pada foto tetap sama.

Yang berbeda hanyalah tingkat detailnya.

---

Demikian pula:

```python
np.linspace(0, t, 100)
```

dan

```python
np.linspace(0, t, 1000)
```

menggambarkan gerakan yang sama.

Perbedaannya hanya pada jumlah titik yang dihitung.

---

# 🌎 Perspektif Fisika

Dalam fisika, waktu dianggap sebagai variabel kontinu.

Artinya:

```math
0 \le t \le t_{flight}
```

memiliki tak hingga banyak nilai.

Contoh:

```math
0.1
```

```math
0.11
```

```math
0.111
```

```math
0.1111
```

dan seterusnya.

---

Masalahnya:

> Komputer tidak dapat menghitung tak hingga banyak nilai.

Karena itu kita melakukan pendekatan dengan mengambil sejumlah sampel waktu.

Contoh:

```python
np.linspace(0, t_flight, 100)
```

atau

```python
np.linspace(0, t_flight, 500)
```

---

# 🧠 Makna Sebenarnya dari `np.linspace()`

Saat menulis:

```python
t = np.linspace(0, t_flight, 100)
```

secara konseptual kita sedang mengatakan:

> Ambil 100 momen waktu yang tersebar merata dari awal gerak hingga akhir gerak, kemudian hitung posisi dan kecepatan benda pada setiap momen tersebut.

---

# 🎯 Ringkasan Singkat

✅ `100` atau `500` bukan rumus fisika

✅ Angka tersebut adalah jumlah titik sampel

✅ Semakin besar jumlah sampel, grafik semakin halus

✅ Fisika geraknya tidak berubah

✅ Waktu dalam fisika bersifat kontinu

✅ Komputer menggunakan sampel untuk mendekati nilai kontinu

✅ `np.linspace()` sangat sering digunakan untuk simulasi gerak, grafik fungsi matematika, dan visualisasi data ilmiah

---

# 💡 Cara Berpikir yang Benar

Jangan melihat:

```python
np.linspace(0, t_flight, 100)
```

sebagai:

> "Rumus fisika"

Tetapi lihat sebagai:

> "Cara komputer mengambil banyak momen waktu agar gerakan kontinu dapat direpresentasikan dan divisualisasikan."

Itulah alasan hampir semua simulasi fisika menggunakan `np.linspace()`.
