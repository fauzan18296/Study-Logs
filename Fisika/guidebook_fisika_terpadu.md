# 🌌 Guidebook Fisika Terpadu: Panduan Master 46 Episode Crash Course Physics

> **Panduan Praktis, Konseptual, & Referensi Rumus untuk Menyelesaikan Soal dan Project Fisika**
>
> *Dirancang khusus untuk menguraikan kebingungan konsep, memahami makna simbol di balik rumus, dan menjembatani teori ke dalam aplikasi nyata.*

## 📑 Daftar Isi

1. [Bab 1: Pendahuluan & Strategi Belajar Fisika](#-bab-1-pendahuluan--strategi-belajar-fisika)

2. [Bab 2: Kinematika & Mekanika Klasik Newton (Ep. 1 - 13)](#-bab-2-kinematika--mekanika-klasik-newton-ep-1---13)

3. [Bab 3: Mekanika Fluida, Gelombang, & Termodinamika (Ep. 14 - 24)](#-bab-3-mekanika-fluida-gelombang--termodinamika-ep-14---24)

4. [Bab 4: Kelistrikan, Magnetisme, & Elektromagnetisme (Ep. 25 - 37)](#-bab-4-kelistrikan-magnetisme--elektromagnetisme-ep-25---37)

5. [Bab 5: Optik Geometri & Gelombang Cahaya (Ep. 38 - 41)](#-bab-5-optik-geometri--gelombang-cahaya-ep-38---41)

6. [Bab 6: Fisika Modern, Kuantum, & Kosmologi (Ep. 42 - 46)](#-bab-6-fisika-modern-kuantum--kosmologi-ep-42---46)

7. [Bab 7: Kamus Besar Simbol & Konsep Rumus Fisika](#-bab-7-kamus-besar-simbol--konsep-rumus-fisika)

## 🧭 Bab 1: Pendahuluan & Strategi Belajar Fisika

Pernahkah kamu merasa bingung saat melihat sekumpulan rumus fisika di papan tulis? Mengapa sebuah soal terlihat sangat sulit padahal rumusnya pendek? Kebingungan ini biasanya muncul bukan karena kamu tidak pintar, melainkan karena kita sering menghafal rumus *tanpa memahami konteks fisiknya* dan *arti dari simbol-simbol di dalamnya*.

Guidebook ini hadir untuk mengubah cara pandangmu:

1. **Fisika adalah Cerita Realita:** Setiap rumus adalah ringkasan dari bagaimana alam semesta bekerja.

2. **Pahami Variabel Sebelum Menghitung:** Jangan pernah memasukkan angka ke rumus sebelum kamu tahu apa arti fisik dari simbol tersebut.

3. **Gunakan Panduan Ini saat Buntu:** Gunakan buku pegangan ini saat mengerjakan PR, ujian, atau merancang *project* sains/teknik.

## 🏃 Bab 2: Kinematika & Mekanika Klasik Newton (Ep. 1 - 13)

Bagian ini membahas bagaimana benda bergerak, mengapa benda bisa bergerak, dan bagaimana energi serta momentum bekerja di dunia makroskopis.

### 🎯 Peta Konsep & Navigasi Episode

* **Ep. 1 - 4 (Kinematika & Kalkulus):** Gerak 1D & 2D, turunan, integral, dan vektor.

* **Ep. 5 - 10 (Dinamika & Hukum Newton):** Hukum Newton, gesekan, gerak melingkar, gravitasi, usaha, energi, dan momentum.

* **Ep. 11 - 13 (Rotasi & Statika):** Torsi, momentum sudut, dan kesetimbangan benda tegar.

### 📝 Bedah Materi & Contoh Soal Praktis

#### 1. Kinematika 1D & GLBB (Ep. 1 - 3)

* **Konsep:** Kinematika mendeskripsikan *bagaimana* benda bergerak tanpa mempedulikan penyebabnya. Turunan posisi terhadap waktu menghasilkan kecepatan, dan turunan kecepatan menghasilkan percepatan. Sebaliknya, integral percepatan menghasilkan kecepatan, dan integral kecepatan menghasilkan posisi.

* **Rumus Utama (Percepatan Konstan):**

```math
v = v_0 + at
```

```math
\Delta x = v_0 t + \frac{1}{2}a t^2
```

```math
v^2 = v_0^2 + 2a \Delta x
```

* **Studi Kasus Soal:**
  Sebuah mobil balap diam di garis start ($v_0 = 0 \, \text{m/s}$). Saat lampu hijau menyala, mobil digas dengan percepatan konstan $a = 4 \, \text{m/s}^2$. Di manakah posisi mobil setelah $t = 5 \, \text{s}$?

  * *Penyelesaian:* Gunakan rumus posisi GLBB.

```math
x = x_0 + v_0 t + \frac{1}{2}at^2 = 0 + (0)(5) + \frac{1}{2}(4)(5)^2 = 0 + 0 + 50 = 50 \text{ meter}
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
\sum F = F_{\text{dorong}} - f_k = 200 - 50 = 150 \text{ N}
```

```math
a = \frac{\sum F}{m} = \frac{150}{50} = 3 \text{ m/s}^2 \text{ (ke arah kanan)}
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
gh = \frac{1}{2}v^2 \implies v = \sqrt{2gh} = \sqrt{2(10)(5)} = \sqrt{100} = 10 \text{ m/s}
```

## 🌊 Bab 3: Mekanika Fluida, Gelombang, & Termodinamika (Ep. 14 - 24)

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

* **Studi Kasus Soal:**
  Sebuah pegas memiliki konstanta $k = 200 \, \text{N/m}$. Jika ditarik sejauh $x = 0.1 \, \text{m}$ dari posisi normal, berapa besar gaya pemulih pegas tersebut?

  * *Penyelesaian:*

```math
F = -(200)(0.1) = -20 \text{ N}
```

  *(Tanda negatif menunjukkan arah gaya berlawanan dengan arah tarikan).*

#### 2. Prinsip Archimedes & Gaya Apung (Ep. 14)

* **Konsep:** Benda yang dicelupkan ke dalam fluida akan mendesak sejumlah zat cair. Gaya ke atas yang diterima benda sama dengan berat fluida yang dipindahkan.

* **Rumus Utama:**

```math
F_b = \rho_{\text{fluida}} V_{\text{tercelup}} g
```

* **Studi Kasus Soal:**
  Sebuah balok kayu bervolume $0.5 \, \text{m}^3$ tercelup seluruhnya di dalam air ($\rho = 1000 \, \text{kg/m}^3$, $g = 10 \, \text{m/s}^2$). Berapa gaya angkat yang dialami balok?

  * *Penyelesaian:*

```math
F_b = (1000)(0.5)(10) = 5000 \text{ N}
```

#### 3. Kalor dan Perubahan Suhu (Ep. 22)

* **Konsep:** Suhu adalah ukuran rata-rata energi kinetik partikel. Kalor adalah transfer energi termal akibat perbedaan suhu.

* **Rumus Utama:**

```math
Q = mc\Delta T
```

* **Studi Kasus Soal:**
  Berapa energi kalor yang dibutuhkan untuk memanaskan $2 \, \text{kg}$ air ($c = 4200 \, \text{J/kg}\cdot^\circ\text{C}$) dari suhu $20^\circ\text{C}$ menjadi mendidih di $100^\circ\text{C}$?

  * *Penyelesaian:* $\Delta T = 100 - 20 = 80^\circ\text{C}$.

```math
Q = (2)(4200)(80) = 672.000 \text{ Joule} = 672 \text{ kJ}
```

## ⚡ Bab 4: Kelistrikan, Magnetisme, & Elektromagnetisme (Ep. 25 - 37)

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

* **Studi Kasus Soal:**
  Sebuah lampu bohlam memiliki hambatan $R = 24 \, \Omega$ dan dihubungkan ke sumber tegangan $V = 12 \, \text{V}$. Berapa arus yang mengalir?

  * *Penyelesaian:*

```math
I = \frac{V}{R} = \frac{12}{24} = 0.5 \text{ Ampere}
```

#### 2. Gaya Lorentz pada Kawat Berarus (Ep. 32)

* **Konsep:** Kawat yang dialiri arus listrik di dalam medan magnet akan mengalami gaya dorong mekanik.

* **Rumus Utama:**

```math
F = I L B \sin(\theta)
```

* **Studi Kasus Soal:**
  Kawat sepanjang $L = 2 \, \text{m}$ dialiri arus $I = 5 \, \text{A}$ diletakkan tegak lurus ($\theta = 90^\circ$, $\sin 90^\circ = 1$) di dalam medan magnet seragam $B = 0.4 \, \text{Tesla}$. Berapa gaya Lorentz yang dialami kawat?

  * *Penyelesaian:*

```math
F = (5)(2)(0.4)(1) = 4 \text{ Newton}
```

## 🌈 Bab 5: Optik Geometri & Gelombang Cahaya (Ep. 38 - 41)

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

* **Studi Kasus Soal:**
  Sinar laser dari udara ($n_1 = 1$) masuk ke air kolam ($n_2 = 1.33$) dengan sudut datang $30^\circ$ ($\sin 30^\circ = 0.5$). Berapa sudut pembiasannya ($\theta_2$)?

  * *Penyelesaian:*

```math
(1)(0.5) = (1.33) \sin(\theta_2) \implies \sin(\theta_2) = \frac{0.5}{1.33} \approx 0.375
```

```math
\theta_2 = \arcsin(0.375) \approx 22^\circ
```

#### 2. Persamaan Lensa Tipis (Ep. 41)

* **Konsep:** Hubungan matematis antara jarak fokus lensa, jarak benda, dan jarak bayangan yang terbentuk.

* **Rumus Utama:**

```math
\frac{1}{f} = \frac{1}{d_o} + \frac{1}{d_i}
```

* **Studi Kasus Soal:**
  Benda diletakkan sejauh $d_o = 30 \, \text{cm}$ di depan lensa cembung yang memiliki jarak fokus $f = 10 \, \text{cm}$. Di manakah bayangan terbentuk ($d_i$)?

  * *Penyelesaian:*

```math
\frac{1}{10} = \frac{1}{30} + \frac{1}{d_i} \implies \frac{1}{d_i} = \frac{1}{10} - \frac{1}{30} = \frac{3 - 1}{30} = \frac{2}{30} = \frac{1}{15}
```

```math
d_i = 15 \text{ cm} \text{ (di belakang lensa)}
```

## ⚛️ Bab 6: Fisika Modern, Kuantum, & Kosmologi (Ep. 42 - 46)

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

* **Studi Kasus Soal (Teoritis):**
  Jika massa sebesar $m = 0.001 \, \text{kg}$ ($1 \, \text{gram}$) dikonversi 100% menjadi energi, berapa besar energi yang dihasilkan? (Kecepatan cahaya $c \approx 3 \times 10^8 \, \text{m/s}$).

  * *Penyelesaian:*

```math
E = (0.001) \cdot (3 \times 10^8)^2 = (0.001) \cdot (9 \times 10^{16}) = 9 \times 10^{13} \text{ Joule}
```

## 📖 Bab 7: Kamus Besar Simbol & Konsep Rumus Fisika

Bagian ini dirancang khusus untuk menjawab kebingungan terbesarmu saat melihat simbol-simbol asing dalam rumus fisika. Simpan bagian ini sebagai referensi cepat!

| Simbol / Notasi | Nama Simbol | Konsep & Arti Fisik | Satuan Internasional (SI) | 
 | ----- | ----- | ----- | ----- | 
| $v$ | Kecepatan (*Velocity*) | Laju perpindahan posisi benda terhadap perubahan waktu. | meter per sekon ($\text{m/s}$) | 
| $u$ **atau** $v_0$ | Kecepatan Awal | Kecepatan objek pada titik awal pengamatan ($t = 0$). | $\text{m/s}$ | 
| $a$ | Percepatan (*Acceleration*) | Laju perubahan kecepatan tiap satuan waktu. | meter per sekon kuadrat ($\text{m/s}^2$) | 
| $x$ **atau** $s$ | Posisi / Jarak | Lokasi atau panjang lintasan linear objek dalam koordinat. | meter ($\text{m}$) | 
| $\Delta x$ | Perpindahan | Perubahan jarak bersih dari titik awal ke titik akhir (vektor). | meter ($\text{m}$) | 
| $t$ | Waktu (*Time*) | Durasi berlangsungnya suatu kejadian atau gerak. | sekon ($\text{s}$) | 
| $m$ | Massa (*Mass*) | Jumlah materi dalam suatu benda; ukuran tingkat kelembaman/inersia. | kilogram ($\text{kg}$) | 
| $F$ | Gaya (*Force*) | Dorongan atau tarikan yang dapat mengubah keadaan gerak benda. | Newton ($\text{N} = \text{kg}\cdot\text{m/s}^2$) | 
| $\sum F$ | Resultan Gaya | Jumlah vektor seluruh gaya yang bekerja secara bersamaan pada suatu sistem. | Newton ($\text{N}$) | 
| $f_k$ **/** $f_s$ | Gaya Gesek (Kinetik/Statis) | Gaya sentuh sejajar bidang yang menghambat pergerakan benda. | Newton ($\text{N}$) | 
| $\mu$ | Koefisien Gesek | Tingkat kekasaran permukaan bidang (tanpa satuan). | *Tanpa Satuan* (Dimensi 1) | 
| $N$ | Gaya Normal | Gaya tekan tegak lurus yang diberikan permukaan bidang terhadap benda. | Newton ($\text{N}$) | 
| $G$ | Konstanta Gravitasi Universal | Tetapan universal yang mengatur kekuatan tarik-menarik antar massa. | $\text{N}\cdot\text{m}^2/\text{kg}^2$ | 
| $g$ | Percepatan Gravitasi Bumi | Percepatan tarik bumi terhadap benda di dekat permukaannya ($\approx 9.8$ atau $10$). | $\text{m/s}^2$ | 
| $W$ | Usaha (*Work*) | Energi yang ditransfer saat gaya memindahkan benda sejauh jarak tertentu. | Joule ($\text{J} = \text{N}\cdot\text{m}$) | 
| $EK$ | Energi Kinetik | Energi yang dimiliki benda karena gerakannya. | Joule ($\text{J}$) | 
| $EP$ | Energi Potensial | Energi tersimpan yang dimiliki benda karena posisi atau wujudnya. | Joule ($\text{J}$) | 
| $P$ | Daya / Tekanan | Daya ($P = W/t$, Watt) adalah laju usaha; Tekanan ($P = F/A$, Pascal) adalah gaya per luas. | Watt ($\text{W}$) atau Pascal ($\text{Pa}$) | 
| $p$ | Momentum Linear | Ukuran kesulitan menghentikan benda bergerak ($p = mv$). | $\text{kg}\cdot\text{m/s}$ | 
| $\tau$ **(Tau)** | Torsi / Momen Gaya | Gaya puntir yang memicu terjadinya gerak rotasi/putar pada benda. | Newton-meter ($\text{N}\cdot\text{m}$) | 
| $I$ | Momen Inersia / Arus | Inersia rotasi benda ($I = \sum mr^2$) atau laju aliran muatan listrik (Ampere). | $\text{kg}\cdot\text{m}^2$ atau Ampere ($\text{A}$) | 
| $\omega$ **(Omega)** | Kecepatan Sudut | Seberapa cepat sudut berputar tiap satuan waktu dalam gerak melingkar/rotasi. | radian per sekon ($\text{rad/s}$) | 
| $\alpha$ **(Alpha)** | Percepatan Sudut | Laju perubahan kecepatan sudut terhadap waktu. | $\text{rad/s}^2$ | 
| $\rho$ **(Rho)** | Massa Jenis (*Density*) | Kerapatan massa zat per satuan volume ($\rho = m/V$). | $\text{kg/m}^3$ | 
| $V$ | Volume / Tegangan | Ruang yang ditempati zat ($m^3$) atau beda potensial listrik/voltase ($\text{Volt}$). | $\text{m}^3$ atau Volt ($\text{V}$) | 
| $f$ | Frekuensi | Jumlah getaran atau gelombang yang lewat dalam satu sekon. | Hertz ($\text{Hz} = 1/\text{s}$) | 
| $T$ | Periode | Waktu yang dibutuhkan untuk menyelesaikan satu siklus penuh getaran/gelombang. | sekon ($\text{s}$) | 
| $\lambda$ **(Lambda)** | Panjang Gelombang | Jarak fisik antara dua puncak gelombang yang berurutan. | meter ($\text{m}$) | 
| $Q$ | Kalor / Muatan Listrik | Energi panas yang berpindah ($J$) atau total muatan listrik dalam Coulomb ($C$). | Joule ($\text{J}$) atau Coulomb ($\text{C}$) | 
| $c$ | Kalor Jenis / Kelajuan Cahaya | Kalor untuk menaikkan suhu zat ($\text{J/kg}\cdot^\circ\text{C}$) atau kecepatan cahaya di vakum ($3 \times 10^8 \, \text{m/s}$). | $\text{J/kg}\cdot^\circ\text{C}$ atau $\text{m/s}$ | 
| $\Delta U$ | Perubahan Energi Dalam | Total energi mikroskopik di dalam sistem termodinamika. | Joule ($\text{J}$) | 
| $k$ | Konstanta Pegas / Coulomb | Kekakuan pegas ($\text{N/m}$) atau konstanta elektrostatik ($\approx 8.99 \times 10^9$). | $\text{N/m}$ atau $\text{N}\cdot\text{m}^2/\text{C}^2$ | 
| $E$ | Medan Listrik / Energi | Kekuatan medan listrik ($\text{N/C}$) atau total energi relativistik ($\text{J}$). | $\text{N/C}$ atau Joule ($\text{J}$) | 
| $R$ | Hambatan Listrik | Hambatan atau rintangan terhadap aliran arus listrik dalam kawat. | Ohm ($\Omega$) | 
| $B$ | Medan Magnet (*Magnetic Field*) | Kepadatan fluks atau kekuatan medan magnet di suatu titik ruang. | Tesla ($\text{T}$) | 
| $n$ | Indeks Bias | Perbandingan kecepatan cahaya di vakum dengan kecepatan di medium. | *Tanpa Satuan* | 
| $f$ | Fokus Lensa / Cermin | Titik kumpul utama cahaya pantul atau bias pada perangkat optik. | meter ($\text{m}$) atau sentimeter ($\text{cm}$) | 

> 💡 *Gunakan panduan ini secara aktif: saat mengerjakan soal, buka bab yang relevan, periksa makna simbol di Bab 7, dan ikuti langkah-langkah bedah rumusnya. Selamat belajar dan merancang project fisikamu!*