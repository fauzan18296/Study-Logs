# 📚 Buku Panduan Lengkap: PHP & Laravel
> **Dari Konsep Dasar, Arsitektur, Hingga Penerapan Praktis**

---

## 📋 Daftar Isi

- [📖 BAB 1: Pengenalan & Dasar-Dasar PHP](#-bab-1-pengenalan--dasar-dasar-php)
  - [1.1 Apa itu PHP?](#11-apa-itu-php)
  - [1.2 Syntax Dasar & Tipe Data](#12-syntax-dasar--tipe-data)
  - [1.3 Control Flow](#13-control-flow)
  - [1.4 Fungsi & Scope Variabel](#14-fungsi--scope-variabel)
- [🧩 BAB 2: Pemrograman Berbasis Objek (OOP) PHP](#-bab-2-pemrograman-berbasis-objek-oop-php)
  - [2.1 Class & Object](#21-class--object)
  - [2.2 Tiga Pilar OOP](#22-tiga-pilar-oop)
  - [2.3 Interface vs Abstract Class](#23-interface-vs-abstract-class)
  - [2.4 Trait & Namespace](#24-trait--namespace)
- [🏗️ BAB 3: Core Concepts Laravel Framework](#️-bab-3-core-concepts-laravel-framework)
  - [3.1 Arsitektur Model-View-Controller (MVC)](#31-arsitektur-model-view-controller-mvc)
  - [3.2 Service Container & Dependency Injection](#32-service-container--dependency-injection)
  - [3.3 Service Providers](#33-service-providers)
  - [3.4 Request Lifecycle & Middleware](#34-request-lifecycle--middleware)
- [⚙️ BAB 4: Komponen Utama Laravel](#️-bab-4-komponen-utama-laravel)
  - [4.1 Routing & Controller](#41-routing--controller)
  - [4.2 Blade Templating Engine](#42-blade-templating-engine)
  - [4.3 Database: Migration, Seeder, & Factory](#43-database-migration-seeder--factory)
  - [4.4 Eloquent ORM & Relasi](#44-eloquent-orm--relasi)
- [🚀 BAB 5: Penerapan Praktis - Aplikasi CRUD](#-bab-5-penerapan-praktis---aplikasi-crud)
  - [5.1 Persiapan Project](#51-persiapan-project)
  - [5.2 Migration & Model](#52-migration--model)
  - [5.3 Controller & Validasi](#53-controller--validasi)
  - [5.4 Integrasi View Blade](#54-integrasi-view-blade)
- [💡 Penutup & Best Practices](#-penutup--best-practices)

---

## 📖 BAB 1: Pengenalan & Dasar-Dasar PHP

### 1.1 Apa itu PHP?

**PHP** (*PHP: Hypertext Preprocessor*) adalah bahasa pemrograman *scripting* di sisi server (*server-side*) yang bersifat *open-source*. 

> 💡 **Fungsi Utama PHP:**
> - Memproses form HTML dan menyimpan data ke database.
> - Mengelola *session*, *cookie*, dan autentikasi pengguna.
> - Menghasilkan konten halaman web yang dinamis.

---

### 1.2 Syntax Dasar & Tipe Data

Setiap kode PHP diawali dengan tag `<?php` dan diakhiri dengan `?>`.

```php
<?php
// Deklarasi Variabel
$nama      = "Budi Santoso";                  // String
$umur      = 25;                             // Integer
$ipk       = 3.75;                           // Float
$isStudent = true;                           // Boolean
$hobi      = ["Membaca", "Koding", "Musik"]; // Array

// Output Data
echo "Nama: " . $nama . "<br>";
echo "Status: " . ($isStudent ? 'Aktif' : 'Tidak Aktif');
?>
```

---

### 1.3 Control Flow

#### 🔀 Percabangan (`if-else`)

```php
<?php
$nilai = 80;

if ($nilai >= 85) {
    echo "Predikat: A";
} elseif ($nilai >= 70) {
    echo "Predikat: B";
} else {
    echo "Predikat: C";
}
?>
```

#### 🔁 Perulangan (`foreach`)

```php
<?php
$buahs = ["Apel", "Jeruk", "Mangga"];

foreach ($buahs as $index => $buah) {
    echo "Buah ke-{$index}: {$buah}<br>";
}
?>
```

---

### 1.4 Fungsi & Scope Variabel

```php
<?php
// Menggunakan Type Hinting & Return Type
function hitungLuasPersegi(float $panjang, float $lebar): float 
{
    return $panjang * $lebar;
}

$luas = hitungLuasPersegi(10.5, 5.0);
echo "Luas Persegi Panjang: " . $luas;
?>
```

---

## 🧩 BAB 2: Pemrograman Berbasis Objek (OOP) PHP

### 2.1 Class & Object

| Istilah | Penjelasan | Analogia |
| :--- | :--- | :--- |
| **Class** | Cetak biru (*blueprint*) untuk membuat objek | Cetak biru mobil |
| **Object** | Hasil instansiasi riil dari sebuah Class | Mobil nyata hasil rakitan |

```php
<?php
class Mobil 
{
    // Property
    public string $merk;
    public string $warna;

    // Constructor
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
$myCar = new Mobil("Toyota", "Hitam");
echo $myCar->jalankan();
?>
```

---

### 2.2 Tiga Pilar OOP

```
 ┌─────────────────────────────────────────────────────────────┐
 │                       PILAR OOP                             │
 ├──────────────────┬───────────────────────┬──────────────────┤
 │  Encapsulation   │      Inheritance      │   Polymorphism   │
 │ (Pembungkusan)   │      (Pewarisan)      │ (Banyak Bentuk)  │
 └──────────────────┴───────────────────────┴──────────────────┘
```

```php
<?php
// Parent Class (Encapsulation & Inheritance)
class Kendaraan 
{
    protected string $nama;

    public function __construct(string $nama) 
    {
        $this->nama = $nama;
    }

    public function klakson(): string 
    {
        return "Beep beep!";
    }
}

// Child Class (Polymorphism / Method Override)
class Motor extends Kendaraan 
{
    public function klakson(): string 
    {
        return "Tin tin! Motor {$this->nama} lewat.";
    }
}

$motor = new Motor("Honda");
echo $motor->klakson();
?>
```

---

### 2.3 Interface vs Abstract Class

```php
<?php
// Interface sebagai Kontrak
interface PaymentGatewayInterface 
{
    public function pay(float $amount): bool;
}

class MidtransPayment implements PaymentGatewayInterface 
{
    public function pay(float $amount): bool 
    {
        // Logika proses pembayaran
        return true;
    }
}
?>
```

---

### 2.4 Trait & Namespace

* 📌 **Trait:** Membagikan metode antar class tanpa keterikatan hierarki pewarisan.
* 📌 **Namespace:** Mengorganisir class dan menghindari terjadinya bentrok nama class.

```php
<?php
namespace App\Services;

trait Loggable 
{
    public function log(string $message): void 
    {
        echo "[LOG - " . date('Y-m-d H:i:s') . "]: " . $message;
    }
}

class UserService 
{
    use Loggable; // Menggunakan Trait

    public function createUser(): void 
    {
        $this->log("User baru berhasil ditambahkan.");
    }
}
?>
```

---

## 🏗️ BAB 3: Core Concepts Laravel Framework

### 3.1 Arsitektur Model-View-Controller (MVC)

```
 [ User Request ] ───> [ Route ] ───> [ Controller ]
                                            │
                                  ┌─────────┴─────────┐
                                  ▼                   ▼
                              [ Model ]           [ View ]
                                  │                   │
                            ( Database )        ( User UI )
```

---

### 3.2 Service Container & Dependency Injection

> 🎯 **Dependency Injection (DI)** adalah teknik di mana ketergantungan sebuah *class* dimasukkan secara otomatis dari luar melalui *constructor* atau *method*, alih-alih diinstansiasi secara manual di dalam *class* tersebut.

```php
<?php
namespace App\Http\Controllers;

use App\Repositories\UserRepository;

class UserController extends Controller 
{
    protected UserRepository $users;

    // Automatic Dependency Injection via Constructor
    public function __construct(UserRepository $users) 
    {
        $this->users = $users;
    }

    public function index() 
    {
        return response()->json($this->users->all());
    }
}
?>
```

---

### 3.3 Service Providers

Service Provider adalah **jantung pendaftaran aplikasi**. Semua konfigurasi paket, *event listener*, *middleware*, dan registrasi *binding* di dalam Service Container diproses di sini.

---

### 3.4 Request Lifecycle & Middleware

```
 HTTP Request 
      │
      ▼
 public/index.php
      │
      ▼
 HTTP Kernel ───> [ Middleware Filter ] ───> [ Routing & Controller ]
                                                     │
 HTTP Response <─────────────────────────────────────┘
```

---

## ⚙️ BAB 4: Komponen Utama Laravel

### 4.1 Routing & Controller

```php
// routes/web.php
use App\Http\Controllers\ProductController;

Route::get('/products', [ProductController::class, 'index'])->name('products.index');
Route::post('/products', [ProductController::class, 'store'])->name('products.store');
```

---

### 4.2 Blade Templating Engine

```blade
{{-- resources/views/products/index.blade.php --}}
@extends('layouts.app')

@section('content')
    <h1 class="title">Daftar Produk</h1>
    <ul>
        @foreach($products as $product)
            <li>{{ $product->name }} - Rp {{ number_format($product->price) }}</li>
        @endforeach
    </ul>
@endsection
```

---

### 4.3 Database: Migration, Seeder, & Factory

#### 📝 Migration Example

```php
// database/migrations/xxxx_create_products_table.php
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

---

### 4.4 Eloquent ORM & Relasi

```php
// Relasi One to Many (Kategori Memiliki Banyak Produk)
class Category extends Model 
{
    public function products() 
    {
        return $this->hasMany(Product::class);
    }
}

class Product extends Model 
{
    public function category() 
    {
        return $this->belongsTo(Category::class);
    }
}
```

---

## 🚀 BAB 5: Penerapan Praktis - Aplikasi CRUD

### 5.1 Persiapan Project

```bash
# 1. Buat project baru
laravel new app-crud-produk

# 2. Masuk ke direktori project
cd app-crud-produk
```

Konfigurasi `.env`:
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

Jalankan perintah Artisan untuk membuat Model, Migration, dan Controller sekaligus:

```bash
php artisan make:model Product -mc
```

Jalankan migrasi database:
```bash
php artisan migrate
```

Edit file Model (`app/Models/Product.php`):
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
?>
```

---

### 5.3 Controller & Validasi

Edit file Controller (`app/Http/Controllers/ProductController.php`):

```php
<?php
namespace App\Http\Controllers;

use App\Models\Product;
use Illuminate\Http\Request;

class ProductController extends Controller
{
    public function index() 
    {
        $products = Product::latest()->get();
        return view('products.index', compact('products'));
    }

    public function create() 
    {
        return view('products.create');
    }

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

    public function edit(Product $product) 
    {
        return view('products.edit', compact('product'));
    }

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

    public function destroy(Product $product) 
    {
        $product->delete();
        return redirect()->route('products.index')->with('success', 'Produk berhasil dihapus!');
    }
}
?>
```

Tambahkan Resource Route (`routes/web.php`):
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

#### 📄 2. Halaman Utama (`resources/views/products/index.blade.php`)

```blade
@extends('layouts.app')

@section('content')
<div class="d-flex justify-content-between align-items-center mb-4">
    <h2>📦 Daftar Produk</h2>
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
                    <th>Judul</th>
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
                                <button class="btn btn-sm btn-danger" onclick="return confirm('Yakin ingin menghapus produk ini?')">Hapus</button>
                            </form>
                        </td>
                    </tr>
                @empty
                    <tr>
                        <td colspan="4" class="text-center text-muted py-4">Belum ada data produk.</td>
                    </tr>
                @endforelse
            </tbody>
        </table>
    </div>
</div>
@endsection
```

#### 📝 3. Form Input (`resources/views/products/create.blade.php`)

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

## 💡 Penutup & Best Practices

Berikut beberapa tips penting (*best practices*) dalam pengembangan menggunakan Laravel:

> 🛡️ **1. Keamanan Aplikasi**
> - Selalu sertakan `@csrf` dalam setiap formulir HTML.
> - Hindari penggunaan `DB::raw()` dengan input langsung dari pengguna untuk mencegah **SQL Injection**.

> ⚡ **2. Performa Query (Eager Loading)**
> - Gunakan Eager Loading (`Product::with('category')->get()`) untuk menghindari masalah **N+1 Query Problem**.

> 🧼 **3. Kode yang Bersih (Clean Code)**
> - Terapkan prinsip **DRY** (*Don't Repeat Yourself*).
> - Manfaatkan **Form Request Validation** terpisah jika aturan validasi formulir cukup rumit.