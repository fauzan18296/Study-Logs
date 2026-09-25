# 🌌 Guidebook Fisika Terpadu: Panduan Master 46 Episode Crash Course Physics

> **Panduan Praktis, Konseptual, & Referensi Rumus untuk Menyelesaikan Soal dan Project Fisika**
>
> *Dirancang khusus untuk menguraikan kebingungan konsep, memahami makna simbol di balik rumus, dan menjembatani teori ke dalam aplikasi nyata.*

## 📑 Daftar Isi

1. [Bab 1: Pendahuluan & Strategi Belajar Fisika](#-bab-1-pendahuluan--strategi-belajar-fisika)

2. [Bab 2: Modul Spesial Kinematika — Panduan Lengkap GLB & GLBB](#-bab-2-modul-spesial-kinematika--panduan-lengkap-glb--glbb)

3. [Bab 3: Kinematika & Mekanika Klasik Newton (Ep. 1 - 13)](#-bab-3-kinematika--mekanika-klasik-newton-ep-1---13)

4. [Bab 4: Mekanika Fluida, Gelombang, & Termodinamika (Ep. 14 - 24)](#-bab-4-mekanika-fluida-gelombang--termodinamika-ep-14---24)

5. [Bab 5: Kelistrikan, Magnetisme, & Elektromagnetisme (Ep. 25 - 37)](#-bab-5-kelistrikan-magnetisme--elektromagnetisme-ep-25---37)

6. [Bab 6: Optik Geometri & Gelombang Cahaya (Ep. 38 - 41)](#-bab-6-optik-geometri--gelombang-cahaya-ep-38---41)

7. [Bab 7: Fisika Modern, Kuantum, & Kosmologi (Ep. 42 - 46)](#-bab-7-fisika-modern-kuantum--kosmologi-ep-42---46)

8. [Bab 8: Kamus Besar Simbol & Konsep Rumus Fisika](#-bab-8-kamus-besar-simbol--konsep-rumus-fisika)

---

## 🧭 Bab 1: Pendahuluan & Strategi Belajar Fisika

Pernahkah kamu merasa bingung saat melihat sekumpulan rumus fisika di papan tulis? Mengapa sebuah soal terlihat sangat sulit padahal rumusnya pendek? Kebingungan ini biasanya muncul bukan karena kamu tidak pintar, melainkan karena kita sering menghafal rumus *tanpa memahami konteks fisiknya* dan *arti dari simbol-simbol di dalamnya*.

Guidebook ini hadir untuk mengubah cara pandangmu:
1. **Fisika adalah Cerita Realita:** Setiap rumus adalah ringkasan dari bagaimana alam semesta bekerja.
2. **Pahami Variabel Sebelum Menghitung:** Jangan pernah memasukkan angka ke rumus sebelum kamu tahu apa arti fisik dari simbol tersebut.
3. **Gunakan Panduan Ini saat Buntu:** Gunakan buku pegangan ini saat mengerjakan PR, ujian, atau merancang *project* sains/teknik.

---

## 🏎️ Bab 2: Modul Spesial Kinematika — Panduan Lengkap GLB & GLBB

Sebelum masuk ke kalkulus tingkat lanjut atau dinamika gaya, fondasi utama dunia gerak terletak pada dua konsep dasar: **Gerak Lurus Beraturan (GLB)** dan **Gerak Lurus Berubah Beraturan (GLBB)**. Banyak siswa terjebak karena salah mengenali kapan suatu benda mengalami kecepatan tetap atau percepatan tetap.

---

### 1. Gerak Lurus Beraturan (GLB)

#### 🌟 Konsep & Analogi Sehari-hari
Bayangkan kamu sedang menyetir mobil di jalan tol lurus yang sepi. Kamu mengunci kecepatan spidometer di angka $60 \, \text{km/jam}$ dan tidak menginjak gas ataupun rem sama sekali. Kondisi inilah yang disebut **GLB**.
* **Ciri Utama:** Kecepatan konstan ($v = \text{tetap}$), tidak ada percepatan ($a = 0$).
* **Implikasi Fisik:** Setiap detik, menit, atau jam, jarak yang kamu tempuh selalu sama besar.

#### 📐 Kumpulan Rumus GLB
Dalam GLB, hanya ada satu persamaan utama yang diturunkan dari definisi kecepatan:

```math
s = v \cdot t
```

Jika dicari variabel lainnya:
* Mencari kecepatan ($v$):

```math
v = \frac{s}{t}
```

* Mencari waktu ($t$):

```math
t = \frac{s}{v}
```

#### 📝 Studi Kasus & Bedah Soal GLB
**Soal:** Sebuah kereta melaju di atas rel lurus dengan kecepatan konstan sebesar $72 \, \text{km/jam}$. Berapa meter jarak yang ditempuh oleh kereta tersebut setelah melaju selama $10 \, \text{sekon}$?

* **Langkah 1 (Analisis & Konversi Satuan):** Satuan waktu adalah sekon ($\text{s}$), tetapi kecepatan masih dalam kilometer per jam ($\text{km/jam}$). Kita wajib mengubahnya ke meter per sekon ($\text{m/s}$).

```math
v = 72 \times \frac{1000 \, \text{meter}}{3600 \, \text{sekon}} = 72 \times \frac{5}{18} = 20 \, \text{m/s}
```

* **Langkah 2 (Penerapan Rumus):** Masukkan nilai ke dalam rumus jarak GLB ($s = v \cdot t$).

```math
s = (20 \, \text{m/s}) \cdot (10 \, \text{s}) = 200 \, \text{meter}
```
* **Kesimpulan:** Kereta tersebut berhasil menempuh jarak sejauh $200 \, \text{meter}$.

---

### 2. Gerak Lurus Berubah Beraturan (GLBB)

#### 🌟 Konsep & Analogi Sehari-hari
Sekarang, bayangkan lampu lalulintas berubah menjadi hijau. Kamu menginjak pedal gas mobilmu semakin dalam secara konstan. Mobilmu mulai melaju dari diam dan kecepatannya bertambah setiap detik. Kondisi di mana kecepatan bertambah atau berkurang secara teratur inilah yang disebut **GLBB**.
* **Ciri Utama:** Percepatan konstan ($a = \text{tetap}$). Kecepatan benda berubah secara beraturan terhadap waktu.
* **Jenis GLBB:** 
  1. *GLBB Dipercepat:* Kecepatan bertambah seiring waktu ($a$ bernilai positif, arah percepatan searah kecepatan).
  2. *GLBB Diperlambat:* Kecepatan berkurang atau direm secara teratur ($a$ bernilai negatif/retardasi, arah percepatan berlawanan arah kecepatan).

#### 📐 Tiga Rumus Sakti GLBB
Untuk menyelesaikan semua persoalan GLBB, kamu hanya membutuhkan 3 persamaan utama ini:

1. **Persamaan Kecepatan terhadap Waktu:**

```math
v_t = v_0 + a \cdot t
```

2. **Persamaan Jarak terhadap Waktu:**

```math
s = v_0 \cdot t + \frac{1}{2} a \cdot t^2
```

3. **Persamaan Bebas Waktu (Hubungan Kecepatan dan Jarak):**

```math
v_t^2 = v_0^2 + 2 \cdot a \cdot s
```

#### 📝 Studi Kasus & Bedah Soal GLBB (Dipercepat)
**Soal:** Sebuah pesawat mainan remote control mulai bergerak dari keadaan diam ($v_0 = 0$) di landasan pacu. Pesawat tersebut mengalami percepatan konstan sebesar $4 \, \text{m/s}^2$. Berapa kecepatan pesawat dan berapa jarak yang ditempuhnya setelah bergerak selama $5 \, \text{sekon}$?

* **Langkah 1 (Identifikasi Diketahui & Ditanya):**
  * Kecepatan awal ($v_0$) = $0 \, \text{m/s}$ (karena mulai dari diam)
  * Percepatan ($a$) = $4 \, \text{m/s}^2$
  * Waktu ($t$) = $5 \, \text{s}$
  * Ditanya: Kecepatan akhir ($v_t$) dan Jarak ($s$).

* **Langkah 2 (Mencari Kecepatan Akhir $v_t$):** Gunakan rumus pertama GLBB.

```math
v_t = v_0 + a \cdot t
```

```math
v_t = 0 + (4 \, \text{m/s}^2) \cdot (5 \, \text{s}) = 20 \, \text{m/s}
```

* **Langkah 3 (Mencari Jarak $s$):** Gunakan rumus kedua GLBB.

```math
s = v_0 \cdot t + \frac{1}{2} a \cdot t^2
```

```math
s = (0 \cdot 5) + \frac{1}{2} \cdot (4) \cdot (5)^2
```

```math
s = 0 + 2 \cdot (25) = 50 \, \text{meter}
```
* **Kesimpulan:** Setelah $5$ detik, kecepatan pesawat mencapai $20 \, \text{m/s}$ dengan jarak tempuh sejauh $50 \, \text{meter}$.

---

### 3. GLBB Khusus: Gerak Jatuh Bebas (GJB)

#### 🌟 Konsep & Analogi
Jika kamu menjatuhkan sebuah batu dari atas gedung tanpa lemparan awal, batu tersebut akan jatuh ke bumi akibat tarikan gravitasi. Gerak jatuh bebas adalah kasus khusus dari GLBB vertikal di mana:
* Kecepatan awal nol ($v_0 = 0$).
* Percepatan benda digantikan oleh percepatan gravitasi bumi ($a = g \approx 9.8$ atau $10 \, \text{m/s}^2$).
* Jarak horizontal ($s$) digantikan oleh ketinggian vertikal ($h$).

#### 📐 Rumus Turunan Gerak Jatuh Bebas

```math
v_t = g \cdot t
```

```math
h = \frac{1}{2} g \cdot t^2
```

```math
v_t^2 = 2 \cdot g \cdot h
```

---

## 🏃 Bab 3: Kinematika & Mekanika Klasik Newton (Ep. 1 - 13)

Bagian ini membahas bagaimana benda bergerak, mengapa benda bisa bergerak, dan bagaimana energi serta momentum bekerja di dunia makroskopis.

### 🎯 Peta Konsep & Navigasi Episode
* **Ep. 1 - 4 (Kinematika & Kalkulus):** Gerak 1D & 2D, turunan, integral, dan vektor.
* **Ep. 5 - 10 (Dinamika & Hukum Newton):** Hukum Newton, gesekan, gerak melingkar, gravitasi, usaha, energi, dan momentum.
* **Ep. 11 - 13 (Rotasi & Statika):** Torsi, momentum sudut, dan kesetimbangan benda tegar.

### 📝 Bedah Materi & Contoh Soal Praktis

#### 1. Kinematika Turunan & Integral (Ep. 2 - 3)
* **Konsep:** Kinematika tingkat lanjut menggunakan kalkulus untuk mencari kecepatan sesaat dari fungsi posisi, dan sebaliknya.
* **Rumus Utama:**

```math
v(t) = \frac{dx}{dt}
```

```math
x(t) = \int v(t) \, dt
```

#### 2. Hukum II Newton & Dinamika (Ep. 5)
* **Konsep:** Hukum II Newton menjelaskan hubungan sebab-akibat antara gaya eksternal total yang bekerja pada suatu objek, massa benda (kelembaman/inersia), dan percepatan yang timbul.
* **Rumus Utama:**

```math
\sum \vec{F} = m\vec{a}
```

* **Studi Kasus Soal:**
  Anda mendorong lemari es bermassa $50 \, \text{kg}$ ke kanan dengan gaya $200 \, \text{N}$. Terdapat gaya gesek lantai sebesar $50 \, \text{N}$ ke kiri. Berapa percepatan lemari es tersebut?
  * *Penyelesaian:* Hitung resultan gaya ($\sum F$).

```math
\sum F = F_{\text{dorong}} - f_k = 200 - 50 = 150 \, \text{N}
```

```math
a = \frac{\sum F}{m} = \frac{150}{50} = 3 \, \text{m/s}^2 \text{ (ke arah kanan)}
```

#### 3. Kekekalan Energi Mekanik (Ep. 9)
* **Konsep:** Energi tidak dapat diciptakan atau dimusnahkan, hanya berubah bentuk. Dalam sistem tertutup tanpa gaya non-konservatif (seperti gesekan udara), jumlah Energi Potensial dan Energi Kinetik selalu konstan.
* **Rumus Utama:**

```math
EP_1 + EK_1 = EP_2 + EK_2
```
Di mana $EP = mgh$ dan $EK = \frac{1}{2}mv^2$.

* **Studi Kasus Soal:**
  Buah kelapa bermassa $2 \, \text{kg}$ berada di pohon setinggi $5 \, \text{m}$ ($g = 10 \, \text{m/s}^2$). Berapa kecepatan kelapa saat menyentuh tanah?
  * *Penyelesaian:* Energi mekanik di atas sama dengan di tanah.

```math
mgh + 0 = 0 + \frac{1}{2}mv^2
```
Coret massa $m$ di kedua sisi karena sama:

```math
gh = \frac{1}{2}v^2 \implies v = \sqrt{2gh} = \sqrt{2(10)(5)} = \sqrt{100} = 10 \, \text{m/s}
```

---

## 🌊 Bab 4: Mekanika Fluida, Gelombang, & Termodinamika (Ep. 14 - 24)

Mempelajari zat alir, getaran harmonik, gelombang mekanik, bunyi, kalor, serta hukum-hukum termodinamika.

### 🎯 Peta Konsep & Navigasi Episode
* **Ep. 14 - 15 (Fluida):** Tekanan hidrostatis, prinsip Archimedes, kontinuitas, dan persamaan Bernoulli.
* **Ep. 16 - 19 (Gelombang & Bunyi):** Gerak harmonik sederhana (pegas/bandul), gelombang berjalan, efek Doppler, dan fisika musik.
* **Ep. 20 - 24 (Termodinamika):** Suhu, teori kinetik gas, perpindahan kalor, Hukum I & II Termodinamika, dan siklus mesin Carnot.

### 📝 Bedah Materi & Contoh Soal Praktis

#### 1. Gerak Harmonik Sederhana / Pegas (Ep. 16)
* **Konsep:** Ketika benda ditarik dari titik setimbangnya lalu dilepaskan, ada gaya pemulih yang berbanding lurus dengan simpangannya dan selalu mengarah ke titik setimbang.
* **Rumus Utama (Hukum Hooke):**

```math
F = -kx
```

#### 2. Prinsip Archimedes & Gaya Apung (Ep. 14)
* **Konsep:** Benda yang dicelupkan ke dalam fluida akan mendesak sejumlah zat cair. Gaya ke atas yang diterima benda sama dengan berat fluida yang dipindahkan.
* **Rumus Utama:**

```math
F_b = \rho_{\text{fluida}} V_{\text{tercelup}} g
```

#### 3. Kalor dan Perubahan Suhu (Ep. 22)
* **Konsep:** Suhu adalah ukuran rata-rata energi kinetik partikel. Kalor adalah transfer energi termal akibat perbedaan suhu.
* **Rumus Utama:**

```math
Q = mc\Delta T
```

---

## ⚡ Bab 5: Kelistrikan, Magnetisme, & Elektromagnetisme (Ep. 25 - 37)

Dunia muatan statis, medan listrik, arus listrik dalam rangkaian, gaya magnetik, hingga gelombang elektromagnetik Maxwell.

### 🎯 Peta Konsep & Navigasi Episode
* **Ep. 25 - 28 (Listrik Statis & Arus):** Hukum Coulomb, medan listrik, potensial, kapasitor, dan Hukum Ohm.
* **Ep. 29 - 31 (Rangkaian DC & Kirchhoff):** Aturan simpul/loop Kirchhoff dan rangkaian RC.
* **Ep. 32 - 37 (Magnetisme & Induksi):** Gaya Lorentz, Hukum Ampère, induksi Faraday-Lenz, transformator, dan Persamaan Maxwell.

### 📝 Bedah Materi & Contoh Soal Praktis

#### 1. Hukum Ohm (Ep. 28)
* **Konsep:** Hambatan ($R$) adalah rintangan aliran elektron. Tegangan ($V$) adalah pendorongnya, dan Arus ($I$) adalah laju alirannya.
* **Rumus Utama:**

```math
V = I \cdot R
```

#### 2. Gaya Lorentz pada Kawat Berarus (Ep. 32)
* **Konsep:** Kawat yang dialiri arus listrik di dalam medan magnet akan mengalami gaya dorong mekanik.
* **Rumus Utama:**

```math
F = I L B \sin(\theta)
```

---

## 🌈 Bab 6: Optik Geometri & Gelombang Cahaya (Ep. 38 - 41)

Bagaimana cahaya merambat, memantul, membias melalui lensa/cermin, serta menunjukkan sifat interferensi dan difraksi gelombang.

### 🎯 Peta Konsep & Navigasi Episode
* **Ep. 38 - 39 (Optik & Pembiasan):** Hukum pemantulan dan Hukum Snellius pembiasan cahaya.
* **Ep. 40 - 41 (Interferensi & Alat Optik):** Eksperimen celah ganda Young, lapisan tipis, serta rumus lensa tipis.

### 📝 Bedah Materi & Contoh Soal Praktis

#### 1. Hukum Snellius Pembiasan (Ep. 38)
* **Konsep:** Saat cahaya berpindah dari medium renggang ke padat, kecepatan cahaya berkurang dan jalurnya berbelok mendekati garis normal.
* **Rumus Utama:**

```math
n_1 \sin(\theta_1) = n_2 \sin(\theta_2)
```

#### 2. Persamaan Lensa Tipis (Ep. 41)
* **Konsep:** Hubungan matematis antara jarak fokus lensa, jarak benda, dan jarak bayangan yang terbentuk.
* **Rumus Utama:**

```math
\frac{1}{f} = \frac{1}{d_o} + \frac{1}{d_i}
```

---

## ⚛️ Bab 7: Fisika Modern, Kuantum, & Kosmologi (Ep. 42 - 46)

Memasuki batas terkecil alam semesta (kuantum) dan batas terbesar kosmos (relativitas dan astrofisika).

### 🎯 Peta Konsep & Navigasi Episode
* **Ep. 42 (Relativitas Khusus):** Dilasi waktu dan kesetaraan massa-energi $E = mc^2$.
* **Ep. 43 - 44 (Mekanika Kuantum):** Foton, efek fotolistrik, dualisme gelombang-partikel, dan prinsip ketidakpastian Heisenberg.
* **Ep. 45 - 46 (Fisika Nuklir & Kosmologi):** Fisi/fusi nuklir, ekspansi alam semesta, serta teori Big Bang.

### 📝 Bedah Materi & Contoh Soal Praktis

#### 1. Kesetaraan Massa-Energi (Ep. 42)
* **Konsep:** Massa materi pada dasarnya adalah bentuk terkonsentrasi dari energi murni. Sedikit saja massa yang dimusnahkan dapat menghasilkan energi yang sangat masif.
* **Rumus Utama:**

```math
E = mc^2
```

---

## 📖 Bab 8: Kamus Besar Simbol & Konsep Rumus Fisika

Bagian ini dirancang khusus untuk menjawab kebingungan terbesarmu saat melihat simbol-simbol asing dalam rumus fisika. Simpan bagian ini sebagai referensi cepat!

| Simbol / Notasi | Nama Simbol | Konsep & Arti Fisik | Satuan Internasional (SI) |
| :--- | :--- | :--- | :--- |
| $v$ | Kecepatan (*Velocity*) | Laju perpindahan posisi benda terhadap perubahan waktu. | meter per sekon ($\text{m/s}$) |
| $v_0$ | Kecepatan Awal | Kecepatan objek pada awal pengamatan ($t = 0$). | $\text{m/s}$ |
| $v_t$ | Kecepatan Akhir | Kecepatan objek pada waktu tertentu ($t$) setelah mengalami perubahan. | $\text{m/s}$ |
| $a$ | Percepatan (*Acceleration*) | Laju perubahan kecepatan tiap satuan waktu. | meter per sekon kuadrat ($\text{m/s}^2$) |
| $s$ atau $x$ | Jarak / Posisi | Panjang lintasan linear atau lokasi objek dalam koordinat. | meter ($\text{m}$) |
| $\Delta x$ | Perpindahan | Perubahan jarak bersih dari titik awal ke titik akhir (vektor). | meter ($\text{m}$) |
| $t$ | Waktu (*Time*) | Durasi berlangsungnya suatu kejadian atau gerak. | sekon ($\text{s}$) |
| $m$ | Massa (*Mass*) | Jumlah materi dalam suatu benda; ukuran tingkat kelembaman/inersia. | kilogram ($\text{kg}$) |
| $F$ | Gaya (*Force*) | Dorongan atau tarikan yang dapat mengubah keadaan gerak benda. | Newton ($\text{N} = \text{kg}\cdot\text{m/s}^2$) |
| $\sum F$ | Resultan Gaya | Jumlah vektor seluruh gaya yang bekerja secara bersamaan pada suatu sistem. | Newton ($\text{N}$) |
| $f_k$ / $f_s$ | Gaya Gesek (Kinetik/Statis) | Gaya sentuh sejajar bidang yang menghambat pergerakan benda. | Newton ($\text{N}$) |
| $\mu$ | Koefisien Gesek | Tingkat kekasaran permukaan bidang (tanpa satuan). | *Tanpa Satuan* |
| $N$ | Gaya Normal | Gaya tekan tegak lurus yang diberikan permukaan bidang terhadap benda. | Newton ($\text{N}$) |
| $G$ | Konstanta Gravitasi Universal | Tetapan universal yang mengatur kekuatan tarik-menarik antar massa. | $\text{N}\cdot\text{m}^2/\text{kg}^2$ |
| $g$ | Percepatan Gravitasi Bumi | Percepatan tarik bumi terhadap benda di dekat permukaannya ($\approx 9.8$ atau $10$). | $\text{m/s}^2$ |
| $W$ | Usaha (*Work*) | Energi yang ditransfer saat gaya memindahkan benda sejauh jarak tertentu. | Joule ($\text{J} = \text{N}\cdot\text{m}$) |
| $EK$ | Energi Kinetik | Energi yang dimiliki benda karena gerakannya. | Joule ($\text{J}$) |
| $EP$ | Energi Potensial | Energi tersimpan yang dimiliki benda karena posisi atau wujudnya. | Joule ($\text{J}$) |
| $P$ | Daya / Tekanan | Daya ($P = W/t$, Watt); Tekanan ($P = F/A$, Pascal). | Watt ($\text{W}$) atau Pascal ($\text{Pa}$) |
| $p$ | Momentum Linear | Ukuran kesulitan menghhentikan benda bergerak ($p = mv$). | $\text{kg}\cdot\text{m/s}$ |
| $\tau$ | Torsi / Momen Gaya | Gaya puntir yang memicu terjadinya gerak rotasi/putar pada benda. | Newton-meter ($\text{N}\cdot\text{m}$) |
| $I$ | Momen Inersia / Arus | Inersia rotasi benda ($I = \sum mr^2$) atau arus listrik (Ampere). | $\text{kg}\cdot\text{m}^2$ atau Ampere ($\text{A}$) |
| $\omega$ | Kecepatan Sudut | Seberapa cepat sudut berputar tiap satuan waktu dalam gerak melingkar. | radian per sekon ($\text{rad/s}$) |
| $\alpha$ | Percepatan Sudut | Laju perubahan kecepatan sudut terhadap waktu. | $\text{rad/s}^2$ |
| $\rho$ | Massa Jenis (*Density*) | Kerapatan massa zat per satuan volume ($\rho = m/V$). | $\text{kg/m}^3$ |
| $V$ | Volume / Tegangan | Ruang yang ditempati zat ($\text{m}^3$) atau beda potensial listrik ($\text{Volt}$). | $\text{m}^3$ atau Volt ($\text{V}$) |
| $f$ | Frekuensi | Jumlah getaran atau gelombang yang lewat dalam satu sekon. | Hertz ($\text{Hz}$) |
| $T$ | Periode | Waktu yang dibutuhkan untuk menyelesaikan satu siklus penuh getaran. | sekon ($\text{s}$) |
| $\lambda$ | Panjang Gelombang | Jarak fisik antara dua puncak gelombang yang berurutan. | meter ($\text{m}$) |
| $Q$ | Kalor / Muatan Listrik | Energi panas yang berpindah ($\text{J}$) atau total muatan listrik dalam Coulomb ($\text{C}$). | Joule ($\text{J}$) atau Coulomb ($\text{C}$) |
| $c$ | Kalor Jenis / Kelajuan Cahaya | Kalor jenis zat ($\text{J/kg}\cdot^\circ\text{C}$) atau kecepatan cahaya di vakum ($3 \times 10^8 \, \text{m/s}$). | $\text{J/kg}\cdot^\circ\text{C}$ atau $\text{m/s}$ |
| $\Delta U$ | Perubahan Energi Dalam | Total energi mikroskopik di dalam sistem termodinamika. | Joule ($\text{J}$) |
| $k$ | Konstanta Pegas / Coulomb | Kekakuan pegas ($\text{N/m}$) atau konstanta elektrostatik ($\approx 8.99 \times 10^9$). | $\text{N/m}$ atau $\text{N}\cdot\text{m}^2/\text{C}^2$ |
| $E$ | Medan Listrik / Energi | Kekuatan medan listrik ($\text{N/C}$) atau total energi relativistik ($\text{J}$). | $\text{N/C}$ atau Joule ($\text{J}$) |
| $R$ | Hambatan Listrik | Hambatan atau rintangan terhadap aliran arus listrik dalam kawat. | Ohm ($\Omega$) |
| $B$ | Medan Magnet (*Magnetic Field*) | Kekuatan medan magnet di suatu titik ruang. | Tesla ($\text{T}$) |
| $n$ | Indeks Bias | Perbandingan kecepatan cahaya di vakum dengan kecepatan di medium. | *Tanpa Satuan* |

> 💡 *Gunakan panduan ini secara aktif: saat mengerjakan soal, buka bab yang relevan, periksa makna simbol di Bab 8, dan ikuti langkah-langkah bedah rumusnya. Selamat belajar dan merancang project fisikamu!*