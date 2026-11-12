# 🚀 Panduan Arsitektur & Workflow Pengembangan SaaS Machine Learning

Dokumen ini merangkum struktur proyek, alur kerja pengembangan (*workflow*) untuk perangkat dengan spesifikasi terbatas, pemanfaatan Docker pada Linux Mint, serta pemilihan *tech stack* terbaik untuk layanan Machine Learning / Deep Learning dalam ekosistem **SaaS (Software as a Service)**.

---

## 1. Struktur Folder Proyek (Monorepo Architecture)

Untuk proyek SaaS yang menggunakan **React** (Frontend), **Express.js** (Backend API), dan **Python** (ML/DL Service), pendekatan **Monorepo** adalah pilihan paling efisien. Struktur ini memisahkan logika antarmuka pengguna, logika bisnis, dan komputasi model AI secara modular.

```text
my-ml-saas/
├── .env                    # Environment variables global
├── .gitignore
├── README.md
├── docker-compose.yml      # Orkestrasi seluruh container (Backend, Frontend, ML)
│
├── backend/                # Express.js API Server (Gateway & Business Logic)
│   ├── src/
│   │   ├── config/         # Konfigurasi database, koneksi ML service, env
│   │   ├── controllers/    # Handler endpoint (auth, prediction, user, billing)
│   │   ├── middleware/     # Auth JWT, error handling, rate limiting, quota check
│   │   ├── models/         # Skema database (Prisma, Sequelize, Mongoose)
│   │   ├── routes/         # Definisi rute API (auth.routes.js, predict.routes.js)
│   │   ├── services/       # Logika bisnis & komunikasi HTTP ke ML Service
│   │   ├── utils/          # Fungsi pembantu (logger, formatters)
│   │   └── server.js       # Entry point aplikasi Express
│   ├── Dockerfile          # Konfigurasi container Express.js
│   ├── .env
│   └── package.json
│
├── frontend/               # React (Vite / SPA)
│   ├── public/             # Aset statis (favicon, logo)
│   ├── src/
│   │   ├── assets/         # Gambar, ikon, font
│   │   ├── components/     # Komponen UI reusable (Button, Modal, Card, Chart)
│   │   ├── features/       # Modul berbasis fitur (auth, dashboard, billing)
│   │   ├── hooks/          # Custom React hooks (useAuth, useFetch)
│   │   ├── layouts/        # Tata letak halaman (DashboardLayout, AuthLayout)
│   │   ├── pages/          # Halaman utama aplikasi (Login, Dashboard, Predict)
│   │   ├── services/       # Konfigurasi API client (Axios instance)
│   │   ├── store/          # State management (Zustand, Redux Toolkit, Context)
│   │   ├── utils/          # Helper & formatter (tanggal, mata uang)
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── Dockerfile          # Konfigurasi container React (Vite + Nginx)
│   ├── .env
│   ├── index.html
│   └── package.json
│
└── ml-pipeline/            # Python ML/DL Microservice & Research Pipeline
    ├── app/                # FastAPI untuk melayani inferensi model
    │   ├── main.py         # Entry point API FastAPI
    │   └── model_loader.py # Logika pemuatan bobot model ke memori
    ├── notebooks/          # File Jupyter (.ipynb) untuk eksplorasi & Google Colab
    │   ├── 01_data_preprocessing.ipynb
    │   └── 02_model_training.ipynb
    ├── scripts/            # Script Python murni untuk otomatisasi
    │   ├── train.py
    │   └── inference.py
    ├── artifacts/          # Penyimpanan bobot model terlatih (.pth, .h5, .onnx)
    ├── dataset/            # Sampel data kecil untuk uji coba lokal
    ├── Dockerfile          # Konfigurasi container Python FastAPI
    └── requirements.txt    # Daftar dependencies Python
```

---

## 2. Strategi Pengembangan untuk Spesifikasi PC Terbatas

Jika spesifikasi PC lokal terbatas (misalnya menggunakan prosesor lawas seperti Intel Core i5 Gen-4, RAM 8GB, dan GPU non-CUDA seperti GT 710), proses pelatihan (*training*) Deep Learning tidak disarankan dijalankan secara lokal.

### Alur Kerja Hybrid (VS Code Lokal + Google Colab)

| Tahapan | Lingkungan Eksekusi | Keterangan & Tools |
| :--- | :--- | :--- |
| **UI & API Development** | **PC Lokal (VS Code)** | Pengembangan kode React dan Express.js sangat ringan dan tidak membutuhkan GPU bertenaga tinggi. |
| **Penyimpanan Dataset** | **Google Drive** | Menyimpan dataset berukuran besar agar tidak memenuhi kapasitas penyimpanan lokal. |
| **Model Training (DL)** | **Google Colab (Cloud GPU)** | Menghubungkan VS Code lokal ke *remote kernel* Google Colab via ekstensi Jupyter untuk memanfaatkan GPU gratis (T4). |
| **Model Export** | **Artifacts (`ml-pipeline/artifacts/`)** | Bobot model hasil *training* diunduh dalam format standar (`.pth`, `.h5`, atau `.onnx`) untuk digunakan pada tahap inferensi. |

---

## 3. Optimasi Docker pada Sistem Operasi Linux Mint

Penggunaan **Docker** dalam arsitektur Monorepo memungkinkan setiap layanan dikemas dalam *environment* yang terisolasi dan konsisten antara komputer lokal (*development*) dan server *cloud* (*production*).

### Keunggulan Menggunakan Linux Mint:
1. **Native Execution (Tanpa Virtualisasi Berat)**: Berbeda dengan Windows yang memerlukan lapisan virtualisasi WSL2/Hyper-V, Docker di Linux berjalan langsung di atas *kernel* sistem operasi (*bare-metal performance*).
2. **Konsumsi RAM Minimal**: Linux Mint (terutama edisi XFCE/MATE) hanya memakan sekitar 500MB–1GB RAM saat *idle*, menyisakan ruang memori yang jauh lebih lega bagi VS Code, Node.js, dan container Docker pada perangkat dengan RAM 8GB.
3. **Selektivitas Deployment**: Dengan `Dockerfile` terpisah di tiap direktori, Anda dapat men-*deploy* layanan secara terpisah (misalnya Frontend di Vercel, Backend Express di VPS, dan ML Service di Hugging Face Spaces/Render).

### Tips Menghemat Memori Saat Menggunakan Docker Compose:
* Jalankan layanan secara selektif menggunakan perintah:
  ```bash
  docker compose up backend db
  ```
* Batasi alokasi memori maksimal pada file `docker-compose.yml` untuk mencegah *system freeze*:
  ```yaml
  services:
    backend:
      image: node:18-alpine
      deploy:
        resources:
          limits:
            memory: 512M
  ```

---

## 4. Arsitektur Layanan: Express.js vs FastAPI (Python)

Dalam pengembangan SaaS Machine Learning, **sangat disarankan untuk memisahkan layanan ML/DL dari backend utama Express.js** menggunakan **FastAPI**.

### Perbandingan Tech Stack untuk ML Serving

* **Mengapa Tidak Digabung ke Express.js?**
  * Ekosistem Deep Learning (PyTorch, TensorFlow, Scikit-Learn, Hugging Face) berbasis pada bahasa Python.
  * Menjalankan model Python dari Node.js menggunakan `child_process` sangat lambat, memicu *bottleneck*, dan berisiko menyebabkan *memory leak* saat menangani banyak pengguna secara bersamaan.

* **Mengapa Memilih FastAPI Dibandingkan Django?**
  * **FastAPI** dirancang khusus sebagai *micro-framework* API modern yang ringan, mendukung pemrosesan asinkron (`async/await`), memiliki dokumentasi otomatis (Swagger UI), dan memiliki kecepatan eksekusi yang sangat tinggi.
  * **Django** bersifat *monolithic* dan membawa banyak fitur bawaan (ORM, admin panel) yang tidak diperlukan jika hanya digunakan sebagai layanan inferensi model AI.

### Diagram Alur Komunikasi Sistem (3-Tier Microservices)

```text
┌─────────────────────────┐
│   React.js (Frontend)   │  ──> Antarmuka Pengguna (Dashboard, Input Data, Visualisasi)
└────────────┬────────────┘
             │ HTTP / REST API (JSON)
             ▼
┌─────────────────────────┐
│  Express.js (Gateway)   │  ──> Autentikasi JWT, Database User, Billing/Kuota, Rate Limit
└────────────┬────────────┘
             │ Internal HTTP Request
             ▼
┌─────────────────────────┐
│  FastAPI (ML Service)   │  ──> Memuat Model (.pth/.h5) & Eksekusi Prediksi AI
└─────────────────────────┘
```