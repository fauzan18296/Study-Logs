# 📐 Dua Persamaan Garis: Menentukan Hubungan Antar Garis

> **Inti konsep:** Memiliki **2 persamaan garis** tidak otomatis berarti kedua garis tersebut sejajar atau tegak lurus.

---

## 1. 🧠 Dua Persamaan ≠ Dua Garis Sejajar

Misalkan kita memiliki:

$$
\begin{cases}
y = 2x + 1\\
y = 3x - 4
\end{cases}
$$

Kita memang memiliki **dua garis**, tetapi belum mengetahui hubungan keduanya.

Cari gradien masing-masing:

$$
m_1 = 2
$$

$$
m_2 = 3
$$

Kemudian bandingkan.

Karena:

$$
m_1 \neq m_2
$$

dan

$$
m_1m_2 = 2(3)=6\neq -1
$$

maka kedua garis **tidak sejajar dan tidak tegak lurus**.

Keduanya hanya **berpotongan**.

---

# 2. 📊 Kemungkinan Hubungan Dua Garis

| Hubungan                | Syarat                               |
| ----------------------- | ------------------------------------ |
| 🟰 **Sejajar** | $m_1=m_2$, tetapi $b_1\neq b_2$ |
| ⟂ **Tegak lurus** | $m_1m_2=-1$ |
| ✕ **Berpotongan biasa** | $m_1\neq m_2$ dan $m_1m_2\neq-1$ |
| 🟰 **Garis yang sama** | $m_1=m_2$ dan $b_1=b_2$ |

> **Catatan:** Dua garis dengan gradien sama tidak selalu merupakan dua garis sejajar yang berbeda. Jika intersepnya juga sama, sebenarnya itu **garis yang sama**.

---

# 3. 🟢 Syarat Garis Sejajar

Dua garis sejajar memiliki **gradien yang sama**:

$$
\boxed{m_1=m_2}
$$

Contoh:

$$
y=2x+1
$$

$$
y=2x+5
$$

Maka:

$$
m_1=2
$$

$$
m_2=2
$$

Sehingga:

$$
\boxed{m_1=m_2}
$$

Keduanya sejajar karena memiliki kemiringan yang sama, tetapi berada pada posisi yang berbeda.

### ⚠️ Jangan salah memahami

Sejajar **bukan berarti nilai \(x\)-nya sama**.

Yang sama adalah **gradiennya**, yaitu perbandingan perubahan \(y\) terhadap perubahan \(x\).

---

# 4. 🔵 Syarat Garis Tegak Lurus

Dua garis tegak lurus memenuhi:

$$
\boxed{m_1m_2=-1}
$$

Sehingga jika \(m_1\) sudah diketahui:

$$
\boxed{m_2=-\frac{1}{m_1}}
$$

### Contoh

Jika:

$$
m_1=2
$$

maka:

$$
m_2=-\frac{1}{2}
$$

Cek:

$$
2\left(-\frac12\right)=-1
$$

Maka kedua garis tegak lurus.

---

# 5. 🟡 Jika \(m_1\) Sudah Ditemukan, Apakah Harus Mencari \(m_2\)?

**Tidak selalu.**

Jangan menggunakan pola berpikir:

> "Saya sudah menemukan \(m_1\), jadi sekarang harus mencari \(m_2\)."

Yang benar:

> **Cari \(m_2\) hanya jika memang ada garis kedua yang perlu dianalisis atau ditentukan.**

### Contoh 1 — Hanya mencari gradien

> Tentukan gradien garis \(y=3x+5\).

Langsung:

$$
m=3
$$

**Selesai.**

Tidak perlu mencari \(m_2\).

---

### Contoh 2 — Mencari garis sejajar

> Tentukan garis yang sejajar dengan \(y=3x+5\).

Karena sejajar:

$$
m_2=m_1
$$

Maka:

$$
m_2=3
$$

---

### Contoh 3 — Mencari garis tegak lurus

> Tentukan garis yang tegak lurus dengan \(y=3x+5\).

Karena tegak lurus:

$$
m_1m_2=-1
$$

$$
3m_2=-1
$$

$$
m_2=-\frac13
$$

---

# 6. 🧭 Cara Berpikir Saat Menemukan Dua Persamaan

Ketika melihat dua persamaan, **jangan langsung menganggap keduanya sejajar atau tegak lurus**.

Gunakan alur berikut:

```text
          Diketahui dua persamaan
                   │
                   ▼
            Apakah keduanya
              garis linear?
                   │
                   ▼
          Cari m₁ dan m₂
                   │
                   ▼
        Apa yang ditanyakan?
                   │
       ┌───────────┼───────────┐
       ▼           ▼           ▼
   Sejajar    Tegak lurus   Hubungan umum
       │           │           │
       ▼           ▼           ▼
   m₁ = m₂    m₁m₂ = -1    Bandingkan m₁,m₂
```

---

# 7. 🔍 Jangan Mengasumsikan Hubungan

Misalnya diberikan:

$$
y=2x+1
$$

$$
y=5x-3
$$

Jangan langsung berkata:

> "Karena ada dua persamaan, berarti saya harus mencari garis sejajar."

❌ Itu asumsi yang tidak diberikan oleh soal.

Yang dapat kita simpulkan hanya:

$$
m_1=2
$$

$$
m_2=5
$$

Kemudian:

$$
m_1\neq m_2
$$

dan:

$$
m_1m_2=10\neq-1
$$

Jadi keduanya **berpotongan biasa**.

---

# 8. 🧩 Perbedaan "Diberikan" dan "Diminta"

Ini sangat penting dalam mengerjakan soal.

### Jika soal mengatakan:

> "Garis \(g_2\) **sejajar** dengan \(g_1\)"

Maka hubungan yang diberikan adalah:

$$
m_2=m_1
$$

---

### Jika soal mengatakan:

> "Garis \(g_2\) **tegak lurus** dengan \(g_1\)"

Maka:

$$
m_1m_2=-1
$$

---

### Jika soal hanya memberikan:

$$
g_1:y=2x+1
$$

$$
g_2:y=3x-4
$$

Maka **belum ada alasan untuk menganggap keduanya sejajar atau tegak lurus**.

Kita perlu melihat apa yang sebenarnya ditanyakan.

---

# 🧠 Inti yang Harus Diingat

> ### **Dua persamaan garis hanya berarti kita memiliki dua garis.**
>
> **Hubungan antara kedua garis harus ditentukan dari informasi atau pertanyaan dalam soal.**

### Rumus utama:

**Sejajar**

$$
\boxed{m_1=m_2}
$$

**Tegak lurus**

$$
\boxed{m_1m_2=-1}
$$

**Berpotongan biasa**

$$
\boxed{m_1\neq m_2 \quad \text{dan} \quad m_1m_2\neq-1}
$$

---

## 🎯 Pola berpikir singkat

```text
Ada 2 persamaan
       ↓
Ada 2 garis?
       ↓
Cari / identifikasi m₁ dan m₂
       ↓
Lihat informasi soal
       ↓
┌──────────────┬─────────────────┐
│ "sejajar"    │ "tegak lurus"   │
│              │                 │
│ m₁ = m₂      │ m₁m₂ = -1       │
└──────────────┴─────────────────┘
```

> **Jangan mencari hubungan yang tidak diminta.**
>
> **Cari hubungan hanya ketika informasi soal memang mengharuskannya.**
