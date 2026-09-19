# 📐 Hubungan `f(x)`, `y`, dan Gradien pada Persamaan Linear

> [!NOTE]
> **Inti konsep:** `y` dan `f(x)` sama-sama dapat merepresentasikan **nilai output**.
> Saat mencari gradien, kita sering menggunakan `y` karena bentuk umum persamaan garis ditulis sebagai:
>
> $$
> y = mx + b
> $$

---

## 1. Apa itu `x` dan `y`?

Pada persamaan:

$$
y = mx + b
$$

kita dapat memahami:

| Simbol | Peran                     | Contoh                  |
| :----: | ------------------------- | ----------------------- |
|   `x`  | Input / variabel bebas    | Jumlah jam              |
|   `y`  | Output / variabel terikat | Total biaya             |
|   `m`  | Gradien                   | Perubahan biaya per jam |
|   `b`  | Intercept / konstanta     | Biaya ketika `x = 0`    |

Jadi misalnya:

$$
y = 3x + 5
$$

artinya:

* `x` = jumlah jam
* `y` = total biaya
* `3` = biaya bertambah $3 setiap tambahan 1 jam
* `5` = biaya awal ketika jam = 0

---

# 2. Lalu apa hubungannya dengan `f(x)`?

Fungsi linear juga bisa ditulis:

$$
f(x) = mx + b
$$

Contohnya:

$$
f(x) = 3x + 5
$$

Secara konsep:

$$
\boxed{f(x)=y}
$$

Sehingga:

$$
f(x)=3x+5
$$

dapat ditulis menjadi:

$$
y=3x+5
$$

### Jadi `f(x)` bukan berubah menjadi `y`

Lebih tepatnya:

> **`f(x)` dan `y` digunakan untuk merepresentasikan nilai output yang sama.**

Contoh:

$$
f(10)=3(10)+5
$$

$$
f(10)=35
$$

Karena:

$$
y=f(x)
$$

maka ketika:

$$
x=10
$$

kita juga dapat mengatakan:

$$
y=35
$$

---

# 3. Kenapa saat mencari gradien menggunakan `y`?

Karena gradien mengukur:

> **seberapa besar perubahan output dibandingkan perubahan input.**

Output direpresentasikan oleh `y`, sedangkan input direpresentasikan oleh `x`.

Maka:

$$
\boxed{m=\frac{\Delta y}{\Delta x}}
$$

atau:

$$
\boxed{m=\frac{y_2-y_1}{x_2-x_1}}
$$

Dengan kata lain:

```text
       perubahan output
m = -----------------------
       perubahan input

       perubahan y
m = ----------------
       perubahan x
```

---

# 4. Contoh dengan fungsi biaya

Misalkan:

* 10 jam → biaya $45
* 25 jam → biaya $87

Kita mempunyai dua titik:

$$
(x_1,y_1)=(10,45)
$$

$$
(x_2,y_2)=(25,87)
$$

Perhatikan bahwa:

```text
x → jam penggunaan
y → total biaya
```

Maka gradien:

$$
m=\frac{y_2-y_1}{x_2-x_1}
$$

$$
m=\frac{87-45}{25-10}
$$

$$
m=\frac{42}{15}
$$

$$
\boxed{m=2.8}
$$

Artinya:

> Setiap tambahan **1 jam penggunaan**, biaya bertambah sekitar **$2.80**.

---

# 5. Kenapa tidak menggunakan `f(x)` langsung?

Sebenarnya **boleh**.

Karena:

$$
y=f(x)
$$

maka secara konsep kita juga dapat menulis:

$$
m=
\frac{f(x_2)-f(x_1)}
{x_2-x_1}
$$

Misalnya:

$$
f(x_1)=45
$$

dan:

$$
f(x_2)=87
$$

maka:

$$
m=
\frac{f(25)-f(10)}
{25-10}
$$

$$
m=
\frac{87-45}{25-10}
$$

$$
m=2.8
$$

Hasilnya tetap sama.

Jadi penggunaan `y` hanyalah **notasi yang lebih sederhana dan umum ketika membahas garis dan gradien**.

---

# 6. Hubungan seluruh simbol

Cara paling mudah mengingatnya:

```text
                 Fungsi
                   │
                   ▼
              f(x) = mx + b
                   │
                   │ f(x) = y
                   ▼
               y = mx + b
                   │
          ┌────────┴────────┐
          ▼                 ▼
          x                 y
       Input              Output
          │                 │
          └───────┬─────────┘
                  ▼
              Gradien
                  │
                  ▼
          Δy
      m = ────
          Δx
```

---

# 🧠 7. Cara berpikir yang paling penting

Jangan menghafal:

> "`f(x)` berubah menjadi `y`."

Lebih tepat pahami:

> **`f(x)` adalah nilai output dari fungsi ketika diberikan input `x`, dan nilai output tersebut dapat kita beri nama `y`.**

Sehingga:

$$
\boxed{y=f(x)}
$$

Kemudian untuk garis linear:

$$
\boxed{y=mx+b}
$$

Dan karena gradien mengukur perubahan `y` terhadap perubahan `x`:

$$
\boxed{m=\frac{\Delta y}{\Delta x}}
$$

---

## 🔑 Ringkasan

| Konsep      | Makna                                             |
| ----------- | ------------------------------------------------- |
| `x`         | Input / variabel bebas                            |
| `f(x)`      | Output fungsi pada input `x`                      |
| `y`         | Nama lain untuk output                            |
| `m`         | Gradien / laju perubahan                          |
| `b`         | Intercept / nilai `y` ketika `x = 0`              |
| `y = f(x)`  | Output fungsi dapat direpresentasikan sebagai `y` |
| `m = Δy/Δx` | Gradien = perubahan output ÷ perubahan input      |

### ⭐ Rumus utama

$$
\boxed{f(x)=y}
$$

$$
\boxed{y=mx+b}
$$

$$
\boxed{m=\frac{y_2-y_1}{x_2-x_1}}
$$

> **Inti akhirnya:**
> `x` menunjukkan **input**, `y` menunjukkan **output**, dan `m` menunjukkan **seberapa cepat output berubah ketika input berubah**.
