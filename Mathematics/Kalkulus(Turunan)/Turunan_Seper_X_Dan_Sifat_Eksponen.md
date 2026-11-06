# Catatan Matematika: Turunan Fungsi Aljabar dan Sifat Eksponen Negatif

Catatan ini membahas langkah demi langkah cara mencari turunan dari fungsi aljabar berbentuk pecahan, lengkap dengan penjelasan logis di balik perubahan tanda eksponen dan aturan perkalian tandanya.

---

## 1. Cara Menurunkan Fungsi $1/x$

Turunan pertama dari fungsi 
```math
f(x) = \frac{1}{x} 
```

adalah:

```math
f'(x) = -\frac{1}{x^2}
```

### Langkah-Langkah Penyelesaian (Aturan Pangkat / *Power Rule*)

1. **Ubah Bentuk Pecahan Menjadi Pangkat Negatif**  
   Sebelum diturunkan, ubah posisi variabel agar tidak lagi berada di bawah pecahan (penyebut).
   ```math 
   \frac{1}{x} = x^{-1}
   ```

2. **Terapkan Aturan Pangkat**  
   Gunakan rumus umum turunan 
    ```math 
    \frac{d}{dx}[x^n] = n \cdot x^{n-1}
    ```
    . Jatuhkan pangkat awal ($n = -1$) ke depan sebagai pengali, lalu kurangi pangkatnya dengan $1$. 
    ```math
        \frac{d}{dx} [x^{-1}] = -1 \cdot x^{-1 - 1}
    ```

3. **Hitung Hasil Pangkat Baru**  
    ```math
        -1 \cdot x^{-2}
    ```

4. **Kembalikan ke Bentuk Pecahan Positif**
    Ubah kembali pangkat negatif menjadi bentuk pecahan agar hasilnya lebih rapi.
    ```math
        -x^{-2} = -\frac{1}{x^2}
    ```

---

## 2. Mengapa Pangkatnya Berubah Tanda Menjadi Negatif?

Perubahan dari $$(\frac{1}{x})$$  menjadi $$x^{-1}$$ terjadi karena **Sifat Eksponen (Pangkat)** dalam matematika. Tanda minus pada pangkat merupakan sebuah "simbol kode" yang berarti **"seper" atau pembagian**, bukan berarti nilai bilangannya negatif.

Ada dua cara logis untuk memahami aturan ini:

### Pendekatan Pola Pembagian Berulang
Jika kita perhatikan pola pembagian angka 10 dengan basis yang pangkatnya terus dikurangi 1:
* $10^3 = 1000$
* $10^2 = 100$ *(dibagi 10)*
* $10^1 = 10$ *(dibagi 10)*
* $10^0 = 1$ *(dibagi 10)*

Jika pola pengurangan pangkat dilanjutkan ke area negatif, operasinya harus tetap sama yaitu **dibagi 10**:
* $10^{-1} = 1 \div 10 = \mathbf{\frac{1}{10}}$
* $10^{-2} = 1 \div 100 = \mathbf{\frac{1}{10^2}}$

> **Kesimpulan Pola:** Konsep yang sama berlaku pada variabel $x$, di mana $$(x^{-1} = \frac{1}{x})$$.

### Pendekatan Hukum Eksponen
Berdasarkan hukum pembagian perpangkatan:
```math
\frac{x^a}{x^b} = x^{a - b}
```

Ingat kembali sifat matematika dasar bahwa semua bilangan (kecuali 0) jika dipangkatkan 0 hasilnya adalah 1 ($x^0 = 1$). Sementara variabel $x$ pada dasarnya adalah $x^1$.

```math
\frac{1}{x} = \frac{x^0}{x^1} = x^{0 - 1} = x^{-1}
```

---

## 3. Mengapa Hasil Akhir Turunannya Berubah Menjadi Negatif?

Ada dua alasan mengapa hasil akhirnya wajib memiliki tanda negatif ($-$).

### Alasan Aljabar (Perkalian Tanda)
Saat menerapkan aturan pangkat pada $x^{-1}$, angka $-1$ maju ke depan sebagai pengali. Karena koefisien awal di depan variabel $x$ adalah $+1$ (positif), maka terjadi operasi perkalian tanda:
```math
(\text{Negatif}) \times (\text{Positif}) = \text{Negatif}
```
```math
-1 \times 1 = -1
```

### Alasan Grafis (Geometri Kalkulus)
Turunan merupakan representasi dari **kemiringan (gradien) garis singgung** sebuah kurva. 

* Grafik dari fungsi $$f(x) (= \frac{1}{x})$$ adalah kurva hiperbola yang **selalu bergerak turun** jika dibaca dari arah kiri ke kanan.
* Karena grafiknya selalu menurun, maka nilai kemiringannya (gradiennya) otomatis **pasti selalu negatif**. 
* Tanda minus pada $$(-\frac{1}{x^2})$$ bertugas memastikan bahwa nilai turunan fungsi tersebut akan selalu bernilai negatif untuk angka $x$ berapapun yang dimasukkan.
