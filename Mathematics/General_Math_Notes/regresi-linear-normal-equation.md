# Menghitung Bobot Optimal dan Intercept pada Regresi Linear (Metode Normal Equation)

Dokumen ini menjelaskan bagaimana formula matematika **Normal Equation** (Ordinary Least Squares - OLS) bekerja untuk mencari bobot optimal (*weight*) sekaligus nilai potong sumbu (*intercept*) dalam model Regresi Linear menggunakan trik augmentasi matriks (*Bias Trick*).

---

## 1. Formula Dasar (Normal Equation)

Untuk mencari bobot optimal, kita menggunakan rumus analitis langsung (sekali hitung) tanpa perlu proses iteratif seperti *Gradient Descent*:

```math
\(\mathbf{w}_{opt} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y} \%\%\)MAGIT_PARSER_PROTECT%%```

### Keterangan Komponen:
*   **$\mathbf{w}_{opt}$** : Vektor kolom berisi bobot (*weight*) dan *intercept* optimal yang dicari.
*   **$\mathbf{X}$** : Matriks fitur atau data input.
*   **$\mathbf{X}^T$** : Transpose dari matriks fitur $\mathbf{X}$.
*   **$(\mathbf{X}^T \mathbf{X})^{-1}$** : Invers dari hasil perkalian matriks $\mathbf{X}^T$ dengan $\mathbf{X}$.
*   **$\mathbf{y}$** : Vektor kolom dari target atau nilai asli yang ingin diprediksi.

---

## 2. Cara Otomatis Mencari Intercept (*Bias Trick*)

Agar rumus di atas bisa menghitung *intercept* sekaligus bersama *weight* lainnya secara otomatis, kita harus melakukan **Augmentasi Fitur** (menambahkan kolom angka 1) pada matriks $\mathbf{X}$ sebelum proses kalkulasi dimulai.

### Langkah-Langkah:
1.  Tambahkan **kolom berisi angka 1** pada **kolom pertama** matriks fitur $\mathbf{X}$. Kolom ini mewakili komponen bias atau *intercept*.
2.  Lakukan operasi matematika sesuai rumus Normal Equation seperti biasa.

### Representasi Visual Perubahan Matriks:

Jika data asli Anda hanya memiliki 1 fitur ($x$), bentuk matriks $\mathbf{X}$ yang baru dimodifikasi menjadi:

```math
\(\mathbf{X} = \begin{bmatrix} 1 & x_{11} \\ 1 & x_{21} \\ 1 & x_{31} \end{bmatrix} \%\%\)MAGIT_PARSER_PROTECT%%```

Ketika di-transpose ($\mathbf{X}^T$), kolom pertama yang berisi angka 1 otomatis berubah posisi menjadi **baris pertama**:

```math
\(\mathbf{X}^T = \begin{bmatrix} 1 & 1 & 1 \\ x_{11} & x_{21} & x_{31} \end{bmatrix} \%\%\)MAGIT_PARSER_PROTECT%%```

---

## 3. Memahami Hasil Akhir Vektor $\mathbf{w}_{opt}$

Hasil akhir dari perhitungan rumus di atas bukanlah sebuah matriks lebar, melainkan sebuah **vektor kolom vertikal**. Posisi nilai *intercept* dan *weight* ditentukan secara berurutan berdasarkan **barisnya** (dari atas ke bawah):

```math
\(\mathbf{w}_{opt} = \begin{bmatrix} \text{Baris 1} \\ \text{Baris 2} \end{bmatrix} = \begin{bmatrix} \text{Intercept } (w_0) \\ \text{Weight } (w_1) \end{bmatrix} \%\%\)MAGIT_PARSER_PROTECT%%```

*   **Baris 1 (Paling Atas):** Menghasilkan nilai **Intercept** ($w_0$). Hal ini karena pada matriks $\mathbf{X}$, angka 1 diletakkan di kolom pertama.
*   **Baris 2 (Di Bawahnya):** Menghasilkan nilai **Weight** ($w_1$) untuk fitur pertama Anda.

### Skalabilitas untuk Multi-Fitur
Jika di kemudian hari data Anda berkembang memiliki 3 fitur berbeda, maka struktur baris pada vektor hasil akhirnya akan memanjang ke bawah seperti ini:

```math
\(\mathbf{w}_{opt} = \begin{bmatrix} w_0 \\ w_1 \\ w_2 \\ w_3 \end{bmatrix} \rightarrow \begin{bmatrix} \text{\textbf{Intercept}} \\ \text{Weight Fitur 1} \\ \text{Weight Fitur 2} \\ \text{Weight Fitur 3} \end{bmatrix} \%\%\)MAGIT_PARSER_PROTECT%%```

---

## 4. Alur Kerja Perhitungan (Ringkasan)

Seluruh proses manipulasi matriks hingga menghasilkan nilai prediksi yang presisi digabungkan dalam satu alur kerja linear berikut:
```math
[Data Asli X]
│
▼
[Tambah Kolom 1 di Depan] ──> Menghasilkan matriks X baru (kolom 1 mewakili bias)
│
▼
[Hitung X Transpose] ───────> Kolom pertama angka 1 otomatis berotasi menjadi baris pertama
│
▼
[Operasikan Rumus OLS] ─────> \mathbf{w}_{opt} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}
│
▼
[Hasil Akhir Vektor] ───────> Baris 1 otomatis menjadi Intercept (w0), Baris 2 menjadi Weight (w1)
```
Alur perhitungan ini secara matematis mengunci persamaan regresi linear agar tetap terjaga dalam bentuk standarnya:

```math
\(y = w_0 \cdot (1) + w_1 \cdot (x)\)
```

Dengan integrasi alur ini, perkalian matriks tidak akan tertukar karena letak *intercept* ($w_0$) yang berada di baris pertama linier dengan keberadaan angka 1 di kolom pertama matriks data input.


