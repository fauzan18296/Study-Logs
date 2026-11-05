# 📘 Catatan Kalkulus: Penurunan Fungsi Loss & Optimasi Bobot

Dokumen ini berisi rangkuman latihan kalkulus mengenai penurunan **Fungsi Loss (Mean Squared Error - MSE)** terhadap bobot ($w$), evaluasi penyelesaian menggunakan aturan praktis (*Power Rule*), serta penjabaran lengkap menggunakan **Definisi Limit Turunan**.

---

## 📌 1. Soal Latihan

Diberikan sebuah fungsi Loss sederhana terhadap bobot $w$:

```math
L(w) = 3w^2 - 12w + 15
```

**Pertanyaan:**
1. Cari turunan pertama dari $L(w)$ terhadap $w$, yaitu $\frac{dL}{dw}$, menggunakan definisi limit turunan (aturan aljabar dasar turunan).
2. Tentukan nilai $w$ di mana fungsi Loss mencapai titik minimum absolutnya (stasioner) dengan memanfaatkan konsep turunan pertama sama dengan zero.

---

## 💡 2. Penyelesaian Metode Praktis (Power Rule)

Metode ini adalah metode umum yang efisien dan sering digunakan dalam pemodelan *Machine Learning* / *Data Science*.

### A. Mencari Turunan Pertama $L'(w)$
Menggunakan aturan pangkat (*Power Rule*):
- $\frac{d}{dw}(3w^2) = 3 \cdot (2w^{2-1}) = 6w$
- $\frac{d}{dw}(-12w) = -12 \cdot (1w^{1-1}) = -12$
- $\frac{d}{dw}(15) = 0$

```math
L'(w) = 6w - 12
```

### B. Mencari Titik Stasioner (Minimum Absolut)
Syarat titik stasioner adalah turunan pertama bernilai nol ($L'(w) = 0$):

```math
6w - 12 = 0
```
```math
6w = 12
```
```math
w = \frac{12}{6} = 2
```

> **Hasil:** Nilai bobot optimal yang meminimalkan fungsi Loss adalah **$w = 2$**.

---

## 🔬 3. Penjabaran Lengkap: Definisi Limit Turunan

Secara formal, turunan pertama didefinisikan sebagai limit dari rasio perubahan fungsi ketika perubahan parameter ($h$) mendekati nol:

```math
L'(w) = \lim_{h \to 0} \frac{L(w+h) - L(w)}{h}
```

Berikut adalah langkah-langkah aljabar mendetail untuk membuktikannya:

### Langkah 1: Substitusi Parameter Fungsi
Ganti setiap variabel $w$ pada fungsi $L(w)$ menjadi $(w+h)$:

- **Fungsi awal:** 
  ```math
  L(w) = 3w^2 - 12w + 15
  ```
- **Fungsi dengan substitusi $(w+h)$:**
  ```math
  L(w+h) = 3(w+h)^2 - 12(w+h) + 15
  ```

Masukkan kedua bentuk ke dalam rumus limit:

```math
L'(w) = \lim_{h \to 0} \frac{[3(w+h)^2 - 12(w+h) + 15] - [3w^2 - 12w + 15]}{h}
```

---

### Langkah 2: Jabarkan Operasi Aljabar
Jabarkan kuadrat $(w+h)^2 = w^2 + 2wh + h^2$ dan distribusikan pengalinya:

1. $3(w+h)^2 = 3(w^2 + 2wh + h^2) = 3w^2 + 6wh + 3h^2$
2. $-12(w+h) = -12w - 12h$
3. $-(3w^2 - 12w + 15) = -3w^2 + 12w - 15$

Tuliskan kembali bentuk limit yang telah dijabarkan:

```math
L'(w) = \lim_{h \to 0} \frac{3w^2 + 6wh + 3h^2 - 12w - 12h + 15 - 3w^2 + 12w - 15}{h}
```

---

### Langkah 3: Penyederhanaan Suku (Saling Menghilangkan)
Kelompokkan dan eliminasi suku-suku berlawanan tanda yang ada pada pembilang:
- $(3w^2 - 3w^2) = 0$
- $(-12w + 12w) = 0$
- $(15 - 15) = 0$

Pembilang kini hanya menyisakan suku-suku yang memiliki variabel $h$:

```math
L'(w) = \lim_{h \to 0} \frac{6wh + 3h^2 - 12h}{h}
```

---

### Langkah 4: Faktorisasi & Eliminasi $h$
Keluarkan faktor $h$ dari pembilang agar bisa dicoret dengan $h$ pada penyebut:

```math
L'(w) = \lim_{h \to 0} \frac{h(6w + 3h - 12)}{h}
```

Coret variabel $h$ pada pembilang dan penyebut:

```math
L'(w) = \lim_{h \to 0} (6w + 3h - 12)
```

---

### Langkah 5: Substitusi Nilai $h \to 0$
Setelah pembuat nol di penyebut hilang, lakukan substitusi $h = 0$:

```math
L'(w) = 6w + 3(0) - 12
```

```math
L'(w) = 6w - 12
```

---

## 🎯 4. Evaluasi & Ringkasan Perbandingan

| Kriteria | Power Rule (Aturan Praktis) | Definisi Limit ($\lim_{h \to 0}$) |
| :--- | :--- | :--- |
| **Kecepatan** | Sangat Cepat & Efisien | Butuh Penjabaran Aljabar Panjang |
| **Kebutuhan Praktis** | Digunakan dalam *Koding*, *Optimization*, & *Gradient Descent* | Digunakan untuk Pembuktian Konseptual/Teoretis |
| **Hasil Akhir** | **$6w - 12$** | **$6w - 12$** |

### 🔍 Catatan Penting Penulisan:
1. **Pemisah Operasi:** Hindari penulisan perkalian menggunakan titik tunggal yang menyerupai desimal (contoh: $2.3$ ditulis menjadi $2 \cdot 3$ atau $(2)(3)$).
2. **Redundansi Suku:** Suku $+0$ pada turunan konstanta disederhanakan agar notasi bersih.
3. **Kesesuaian Notasi:** Pastikan penulisan variabel (seperti $w$ dan $u$) terlihat jelas dan berbeda agar tidak menimbulkan salah tafsir saat dibaca.