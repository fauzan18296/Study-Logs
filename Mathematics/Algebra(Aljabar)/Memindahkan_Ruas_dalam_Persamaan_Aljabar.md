# 📐 Memindahkan Ruas dalam Persamaan Aljabar

### Memahami kenapa tanda berubah ketika variabel atau konstanta dipindahkan

---

> 💡 **Ide utama**
>
> Dalam aljabar, sebenarnya kita **tidak benar-benar memindahkan sesuatu secara sembarangan**.
>
> Yang kita lakukan adalah **melakukan operasi yang sama pada kedua ruas** agar persamaan tetap setara.

---

## ⚖️ 1. Persamaan seperti timbangan

Misalnya:

$$
120 = 2.8x + 17
$$

Tanda `=` berarti kedua ruas memiliki **nilai yang sama**.

```text
        RUAS KIRI       =       RUAS KANAN

           120          =       2.8x + 17
```

Karena keduanya seimbang, kita tidak boleh mengubah hanya satu ruas tanpa memperhitungkan ruas lainnya.

---

# 🔄 2. Apa yang dimaksud "memindahkan ruas"?

Misalnya:

$$
120 = 2.8x + 17
$$

Kita ingin menghilangkan `+17` dari ruas kanan.

Cara yang sebenarnya:

$$
120 - 17 = 2.8x + 17 - 17
$$

Sehingga:

$$
103 = 2.8x
$$

Secara singkat, kita sering menulis:

$$
120 = 2.8x + 17
$$

$$
120 - 17 = 2.8x
$$

Lalu mengatakan:

> **"17 dipindahkan ke kiri dan tandanya berubah menjadi -17."**

⚠️ Tetapi ini hanyalah **cara singkat**.

Konsep sebenarnya adalah:

$$
\boxed{\text{Mengurangi kedua ruas dengan }17}
$$

---

# 🧠 3. Kenapa tandanya terlihat berubah?

Perhatikan:

$$
120 = 2.8x + 17
$$

Kita melakukan `-17` pada **kedua ruas**:

$$
120 - 17 = 2.8x + 17 - 17
$$

Di ruas kanan:

$$
+17 - 17 = 0
$$

Maka tersisa:

$$
103 = 2.8x
$$

Jadi bukan karena ada aturan ajaib bahwa:

> ❌ `+17` kalau pindah pasti menjadi `-17`.

Melainkan karena kita menggunakan **operasi invers** untuk menghilangkan `+17`.

---

# 🔢 4. Contoh mencari nilai \(x\)

Misalkan:

$$
120 = 2.8x + 17
$$

### Langkah 1 — Hilangkan \(+17\)

$$
120 - 17 = 2.8x
$$

$$
103 = 2.8x
$$

### Langkah 2 — Hilangkan perkalian \(2.8\)

Karena:

$$
2.8x = 2.8 \times x
$$

maka kita bagi kedua ruas dengan \(2.8\):

$$
\frac{103}{2.8} = \frac{2.8x}{2.8}
$$

Sehingga:

$$
x \approx 36.79
$$

Jadi:

$$
\boxed{x \approx 36.79\text{ jam}}
$$

---

# 🔁 5. Prinsip operasi invers

| Operasi      | Operasi untuk membatalkan |
| ------------ | ------------------------- |
| \(+a\)       | \(-a\)                    |
| \(-a\)       | \(+a\)                    |
| \(\times a\) | \(\div a\)                |
| \(\div a\)   | \(\times a\)              |

Contoh:

### Penjumlahan

$$
x + 5 = 12
$$

Kurangi kedua ruas dengan 5:

$$
x + 5 - 5 = 12 - 5
$$

$$
x = 7
$$

### Perkalian

$$
3x = 12
$$

Bagi kedua ruas dengan 3:

$$
\frac{3x}{3} = \frac{12}{3}
$$

$$
x = 4
$$

---

# 🚨 6. Kesalahan konsep yang perlu dihindari

Jangan memahami aljabar sebagai:

> ❌ **"Kalau pindah ruas, tandanya berubah."**

Lebih baik pahami sebagai:

> ✅ **"Saya melakukan operasi invers pada kedua ruas untuk mempertahankan kesetaraan persamaan."**

Aturan **"pindah ruas → tanda berubah"** memang berguna sebagai **shortcut**, tetapi kalau hanya menghafalnya, kamu bisa bingung ketika persamaan menjadi lebih kompleks.

---

# 🎯 7. Hubungannya dengan fungsi biaya

Misalnya:

$$
f(x) = 2.8x + 17
$$

dan kamu memiliki anggaran:

$$
f(x) = 120
$$

Maka:

$$
120 = 2.8x + 17
$$

Kita mencari \(x\):

$$
120 - 17 = 2.8x
$$

$$
103 = 2.8x
$$

$$
x = \frac{103}{2.8}
$$

$$
\boxed{x \approx 36.79}
$$

Artinya, berdasarkan fungsi tersebut, **anggaran $120 menghasilkan sekitar 36,79 jam penggunaan**.

---

# 🧩 Ringkasan

```text
              PERSAMAAN
                  │
                  ▼
       Kedua ruas harus tetap
          setara / seimbang
                  │
                  ▼
     ┌─────────────────────────┐
     │ Lakukan operasi yang    │
     │ sama pada kedua ruas    │
     └─────────────────────────┘
                  │
                  ▼
          Gunakan operasi invers
                  │
          ┌───────┴────────┐
          ▼                ▼
        + ↔ −            × ↔ ÷
          │                │
          └───────┬────────┘
                  ▼
            Cari variabel
```

### 🧠 Kalimat kunci

> **"Memindahkan ruas" hanyalah cara singkat untuk menjelaskan operasi invers yang dilakukan pada kedua ruas persamaan.**
>
> Tujuan akhirnya adalah **mengisolasi variabel tanpa mengubah kesetaraan persamaan**.
