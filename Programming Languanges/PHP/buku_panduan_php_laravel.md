# 📘 BUKU PANDUAN PENGEMBANGAN WEB: PHP & LARAVEL
> **Edisi Komprehensif:** Dari Konsep Dasar, Pemrograman Berbasis Objek (OOP), Arsitektur Framework, Hingga Implementasi Praktis Aplikasi CRUD.

---

## 📋 DAFTAR ISI

* [📖 BAB 1: Pengenalan & Dasar-Dasar PHP](#-bab-1-pengenalan--dasar-dasar-php)
  * [1.1 Apa itu PHP & Cara Kerjanya](#11-apa-itu-php--cara-kerjanya)
  * [1.2 Syntax Dasar & Tipe Data](#12-syntax-dasar--tipe-data)
  * [1.3 Control Flow (Percabangan & Perulangan)](#13-control-flow-percabangan--perulangan)
  * [1.4 Fungsi & Scope Variabel](#14-fungsi--scope-variabel)
* [🧩 BAB 2: Pemrograman Berbasis Objek (OOP) PHP](#-bab-2-pemrograman-berbasis-objek-oop-php)
  * [2.1 Class & Object](#21-class--object)
  * [2.2 Tiga Pilar Utama OOP](#22-tiga-pilar-utama-oop)
  * [2.3 Interface vs Abstract Class](#23-interface-vs-abstract-class)
  * [2.4 Trait & Namespace](#24-trait--namespace)
* [🏗️ BAB 3: Core Concepts Laravel Framework](#️-bab-3-core-concepts-laravel-framework)
  * [3.1 Arsitektur Model-View-Controller (MVC)](#31-arsitektur-model-view-controller-mvc)
  * [3.2 Service Container & Dependency Injection](#32-service-container--dependency-injection)
  * [3.3 Service Providers](#33-service-providers)
  * [3.4 Request Lifecycle & Middleware](#34-request-lifecycle--middleware)
* [⚙️ BAB 4: Komponen Utama Laravel](#️-bab-4-komponen-utama-laravel)
  * [4.1 Routing & Controller](#41-routing--controller)
  * [4.2 Blade Templating Engine](#42-blade-templating-engine)
  * [4.3 Database Tools: Migration, Seeder, & Factory](#43-database-tools-migration-seeder--factory)
  * [4.4 Eloquent ORM & Relasi Antar Tabel](#44-eloquent-orm--relasi-antar-tabel)
* [🚀 BAB 5: Penerapan Praktis - Aplikasi CRUD Produk](#-bab-5-penerapan-praktis---aplikasi-crud-produk)
  * [5.1 Persiapan Project & Konfigurasi](#51-persiapan-project--konfigurasi)
  * [5.2 Migration & Model](#52-migration--model)
  * [5.3 Controller & Validasi](#53-controller--validasi)
  * [5.4 Integrasi View Blade](#54-integrasi-view-blade)
* [💡 Penutup & Best Practices](#-penutup--best-practices)

---

## 📖 BAB 1: Pengenalan & Dasar-Dasar PHP

### 1.1 Apa itu PHP & Cara Kerjanya

**PHP** (*PHP: Hypertext Preprocessor*) adalah bahasa pemrograman *scripting* di sisi server (*server-side*) yang bersifat *open-source*. PHP dirancang khusus untuk pengembangan web dan dapat disisipkan langsung ke dalam kode HTML.

> 💡 **CARA KERJA PHP:**
> 1. Browser mengirimkan permintaan (*HTTP Request*) untuk halaman `.php` ke Web Server.
> 2. Web Server (Apache/Nginx) meneruskan permintaan ke modul PHP.
> 3. PHP mengeksekusi kode, memproses logika bisnis, dan berkomunikasi dengan database.
> 4. PHP menghasilkan output berupa teks **HTML/CSS/JS murni** dan mengembalikannya ke Web Server.
> 5. Web Server mengirimkan HTML tersebut ke browser pengakses. *Browser tidak pernah melihat kode PHP aslinya.*

#### Fungsi Utama PHP:
* **Pengolahan Form:** Menerima, memvalidasi, dan mengolah data input dari pengguna.
* **Manajemen Sesi & Keamanan:** Mengelola *cookie* dan *session* untuk sistem login pengguna.
* **Interaksi Database:** Menyimpan, mengambil, mengubah, dan menghapus data pada database (MySQL, PostgreSQL, dsb).
* **Generasi Konten Dinamis:** Membuat halaman web yang menyesuaikan kontennya berdasarkan data real-time.

---

### 1.2 Syntax Dasar & Tipe Data

Setiap script PHP harus diawali dengan tag `<?php` dan ditutup dengan `?>` (tag penutup wajib diabaikan jika file hanya berisi kode PHP murni untuk mencegah isu header).

#### Aturan Variabel
* Variabel diawali dengan tanda dollar (`$`).
* bersifat *case-sensitive* (`$nama` dan `$Nama` adalah dua variabel berbeda).
* Nama variabel harus dimulai dengan huruf atau garis bawah (`_`), tidak boleh diawali angka.

#### Tipe Data Utama:
| Tipe Data | Deskripsi | Contoh |
| :--- | :--- | :--- |
| `String` | Teks | `"Budi Santoso"` |
| `Integer` | Angka Bulat | `25`, `-10` |
| `Float` | Angka Desimal | `3.14`, `85.5` |
| `Boolean` | Nilai Kebenaran | `true` atau `false` |
| `Array` | Kumpulan Nilai | `["Apel", "Jeruk"]` |
| `NULL` | Variabel tanpa nilai | `null` |

```php
<?php
// Deklarasi Variabel
$nama      = "Budi Santoso";                  // String
$umur      = 25;                             // Integer
$ipk       = 3.75;                           // Float
$isStudent = true;                           // Boolean
$hobi      = ["Membaca", "Koding", "Musik"]; // Array Indexed

// Array Asosiatif (Key => Value)
$mahasiswa = [
    "nim"     => "123456",
    "jurusan" => "Teknik Informatika"
];

// Output Data
echo "Nama: " . $nama . "<br>";
echo "Status: " . ($isStudent ? 'Aktif' : 'Tidak Aktif') . "<br>";
echo "Hobi Utama: " . $hobi[0] . "<br>";
echo "Jurusan: " . $mahasiswa["jurusan"];
```

---

### 1.3 Control Flow (Percabangan & Perulangan)

Control flow menentukan alur eksekusi program berdasarkan kondisi atau perulangan tertentu.

#### 🔀 Percabangan (`if`, `elseif`, `else`, `switch`)

```php
<?php
$nilai = 80;

// Percabangan IF-ELSEIF-ELSE
if ($nilai >= 85) {
    echo "Predikat: A (Sangat Memuaskan)";
} elseif ($nilai >= 70) {
    echo "Predikat: B (Memuaskan)";
} else {
    echo "Predikat: C (Cukup)";
}

// Percabangan SWITCH-CASE
$peran = "admin";
switch ($peran) {
    case "admin":
        echo "Akses Penuh Sistem";
        break;
    case "editor":
        echo "Akses Edit Konten";
        break;
    default:
        echo "Akses Tamu Terbatas";
}
```

#### 🔁 Perulangan (`for`, `while`, `foreach`)

`foreach` adalah fitur perulangan yang dirancang khusus untuk memproses elemen-elemen pada *Array*.

```php
<?php
// Perulangan FOR
for ($i = 1; $i <= 3; $i++) {
    echo "Proses Log Ke-{$i}<br>";
}

// Perulangan FOREACH
$produk = [
    ["nama" => "Laptop", "harga" => 8000000],
    ["nama" => "Mouse",  "harga" => 150000]
];

foreach ($produk as $item) {
    echo "Barang: " . $item["nama"] . " - Harga: Rp " . number_format($item["harga"]) . "<br>";
}
```

---

### 1.4 Fungsi & Scope Variabel

Fungsi (*Function*) adalah blok kode yang terisolasi dan dirancang untuk menjalankan tugas tertentu agar kode dapat digunakan kembali (*reusable*).

#### Scope Variabel
* **Local Scope:** Variabel yang dideklarasikan di dalam fungsi hanya hidup dan dapat diakses di dalam fungsi tersebut.
* **Global Scope:** Variabel yang dideklarasikan di luar fungsi. Untuk menggunakannya di dalam fungsi, harus menggunakan kata kunci `global`.

#### Type Hinting & Return Type
PHP modern mendukung deklarasi tipe data pada parameter dan nilai kembalian (*return type*) untuk menjamin keakuratan tipe data.

```php
<?php
$tarifPajak = 0.11; // Variabel Global

function hitungTotalPembayaran(float $hargaBase, int $jumlah): float 
{
    global $tarifPajak; // Mengakses variabel global
    
    $subtotal = $hargaBase * $jumlah;
    $total    = $subtotal + ($subtotal * $tarifPajak);
    
    return $total;
}

$total = hitungTotalPembayaran(100000.0, 2);
echo "Total Bayar: Rp " . number_format($total, 0, ',', '.');
```

---

## 🧩 BAB 2: Pemrograman Berbasis Objek (OOP) PHP

Object-Oriented Programming (OOP) adalah paradigma pemrograman berbasis "objek" yang memisahkan program ke dalam modul-modul yang saling berhubungan.

### 2.1 Class & Object

> 📌 **ANALOGI PERBEDAAN:**
> * **Class:** Cetak biru / Denah arsitektur rumah.
> * **Object:** Rumah fisik asli yang dibangun berdasarkan denah tersebut.
> * **Property:** Ciri khas fisik rumah (warna cat, jumlah kamar).
> * **Method:** Aktivitas yang bisa dilakukan di rumah (menyalakan lampu, membuka pintu).

```php
<?php
class Mobil 
{
    // Property
    public string $merk;
    public string $warna;

    // Constructor: Dipanggil otomatis saat objek dibuat (instansiasi)
    public function __construct(string $merk, string $warna) 
    {
        $this->merk  = $merk;
        $this->warna = $warna;
    }

    // Method
    public function jalankan(): string 
    {
        return "Mobil {$this->merk} berwarna {$this->warna} sedang melaju.";
    }
}

// Instansiasi Objek
$mobilSaya = new Mobil("Toyota", "Hitam");
echo $mobilSaya->jalankan();
```

---

### 2.2 Tiga Pilar Utama OOP

```
 ┌─────────────────────────────────────────────────────────────┐
 │                       PILAR UTAMA OOP                       │
 ├──────────────────┬───────────────────────┬──────────────────┤
 │  Encapsulation   │      Inheritance      │   Polymorphism   │
 │ (Pembungkusan)   │      (Pewarisan)      │ (Banyak Bentuk)  │
 └──────────────────┴───────────────────────┴──────────────────┘
```

#### 🛡️ 1. Encapsulation (Penyembunyian Data)
Membatasi akses langsung ke property/method internal untuk melindungi integritas data. Diatur menggunakan *Visibility Modifiers*:
* `public`: Dapat diakses dari mana saja.
* `protected`: Hanya dapat diakses di dalam class itu sendiri dan class turunannya (*child class*).
* `private`: Hanya dapat diakses dari dalam class itu sendiri secara internal.

#### 🧬 2. Inheritance (Pewarisan)
Kemampuan sebuah *Child Class* untuk mewarisi property dan method dari *Parent Class* menggunakan kata kunci `extends`.

#### 🎭 3. Polymorphism (Banyak Bentuk)
Kemampuan class turunan untuk mengubah atau menyesuaikan (*override*) implementasi method yang diwarisi dari parent class.

```php
<?php
// Parent Class
class Kendaraan 
{
    protected string $nama; // Protected: hanya internal & child class

    public function __construct(string $nama) 
    {
        $this->nama = $nama;
    }

    public function klakson(): string 
    {
        return "Bunyi klakson standar.";
    }
}

// Child Class (Inheritance)
class Motor extends Kendaraan 
{
    // Polymorphism: Method Overriding
    public function klakson(): string 
    {
        return "Tin tin! Motor {$this->nama} melintas.";
    }
}

$motor = new Motor("Honda");
echo $motor->klakson(); // Output: Tin tin! Motor Honda melintas.
```

---

### 2.3 Interface vs Abstract Class

Keduanya digunakan untuk memprioritaskan abstraksi dan standardisasi arsitektur kode.

| Fitur | Abstract Class | Interface |
| :--- | :--- | :--- |
| **Isi Method** | Boleh berisi method konkrit (ber-body) & abstrak | HANYA berisi deklarasi signature method |
| **Property** | Boleh memiliki property dengan beragam visibility | HANYA boleh berisi nilai Konstanta |
| **Penerapan** | Menggunakan kata kunci `extends` | Menggunakan kata kunci `implements` |
| **Keterbatasan** | 1 class hanya bisa murni meng-extends 1 parent | 1 class bisa meng-implements **banyak** interface |

```php
<?php
// Interface sebagai Kontrak Standar Pembayaran
interface PaymentGatewayInterface 
{
    public function processPayment(float $amount): bool;
}

// Implementasi Kontrak
class MidtransPayment implements PaymentGatewayInterface 
{
    public function processPayment(float $amount): bool 
    {
        // Logika spesifik integrasi API Midtrans
        echo "Memproses pembayaran Rp{$amount} via Midtrans.";
        return true;
    }
}
```

---

### 2.4 Trait & Namespace

#### 📌 Trait
PHP tidak mendukung *multiple inheritance* (satu class menurunkan dua class parent sekaligus). **Trait** digunakan untuk membagikan kelompok method secara horizontal antar class independen.

#### 📌 Namespace
Sistem pengelompokan class (mirip struktur folder) untuk mencegah bentrok nama class (*class name collision*) dari berbagai library.

```php
<?php
namespace App\Services; // Penentuan Namespace

trait Loggable 
{
    public function logActivity(string $msg): void 
    {
        echo "[LOG " . date('Y-m-d H:i:s') . "]: " . $msg;
    }
}

class UserService 
{
    use Loggable; // Menggunakan Trait

    public function registerUser(): void 
    {
        // Logika pendaftaran...
        $this->logActivity("User baru berhasil didaftarkan.");
    }
}
```

---

## 🏗️ BAB 3: Core Concepts Laravel Framework

Laravel adalah framework PHP berbasis arsitektur modern yang mempermudah pembuatan aplikasi web dengan sintaks yang elegan.

### 3.1 Arsitektur Model-View-Controller (MVC)

Pola arsitektur software yang memisahkan aplikasi menjadi 3 komponen utama:

```
 [ HTTP Request ] ───> [ Route ] ───> [ Controller ]
                                             │
                                   ┌─────────┴─────────┐
                                   ▼                   ▼
                               [ Model ]           [ View ]
                                   │                   │
                             ( Database )        ( User UI )
```

* **Model:** Mengurus logika data dan interaksi ke database.
* **View:** Mengurus tampilan antarmuka (UI) dalam format HTML/Blade.
* **Controller:** Menjadi perantara utama yang menerima *Request*, mengambil data melalui *Model*, lalu mengirimkan data tersebut ke *View*.

---

### 3.2 Service Container & Dependency Injection

#### 1. What is Dependency Injection (DI)?
Dependency Injection adalah teknik di mana sebuah class menerima objek (*dependency*) yang dibutuhkannya dari luar, bukan membuat objek tersebut sendiri secara manual dengan kata kunci `new`.

* ❌ **Tanpa DI (Tightly Coupled):**
  ```php
  class UserController {
      private $mailer;
      public function __construct() {
          $this->mailer = new Mailer(); // Terikat erat dengan class Mailer
      }
  }
  ```

* ✅ **Dengan DI (Loosely Coupled):**
  ```php
  class UserController {
      private $mailer;
      public function __construct(Mailer $mailer) { // Disuntikkan secara otomatis dari luar
          $this->mailer = $mailer;
      }
  }
  ```

#### 2. Service Container
Service Container adalah **manajer dependensi otomatis** di Laravel. Ketika sebuah Controller membutuhkan class tertentu, Service Container akan membedah dependensinya, membuatkan instance-nya, lalu menyuntikkannya secara otomatis (*Automatic Dependency Resolution*).

---

### 3.3 Service Providers

**Service Provider** adalah tempat utama untuk melakukan bootstrap (*inisialisasi awal*) aplikasi Laravel. Semua komponen dasar seperti pendaftaran Service Container, Event Listener, Route, dan Middleware dikonfigurasi di sini.

Memiliki 2 method utama:
1. `register()`: Tempat untuk *binding* service ke Service Container.
2. `boot()`: Tempat untuk mengeksekusi kode *setelah* semua provider lain selesai didaftarkan.

---

### 3.4 Request Lifecycle & Middleware

#### 🔄 Request Lifecycle (Siklus Hidup Permintaan)

```
 HTTP Request 
      │
      ▼
 public/index.php (Entry Point)
      │
      ▼
 HTTP Kernel (Load Configuration & Service Providers)
      │
      ▼
 Middleware Stack (Pemeriksaan Keamanan & Token)
      │
      ▼
 Routing & Controller (Eksekusi Logika Bisnis)
      │
      ▼
 HTTP Response (Kembali ke Browser Pengguna)
```

#### 🛡️ Middleware
Middleware bertindak sebagai **pintu penyaring (filter)** antara *Request* dan *Controller*.

> 💡 **CONTOH PENGGUNAAN MIDDLEWARE:**
> * **Autentikasi (`auth`):** Memastikan pengguna sudah login sebelum mengakses halaman Dashboard.
> * **Verifikasi Role:** Memastikan hanya pengguna ber-role `admin` yang bisa mengakses menu manajemen user.
> * **CSRF Protection:** Mencegah serangan pemalsuan permintaan antar-situs.

---

## ⚙️ BAB 4: Komponen Utama Laravel

### 4.1 Routing & Controller

* **Routing:** Menghubungkan URL browser dengan method tertentu pada Controller.
* **Controller:** Menampung seluruh logika penanganan *request*.

```php
// routes/web.php
use App\Http\Controllers\ProductController;

// Named Route
Route::get('/products', [ProductController::class, 'index'])->name('products.index');
Route::post('/products', [ProductController::class, 'store'])->name('products.store');
```

---

### 4.2 Blade Templating Engine

Blade adalah engine templating bawaan Laravel. Blade memperbolehkan penulisan sintaks PHP dengan sangat ringkas dan mendukung fitur *Template Inheritance*.

```blade
{{-- resources/views/products/index.blade.php --}}
@extends('layouts.app') {{-- Inherit dari Layout Utama --}}

@section('content')
    <h1 class="title">Daftar Produk</h1>
    
    @if($products->isEmpty())
        <div class="alert alert-warning">Tidak ada produk tersedia.</div>
    @else
        <ul>
            @foreach($products as $product)
                <li>{{ $product->name }} - Rp {{ number_format($product->price) }}</li>
            @endforeach
        </ul>
    @endif
@endsection
```

---

### 4.3 Database Tools: Migration, Seeder, & Factory

| Tools | Fungsi Utama |
| :--- | :--- |
| **Migration** | *Version control* skema database menggunakan kode PHP tanpa perlu menyentuh SQL manual. |
| **Seeder** | Script pengisi data awal (*initial/master data*) ke database. |
| **Factory** | Generator data tiruan (*dummy data*) berkapasitas besar untuk keperluan uji coba (*testing*). |

```php
// database/migrations/xxxx_create_products_table.php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration {
    public function up(): void
    {
        Schema::create('products', function (Blueprint $table) {
            $table->id();
            $table->string('title');
            $table->text('description');
            $table->integer('stock');
            $table->decimal('price', 12, 2);
            $table->timestamps(); // Kolom created_at & updated_at
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('products');
    }
};
```

---

### 4.4 Eloquent ORM & Relasi Antar Tabel

**Eloquent ORM** (*Object-Relational Mapper*) mempermudah interaksi database dengan memetakan tabel database menjadi Objek PHP.

#### Tipe Relasi Utama:
1. **One to One:** `hasOne()` & `belongsTo()`
2. **One to Many:** `hasMany()` & `belongsTo()`
3. **Many to Many:** `belongsToMany()`

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Category extends Model 
{
    // Relasi: Satu Kategori memiliki BANYAK Produk
    public function products() 
    {
        return $this->hasMany(Product::class);
    }
}

class Product extends Model 
{
    // Relasi: Produk MILIK dari satu Kategori
    public function category() 
    {
        return $this->belongsTo(Category::class);
    }
}
```

---

## 🚀 BAB 5: Penerapan Praktis - Aplikasi CRUD Produk

Instruksi praktis pembuatan fitur CRUD Produk (Create, Read, Update, Delete) secara terstruktur.

### 5.1 Persiapan Project & Konfigurasi

Jalankan perintah berikut pada terminal:

```bash
# 1. Buat project Laravel baru
laravel new app-crud-produk

# 2. Masuk ke direktori project
cd app-crud-produk
```

Konfigurasi koneksi database pada file `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=db_laravel_crud
DB_USERNAME=root
DB_PASSWORD=
```

---

### 5.2 Migration & Model

Jalankan Artisan command untuk membuat Model, Migration, dan Controller sekaligus:

```bash
php artisan make:model Product -mc
```

Buka file migration `database/migrations/xxxx_create_products_table.php` dan sesuaikan skemanya:

```php
public function up(): void
{
    Schema::create('products', function (Blueprint $table) {
        $table->id();
        $table->string('title');
        $table->text('description');
        $table->integer('stock');
        $table->decimal('price', 12, 2);
        $table->timestamps();
    });
}
```

Jalankan migrasi tabel ke database:

```bash
php artisan migrate
```

Konfigurasi properti `$fillable` pada Model `app/Models/Product.php` untuk mengizinkan penambahan data massal (*Mass Assignment*):

```php
<?php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Product extends Model
{
    use HasFactory;

    protected $fillable = ['title', 'description', 'stock', 'price'];
}
```

---

### 5.3 Controller & Validasi

Buka `app/Http/Controllers/ProductController.php` dan lengkapi seluruh method CRUD:

```php
<?php
namespace App\Http\Controllers;

use App\Models\Product;
use Illuminate\Http\Request;

class ProductController extends Controller
{
    // 1. READ: Tampilkan Semua Data
    public function index() 
    {
        $products = Product::latest()->get();
        return view('products.index', compact('products'));
    }

    // 2. CREATE: Form Tambah
    public function create() 
    {
        return view('products.create');
    }

    // 3. CREATE: Simpan Data Baru
    public function store(Request $request) 
    {
        $request->validate([
            'title'       => 'required|min:3',
            'description' => 'required',
            'stock'       => 'required|numeric',
            'price'       => 'required|numeric',
        ]);

        Product::create($request->all());
        return redirect()->route('products.index')->with('success', 'Produk berhasil ditambahkan!');
    }

    // 4. UPDATE: Form Edit Data
    public function edit(Product $product) 
    {
        return view('products.edit', compact('product'));
    }

    // 5. UPDATE: Simpan Perubahan Data
    public function update(Request $request, Product $product) 
    {
        $request->validate([
            'title'       => 'required|min:3',
            'description' => 'required',
            'stock'       => 'required|numeric',
            'price'       => 'required|numeric',
        ]);

        $product->update($request->all());
        return redirect()->route('products.index')->with('success', 'Produk berhasil diperbarui!');
    }

    // 6. DELETE: Hapus Data
    public function destroy(Product $product) 
    {
        $product->delete();
        return redirect()->route('products.index')->with('success', 'Produk berhasil dihapus!');
    }
}
```

Daftarkan Resource Route pada `routes/web.php`:

```php
use App\Http\Controllers\ProductController;

Route::resource('products', ProductController::class);
```

---

### 5.4 Integrasi View Blade

#### 🖥️ 1. Master Layout (`resources/views/layouts/app.blade.php`)

```blade
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Kelola Produk</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body class="bg-light">
    <div class="container mt-5 mb-5">
        @yield('content')
    </div>
</body>
</html>
```

#### 📄 2. Halaman Index / Read (`resources/views/products/index.blade.php`)

```blade
@extends('layouts.app')

@section('content')
<div class="d-flex justify-content-between align-items-center mb-4">
    <h2>📦 Kelola Data Produk</h2>
    <a href="{{ route('products.create') }}" class="btn btn-primary">+ Tambah Produk</a>
</div>

@if(session('success'))
    <div class="alert alert-success">{{ session('success') }}</div>
@endif

<div class="card shadow-sm">
    <div class="card-body p-0">
        <table class="table table-striped table-hover mb-0">
            <thead class="table-dark">
                <tr>
                    <th>Judul Produk</th>
                    <th>Stok</th>
                    <th>Harga</th>
                    <th class="text-center">Aksi</th>
                </tr>
            </thead>
            <tbody>
                @forelse($products as $product)
                    <tr>
                        <td class="align-middle">{{ $product->title }}</td>
                        <td class="align-middle">{{ $product->stock }}</td>
                        <td class="align-middle">Rp {{ number_format($product->price, 0, ',', '.') }}</td>
                        <td class="text-center align-middle">
                            <a href="{{ route('products.edit', $product->id) }}" class="btn btn-sm btn-warning">Edit</a>
                            <form action="{{ route('products.destroy', $product->id) }}" method="POST" class="d-inline">
                                @csrf
                                @method('DELETE')
                                <button class="btn btn-sm btn-danger" onclick="return confirm('Yakin ingin menghapus?')">Hapus</button>
                            </form>
                        </td>
                    </tr>
                @empty
                    <tr>
                        <td colspan="4" class="text-center text-muted py-4">Belum ada data produk tersedia.</td>
                    </tr>
                @endforelse
            </tbody>
        </table>
    </div>
</div>
@endsection
```

#### 📝 3. Form Input Data (`resources/views/products/create.blade.php`)

```blade
@extends('layouts.app')

@section('content')
<div class="row justify-content-center">
    <div class="col-md-8">
        <div class="card shadow-sm">
            <div class="card-header bg-primary text-white">
                <h4 class="mb-0">Tambah Produk Baru</h4>
            </div>
            <div class="card-body">
                <form action="{{ route('products.store') }}" method="POST">
                    @csrf
                    <div class="mb-3">
                        <label class="form-label">Judul Produk</label>
                        <input type="text" name="title" class="form-control @error('title') is-invalid @enderror" value="{{ old('title') }}">
                        @error('title') <div class="invalid-feedback">{{ $message }}</div> @enderror
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Deskripsi</label>
                        <textarea name="description" class="form-control @error('description') is-invalid @enderror" rows="3">{{ old('description') }}</textarea>
                        @error('description') <div class="invalid-feedback">{{ $message }}</div> @enderror
                    </div>
                    <div class="row mb-3">
                        <div class="col-md-6">
                            <label class="form-label">Stok</label>
                            <input type="number" name="stock" class="form-control @error('stock') is-invalid @enderror" value="{{ old('stock') }}">
                            @error('stock') <div class="invalid-feedback">{{ $message }}</div> @enderror
                        </div>
                        <div class="col-md-6">
                            <label class="form-label">Harga (Rp)</label>
                            <input type="number" name="price" class="form-control @error('price') is-invalid @enderror" value="{{ old('price') }}">
                            @error('price') <div class="invalid-feedback">{{ $message }}</div> @enderror
                        </div>
                    </div>
                    <button type="submit" class="btn btn-success">Simpan Produk</button>
                    <a href="{{ route('products.index') }}" class="btn btn-secondary">Batal</a>
                </form>
            </div>
        </div>
    </div>
</div>
@endsection
```

---

## 💡 PENUTUP & BEST PRACTICES

> 🛡️ **1. Keamanan Aplikasi**
> * **CSRF Protection:** Selalu gunakan direktif `@csrf` pada setiap form HTML untuk mencegah serangan *Cross-Site Request Forgery*.
> * **SQL Injection:** Hindari query SQL manual (*raw query*). Manfaatkan selalu fitur Eloquent ORM atau Query Builder yang memproteksi query melalui *parameter binding*.

> ⚡ **2. Optimasi Performa (N+1 Query Problem)**
> * Hindari pemanggilan query database berulang di dalam *looping*.
> * Gunakan teknik **Eager Loading** (`Product::with('category')->get()`) alih-alih Lazy Loading saat menampilkan data berelasi.

> 🧼 **3. Kode yang Clean & Terstruktur**
> * **Fat Model, Skinny Controller:** Controller harus dibuat seringkas mungkin. Pindahkan kalkulasi atau logika bisnis kompleks ke dalam Model, Service Class, atau Action Class.
> * **Form Request:** Apabila aturan validasi form sudah panjang, pisahkan ke dalam class Form Request khusus (`php artisan make:request StoreProductRequest`).