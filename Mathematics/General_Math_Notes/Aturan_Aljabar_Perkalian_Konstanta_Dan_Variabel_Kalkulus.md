# Catatan Aljabar: Aturan Operasi antara Konstanta dan Variabel dalam Penyederhanaan Kalkulus

Catatan ini meluruskan konsep dasar aljabar mengenai kapan konstanta dan variabel **boleh** dioperasikan dan kapan **tidak boleh** digabungkan, terutama saat melakukan penyederhanaan pada hasil akhir turunan Aturan Rantai.

---

## 📌 Inti Aturan Aljabar

Kunci utama pemisahan konstanta dan variabel bergantung sepenuhnya pada **jenis operasi matematika** yang digunakan:

*   ❌ **Penjumlahan & Pengurangan:** **TIDAK BOLEH** digabungkan (karena bukan suku sejenis).
*   ✅ **Perkalian & Pembagian:** **SANGAT BOLEH** dioperasikan langsung pada koefisiennya.

---

## 🔍 Perbandingan dan Analogi Operasi

### 1. Operasi Penjumlahan & Pengurangan (Dilarang Digabung)
Konstanta dan variabel diibaratkan seperti jenis barang yang berbeda (misal: mangga dan apel), sehingga tidak bisa dijumlahkan menjadi satu kesatuan suku.
*   **Contoh:** 
    ```math
    4 + 2x \neq 6x
    ```
*   **Catatan:** Hasilnya harus tetap ditulis berupa dua suku terpisah yaitu  ```math 4 + 2x ```. Aturan ini juga berlaku ketat dalam sistem pertidaksamaan.

### 2. Operasi Perkalian & Pembagian (Wajib Dioperasikan)
Perkalian berarti melipatgandakan jumlah variabel yang ada. Jika Anda memiliki $4$ kotak dan setiap kotak berisi $2x$ apel, maka total apel keseluruhan adalah $8x$.
*   **Contoh:** 
    ```math
    4 \cdot (2x) = 8x
    ```
*   **Cara Kerja:** Kalikan sesama angka/konstanta penyusunnya ($4 \times 2 = 8$), lalu ikuti dengan variabel $x$ di belakangnya.

---

## 🧮 Implementasi pada Kasus Turunan Aturan Rantai

Pada proses akhir turunan fungsi kuadrat sebelumnya, kita dihadapkan pada persamaan berikut:

```math
\frac{dy}{dx} = 4(x^2 + 1)^3 \cdot (2x)
```

Hubungan antar-suku pada persamaan di atas sepenuhnya adalah **operasi perkalian**. Berdasarkan sifat komutatif aljabar, posisi perkalian bebas ditukar atau dikelompokkan ulang untuk mempermudah perhitungan:

```math
\frac{dy}{dx} = [4 \cdot 2x] \cdot (x^2 + 1)^3
```

Karena ```math \(4 \cdot 2x\) ``` berbentuk operasi perkalian, maka keduanya **bisa dan wajib** dikalikan langsung menjadi **```math 8x ```**.

```math
\frac{dy}{dx} = 8x(x^2 + 1)^3
```

---

## 💡 Kesimpulan Singkat untuk Diingat
> *   **Jangan pernah** menambahkan angka bebas dengan angka yang menempel pada variabel ($4 + 2x \rightarrow$ **Stop!**).
> *   **Selalu kalikan** angka bebas dengan angka koefisien variabel jika hubungannya adalah perkalian ($4 \cdot 2x = 8x \rightarrow$ **Lanjutkan!**).
