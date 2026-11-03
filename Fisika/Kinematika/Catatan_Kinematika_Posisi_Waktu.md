# Catatan Kinematika: Persamaan Posisi Terhadap Waktu $x(t)$

Catatan ini merangkum analisis rumus posisi terhadap waktu $x(t)$ dalam kinematika, khususnya untuk kasus benda yang mengalami perubahan dari kecepatan konstan awal ke kecepatan konstan akhir.

---

## 📌 Konsep Dasar & Satuan dalam Kinematika
Sebelum masuk ke rumus, sangat penting untuk memahami simbol dan Satuan Internasional (SI) agar tidak tertukar:

* **$x(t)$** : Posisi atau Jarak akhir pada waktu $t$, dengan satuan **meter (m)**.
* **$v$ atau $v(t)$** : Kecepatan, dengan satuan **meter per sekon (m/s)**.
* **$a$** : Percepatan atau Perlambatan, dengan satuan **meter per sekon kuadrat (m/s²)**.
* **$t$** : Waktu, dengan satuan **sekon atau detik (s)**.

---

## 🏎️ Analisis Kasus: Gerak Dua Fase (Konstan $\rightarrow$ Konstan)
Kasus yang dianalisis adalah sebuah benda yang awalnya bergerak dengan kecepatan konstan pertama, lalu berubah menjadi kecepatan konstan kedua.

* **Fase 1:** Kecepatan konstan awal ($v_0$) = $10 \text{ m/s}$ (pada saat $t = 0$)
* **Fase 2:** Kecepatan konstan akhir ($v$) = $4 \text{ m/s}$

### Rumus Posisi Akhir $x(t)$ pada Fase Kedua
Untuk mencari posisi benda ketika sudah berada di fase kedua (saat kecepatannya stabil di $4 \text{ m/s}$), kita menggunakan rumus Gerak Lurus Beraturan (GLB):

```math
x(t) = x_0 + v \(\cdot\) t
```

Jika kita masukkan nilai kecepatan konstan fase kedua ($v = 4 \text{ m/s}$), maka rumusnya menjadi:

```math
x(t) = x_0 + 4t
```

> ⚠️ **Catatan Penting tentang $x_0$:**  
> Nilai $x_0$ di sini bukanlah nol, melainkan **total jarak yang sudah ditempuh benda selama Fase 1** (saat kecepatannya masih $10 \text{ m/s}$).

---

## ❓ Pertanyaan-Pertanyaan Kunci yang Terjawab

### 1. Apakah nilai $t$ perlu dicari angkanya?
* **Tidak perlu:** Jika tujuan Anda hanya ingin membuat **rumus fungsi atau persamaan posisi**. Huruf $t$ dibiarkan tetap sebagai variabel agar persamaannya bisa digunakan untuk menghitung posisi di detik ke berapa pun.
* **Perlu:** Jika di dalam soal terdapat pertanyaan spesifik, seperti: *"Pada detik ke berapakah benda mencapai posisi tertentu (misal 50 meter)?"*.

### 2. Setelah menemukan hasil akhir $x(t)$, apa satuannya?
* Satuannya adalah **meter (m)**, bukan $\text{m/s}^2$.
* **Pembuktian Satuan secara Dimensi:**

```math
x(t) \(= (\text{meter}) + \left( \frac{\text{meter}}{\text{sekon}} \times \text{sekon} \right) = \text{meter (m)} \%\%\)MAGIT_PARSER_PROTECT%%```

---

## 💡 Contoh Cara Penerapan Rumus

Misalkan di soal diketahui benda bergerak di Fase 1 (kecepatan $10 \text{ m/s}$) selama **$3 \text{ sekon}$**, lalu setelah itu kecepatannya berubah menjadi konstan **$4 \text{ m/s}$**.

1. **Cari Jarak Awal ($x_0$):**
```math
\(x_0 = v_{\text{fase1}} \times t_{\text{fase1}} = 10 \times 3 = 30 \text{ meter} \%\%\)MAGIT_PARSER_PROTECT%%```

2. **Masukkan ke Rumus Fungsi Posisi Akhir:**
```math
x(t) = 30 + 4t
```

3. **Menghitung Posisi pada Detik Tertentu (Misal $t = 5 \text{ sekon}$ di fase kedua):**
```math
x\((5) = 30 + 4(5) = 30 + 20 = 50 \text{ meter} \%\%\)MAGIT_PARSER_PROTECT%%```
