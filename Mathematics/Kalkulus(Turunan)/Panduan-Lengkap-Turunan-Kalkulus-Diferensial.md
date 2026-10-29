<div align="center">

# 📘 PANDUAN LENGKAP TURUNAN
### Kalkulus Diferensial — Dari Konsep Dasar hingga Machine Learning

**Belajar bertahap · Contoh terstruktur · Latihan mandiri**

</div>

---

> [!NOTE]
> **Tujuan catatan**
> Memahami makna turunan, menghitung turunan berbagai fungsi, menganalisis grafik dan titik optimum, lalu menghubungkannya dengan optimisasi Machine Learning.
>
> **Level:** Pemula → Menengah  
> **Nama file:** `Panduan-Lengkap-Turunan-Kalkulus-Diferensial.md`

> [!TIP]
> **Cara menggunakan panduan ini**
> Pelajari satu bagian setiap sesi. Kerjakan contoh dengan tangan terlebih dahulu, lalu tutup catatan dan coba latihan mandiri. Jangan lanjut hanya karena sudah hafal rumus—pastikan kamu memahami alasan di baliknya.


---

## 🧭 Peta Materi

> **Urutan yang disarankan:** Fondasi → Definisi turunan → Aturan hitung → Analisis grafik → Turunan parsial → Gradient Descent.
>
> Bagian **1–5** membangun fondasi, **6–13** membahas konsep dan teknik hitung, **14–18** menghubungkan turunan dengan optimisasi, sedangkan **19–23** berisi evaluasi dan referensi cepat.

## 📚 Daftar Isi

1. [Tujuan Pembelajaran](#1-tujuan-pembelajaran)
2. [Prasyarat Matematika](#2-prasyarat-matematika)
3. [Konsep Fungsi dan Grafik](#3-konsep-fungsi-dan-grafik)
4. [Gradien dan Laju Perubahan](#4-gradien-dan-laju-perubahan)
5. [Limit dan Kontinuitas](#5-limit-dan-kontinuitas)
6. [Definisi Turunan](#6-definisi-turunan)
7. [Notasi Turunan](#7-notasi-turunan)
8. [Aturan Dasar Turunan](#8-aturan-dasar-turunan)
9. [Aturan Perkalian Pembagian dan Rantai](#9-aturan-perkalian-pembagian-dan-rantai)
10. [Turunan Berbagai Jenis Fungsi](#10-turunan-berbagai-jenis-fungsi)
11. [Turunan Implisit](#11-turunan-implisit)
12. [Turunan Orde Kedua dan Lebih Tinggi](#12-turunan-orde-kedua-dan-lebih-tinggi)
13. [Diferensial dan Aproksimasi Linear](#13-diferensial-dan-aproksimasi-linear)
14. [Analisis Perilaku Grafik](#14-analisis-perilaku-grafik)
15. [Titik Kritis dan Optimisasi](#15-titik-kritis-dan-optimisasi)
16. [Turunan Parsial dan Gradien](#16-turunan-parsial-dan-gradien)
17. [Gradient Descent](#17-gradient-descent)
18. [Hubungan dengan Machine Learning](#18-hubungan-dengan-machine-learning)
19. [Kesalahan Umum](#19-kesalahan-umum)
20. [Strategi Belajar](#20-strategi-belajar)
21. [Latihan Bertahap](#21-latihan-bertahap)
22. [Ringkasan Rumus](#22-ringkasan-rumus)
23. [Glosarium](#23-glosarium)

---


## 🎯 1. Tujuan Pembelajaran

Setelah menyelesaikan panduan ini, kamu diharapkan mampu:

- Menjelaskan turunan sebagai laju perubahan sesaat dan gradien garis singgung.
- Memahami peran limit dalam definisi turunan.
- Menggunakan aturan turunan dengan tepat.
- Menurunkan fungsi polinomial, rasional, eksponensial, logaritma, dan trigonometri.
- Membedakan titik stasioner, titik kritis, maksimum, minimum, dan titik belok.
- Menggunakan turunan pertama dan kedua untuk menganalisis grafik.
- Memahami turunan parsial, gradien, dan aturan rantai dalam fungsi multivariabel.
- Menjelaskan dasar matematis Gradient Descent dan backpropagation.

> [!IMPORTANT]
> **Prinsip belajar:** jangan hanya menghafal rumus. Untuk setiap aturan, pahami kapan aturan itu berlaku, mengapa dibutuhkan, dan bagaimana memeriksa hasilnya.


---

## 🧰 2. Prasyarat Matematika

Sebelum mempelajari turunan, pastikan kamu cukup nyaman dengan:

### 2.1 Operasi aljabar

- Penjumlahan, pengurangan, perkalian, dan pembagian.
- Pecahan aljabar dan penyederhanaan.
- Pangkat positif, negatif, dan pecahan.
- Akar kuadrat dan bentuk akar.
- Faktorisasi dan pengembangan kurung.

Contoh identitas:

```math
(x+a)^2=x^2+2ax+a^2
```

```math
x^{-n}=\frac{1}{x^n},\qquad x^{1/2}=\sqrt{x}
```

### 2.2 Persamaan

Kamu perlu mampu menyelesaikan persamaan sederhana, misalnya:

```math
2x-6=0 \quad\Longrightarrow\quad x=3
```

Kemampuan ini dibutuhkan ketika mencari titik kritis dengan menyelesaikan `f'(x) = 0`.

### 2.3 Fungsi

Fungsi memetakan input ke output. Jika `f(x) = x² + 1`, maka:

```math
f(2)=2^2+1=5
```

Pahami domain (input yang diizinkan), range (output yang dihasilkan), dan cara membaca notasi fungsi.

### 2.4 Pangkat dan akar

Bentuk pangkat pecahan dapat ditulis sebagai akar:

```math
x^{1/3}=\sqrt[3]{x}
```

Bentuk akar juga dapat ditulis sebagai pangkat untuk mempermudah diferensiasi.

---


---

## 📈 3. Konsep Fungsi dan Grafik

### 3.1 Jenis fungsi yang sering dijumpai

| Jenis | Contoh | Catatan |
|---|---|---|
| Konstan | `f(x) = 4` | Output tidak berubah |
| Linear | `f(x) = 2x + 1` | Gradien tetap |
| Kuadrat | `f(x) = x² - 3x` | Grafik parabola |
| Polinomial | `f(x) = x³ - 2x + 1` | Gabungan suku berpangkat bulat nonnegatif |
| Rasional | `f(x) = 1/x` | Penyebut tidak boleh nol |
| Eksponensial | `f(x) = eˣ` | Variabel berada di eksponen |
| Logaritma | `f(x) = ln(x)` | Untuk log natural, `x > 0` |
| Trigonometri | `f(x) = sin(x)` | Fungsi periodik |

### 3.2 Membaca grafik

Grafik membantu menjawab:

- Apakah fungsi sedang naik atau turun?
- Seberapa curam grafik di suatu titik?
- Di mana fungsi mencapai nilai rendah atau tinggi?
- Apakah ada sudut tajam atau diskontinuitas?

Turunan menghubungkan perubahan fungsi dengan kemiringan lokal grafik.

---


---

## 📏 4. Gradien dan Laju Perubahan

### 4.1 Gradien garis

Untuk dua titik `(x₁, y₁)` dan `(x₂, y₂)`, gradien garis adalah:

```math
m=\frac{y_2-y_1}{x_2-x_1},\qquad x_2\ne x_1
```

Gradien positif berarti garis naik dari kiri ke kanan; gradien negatif berarti garis turun; gradien nol berarti garis horizontal.

### 4.2 Laju perubahan rata-rata

Untuk fungsi `f`, perubahan rata-rata dari `x` ke `x+h` adalah:

```math
\frac{f(x+h)-f(x)}{h},\qquad h\ne 0
```

Nilai ini adalah gradien garis secan yang melewati dua titik pada grafik.

### 4.3 Laju perubahan sesaat

Turunan mengukur perubahan lokal saat jarak antartitik mendekati nol. Secara geometris, turunan adalah gradien garis singgung jika turunan tersebut ada.

Contoh interpretasi: jika `s(t)` menyatakan posisi terhadap waktu, maka `s'(t)` adalah kecepatan sesaat.

---


---

## ♾️ 5. Limit dan Kontinuitas

### 5.1 Pengertian limit

```math
\lim_{x\to a}f(x)=L
```

Artinya, nilai `f(x)` mendekati `L` ketika `x` mendekati `a`. Nilai fungsi tepat di `a` tidak harus sama dengan limitnya.

### 5.2 Limit kiri dan kanan

Limit dua sisi ada jika limit kiri dan limit kanan ada serta sama:

```math
\lim_{x\to a^-}f(x)=\lim_{x\to a^+}f(x)=L
```

Jika keduanya berbeda, limit dua sisi tidak ada.

### 5.3 Aturan limit dasar

Jika limit-limit yang terlibat ada, maka:

```math
\lim_{x\to a}[f(x)+g(x)]
=\lim_{x\to a}f(x)+\lim_{x\to a}g(x)
```

```math
\lim_{x\to a}[f(x)g(x)]
=\left(\lim_{x\to a}f(x)\right)\left(\lim_{x\to a}g(x)\right)
```

```math
\lim_{x\to a}\frac{f(x)}{g(x)}
=\frac{\lim_{x\to a}f(x)}{\lim_{x\to a}g(x)}
```

Aturan pembagian berlaku jika limit penyebut bukan nol.

### 5.4 Bentuk tak tentu

Bentuk `0/0` bukan jawaban limit. Bentuk ini menandakan bahwa diperlukan analisis lebih lanjut, misalnya faktorisasi atau metode limit lainnya.

Contoh:

```math
\lim_{x\to 2}\frac{x^2-4}{x-2}
```

Faktorkan pembilang untuk `x ≠ 2`:

```math
\frac{x^2-4}{x-2}
=\frac{(x-2)(x+2)}{x-2}=x+2
```

Jadi:

```math
\lim_{x\to 2}\frac{x^2-4}{x-2}=4
```

### 5.5 Kontinuitas

Fungsi `f` kontinu di `x = a` jika:

1. `f(a)` terdefinisi.
2. Limit `f(x)` saat `x` mendekati `a` ada.
3. Limit tersebut sama dengan `f(a)`.

```math
\lim_{x\to a}f(x)=f(a)
```

Diferensiabilitas mengimplikasikan kontinuitas di titik tersebut, tetapi kontinuitas tidak selalu mengimplikasikan diferensiabilitas. Fungsi `f(x) = |x|` kontinu di nol, tetapi tidak memiliki turunan di nol karena ada sudut tajam.

---


---

## 🧠 6. Definisi Turunan

### 6.1 Definisi melalui limit

```math
f'(x)=\lim_{h\to 0}\frac{f(x+h)-f(x)}{h}
```

Turunan di titik `x = a`:

```math
f'(a)=\lim_{h\to 0}\frac{f(a+h)-f(a)}{h}
```

Limit harus ada dan bernilai hingga agar turunan biasa tersebut ada.

### 6.2 Contoh dari definisi

Misalkan:

```math
f(x)=x^2
```

Pertama, hitung:

```math
f(x+h)=(x+h)^2=x^2+2xh+h^2
```

Masukkan ke definisi:

```math
f'(x)=\lim_{h\to 0}\frac{x^2+2xh+h^2-x^2}{h}
```

Sederhanakan untuk `h ≠ 0`:

```math
f'(x)=\lim_{h\to 0}(2x+h)=2x
```

Maka:

```math
f'(x)=2x
```

### 6.3 Makna geometris

- Garis secan melewati dua titik pada kurva.
- Ketika salah satu titik mendekati titik lainnya, gradien secan mendekati gradien garis singgung.
- Nilai limit gradien itu adalah turunan, jika limitnya ada.

### 6.4 Persamaan garis singgung

Jika kurva `y = f(x)` memiliki turunan di `x = a`, garis singgungnya adalah:

```math
y-f(a)=f'(a)(x-a)
```

---


---

## 🔤 7. Notasi Turunan

| Notasi | Makna |
|---|---|
| `f'(x)` | Turunan fungsi `f` terhadap `x` |
| `y'` | Turunan `y` terhadap variabel bebas yang dipahami dari konteks |
| `dy/dx` | Notasi Leibniz untuk turunan |
| `d/dx [f(x)]` | Operator diferensiasi terhadap `x` |
| `f''(x)` | Turunan kedua |
| `∂f/∂x` | Turunan parsial terhadap `x` |
| `∇f` | Gradien fungsi multivariabel |

Notasi `dy/dx` sangat berguna untuk aturan rantai dan kalkulus multivariabel. Dalam konteks turunan biasa, notasi ini dapat dipahami sebagai turunan `y` terhadap `x`.

---


---

## 🧮 8. Aturan Dasar Turunan

### 8.1 Aturan konstanta

```math
\frac{d}{dx}(c)=0
```

Contoh:

```math
\frac{d}{dx}(7)=0
```

Alasannya: output fungsi konstan tidak berubah saat `x` berubah.

### 8.2 Aturan identitas

```math
\frac{d}{dx}(x)=1
```

### 8.3 Aturan pangkat (Power Rule)

```math
\frac{d}{dx}(x^n)=nx^{n-1}
```

Contoh:

```math
\frac{d}{dx}(x^5)=5x^4
```

```math
\frac{d}{dx}(3x^2)=6x
```

Aturan pangkat berlaku pada domain tempat fungsi dan turunannya terdefinisi. Untuk pangkat real atau negatif, perhatikan batas domainnya.

### 8.4 Kelipatan konstanta

```math
\frac{d}{dx}[c f(x)]=c f'(x)
```

Contoh:

```math
\frac{d}{dx}(5x^3)=15x^2
```

### 8.5 Penjumlahan dan pengurangan

```math
\frac{d}{dx}[f(x)\pm g(x)]=f'(x)\pm g'(x)
```

Contoh:

```math
f(x)=3x^3-2x^2+4x-8
```

```math
f'(x)=9x^2-4x+4
```

Turunkan setiap suku secara terpisah.

### 8.6 Pangkat pecahan dan negatif

Ubah akar menjadi pangkat jika membantu:

```math
\sqrt{x}=x^{1/2}
```

```math
\frac{1}{x^2}=x^{-2}
```

Maka:

```math
\frac{d}{dx}\sqrt{x}=\frac{1}{2\sqrt{x}},\qquad x>0
```

```math
\frac{d}{dx}\left(\frac{1}{x^2}\right)=-\frac{2}{x^3},\qquad x\ne 0
```

### 8.7 Turunan fungsi polinomial

Contoh:

```math
f(x)=4x^4-3x^2+2x-9
```

```math
f'(x)=16x^3-6x+2
```

Konstanta `-9` turunannya nol.

---


---

## 🔗 9. Aturan Perkalian, Pembagian, dan Rantai

### 9.1 Product Rule

Jika `y = u(x)v(x)`, maka:

```math
\frac{d}{dx}[uv]=u'v+uv'
```

Contoh:

```math
f(x)=x^2(x+1)
```

```math
f'(x)=2x(x+1)+x^2(1)=3x^2+2x
```

> [!WARNING]
> **Kesalahan umum:** menganggap turunan perkalian sama dengan perkalian kedua turunan. Secara umum, `(uv)'` bukan `u'v'`.

### 9.2 Quotient Rule

Jika `y = u(x)/v(x)` dan `v(x) ≠ 0`, maka:

```math
\frac{d}{dx}\left(\frac{u}{v}\right)
=\frac{u'v-uv'}{v^2}
```

Contoh:

```math
f(x)=\frac{x^2+1}{x}
```

```math
f'(x)=\frac{(2x)(x)-(x^2+1)(1)}{x^2}
=1-\frac{1}{x^2}
```

Untuk fungsi ini, `x ≠ 0`.

### 9.3 Chain Rule

Jika:

```math
y=f(g(x))
```

maka:

```math
\frac{dy}{dx}=f'(g(x))g'(x)
```

Cara berpikir:
1. Identifikasi fungsi luar.
2. Turunkan fungsi luar, dengan bagian dalam tetap.
3. Kalikan dengan turunan fungsi dalam.

Contoh:

```math
y=(3x+1)^4
```

```math
\frac{dy}{dx}=4(3x+1)^3(3)=12(3x+1)^3
```

Contoh dengan eksponensial:

```math
y=e^{x^2}
```

```math
\frac{dy}{dx}=2xe^{x^2}
```

Chain rule sangat penting untuk menurunkan fungsi komposisi, fungsi aktivasi, dan loss yang tersusun dari banyak operasi.

---


---

## 🧩 10. Turunan Berbagai Jenis Fungsi

### 10.1 Eksponensial

```math
\frac{d}{dx}(e^x)=e^x
```

```math
\frac{d}{dx}(a^x)=a^x\ln(a),\qquad a>0
```

Jika eksponennya berupa fungsi `g(x)`, gunakan chain rule:

```math
\frac{d}{dx}e^{g(x)}=e^{g(x)}g'(x)
```

### 10.2 Logaritma

```math
\frac{d}{dx}\ln(x)=\frac{1}{x},\qquad x>0
```

Untuk logaritma nilai mutlak:

```math
\frac{d}{dx}\ln|x|=\frac{1}{x},\qquad x\ne 0
```

Untuk basis `a`:

```math
\frac{d}{dx}\log_a(x)=\frac{1}{x\ln(a)}
```

dengan `a > 0`, `a ≠ 1`, dan `x > 0`.

Jika:

```math
y=\ln(g(x))
```

maka:

```math
\frac{dy}{dx}=\frac{g'(x)}{g(x)}
```

dengan `g(x) > 0` pada domain log natural.

### 10.3 Trigonometri

Sudut pada rumus kalkulus trigonometri dinyatakan dalam radian.

```math
\frac{d}{dx}\sin(x)=\cos(x)
```

```math
\frac{d}{dx}\cos(x)=-\sin(x)
```

```math
\frac{d}{dx}\tan(x)=\sec^2(x)
```

Turunan lanjutan:

```math
\frac{d}{dx}\cot(x)=-\csc^2(x)
```

```math
\frac{d}{dx}\sec(x)=\sec(x)\tan(x)
```

```math
\frac{d}{dx}\csc(x)=-\csc(x)\cot(x)
```

### 10.4 Trigonometri dengan chain rule

```math
\frac{d}{dx}\sin(g(x))=\cos(g(x))g'(x)
```

Contoh:

```math
\frac{d}{dx}\sin(2x)=2\cos(2x)
```

### 10.5 Fungsi nilai mutlak

```math
f(x)=|x|
```

Fungsi ini dapat ditulis:

```math
|x|=\begin{cases}
-x,&x<0\\
x,&x\ge 0
\end{cases}
```

Turunannya adalah `-1` untuk `x < 0` dan `1` untuk `x > 0`, tetapi tidak ada turunan biasa di `x = 0` karena gradien kiri dan kanan berbeda.

### 10.6 Fungsi invers

Jika `f` memiliki invers yang terdiferensiasi dan `f'(f^{-1}(x)) ≠ 0`, maka:

```math
\frac{d}{dx}f^{-1}(x)=\frac{1}{f'(f^{-1}(x))}
```

Contoh penting: turunan fungsi invers trigonometri dan logaritma dapat diturunkan dari prinsip ini.

---


---

## ✍️ 11. Turunan Implisit

Turunan implisit digunakan ketika `y` tidak ditulis secara langsung sebagai fungsi `x`.

Contoh persamaan lingkaran:

```math
x^2+y^2=25
```

Turunkan kedua sisi terhadap `x`. Karena `y` bergantung pada `x`, chain rule diperlukan:

```math
2x+2y\frac{dy}{dx}=0
```

Susun ulang:

```math
\frac{dy}{dx}=-\frac{x}{y},\qquad y\ne 0
```

Turunan implisit berguna untuk kurva, hubungan antarvariabel, dan masalah yang sulit diselesaikan terlebih dahulu menjadi `y = f(x)`.

---


---

## 📉 12. Turunan Orde Kedua dan Lebih Tinggi

### 12.1 Turunan kedua

Turunan kedua adalah turunan dari turunan pertama:

```math
f''(x)=\frac{d}{dx}f'(x)
```

Contoh:

```math
f(x)=x^3-3x^2
```

```math
f'(x)=3x^2-6x
```

```math
f''(x)=6x-6
```

### 12.2 Interpretasi

- Turunan pertama menggambarkan laju perubahan.
- Turunan kedua menggambarkan bagaimana laju perubahan itu berubah.
- Dalam gerak, jika posisi adalah `s(t)`, turunan pertama adalah kecepatan dan turunan kedua adalah percepatan.

### 12.3 Kecekungan

- `f''(x) > 0`: grafik cekung ke atas pada interval tersebut.
- `f''(x) < 0`: grafik cekung ke bawah pada interval tersebut.

### 12.4 Turunan orde lebih tinggi

```math
f^{(n)}(x)=\frac{d^n f}{dx^n}
```

Turunan orde lebih tinggi dipakai dalam analisis fungsi, deret Taylor, fisika, dan optimisasi lanjutan.

---


---

## 📐 13. Diferensial dan Aproksimasi Linear

### 13.1 Diferensial

Jika `y = f(x)`, diferensialnya didefinisikan sebagai:

```math
dy=f'(x)\,dx
```

Untuk perubahan `dx` yang kecil, `dy` dapat menjadi pendekatan bagi perubahan aktual fungsi.

### 13.2 Aproksimasi linear

Dekat titik `x = a`, fungsi dapat didekati oleh garis singgungnya:

```math
f(x)\approx f(a)+f'(a)(x-a)
```

Contoh pendekatan nilai akar atau fungsi non-linear dapat dilakukan dengan memilih titik `a` yang dekat dengan input yang ingin diperkirakan.

### 13.3 Galat pendekatan

Aproksimasi linear umumnya semakin baik ketika `x` semakin dekat dengan `a`, selama fungsi cukup mulus di sekitar titik itu. Aproksimasi ini bukan identitas yang selalu tepat.

---


---

## 🔍 14. Analisis Perilaku Grafik

### 14.1 Interval naik dan turun

Pada interval yang terdiferensiasi:

- `f'(x) > 0`: fungsi naik.
- `f'(x) < 0`: fungsi turun.

Turunan nol pada satu titik tidak cukup untuk menyimpulkan bahwa fungsi naik atau turun pada seluruh interval.

### 14.2 Titik stasioner

Titik stasioner adalah titik pada domain tempat:

```math
f'(x)=0
```

Titik stasioner dapat berupa maksimum lokal, minimum lokal, atau titik stasioner yang bukan ekstremum.

### 14.3 Titik kritis

Bilangan kritis `c` adalah bilangan dalam domain fungsi ketika `f'(c) = 0` atau turunan tidak ada di `c`. Definisi ini harus dibatasi pada titik yang memang berada di domain fungsi.

### 14.4 Uji turunan pertama

Periksa perubahan tanda `f'(x)` di sekitar titik kritis:

- Positif ke negatif: maksimum lokal.
- Negatif ke positif: minimum lokal.
- Tidak berubah tanda: tidak ada ekstremum lokal berdasarkan uji tanda ini.

### 14.5 Uji turunan kedua

Jika `f'(c) = 0`:

```math
f''(c)>0\quad\Longrightarrow\quad \text{minimum lokal}
```

```math
f''(c)<0\quad\Longrightarrow\quad \text{maksimum lokal}
```

Jika `f''(c) = 0`, uji ini tidak memberikan kesimpulan. Gunakan uji lain.

### 14.6 Titik belok

Titik belok adalah titik tempat kecekungan berubah. Perubahan tanda turunan kedua dapat membantu mengidentifikasinya jika turunan kedua tersedia di sekitar titik. Syarat `f''(c) = 0` saja tidak cukup.

Contoh:

```math
f(x)=x^3,\qquad f'(x)=3x^2,\qquad f''(x)=6x
```

Di `x = 0`, turunan pertama nol, tetapi fungsi tetap naik di kedua sisi. Titik itu bukan maksimum atau minimum; kecekungan berubah, sehingga merupakan titik belok stasioner.

---


---

## 🏔️ 15. Titik Kritis dan Optimisasi

### 15.1 Prosedur mencari optimum

1. Tentukan fungsi tujuan.
2. Tentukan domain yang diizinkan.
3. Hitung turunan pertama.
4. Cari titik ketika turunan nol atau tidak ada, selama titik itu ada dalam domain.
5. Periksa tanda turunan pertama atau gunakan turunan kedua.
6. Untuk interval tertutup, evaluasi juga kedua ujung interval.
7. Bandingkan nilai fungsi untuk menentukan optimum global.

### 15.2 Contoh minimum

Misalkan:

```math
f(x)=x^2-4x+5
```

Turunan pertama:

```math
f'(x)=2x-4
```

Cari titik stasioner:

```math
2x-4=0\quad\Longrightarrow\quad x=2
```

Turunan kedua:

```math
f''(x)=2>0
```

Maka `x = 2` merupakan minimum lokal. Karena fungsi kuadrat ini terbuka ke atas pada seluruh bilangan real, titik tersebut juga minimum global.

Nilai minimumnya:

```math
f(2)=2^2-4(2)+5=1
```

### 15.3 Minimum dan maksimum lokal vs global

- **Lokal:** paling rendah atau tinggi dibanding titik-titik di sekitarnya.
- **Global:** paling rendah atau tinggi pada seluruh domain yang dipertimbangkan.

Sebuah fungsi dapat memiliki beberapa minimum lokal, tetapi minimum globalnya hanya satu nilai minimum (meski bisa dicapai di beberapa titik).

### 15.4 Optimisasi pada interval

Jika domainnya `a ≤ x ≤ b`, jangan hanya memeriksa `f'(x) = 0`. Evaluasi titik kritis di bagian dalam interval dan kedua ujungnya.

---


---

## 🧭 16. Turunan Parsial dan Gradien

Bagian ini menjadi jembatan dari kalkulus satu variabel ke Machine Learning.

### 16.1 Fungsi multivariabel

Misalkan:

```math
f(x,y)=x^2+3xy+y^2
```

Output fungsi bergantung pada dua input. Turunan parsial mengukur perubahan terhadap satu variabel dengan variabel lain dianggap konstan.

### 16.2 Turunan parsial terhadap `x`

```math
\frac{\partial f}{\partial x}=2x+3y
```

### 16.3 Turunan parsial terhadap `y`

```math
\frac{\partial f}{\partial y}=3x+2y
```

### 16.4 Gradien

Gradien adalah vektor yang menggabungkan turunan parsial:

```math
\nabla f(x,y)=
\begin{bmatrix}
\frac{\partial f}{\partial x}\\
\frac{\partial f}{\partial y}
\end{bmatrix}
```

Untuk contoh sebelumnya:

```math
\nabla f(x,y)=
\begin{bmatrix}
2x+3y\\
3x+2y
\end{bmatrix}
```

Gradien menunjukkan arah kenaikan tercepat fungsi pada titik yang gradiennya tidak nol. Arah negatif gradien adalah arah penurunan lokal tercepat untuk langkah infinitesimal dengan ukuran Euclidean.

### 16.5 Turunan arah

Untuk vektor satuan `u`, turunan arah adalah:

```math
D_{\mathbf{u}}f=\nabla f\cdot\mathbf{u}
```

Ini mengukur laju perubahan fungsi saat bergerak ke arah tertentu.

### 16.6 Jacobian

Untuk fungsi yang menghasilkan banyak output, Jacobian menyusun turunan parsial seluruh output terhadap seluruh input menjadi sebuah matriks. Jacobian muncul dalam komposisi fungsi dan backpropagation.

### 16.7 Hessian

Hessian adalah matriks turunan parsial orde kedua:

```math
H_f=\begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \cdots & \frac{\partial^2 f}{\partial x_1\partial x_n}\\
\vdots & \ddots & \vdots\\
\frac{\partial^2 f}{\partial x_n\partial x_1} & \cdots & \frac{\partial^2 f}{\partial x_n^2}
\end{bmatrix}
```

Hessian membantu mempelajari kecekungan fungsi multivariabel dan metode optimisasi orde kedua.

---


---

## ⚙️ 17. Gradient Descent

### 17.1 Tujuan

Gradient Descent adalah algoritma optimisasi yang memperbarui parameter agar nilai fungsi tujuan, biasanya loss, berkurang.

### 17.2 Aturan pembaruan satu parameter

```math
w_{\text{baru}}=w_{\text{lama}}-\eta\frac{dL}{dw}
```

Keterangan:

- `w`: parameter model.
- `L`: fungsi loss.
- `dL/dw`: turunan loss terhadap parameter.
- `η`: learning rate atau ukuran langkah.

### 17.3 Banyak parameter

```math
\boldsymbol{\theta}_{\text{baru}}
=\boldsymbol{\theta}_{\text{lama}}-\eta\nabla_{\boldsymbol{\theta}}L
```

### 17.4 Contoh sederhana

Misalkan:

```math
L(w)=(w-3)^2
```

Turunannya:

```math
\frac{dL}{dw}=2(w-3)
```

Dengan `w = 0` dan `η = 0.1`:

```math
\frac{dL}{dw}=2(0-3)=-6
```

```math
w_{\text{baru}}=0-0.1(-6)=0.6
```

Loss awal adalah `9`; loss baru:

```math
L(0.6)=(0.6-3)^2=5.76
```

Pada langkah ini loss berkurang.

### 17.5 Peran learning rate

- Terlalu kecil: pembelajaran dapat berlangsung lambat.
- Terlalu besar: langkah bisa melewati daerah minimum atau membuat loss berosilasi dan meningkat.
- Nilai yang tepat bergantung pada fungsi, skala parameter, dan metode optimisasi.

Gradient Descent tidak menjamin menemukan minimum global untuk setiap fungsi nonkonveks.

### 17.6 Hubungan dengan backpropagation

Backpropagation menghitung gradien loss terhadap parameter jaringan menggunakan aturan rantai secara sistematis. Gradient Descent atau algoritma optimisasi lain kemudian menggunakan gradien itu untuk memperbarui parameter.

> [!IMPORTANT]
> **Perbedaan penting:** backpropagation adalah metode menghitung gradien; Gradient Descent adalah metode menggunakan gradien untuk memperbarui parameter.

---


---

## 🤖 18. Hubungan dengan Machine Learning

### 18.1 Regresi linear

Model sederhana:

```math
\hat{y}=wx+b
```

Loss kuadrat untuk satu contoh:

```math
L(w,b)=(wx+b-y)^2
```

Turunan terhadap `w`:

```math
\frac{\partial L}{\partial w}=2(wx+b-y)x
```

Turunan terhadap `b`:

```math
\frac{\partial L}{\partial b}=2(wx+b-y)
```

Gradien ini memberi informasi bagaimana perubahan `w` dan `b` memengaruhi loss.

### 18.2 Mean Squared Error (MSE)

Untuk `n` contoh:

```math
\{MSE}=\frac{1}{n}\sum_{i=1}^{n}(\hat{y}_i-y_i)^2
```

MSE menghukum kesalahan prediksi besar dengan lebih kuat karena residual dikuadratkan.

### 18.3 Sigmoid

```math
\sigma(z)=\frac{1}{1+e^{-z}}
```

Turunannya:

```math
\sigma'(z)=\sigma(z)(1-\sigma(z))
```

Sigmoid mengubah nilai real menjadi angka antara 0 dan 1. Dalam praktik modern, pemilihan fungsi aktivasi bergantung pada arsitektur dan tugas.

### 18.4 Log loss biner

Untuk label `y ∈ {0,1}` dan probabilitas prediksi `p`:

```math
L=-[y\ln(p)+(1-y)\ln(1-p)]
```

Dalam implementasi, nilai probabilitas ditangani secara numerik dengan hati-hati agar tidak menghitung logaritma nol. Banyak library menyediakan implementasi loss yang stabil secara numerik.

### 18.5 Chain rule dalam jaringan saraf

Jika loss bergantung pada output model, dan output bergantung pada aktivasi serta parameter, chain rule menghubungkan turunan antarbagian:

```math
\frac{\partial L}{\partial w}
=\frac{\partial L}{\partial a}
\frac{\partial a}{\partial z}
\frac{\partial z}{\partial w}
```

Rantai turunan ini adalah salah satu ide utama di balik backpropagation.

### 18.6 Dari matematika ke kode

Urutan latihan implementasi yang disarankan:

1. Hitung turunan fungsi sederhana secara manual.
2. Hitung gradien dengan NumPy.
3. Bandingkan dengan finite differences.
4. Buat Gradient Descent untuk fungsi kuadrat.
5. Implementasikan regresi linear sederhana.
6. Gunakan PyTorch autograd untuk memeriksa gradien.
7. Pelajari bagaimana gradien dihitung pada jaringan saraf.

### 18.7 Finite differences untuk memeriksa turunan

Pendekatan beda hingga terpusat:

```math
f'(x)\approx\frac{f(x+h)-f(x-h)}{2h}
```

Ini berguna untuk memeriksa gradien numerik terhadap turunan analitik. Pilihan `h` terlalu besar menambah galat aproksimasi; terlalu kecil dapat memperbesar galat pembulatan.

---


---

## ⚠️ 19. Kesalahan Umum

### Kesalahan 1 — Menganggap turunan nol pasti optimum

Salah. `f'(c) = 0` hanya menunjukkan titik stasioner jika turunannya ada. Contoh `f(x) = x³` memiliki turunan nol di nol, tetapi bukan maksimum atau minimum lokal.

### Kesalahan 2 — Menganggap fungsi kontinu pasti terdiferensiasi

Salah. `f(x) = |x|` kontinu di nol, tetapi tidak terdiferensiasi di sana.

### Kesalahan 3 — Menghilangkan chain rule

Untuk `(3x + 1)^2`, hasilnya bukan hanya `2(3x + 1)`. Harus dikalikan dengan turunan bagian dalam, yaitu `3`.

### Kesalahan 4 — Salah menerapkan product rule

Turunan perkalian dua fungsi adalah `u'v + uv'`, bukan `u'v'`.

### Kesalahan 5 — Mengabaikan domain

Fungsi `ln(x)` dalam bilangan real hanya terdefinisi untuk `x > 0`; `1/x` tidak terdefinisi di nol. Domain tetap harus diperiksa saat menghitung turunan dan titik kritis.

### Kesalahan 6 — Hanya memeriksa turunan nol saat mencari optimum

Titik tempat turunan tidak ada dan ujung interval juga dapat menjadi kandidat optimum jika berada dalam domain.

### Kesalahan 7 — Menganggap Gradient Descent selalu turun

Langkah yang terlalu besar dapat meningkatkan loss. Penurunan bergantung pada ukuran langkah dan karakteristik fungsi.

### Kesalahan 8 — Menyamakan backpropagation dengan Gradient Descent

Backpropagation menghitung gradien; algoritma optimisasi menggunakan gradien untuk memperbarui parameter.

---


---

## 🗓️ 20. Strategi Belajar

Gunakan pola belajar berikut untuk setiap topik:

1. **Pahami konsep:** jelaskan dengan kata-kata sendiri apa yang diukur atau dilakukan rumus.
2. **Kerjakan contoh:** ikuti setiap langkah dan alasan aljabarnya.
3. **Latihan tanpa catatan:** kerjakan soal serupa tanpa melihat solusi.
4. **Periksa kesalahan:** cari langkah pertama yang salah, bukan sekadar mengganti jawaban.
5. **Visualisasikan:** cocokkan tanda turunan dengan bentuk grafik.
6. **Hubungkan ke kode:** setelah konsep mantap, validasi dengan Python/NumPy.

### Rencana delapan minggu

| Minggu | Materi | Target |
|---|---|---|
| 1 | Aljabar, fungsi, grafik, gradien | Membaca fungsi dan menghitung gradien |
| 2 | Limit, kontinuitas, definisi turunan | Memahami asal rumus turunan |
| 3 | Aturan dasar dan power rule | Menurunkan polinomial |
| 4 | Product, quotient, chain rule | Menurunkan fungsi komposisi |
| 5 | Eksponensial, logaritma, trigonometri, turunan kedua | Menangani fungsi lebih beragam |
| 6 | Grafik, titik kritis, optimisasi | Menganalisis maksimum dan minimum |
| 7 | Turunan parsial, gradien, Jacobian, Hessian dasar | Memahami banyak parameter |
| 8 | Gradient Descent, loss, NumPy, PyTorch | Membuat optimisasi sederhana |

Rencana ini fleksibel. Jika konsep limit atau chain rule belum kuat, luangkan waktu tambahan sebelum melanjutkan.

---


---

## ✏️ 21. Latihan Bertahap

**Petunjuk:** kerjakan dahulu tanpa melihat ringkasan rumus. Untuk setiap jawaban, tuliskan langkahnya dan jelaskan alasan memilih aturan yang digunakan.

### Level 1 — Fondasi

1. Hitung gradien garis yang melalui `(1, 3)` dan `(4, 9)`.
2. Jika `f(x) = 2x + 5`, hitung `f(3)`.
3. Hitung limit berikut:

```math
\lim_{x\to 3}\frac{x^2-9}{x-3}
```

### Level 2 — Aturan turunan

4. Turunkan:

```math
f(x)=5x^4-3x^2+7x-8
```

5. Turunkan:

```math
g(x)=(2x-1)^3
```

6. Turunkan:

```math
h(x)=x^2e^x
```

7. Turunkan:

```math
p(x)=\ln(x^2+1)
```

### Level 3 — Analisis grafik

8. Cari titik kritis dan klasifikasikan untuk:

```math
f(x)=x^2-6x+10
```

9. Jelaskan mengapa `f(x) = x³` memiliki titik stasioner di nol tetapi tidak memiliki maksimum atau minimum lokal di sana.

10. Untuk `f(x) = x²` pada interval `[-1, 3]`, tentukan minimum dan maksimum global dengan mengevaluasi titik kritis dan ujung interval.

### Level 4 — Turunan multivariabel dan ML

11. Hitung gradien:

```math
f(x,y)=x^2+xy+2y^2
```

12. Untuk `L(w) = (w - 4)²`, hitung satu langkah Gradient Descent dari `w = 0` dengan learning rate `0.1`. Hitung juga loss sebelum dan sesudah langkah.

13. Jelaskan perbedaan fungsi turunan, gradien, backpropagation, dan Gradient Descent.

### Kunci jawaban singkat

1. `m = 2`.
2. `f(3) = 11`.
3. `6`.
4. `20x³ - 6x + 7`.
5. `6(2x - 1)²`.
6. `eˣ(x² + 2x)`.
7. `2x/(x² + 1)`.
8. Minimum global di `x = 3`, dengan `f(3) = 1`.
9. Karena turunan tidak berubah tanda di sekitar nol; fungsi tetap naik.
10. Minimum global `0` di `x = 0`; maksimum global `9` di `x = 3`.
11. `∇f = [2x + y, x + 4y]ᵀ`.
12. Gradien awal `-8`, parameter baru `0.8`, loss awal `16`, loss baru `10.24`.
13. Turunan mengukur perubahan lokal; gradien mengumpulkan turunan parsial; backpropagation menghitung gradien dalam jaringan komputasi; Gradient Descent menggunakan gradien untuk memperbarui parameter.

> [!TIP]
> Gunakan kunci singkat untuk memeriksa hasil akhir, bukan menggantikan proses pengerjaan.

---


---

## 📌 22. Ringkasan Rumus

### Definisi dan aturan dasar

```math
f'(x)=\lim_{h\to 0}\frac{f(x+h)-f(x)}{h}
```

```math
\frac{d}{dx}(c)=0,\qquad \frac{d}{dx}(x)=1
```

```math
\frac{d}{dx}(x^n)=nx^{n-1}
```

```math
(cf)'=cf',\qquad (f\pm g)'=f'\pm g'
```

### Aturan lanjutan

```math
(uv)'=u'v+uv'
```

```math
\left(\frac{u}{v}\right)'=\frac{u'v-uv'}{v^2}
```

```math
\frac{d}{dx}f(g(x))=f'(g(x))g'(x)
```

### Fungsi khusus

```math
\frac{d}{dx}e^x=e^x,\qquad
\frac{d}{dx}\ln(x)=\frac{1}{x}
```

```math
\frac{d}{dx}\sin(x)=\cos(x),\qquad
\frac{d}{dx}\cos(x)=-\sin(x)
```

```math
\frac{d}{dx}\tan(x)=\sec^2(x)
```

### Optimisasi

```math
f'(c)=0
```

Persamaan ini mencari kandidat titik stasioner, bukan memastikan optimum dengan sendirinya.

```math
f''(c)>0\Rightarrow \text{minimum lokal}
```

```math
f''(c)<0\Rightarrow \text{maksimum lokal}
```

Kesimpulan uji turunan kedua ini berlaku ketika `f'(c) = 0` dan fungsi cukup terdiferensiasi di sekitar `c`.

### Kalkulus multivariabel dan Machine Learning

```math
\nabla f=
\begin{bmatrix}
\frac{\partial f}{\partial x_1}\\
\vdots\\
\frac{\partial f}{\partial x_n}
\end{bmatrix}
```

```math
\boldsymbol{\theta}_{\text{baru}}
=\boldsymbol{\theta}_{\text{lama}}-\eta\nabla_{\boldsymbol{\theta}}L
```

---


---

## 📚 23. Glosarium

| Istilah | Penjelasan singkat |
|---|---|
| Fungsi | Aturan yang memetakan input ke output |
| Limit | Nilai yang didekati fungsi saat input mendekati titik tertentu |
| Turunan | Laju perubahan sesaat atau gradien lokal |
| Garis secan | Garis yang melewati dua titik pada kurva |
| Garis singgung | Garis yang memiliki gradien lokal kurva di suatu titik |
| Diferensiabel | Memiliki turunan di titik atau interval yang dibahas |
| Titik stasioner | Titik dengan turunan nol |
| Titik kritis | Titik domain tempat turunan nol atau tidak ada |
| Maksimum/minimum lokal | Nilai ekstrem dibandingkan lingkungan sekitarnya |
| Maksimum/minimum global | Nilai ekstrem pada seluruh domain yang ditinjau |
| Kecekungan | Arah lengkungan grafik |
| Turunan parsial | Turunan terhadap satu variabel dengan variabel lain dianggap konstan |
| Gradien | Vektor turunan parsial |
| Jacobian | Matriks turunan pertama fungsi multivariabel |
| Hessian | Matriks turunan kedua fungsi multivariabel |
| Loss function | Ukuran kesalahan atau tujuan yang diminimalkan |
| Learning rate | Ukuran langkah pembaruan parameter |
| Backpropagation | Prosedur menghitung gradien melalui aturan rantai |
| Gradient Descent | Algoritma optimisasi yang memperbarui parameter berdasarkan gradien |

---

---

## 🏁 Penutup

> **Target akhir:** mampu menjelaskan konsep, menghitung turunan, menguji hasil, dan menghubungkannya dengan optimisasi.

Urutan paling penting untuk dikuasai adalah:

**Fungsi dan aljabar → gradien → limit → definisi turunan → aturan turunan → chain rule → analisis grafik → turunan parsial → Gradient Descent.**

Jangan mengukur kemajuan hanya dari banyaknya rumus yang dihafal. Ukur dari kemampuan menjelaskan mengapa rumus digunakan, mengenali batas berlakunya, dan memeriksa apakah hasilnya masuk akal secara matematis maupun grafis.


---

<div align="center">

**Selesai membaca bukan berarti selesai belajar.**  
Pilih satu topik, kerjakan beberapa soal, lalu jelaskan kembali konsepnya dengan bahasamu sendiri.

</div>

> [!NOTE]
> **Catatan format rumus:** isi dokumen mempertahankan blok ` ```math ` sesuai format yang diminta. Namun, GitHub umumnya menampilkan fenced code block sebagai kode, bukan merendernya sebagai persamaan. Jika ingin persamaan tampil ter-render langsung di GitHub, gunakan delimiters matematika `$...$` atau `$$...$$` sesuai kebutuhan.

