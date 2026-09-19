# 📐 Menentukan Gradien Garis Kedua (m₂)

## Dari Gradien Pertama (m₁) ke Hubungan Garis

> **Inti konsep:** Mengetahui \(m_1\) saja **belum cukup** untuk menentukan \(m_2\).
>
> Kita harus mengetahui **hubungan antara kedua garis**: apakah **sejajar** atau **tegak lurus**.

---

## 1. 🔹 Bentuk Umum Persamaan Garis

Persamaan garis lurus umumnya ditulis:

$$
y = mx + b
$$

Keterangan:

| Simbol | Arti                     |
| ------ | ------------------------ |
| \(y\)  | variabel terikat         |
| \(x\)  | variabel                 |
| \(m\)  | **gradien**              |
| \(b\)  | **intersep sumbu-\(y\)** |

Yang perlu diingat:

$$
\boxed{m = \text{koefisien dari }x}
$$

Contoh:

$$
y = 4x + 7
$$

maka:

$$
m=4
$$

dan:

$$
b=7
$$

---

# 2. 🔍 Menemukan \(m_1\)

Jika persamaan pertama sudah berbentuk:

$$
y=m_1x+b_1
$$

maka \(m_1\) adalah koefisien \(x\).

Misalnya:

$$
y=3x+5
$$

maka:

$$
\boxed{m_1=3}
$$

---

# 3. ⚠️ Apakah \(m_1\) Saja Bisa Menentukan \(m_2\)?

**Tidak.**

Misalnya kita sudah mengetahui:

$$
m_1=3
$$

Kita belum bisa langsung mengatakan:

$$
m_2=?
$$

Karena kita belum tahu hubungan antara garis pertama dan garis kedua.

Kita membutuhkan informasi seperti:

* garis kedua **sejajar**, atau
* garis kedua **tegak lurus**.

---

# 4. 🟦 Jika Garis Kedua Sejajar

Dua garis dikatakan **sejajar** jika memiliki gradien yang sama.

$$
\boxed{m_2=m_1}
$$

Misalnya:

$$
m_1=3
$$

Karena garis kedua sejajar:

$$
m_2=m_1
$$

maka:

$$
\boxed{m_2=3}
$$

### Bagaimana dengan \(b\)?

Intersep **boleh berbeda**.

Contoh:

$$
y=3x+2
$$

dan:

$$
y=3x+8
$$

Keduanya memiliki:

$$
m_1=m_2=3
$$

tetapi:

$$
b_1=2
$$

dan:

$$
b_2=8
$$

Jadi keduanya memiliki **kemiringan yang sama**, tetapi berada pada posisi yang berbeda.

> 💡 **Sejajar → gradien sama.**

---

# 5. 🟥 Jika Garis Kedua Tegak Lurus

Jika dua garis saling tegak lurus, gradiennya merupakan **negatif kebalikan**.

Rumus:

$$
\boxed{m_2=-\frac{1}{m_1}}
$$

Misalnya:

$$
m_1=4
$$

Maka:

$$
m_2=-\frac{1}{4}
$$

Jadi:

$$
\boxed{m_2=-\frac14}
$$

### 🔄 Apa maksud "negatif kebalikan"?

Ada dua langkah:

**Langkah 1 — Ambil kebalikan**

$$
4 \rightarrow \frac14
$$

**Langkah 2 — Berikan tanda negatif**

$$
\frac14\rightarrow-\frac14
$$

Sehingga:

$$
\boxed{4\rightarrow-\frac14}
$$

> 💡 **Tegak lurus → gradien = negatif kebalikan.**

---

# 6. 🧠 Alur Berpikir yang Benar

Jika sudah menemukan \(m_1\), jangan langsung mencari \(m_2\).

Gunakan alur:

```text
Cari m₁
  ↓
Baca hubungan kedua garis
  ↓
 ┌──────────────────────┐
 │                      │
Sejajar             Tegak lurus
 │                      │
 ↓                      ↓
m₂ = m₁             m₂ = -1/m₁
 │                      │
 ↓                      ↓
Dapat m₂             Dapat m₂
```

---

# 7. 📌 Ringkasan Rumus

| Hubungan garis | Hubungan gradien               |
| -------------- | ------------------------------ |
| 🟦 Sejajar | $\boxed{m_2=m_1}$ |
| 🟥 Tegak lurus | $\boxed{m_2=-\frac{1}{m_1}}$ |

---

# 8. ⚠️ Hal yang Sering Salah

### ❌ Salah 1 — Menganggap \(m_2\) selalu bisa dicari dari \(m_1\)

Mengetahui:

$$
m_1=5
$$

tidak otomatis berarti kita tahu \(m_2\).

Harus ada informasi tentang hubungan kedua garis.

---

### ❌ Salah 2 — Menganggap garis sejajar harus mempunyai \(b\) yang sama

Tidak benar.

Yang harus sama adalah:

$$
\boxed{m_1=m_2}
$$

Sedangkan:

$$
b_1\neq b_2
$$

masih memungkinkan.

---

### ❌ Salah 3 — Menganggap "tegak lurus" berarti tandanya saja yang dibalik

Misalnya:

$$
m_1=2
$$

Bukan:

$$
m_2=-2
$$

Tetapi:

$$
\boxed{m_2=-\frac12}
$$

Karena harus mengambil **negatif kebalikan**, bukan sekadar mengganti tanda.

---

# 9. 🎯 Cara Cepat Mengingat

### Garis sejajar

> **Kemiringan sama → gradien sama**

$$
\boxed{m_2=m_1}
$$

### Garis tegak lurus

> **Kemiringan saling negatif kebalikan**

$$
\boxed{m_2=-\frac1{m_1}}
$$

---

## ⭐ Kesimpulan Utama

Jika sudah menemukan \(m_1\), **jangan langsung menentukan \(m_2\)**.

Pertama tanyakan:

> **"Apa hubungan garis pertama dan garis kedua?"**

Kemudian:

$$
\boxed{
\begin{cases}
m_2=m_1 & \text{jika sejajar}\\[4pt]
m_2=-\frac1{m_1} & \text{jika tegak lurus}
\end{cases}}
$$

Jadi, **\(m_1\) adalah informasi awal**, sedangkan **hubungan kedua garis menentukan bagaimana kita mendapatkan \(m_2\)**.
