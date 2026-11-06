# Catatan Kalkulus: Perbandingan Aturan Rantai pada Fungsi Dalam Linear vs. Kuadrat serta Aturan Perkalian Koefisien

Catatan ini membahas secara mendalam penggunaan **Aturan Rantai (Chain Rule)** untuk mencari turunan fungsi komposisi. Fokus utama catatan ini adalah membandingkan perbedaan hasil ketika fungsi bagian dalam berbentuk linear vs. kuadrat, serta menegaskan aturan pengoperasian aljabar di tahap akhir (perkalian koefisien).

---

## 📌 Topik 1: Kasus Fungsi Dalam Linear
Diberikan sebuah fungsi dengan bagian dalam berbentuk linear (pangkat satu):

```math
y = (3x + 1)^4
```

### 🔍 Bedah Langkah Turunan:
1. **Turunan Fungsi Luar (Pangkat):** Pangkat $4$ dibawa ke depan, lalu pangkat kurung dikurangi satu.
   ```math
   4(3x + 1)^3
   ```
2. **Turunan Fungsi Dalam:** Turunan dari $(3x + 1)$ adalah **$3$** (konstanta).

### 🧮 Tahap Pengoperasian Akhir:
Gabungkan kedua langkah dengan perkalian aljabar:
```math
\frac{dy}{dx} = 4(3x + 1)^3 \cdot (3)
```
*   **Aturan Perkalian:** Hanya kalikan koefisien bebas di luar kurung, yaitu $4 \cdot 3 = 12$.
*   **Hasil Akhir:**
    ```math
    \frac{dy}{dx} = 12(3x + 1)^3
    ```

---

## 📌 Topik 2: Kasus Fungsi Dalam Kuadrat ($x^2$)
Diberikan sebuah fungsi dengan bagian dalam berbentuk kuadrat (pangkat dua):

```math
y = (x^2 + 1)^4
```

### 🔍 Bedah Langkah Turunan:
1. **Turunan Fungsi Luar (Pangkat):** Pangkat $4$ dibawa ke depan, lalu pangkat kurung dikurangi satu.
   ```math
   4(x^2 + 1)^3
   ```
2. **Turunan Fungsi Dalam:** Turunan dari $(x^2 + 1)$ adalah **$2x$** (mengandung variabel $x$).

### 🧮 Tahap Pengoperasian Akhir:
Gabungkan kedua langkah dengan perkalian aljabar:
```math
\frac{dy}{dx} = 4(x^2 + 1)^3 \cdot (2x)
```
*   **Aturan Perkalian:** Karena operasi perkalian bersifat komutatif, kalikan koefisien/variabel bebas di luar kurung, yaitu $4 \cdot 2x = 8x$.
*   **Hasil Akhir:**
    ```math
    \frac{dy}{dx} = 8x(x^2 + 1)^3
    ```

---

## 💡 Kesimpulan & Aturan Penting Perkalian Aljabar

> ⚠️ **Golden Rule (Aturan Baku):**
> Saat menyelesaikan aturan rantai, **yang dikalikan di akhir hanyalah koefisien atau variabel yang bebas di luar kurung**. 
> 
> Bagian di dalam kurung yang masih memiliki pangkat **TIDAK BOLEH** diganggu gugat atau dikalikan masuk secara langsung, karena operasi pangkat memiliki tingkatan yang lebih tinggi daripada perkalian dalam urutan operasi matematika (*Order of Operations*).

### 📊 Tabel Ringkasan Perbandingan:

| Bentuk Fungsi | Turunan Fungsi Dalam | Proses Perkalian Akhir | Hasil Akhir Turunan |
| :--- | :--- | :--- | :--- |
| **Linear:** $(3x+1)^4$ | $3$ (Konstanta) | $4 \cdot 3$ | $12(3x + 1)^3$ |
| **Kuadrat:** $(x^2+1)^4$ | $2x$ (Variabel) | $4 \cdot 2x$ | $8x(x^2 + 1)^3$ |

