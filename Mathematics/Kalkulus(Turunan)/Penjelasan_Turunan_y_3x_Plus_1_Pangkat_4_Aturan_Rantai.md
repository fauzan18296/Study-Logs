# Catatan Kalkulus: Turunan Fungsi Komposisi menggunakan Aturan Rantai (Chain Rule)

Catatan ini membahas mengenai pemecahan langkah turunan pada fungsi pangkat dalam bentuk fungsi komposisi, khususnya untuk menjawab kebingungan mengenai asal-usul angka perkalian di akhir rumus turunan.

---

## 📌 Topik Utama: Analisis Komponen Turunan
Diberikan sebuah fungsi awal sebagai berikut:

```math
y = (3x + 1)^4
```

Proses penurunan fungsi tersebut menggunakan **Aturan Rantai (Chain Rule)** menghasilkan persamaan:

```math
\frac{dy}{dx} = 4(3x + 1)^3 \cdot (3) = 12(3x + 1)^3
```

---

## 🔍 Bedah Langkah & Struktur Rumus

Untuk memahami dari mana setiap komponen angka tersebut berasal, kita bagi fungsi menjadi dua bagian: **Fungsi Luar** dan **Fungsi Dalam**.

### 1. Turunan Fungsi Luar (Operasi Pangkat)
*   **Proses:** Pangkat mula-mula ($4$) dibawa ke depan sebagai pengali, kemudian pangkat dari fungsi tersebut dikurangi satu ($4 - 1 = 3$).
*   **Hasil Langkah Pertama:**
    ```math
    4(3x + 1)^3
    ```

### 2. Turunan Fungsi Dalam
*   **Proses:** Cari turunan dari fungsi yang berada di dalam kurung, yaitu $(3x + 1)$.
    *   Turunan dari $3x$ adalah **$3$**.
    *   Turunan dari konstanta $1$ adalah **$0$**.
*   **Hasil Langkah Kedua:**
    ```math
    3
    ```

---

## 💡 Kesimpulan Jawaban

> ⚠️ **Pertanyaan:** Apakah angka $(3)$ yang di paling belakang berasal dari pangkatnya?
>
> ❌ **Jawaban:** **Bukan.** Angka $(3)$ di paling belakang **bukan** berasal dari pangkat 3, melainkan merupakan **hasil turunan dari fungsi bagian dalam $\mathbf{(3x + 1)}$**.

### Ringkasan Pemetaan Angka:
*   **$4$** di bagian depan $\rightarrow$ Berasal dari **pangkat mula-mula**.
*   Pangkat **$3$** yang baru $\rightarrow$ Hasil dari **pangkat lama dikurangi satu** ($4 - 1$).
*   Angka **$(3)$** di dalam kurung paling belakang $\rightarrow$ Hasil **turunan fungsi dalam** $\frac{d}{dx}(3x + 1)$.

Gabungan kedua langkah ini kemudian dikalikan secara aljabar:
```math
\frac{dy}{dx} = 4(3x + 1)^3 \cdot (3) = 12(3x + 1)^3
```
