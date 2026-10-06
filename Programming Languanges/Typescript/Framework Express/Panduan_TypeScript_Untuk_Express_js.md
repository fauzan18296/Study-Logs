# 🚀 Panduan TypeScript untuk Express.js

## 📌 Apakah Bisa Menggunakan TypeScript Tanpa Menulis File JavaScript?

Ya, bisa.

Sebagai developer, kita hanya menulis file:

```text
app.ts
```

Contoh:

```ts
function greet(name: string): string {
    return `Halo ${name}`;
}

console.log(greet("Fauzan"));
```

Ketika dijalankan, TypeScript akan mengubahnya menjadi JavaScript secara otomatis.

```text
TypeScript (.ts)
        ↓
   Transpile
        ↓
 JavaScript (.js)
        ↓
 Node.js / Browser
```

> Walaupun kita tidak menulis file JavaScript secara manual, JavaScript tetap dibuat dan dijalankan di balik layar.

---

# 📌 Menjalankan TypeScript Tanpa Membuat File `.js`

## Menggunakan TSX

Install:

```bash
npm install -D typescript tsx
```

Jalankan:

```bash
npx tsx app.ts
```

atau jika sudah global:

```bash
tsx app.ts
```

TSX akan:

* Membaca file `.ts`
* Mengubahnya sementara menjadi JavaScript
* Langsung menjalankannya

Tanpa membuat file `.js` permanen.

---

# 📌 Apa Itu TSX?

Banyak pemula mengira TSX hanya ekstensi file React.

Sebenarnya ada **dua TSX yang berbeda**.

## 1. TSX (Ekstensi File)

Contoh:

```text
App.tsx
```

Artinya:

```text
TypeScript + JSX
```

Biasanya digunakan pada React.

Contoh:

```tsx
type Props = {
    name: string;
};

function Greeting({ name }: Props) {
    return <h1>Hello {name}</h1>;
}
```

---

## 2. TSX (Tool NPM)

Contoh:

```bash
tsx src/index.ts
```

Ini adalah runtime yang digunakan untuk menjalankan TypeScript secara langsung.

Fungsinya mirip:

```bash
node app.js
```

tetapi untuk TypeScript:

```bash
tsx app.ts
```

---

# 📌 JSX vs TSX

## JSX

JSX = JavaScript XML

Contoh:

```jsx
function App() {
    return <h1>Hello World</h1>;
}
```

File:

```text
App.jsx
```

---

## TSX

TSX = TypeScript + JSX

Contoh:

```tsx
function App(): JSX.Element {
    return <h1>Hello World</h1>;
}
```

File:

```text
App.tsx
```

---

## Perbandingan

| JSX                     | TSX               |
| ----------------------- | ----------------- |
| JavaScript + JSX        | TypeScript + JSX  |
| `.jsx`                  | `.tsx`            |
| Tidak ada type checking | Ada type checking |
| Cocok React JS          | Cocok React TS    |

---

# 📌 Apakah TSX Bisa Diinstal Global?

Bisa.

Install:

```bash
npm install -g tsx
```

Cek versi:

```bash
tsx --version
```

Setelah itu:

```bash
tsx app.ts
```

bisa dijalankan dari mana saja.

---

# 📌 Global vs Local Installation

## Global

```bash
npm install -g tsx
```

### Kelebihan

* Praktis
* Bisa dipakai di semua project
* Tidak perlu `npx`

### Kekurangan

* Versi bisa berbeda antar project
* Kurang ideal untuk kolaborasi tim

---

## Local (Direkomendasikan)

```bash
npm install -D tsx typescript
```

Tambahkan script:

```json
{
  "scripts": {
    "dev": "tsx src/index.ts"
  }
}
```

Jalankan:

```bash
npm run dev
```

### Kelebihan

* Konsisten untuk semua developer
* Lebih profesional
* Mudah direproduksi

---

# 📌 TS-Node vs TSX

## TS-Node

Install:

```bash
npm install -D ts-node typescript
```

Jalankan:

```bash
npx ts-node src/server.ts
```

Contoh script:

```json
{
  "scripts": {
    "dev": "ts-node src/server.ts"
  }
}
```

---

## TSX

Install:

```bash
npm install -D tsx typescript
```

Jalankan:

```bash
npx tsx src/server.ts
```

atau:

```bash
npx tsx watch src/server.ts
```

---

# 📌 Mengapa Banyak Project Modern Beralih ke TSX?

TS-Node sering membutuhkan konfigurasi tambahan.

Contoh error yang cukup sering ditemui:

```text
Cannot use import statement outside a module
```

atau

```text
ERR_UNKNOWN_FILE_EXTENSION ".ts"
```

terutama ketika menggunakan ESM.

---

TSX biasanya lebih sederhana:

```bash
tsx src/server.ts
```

langsung berjalan tanpa konfigurasi tambahan yang rumit.

Karena alasan ini, banyak starter template modern menggunakan TSX sebagai development runtime.

---

# 📌 Setup Express.js + TypeScript Modern

## Instalasi

```bash
npm install express
npm install -D typescript tsx @types/express
```

---

## Struktur Folder

```text
project/
│
├── src/
│   └── server.ts
│
├── package.json
├── tsconfig.json
└── node_modules/
```

---

## server.ts

```ts
import express from "express";

const app = express();

app.get("/", (req, res) => {
    res.send("Hello TypeScript");
});

app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

---

## package.json

```json
{
  "scripts": {
    "dev": "tsx watch src/server.ts",
    "build": "tsc",
    "start": "node dist/server.js"
  }
}
```

---

# 📌 Alur Development dan Production

## Development

```bash
npm run dev
```

Alur:

```text
TypeScript
     ↓
   TSX
     ↓
  Running
```

---

## Production

Build:

```bash
npm run build
```

Menjalankan hasil build:

```bash
npm start
```

Alur:

```text
TypeScript
     ↓
    TSC
     ↓
JavaScript
     ↓
   Node.js
```

---

# 🎯 Kesimpulan

## Saat Belajar

Gunakan:

```bash
tsx watch src/server.ts
```

karena:

* Setup lebih sederhana
* Cepat
* Cocok untuk pemula
* Minim error konfigurasi

---

## Saat Project Production

Gunakan:

```text
Development:
TSX

Build:
TSC

Production:
Node.js
```

Karena server production pada akhirnya tetap menjalankan JavaScript hasil build TypeScript.
