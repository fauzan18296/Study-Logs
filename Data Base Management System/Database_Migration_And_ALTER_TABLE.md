# 📚 Database Migration & ALTER TABLE

## 🎯 Apa Itu Migration?

**Migration** adalah proses mengubah struktur (*schema*) database secara terkontrol dan terdokumentasi.

Contohnya:

* Menambah kolom
* Menghapus kolom
* Mengubah tipe data
* Membuat tabel baru
* Menghapus tabel
* Menambahkan index

---

## 🧠 Kesalahan Umum Pemula

Banyak yang mengira:

```text
Migration = ALTER TABLE
```

Padahal sebenarnya:

```text
Migration = Proses perubahan schema database

ALTER TABLE = Salah satu perintah SQL
yang digunakan dalam migration
```

---

## 🔨 Apa Itu ALTER TABLE?

`ALTER TABLE` adalah perintah SQL yang digunakan untuk mengubah struktur tabel yang sudah ada.

Contoh:

```sql
ALTER TABLE users
ADD COLUMN phone VARCHAR(20);
```

Artinya:

1. Cari tabel `users`
2. Tambahkan kolom baru bernama `phone`
3. Tipe data kolom adalah `VARCHAR(20)`

---

## 📊 Sebelum ALTER TABLE

Struktur tabel:

```text
users
├── id
├── name
└── email
```

Contoh data:

| id | name  | email                                   |
| -- | ----- | --------------------------------------- |
| 1  | Ahmad | [ahmad@mail.com](mailto:ahmad@mail.com) |

---

## 📊 Sesudah ALTER TABLE

Struktur tabel:

```text
users
├── id
├── name
├── email
└── phone
```

Contoh data:

| id | name  | email                                   | phone |
| -- | ----- | --------------------------------------- | ----- |
| 1  | Ahmad | [ahmad@mail.com](mailto:ahmad@mail.com) | NULL  |

---

# ⚖️ ALTER TABLE vs Migration Tool

## 1️⃣ ALTER TABLE Langsung

Menjalankan SQL secara manual:

```sql
ALTER TABLE users
ADD COLUMN phone VARCHAR(20);
```

### ✅ Kelebihan

* Mudah dipahami
* Cepat digunakan
* Tidak memerlukan library tambahan

### ❌ Kekurangan

* Tidak ada riwayat perubahan
* Sulit rollback
* Sulit sinkronisasi tim
* Rentan lupa perubahan yang pernah dilakukan

---

## 2️⃣ Menggunakan Migration Tool

Contoh tool:

* Prisma
* Sequelize
* TypeORM
* Knex

Struktur migration:

```text
001_create_users.sql
002_add_phone.sql
003_create_orders.sql
```

Isi file:

```sql
ALTER TABLE users
ADD COLUMN phone VARCHAR(20);
```

Kemudian migration tool akan:

1. Menjalankan migration
2. Menyimpan histori migration
3. Menandai migration yang sudah dieksekusi
4. Mendukung rollback (tergantung tool)

---

## 📈 Versioning Database

Migration membuat database memiliki versi seperti software.

```text
Migration 001
Create users table

↓

Migration 002
Add phone column

↓

Migration 003
Create products table

↓

Migration 004
Create orders table
```

Setiap perubahan tercatat sehingga database dapat berkembang secara terstruktur.

---

# 🛠 Perintah SQL yang Sering Digunakan Dalam Migration

## Membuat Tabel

```sql
CREATE TABLE products (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

---

## Menambah Kolom

```sql
ALTER TABLE users
ADD COLUMN phone VARCHAR(20);
```

---

## Mengubah Tipe Data

```sql
ALTER TABLE users
MODIFY COLUMN phone VARCHAR(30);
```

---

## Menghapus Kolom

```sql
ALTER TABLE users
DROP COLUMN phone;
```

---

## Menghapus Tabel

```sql
DROP TABLE logs;
```

---

## Menambahkan Index

```sql
CREATE INDEX idx_email
ON users(email);
```

---

# 🏗️ Analogi Sederhana

Bayangkan database adalah sebuah rumah.

```text
Database = Rumah

Migration = Proses renovasi rumah

ALTER TABLE = Alat tukang
(Cangkul, Palu, Gergaji, Obeng)
```

Saat melakukan renovasi (migration), kita menggunakan berbagai alat SQL seperti:

* ALTER TABLE
* CREATE TABLE
* DROP TABLE
* CREATE INDEX

---

# 🎯 Kesimpulan

```text
Migration
=
Proses perubahan schema database
yang terstruktur dan memiliki histori.

ALTER TABLE
=
Salah satu perintah SQL yang sering
digunakan dalam migration.
```

Jadi perintah berikut:

```sql
ALTER TABLE users
ADD COLUMN phone VARCHAR(20);
```

✅ Merupakan bagian dari migration

❌ Bukan migration itu sendiri

Migration adalah keseluruhan proses pengelolaan perubahan schema database beserta histori, versi, dan rollback-nya.

