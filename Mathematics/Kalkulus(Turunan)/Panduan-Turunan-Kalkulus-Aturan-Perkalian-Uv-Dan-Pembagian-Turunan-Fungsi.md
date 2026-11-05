# Catatan Matematika: Aturan Turunan (Perkalian & Pembagian)

Catatan ini membahas penggunaan **Aturan Perkalian (Product Rule)** dan **Aturan Pembagian (Quotient Rule)** dalam kalkulus, lengkap dengan syarat penggunaan, contoh soal, dan trik cepatnya.

---

## 📌 1. Aturan Perkalian (Product Rule)

### Kapan Rumus Ini Digunakan?
Rumus ini **wajib** digunakan jika terdapat **dua kelompok/suku yang sama-sama mengandung variabel $x$** dan keduanya saling dikalikan.

### Rumus Utama
Jika $y = u(x) \cdot v(x)$, maka turunannya adalah:

```math
\frac{d}{dx}[uv] = u'v + uv'
```

> 💡 **Cara Mudah Menghafal:** Polanya dilakukan secara **bergantian**. Suku pertama diturunkan dikali suku kedua tetap, **DITAMBAH** suku pertama tetap dikali suku kedua diturunkan.

---

### 🟢 Kondisi 1: Wajib Menggunakan Rumus (Tidak Bisa Disederhanakan)
Gunakan rumus jika kedua fungsi variabel tidak bisa dikalikan masuk secara aljabar (misalnya aljabar dengan trigonometri).

**Contoh Soal:**
Tentukan turunan dari $f(x) = x^2 \cdot \sin(x)$

**Langkah Penyelesaian:**
1. **Misalkan $u$ dan $v$ beserta turunannya:**
   * $u = x^2 \implies u' = 2x$
   * $v = \sin(x) \implies v' = \cos(x)$
2. **Masukkan ke rumus $u'v + uv'$:**

```math
f'(x) = (2x)\sin(x) + (x^2)\cos(x)
```

```math
f'(x) = 2x \sin(x) + x^2 \cos(x)
```

---

### ⚡ Kondisi 2: Bisa Menggunakan Trik Cepat (Perkalian Masuk)
Jika kedua suku berbentuk aljabar biasa, Anda **tidak perlu** memakai rumus $u'v + uv'$. Lebih cepat jika dikalikan masuk terlebih dahulu, baru diturunkan menggunakan aturan pangkat biasa.

**Contoh Soal:**
Tentukan turunan dari $f(x) = x^2(x + 1)$

* **Cara Cepat (Kalian Masuk Dulu):**
  ```math
  f(x) = x^3 + x^2
  ```
  Turunkan langsung:
  ```math
  f'(x) = 3x^2 + 2x
  ```
* **Cara Rumus ($u'v + uv'$):**
  * $u = x^2 \implies u' = 2x$
  * $v = x + 1 \implies v' = 1$
  ```math
  f'(x) = (2x)(x + 1) + (x^2)(1)
  ```
  ```math
  f'(x) = 2x^2 + 2x + x^2 = 3x^2 + 2x
  ```
  *(Hasilnya sama persis, tapi Cara Cepat jauh lebih hemat waktu).*

---

### 🔴 Kondisi 3: Tidak Perlu Rumus Perkalian (Hanya Pengali Angka/Konstanta)
Jika salah satu pengalinya hanya berupa angka biasa (konstanta) tanpa variabel $x$, angka tersebut cukup "diam di tempat".

**Contoh Soal:**
Tentukan turunan dari $f(x) = 5(x^2 + 3)$

**Langkah Penyelesaian:**
```math
f'(x) = 5 \cdot \frac{d}{dx}(x^2 + 3) 
```
```math
f'(x) = 5 \cdot (2x) = 10x
```

---

## 📌 2. Aturan Pembagian (Quotient Rule)

Untuk operasi pembagian antar fungsi variabel, rumus yang digunakan berbeda dengan perkalian. Tanda hubungnya berubah menjadi **kurang (−)** dan wajib dibagi dengan **$v^2$**.

### Rumus Utama
Jika $y = \frac{u(x)}{v(x)}$, maka turunannya adalah:

```math
\frac{d}{dx} \left[ \frac{u}{v} \right] = \frac{u'v - uv'}{v^2}
```

---

## 📊 Ringkasan Strategi Pengerjaan Soal

| Bentuk Soal | Jenis Operasi | Rumus Turunan | Solusi Alternatif Lebih Cepat |
| :--- | :--- | :--- | :--- |
| $y = u \cdot v$ | **Perkalian** | $u'v + uv'$ | Kalikan masuk dulu secara aljabar jika memungkinkan. |
| $y = \frac{u}{v}$ | **Pembagian** | $\frac{u'v - uv'}{v^2}$ | Sederhanakan pangkatnya dulu jika penyebutnya hanya 1 suku tunggal (misal: dibagi $x^2$). |

---
**Rekomendasi Nama File:** `catatan-turunan-product-quotient-rule.md`
