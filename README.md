# 🛵 Ping & Pick MiFa — Web-Based Food Ordering & Delivery System

[![Netlify Status](https://api.netlify.com/api/v1/badges/site-id/deploy-status)](https://jastip-pingandpick-mifa.netlify.app)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat&logo=tailwind-css&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Google Apps Script](https://img.shields.io/badge/Google_Apps_Script-4285F4?style=flat&logo=google&logoColor=white)

> **Live Demo:** [https://jastip-pingandpick-mifa.netlify.app](https://jastip-pingandpick-mifa.netlify.app)

---

## 📌 Business Problem & Solution

### 🚨 Latar Belakang (Problem Statement)
Proses pemesanan makanan Jasa Titip (Jastip) di lingkungan civitas akademika (Dosen & Tendik) seringkali mengalami kendala:
1. **Pesan WhatsApp Berantakan:** Format pesanan dari pelanggan tidak terstruktur dan manual.
2. **Kendala Verifikasi Pembayaran:** Bukti transfer via QRIS sering menumpuk di memori ponsel atau gagal dikirim akibat batasan platform.
3. **Kalkulasi Biaya Manual:** Perhitungan subtotal makanan dan penambahan komisi/jasa per menu berisiko menimbulkan *human error*.

### 💡 Solusi yang Diterapkan (Project Scope)
Membangun web aplikasi pemesanan berbasis frontend-lightweight yang responsif. Aplikasi ini secara otomatis menghitung rinci biaya pesanan, memproses *upload* gambar bukti bayar ke penyimpan awan (Google Drive), dan mengarahkan draf pesanan resmi ke WhatsApp Bisnis Admin.

---

## 🔥 Fitur Utama (Key Features)

- **🛒 Dynamic Order Form & Item Counter:**
  Fitur penambahan pesanan fleksibel dengan 16+ daftar pilihan menu kantin serta opsi input manual menu khusus (*Other Menu*).
  
- **🧮 Automatic Cost & Fee Calculation:**
  Kalkulasi otomatis nominal beli, kuantitas (*Qty*), subtotal, dan pembebanan biaya jasa (Rp 2.000) per varian menu unik.

- **📊 Transparent Summary & Invoice Visual:**
  Pratinjau tagihan ringkas sebelum konfirmasi akhir untuk memastikan akurasi data pemesan dan rincian belanja.

- **☁️ Serverless File Upload via Google Apps Script (GAS):**
  Mengatasi kendala SSL/CORS tanpa server backend berbayar. Bukti pembayaran di-convert ke `Base64`, diunggah ke folder publik Google Drive, dan menghasilkan *public shareable link* secara real-time.

- **📱 WhatsApp Business API Encoding Standard:**
  Pesan otomatis terenkripsi murni (`%0A`, `encodeURIComponent`) untuk memastikan tidak terjadi korupsi karakter atau emoji pada semua OS smartphone.

---

## 🏗️ Arsitektur Sistem (System Architecture)

```text
[ Client / Browser ] 
        │
        ├─► (1) Input Data & Menu ────────► Live Calculation (JS Vanilla)
        │
        ├─► (2) Upload QRIS Proof (Base64) ──► [ GAS Proxy Web App ] ──► [ Google Drive Folder ]
        │                                                                           │
        └─► (3) Direct WA Redirect ◄─────── (Return Drive Link) ────────────────────┘
