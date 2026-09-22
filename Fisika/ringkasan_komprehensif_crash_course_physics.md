# 🌌 Ringkasan Komprehensif: Crash Course Physics (Konsep, Bedah Rumus, dan Penerapan)

*(Berdasarkan Playlist YouTube Crash Course - 46 Episode)*

Catatan ini dirancang untuk memberikan pemahaman fisika yang menyeluruh, dari cara benda jatuh hingga bagaimana alam semesta bekerja di tingkat subatomik. Setiap bagian kini dilengkapi dengan penjelasan konsep yang lebih mendalam, bedah rumus, dan simulasi perhitungan matematisnya.

---

## 1. ⚙️ Mekanika Klasik dan Kinematika (Episode 1-15)

Mekanika adalah pilar utama fisika yang mempelajari gerak dan gaya. 

### A. Kinematika 1D & 2D (Gerak Lurus dan Parabola)

* **Penjelasan Konsep:** Kinematika adalah cara kita mendeskripsikan *bagaimana* benda bergerak (posisi, kecepatan, percepatan) tanpa peduli *apa* yang mendorongnya. Dalam dunia nyata (2D), gerak seperti bola yang dilempar (parabola) dipecah menjadi dua sumbu: sumbu X (gerak mendatar yang konstan tanpa hambatan udara) dan sumbu Y (gerak naik-turun yang dipengaruhi percepatan gravitasi bumi).
* **Bedah Rumus (GLBB - Gerak Lurus Berubah Beraturan):** 
  `x = x0 + v0*t + 0.5 * a * t^2`
  * `x` = Posisi akhir benda.
  * `x0` = Posisi awal (titik mulai).
  * `v0*t` = Kontribusi jarak dari kecepatan awal (`v0`) seiring berjalannya waktu (`t`).
  * `0.5 * a * t^2` = Kontribusi jarak ekstra yang didapat karena benda mengalami percepatan (`a`) yang terus menambah kecepatannya setiap detik kuadrat (`t^2`).
* **Contoh Penerapan Perhitungan:** 
  Sebuah mobil balap diam di garis start (`v0 = 0 m/s`, `x0 = 0 m`). Saat lampu hijau menyala, mobil digas dengan percepatan konstan `a = 4 m/s^2`. Di manakah posisi mobil setelah 5 detik (`t = 5 s`)?
  
  `x = 0 + (0 * 5) + 0.5 * (4) * (5^2)`
  
  `x = 0 + 0 + 2 * (25) = 50 meter`
  
  Jadi, mobil berada 50 meter dari garis start.

### B. Hukum Newton & Dinamika Gaya

* **Penjelasan Konsep:** Jika kinematika adalah *bagaimana* benda bergerak, dinamika (Hukum Newton) menjelaskan *mengapa* benda bergerak. Hukum I menyatakan benda malas berubah (Inersia). Hukum II mengaitkan gaya total, massa, dan percepatan. Hukum III menyatakan setiap aksi memiliki reaksi yang sama dan berlawanan arah.
* **Bedah Rumus (Hukum II Newton):**
  `ΣF = m * a`
  * `ΣF` = Jumlah seluruh gaya yang bekerja pada benda (Newton / N). Ingat, ini adalah vektor (punya arah).
  * `m` = Massa benda (kg), melambangkan "kemalasan" atau inersia benda. Semakin besar massa, semakin kecil percepatan yang dihasilkan.
  * `a` = Percepatan (m/s^2).
* **Contoh Penerapan Perhitungan:**
  Anda mendorong lemari es bermassa 50 kg ke kanan dengan gaya 200 N. Namun ada gaya gesek lantai sebesar 50 N ke kiri. Berapa percepatan lemari es tersebut?
  
  `ΣF = F_dorong - F_gesek = 200 - 50 = 150 N` (ke kanan).
  
  `a = ΣF / m = 150 / 50 = 3 m/s^2`
  
  Lemari es bergerak dengan percepatan 3 m/s^2 ke kanan.

### C. Usaha, Energi, dan Kekekalan Momentum

* **Penjelasan Konsep:** Usaha adalah cara mentransfer energi dari satu sistem ke sistem lain dengan memberikan gaya sepanjang jarak tertentu. Energi Kinetik (gerak) dan Energi Potensial (ketinggian) bisa saling berubah namun totalnya tetap (Kekekalan Energi). Momentum adalah "jumlah gerak" benda yang membuatnya sulit dihentikan.
* **Bedah Rumus (Kekekalan Energi Mekanik):**
  `EM1 = EM2` atau `EP1 + EK1 = EP2 + EK2`
  * `EP` (Energi Potensial Gravitasi) = `m * g * h` (massa × gravitasi × ketinggian). Energi yang tersimpan karena posisi.
  * `EK` (Energi Kinetik) = `0.5 * m * v^2`. Energi karena kecepatan (`v`).
* **Contoh Penerapan Perhitungan:**
  Buah kelapa bermassa 2 kg berada di pohon setinggi 5 m (`g = 10 m/s^2`). Saat belum jatuh, kecepatannya 0, sehingga `EK1 = 0` dan `EP1 = 2 * 10 * 5 = 100 Joule`. Total energinya 100 J. 
  Saat mencapai tanah (ketinggian `h = 0`, `EP2 = 0`), berapakah kecepatan (`v`) kelapa menabrak tanah?
  
  `100 J + 0 = 0 + 0.5 * m * v^2`
  
  `100 = 0.5 * (2) * v^2` -> `v^2 = 100` -> `v = 10 m/s`.

---

## 2. 🌊 Gelombang, Osilasi, dan Fluida (Episode 16-19)

### A. Gerak Harmonik Sederhana (Pegas)

* **Penjelasan Konsep:** Osilasi adalah gerak bolak-balik melewati titik kesetimbangan (seperti bandul atau pegas). Ini terjadi karena ada "gaya pemulih" yang selalu berusaha mengembalikan benda ke posisi diamnya (titik 0).
* **Bedah Rumus (Hukum Hooke):**
  `F = -k * x`
  * `F` = Gaya pemulih (Newton).
  * `k` = Konstanta pegas (N/m). Menunjukkan tingkat "kekerasan" pegas. Semakin besar `k`, semakin kaku pegas tersebut.
  * `x` = Simpangan/perpindahan dari titik normal.
  * Tanda minus (-) menunjukkan arah gaya *selalu berlawanan* dengan arah simpangan (jika ditarik ke bawah, pegas menarik ke atas).
* **Contoh Penerapan Perhitungan:**
  Sebuah pegas memiliki konstanta `k = 200 N/m`. Jika Anda menariknya sejauh 0.1 m (10 cm) dari posisi normalnya, berapa gaya yang diberikan pegas pada tangan Anda?
  
  `F = -(200 * 0.1) = -20 N`
  
  Pegas menarik balik tangan Anda dengan gaya sebesar 20 Newton.

### B. Mekanika Fluida (Gaya Apung/Archimedes)

* **Penjelasan Konsep:** Fluida (zat cair/gas) memberikan tekanan ke segala arah. Hukum Archimedes menyatakan benda yang dicelupkan ke fluida mendapat gaya angkat ke atas yang sama dengan berat fluida yang didesak/dipindahkan oleh benda tersebut. Inilah mengapa kapal besi raksasa bisa mengapung.
* **Bedah Rumus:**
  `FA = ρ * g * V`
  * `FA` = Gaya apung ke atas (Newton).
  * `ρ` (rho) = Massa jenis fluida (kg/m^3), bukan massa jenis benda! Air bernilai sekitar 1000 kg/m^3.
  * `g` = Gravitasi (sekitar 9.8 atau 10 m/s^2).
  * `V` = Volume fluida yang dipindahkan atau volume benda yang tercelup (m^3).
* **Contoh Penerapan Perhitungan:**
  Balok kayu memiliki volume 0.5 m^3 dan seluruhnya tercelup di dalam kolam air (`ρ = 1000`). Berapa gaya angkat yang dialami balok?
  
  `FA = 1000 * 10 * 0.5 = 5000 Newton`

---

## 3. 🔥 Termodinamika (Episode 20-24)

### Kalor dan Asas Black

* **Penjelasan Konsep:** Suhu adalah rata-rata getaran partikel. Kalor (panas) adalah energi yang berpindah akibat perbedaan suhu (dari benda panas ke dingin) hingga mencapai keseimbangan termal (suhu sama). Asas Black adalah bentuk hukum kekekalan energi: panas yang dilepas benda bersuhu tinggi sama dengan panas yang diserap benda bersuhu rendah.
* **Bedah Rumus (Kalor Laten/Sensibel):**
  `Q = m * c * ΔT`
  * `Q` = Kalor / Energi Panas (Joule).
  * `m` = Massa zat (kg).
  * `c` = Kalor jenis (J/kg°C). Menunjukkan "harga" energi untuk menaikkan suhu zat itu. Air punya `c` yang sangat tinggi (susah dipanaskan, lambat dingin).
  * `ΔT` = Perubahan suhu (`T_akhir - T_awal`).
* **Contoh Penerapan Perhitungan:**
  Berapa energi yang dibutuhkan untuk memanaskan 2 kg air (`c = 4200 J/kg°C`) dari suhu 20°C menjadi mendidih di 100°C?
  `ΔT = 100 - 20 = 80°C`.
  
  `Q = 2 * 4200 * 80 = 672.000 Joule` (atau 672 kJ).

---

## 4. ⚡ Kelistrikan dan Kemagnetan (Episode 25-37)

### Hukum Ohm dan Sirkuit Listrik

* **Penjelasan Konsep:** Bayangkan listrik seperti aliran air di pipa. 
  * **Tegangan (Voltase/V)** adalah pompa pendorongnya.
  * **Arus (Ampere/I)** adalah jumlah laju air yang mengalir.
  * **Hambatan (Ohm/R)** adalah batu di dalam pipa yang menghambat aliran air (bisa berupa lampu, TV, atau resistor).
  Semakin besar pompa (V), makin deras arus (I). Semakin banyak sumbatan (R), makin kecil arus (I).
* **Bedah Rumus:**
  `V = I * R` atau `I = V / R`
* **Contoh Penerapan Perhitungan:**
  Sebuah lampu bohlam memiliki hambatan `R = 24 Ω`. Lampu dihubungkan ke aki mobil yang tegangannya `V = 12 Volt`. Berapa arus yang mengalir memanaskan kawat lampu tersebut?
  
  `I = 12 / 24 = 0.5 Ampere`

---

## 5. 💡 Optik dan Sifat Cahaya (Episode 38-41)

### Pembiasan (Hukum Snellius)

* **Penjelasan Konsep:** Cahaya punya kecepatan batas di ruang hampa (3 × 10^8 m/s). Namun jika masuk ke zat yang lebih "padat" (seperti air atau kaca), cahaya melambat. Perubahan kecepatan batas secara asimetris ini menyebabkan lintasan cahaya "patah" atau berbelok. Fenomena ini disebut pembiasan.
* **Bedah Rumus:**
  `n1 * sin(θ1) = n2 * sin(θ2)`
  * `n1`, `n2` = Indeks bias medium 1 dan medium 2. (Udara `n ≈ 1`, kaca `n ≈ 1.5`). Indeks bias adalah perbandingan kecepatan cahaya di ruang hampa vs di medium tersebut.
  * `θ1` = Sudut datang cahaya (diukur dari garis normal tegak lurus permukaan).
  * `θ2` = Sudut bias (setelah masuk medium baru).
* **Contoh Penerapan Perhitungan:**
  Sinar laser ditembakkan dari udara (`n1 = 1`) ke permukaan kolam air (`n2 = 1.33`) dengan sudut datang 30° (`sin 30° = 0.5`). Berapa sudut pembiasannya?
  
  `1 * 0.5 = 1.33 * sin(θ2)`
  
  `sin(θ2) = 0.5 / 1.33 ≈ 0.375`
  
  `θ2 = arcsin(0.375) ≈ 22°`
  
  Sinar berbelok menjadi lebih curam (mendekati garis normal) di dalam air.

---

## 6. 🚀 Fisika Modern & Relativitas (Episode 42-46)

### Relativitas Khusus (Kesetaraan Massa-Energi)

* **Penjelasan Konsep:** Einstein menemukan bahwa laju cahaya selalu konstan siapapun yang melihatnya. Akibatnya, waktu dan panjang bersifat tidak mutlak (relatif). Selain itu, ruang dan materi saling terikat. Massa benda ternyata hanyalah energi yang "membeku" atau terkonsentrasi dalam ruang yang sangat kecil.
* **Bedah Rumus:**
  `E = m * c^2`
  * `E` = Energi (Joule).
  * `m` = Massa materi (kg).
  * `c^2` = Kuadrat kecepatan cahaya (3 × 10^8 m/s dikuadratkan menjadi 9 × 10^16). Angka pengali ini sangat masif!
* **Contoh Penerapan Perhitungan (Teoritis):**
  Jika Anda bisa memusnahkan 1 gram (0.001 kg) massa sebutir kacang hingga berubah 100% murni menjadi energi (seperti dalam reaksi antimateri), seberapa besar energi ledakan yang dihasilkan?
  
  `E = 0.001 * (3 * 10^8)^2`
  
  `E = 0.001 * (9 * 10^16) = 9 * 10^13 Joule`
  
  Energi ini setara dengan ledakan bom atom Hiroshima (sekitar 15 kiloton TNT). Ini membuktikan bahwa di dalam sebuah massa yang sangat kecil, tersimpan energi potensial alam semesta yang luar biasa dahsyat.