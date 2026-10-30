# 📝 Catatan Matematika: Turunan Fungsi Akar

Catatan ini membahas langkah demi langkah mengubah fungsi akar menjadi pangkat pecahan dan cara menyelesaikan turunannya menggunakan **Aturan Pangkat (Power Rule)** serta **Aturan Rantai (Chain Rule)** untuk fungsi kompleks.

---

## 📌 Konsep Dasar

Sebelum menurunkan, kita harus mengubah bentuk akar menjadi bentuk pangkat pecahan terlebih dahulu menggunakan sifat eksponen berikut:

```math
\(\sqrt\)[m]{x^n} \(= x^{\frac{n}{m}} \%\%\)MAGIT_PARSER_PROTECT%%```

> **Ingat:** Jika hanya tertulis $\sqrt{x}$, itu artinya sama dengan $\sqrt[2]{x^1} = x^{\frac{1}{2}}$.

---

## ⚡ Rumus Utama Turunan

Jika kita memiliki fungsi berbentuk pangkat $f(x) = x^n$, maka rumus turunannya ($f'(x)$) adalah:

```math
f'(x) = n \(\cdot\) x^{n-1}
```

### 💡 Trik Cepat Mengurangi Pecahan dengan 1
Saat menghitung pangkat baru ($n - 1$), Anda bisa menggunakan shortcut ini:
```math
\(\text{Pangkat Baru} = \frac{\text{Pembilang} - \text{Penyebut}}{\text{Penyebut}} \%\%\)MAGIT_PARSER_PROTECT%%```

---

## 🧪 Contoh Soal Dasar

### 🔹 Contoh 1: Turunan dari $f(x) = \sqrt{x}$

**Langkah 1: Ubah bentuk akar ke pangkat pecahan**
```math
f(x) \(= x^{\frac{1}{2}} \%\%\)MAGIT_PARSER_PROTECT%%```

**Langkah 2: Aplikasikan aturan turunan**
Kalikan pangkat ke depan, lalu pangkat awal dikurangi 1.
```math
f'(x) \(= \frac{1}{2} \cdot x^{\frac{1}{2} - 1} \%\%\)MAGIT_PARSER_PROTECT%%```

**Langkah 3: Hitung pangkat baru**
Karena $\frac{1}{2} - 1 = -\frac{1}{2}$, maka:
```math
f'(x) \(= \frac{1}{2}x^{-\frac{1}{2}} \%\%\)MAGIT_PARSER_PROTECT%%```

**Langkah 4: Sederhanakan ke bentuk akar kembali**
Ubah pangkat negatif menjadi positif dengan memindahkannya ke bawah (penyebut).
```math
f'(x) \(= \frac{1}{2x^{\frac{1}{2}}} = \frac{1}{2\sqrt{x}} \%\%\)MAGIT_PARSER_PROTECT%%```

---

## 🔗 Aturan Rantai (Chain Rule) untuk Akar Kompleks

Jika di dalam akar bukan hanya $x$, melainkan sebuah fungsi lain (misalnya $f(x) = \sqrt{u}$ di mana $u$ adalah fungsi dari $x$), kita harus menggunakan **Aturan Rantai**:

```math
f'(x) \(= \text{Turunan Luar (Akar)} \times \text{Turunan Dalam (Fungsi }\) u)
```

Secara matematis, jika $f(x) = [u(x)]^n$, maka turunannya:
```math
f'(x) = n \(\cdot [u(x)]^{n-1} \cdot\) u'(x)
```

---

## 🧪 Contoh Soal Aturan Rantai

### 🔹 Contoh 2: Turunan dari $f(x) = \sqrt{3x^2 + 5}$

**Langkah 1: Ubah fungsi menjadi bentuk pangkat pecahan**
Misalkan bagian dalam akar adalah $u = 3x^2 + 5$.
```math
f(x) \(= (3x^2 + 5)^{\frac{1}{2}} \%\%\)MAGIT_PARSER_PROTECT%%```

**Langkah 2: Cari turunan dari fungsi bagian dalam ($u'$)**
```math
u \(= 3x^2 + 5 \implies\) u' = 6x
```

**Langkah 3: Jalankan Aturan Rantai**
Turunkan pangkat luar ($\frac{1}{2}$ ke depan dan kurangi 1), lalu kalikan dengan turunan bagian dalam ($6x$).
```math
f'(x) \(= \frac{1}{2}(3x^2 + 5)^{-\frac{1}{2}} \cdot (6x) \%\%\)MAGIT_PARSER_PROTECT%%```

**Langkah 4: Gabungkan dan Sederhanakan**
Kalikan $\frac{1}{2}$ dengan $6x$ terlebih dahulu:
```math
f'(x) \(= 3x \cdot (3x^2 + 5)^{-\frac{1}{2}} \%\%\)MAGIT_PARSER_PROTECT%%```

Pindahkan pangkat negatif ke bawah dan ubah kembali menjadi akar:
```math
f'(x) \(= \frac{3x}{(3x^2 + 5)^{\frac{1}{2}}} = \frac{3x}{\sqrt{3x^2 + 5}} \%\%\)MAGIT_PARSER_PROTECT%%```

---

## 🛠️ Ringkasan Pola Cepat

Untuk menghemat waktu, berikut pola hasil turunan akar yang sering muncul:

| Fungsi Awal $f(x)$ | Bentuk Pecahan | Hasil Turunan $f'(x)$ |
| :--- | :--- | :--- |
| $\sqrt{x}$ | $x^{\frac{1}{2}}$ | $\frac{1}{2\sqrt{x}}$ |
| $\sqrt[3]{x}$ | $x^{\frac{1}{3}}$ | $\frac{1}{3\sqrt[3]{x^2}}$ |
| $\sqrt{u}$ | $u^{\frac{1}{2}}$ | $\frac{u'}{2\sqrt{u}}$ |

---
*Catatan ini dibuat untuk mempermudah visualisasi turunan pecahan pada platform berbasis Markdown seperti GitHub.*
