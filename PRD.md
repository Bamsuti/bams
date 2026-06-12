# PRD: Aplikasi Bams - Manajemen Toko Skala Kecil

## 1. Latar Belakang & Tujuan
Aplikasi kasir/manajemen toko berbasis web untuk toko kecil (sendal, sepatu, baju) dengan akses internet lambat dan perangkat HP kelas menengah-bawah.

## 2. Target Pengguna
- Pemilik toko skala mikro/kecil
- Operasional via HP mid-low (Chrome/Android)
- Koneksi internet tidak stabil

## 3. Tech Stack
| Layer | Pilihan |
|-------|---------|
| Backend | Laravel 11 |
| Database | MySQL/MariaDB (XAMPP) |
| Frontend | Blade + Tailwind CSS + Alpine.js |
| Cetak | DomPDF (struk/PDF) |
| Auth | Laravel Breeze |

## 4. Fitur Utama

### A. Manajemen Produk
- CRUD produk (nama, kategori, harga beli, harga jual, stok)
- Kategori: Sepatu, Sendal, Baju (+ custom)
- Upload foto produk (opsional, kompresi otomatis)
- Variant: ukuran, warna

### B. Manajemen Stok
- Stok masuk (restock)
- Stok keluar (penjualan)
- Notifikasi stok minimum

### C. Transaksi Penjualan (Kasir)
- Antarmuka kasir cepat mobile-friendly
- Pilih produk → input qty → total otomatis
- Metode bayar: Tunai & Transfer
- Cetak struk (PDF)
- Hitung kembalian otomatis

### D. Ringkasan Harian
- Total penjualan hari ini
- Jumlah transaksi
- Metode pembayaran breakdown

### E. Riwayat Transaksi
- Filter tanggal, produk, metode bayar
- Lihat detail transaksi
- Export PDF/Excel
- Cetak ulang struk

## 5. Arsitektur
```
Bams/
├── app/
│   ├── Http/Controllers/
│   │   ├── ProductController.php
│   │   ├── CategoryController.php
│   │   ├── StockController.php
│   │   ├── TransactionController.php
│   │   └── ReportController.php
│   ├── Models/
│   │   ├── Product.php
│   │   ├── Category.php
│   │   ├── Transaction.php
│   │   └── TransactionItem.php
│   └── Services/
├── database/migrations/
├── resources/views/
│   ├── products/
│   ├── transactions/
│   ├── reports/
│   └── layouts/
└── routes/web.php
```

## 6. Database Schema
- `categories` (id, name, slug)
- `products` (id, category_id, name, sku, buy_price, sell_price, stock, image, variant)
- `transactions` (id, invoice_no, total, payment_method, paid_amount, change_amount, transaction_date)
- `transaction_items` (id, transaction_id, product_id, quantity, price, subtotal)
- `stock_movements` (id, product_id, type, quantity, note)
- `daily_summaries` (id, date, total_sales, total_transactions)

## 7. Optimasi Kecepatan Rendah
- Blade view (no SPA/JS heavy)
- Ukuran halaman < 500kb
- Image kompresi otomatis
- Lazy loading
- Minimal CSS/JS (Tailwind purged + Alpine ringan)

## 8. Mobile-First UI
- Layout responsive (Tailwind)
- Tombol besar (min 44px)
- Input auto-focus numeric untuk kasir
