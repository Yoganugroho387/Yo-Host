# YOHOST ENTERPRISE CLOUD PLATFORM
### Sistem Otomasi Cloud Hosting, Manajemen Domain & Billing Berbasis Web

[![PHP Version](https://img.shields.io/badge/PHP-8.1%20%7C%208.2%20%7C%208.3-blue.svg)]()
[![Architecture](https://img.shields.io/badge/Architecture-Custom%20Lightweight%20MVC-indigo.svg)]()
[![Database](https://img.shields.io/badge/Database-MySQL%20%2F%20MariaDB%20(InnoDB)-lightgrey.svg)]()
[![Security](https://img.shields.io/badge/Security-Multi--Tenant%20Isolated%20%26%202FA-success.svg)]()
[![Design Standard](https://img.shields.io/badge/Design-Zero%20Keyboard%20Emojis%20%7C%20SVG%20Lucide-orange.svg)]()
[![White-Label](https://img.shields.io/badge/White--Label-100%25%20Independent%20Registrar-teal.svg)]()

---

## 1. PENDAHULUAN & PROFIL PRODUK

YoHost adalah platform komputasi awan mandiri (*all-in-one web hosting & domain billing platform*) yang dirancang khusus untuk memenuhi standar operasional perusahaan web hosting modern, agensi digital, dan penyedia infrastruktur cloud. 

Platform ini dibangun dari nol (*from scratch*) dengan arsitektur **Native PHP MVC** berkinerja tinggi tanpa beban library framework pihak ketiga yang berat. Seluruh alur kerja bisnis utama—mulai dari pencarian domain, kalkulasi keranjang belanja, penerbitan tagihan instan, multi-gateway payment, otomatisasi pembuatan akun cPanel di server klaster, hingga pengelolaan record DNS mandiri—berjalan secara otomatis melalui integrasi API privat di sisi server (*Server-Side Proxy*).

### Nilai Utama & Filosofi Desain
- **Kemandirian Penuh (100% White-Label):** Seluruh layanan domain dan hosting tampil secara independen. Tidak ada nama vendor pihak ketiga yang bocor ke browser, inspect element, maupun salinan teks antarmuka.
- **Standar Visual Profesional (Zero Keyboard Emojis Rule):** Seluruh antarmuka publik, client area, dan panel admin bebas dari emoji bawaan keyboard sistem operasi. Semua elemen grafis menggunakan ikon vektor SVG resmi beresolusi tajam (*Lucide Icons*).
- **Keamanan Berlapis (Defense in Depth):** Perlindungan multi-tenant berbasis kepemilikan data pengguna (Anti-IDOR), PDO prepared statements, proteksi CSRF pada seluruh mutasi data, serta audit jejak login perangkat.
- **Layout Adaptif & Konversi Tinggi:** Halaman transaksi seperti keranjang belanja (`/cart`) otomatis menyesuaikan bentuk: menyatu dengan navigasi Client Area saat pengguna login, dan tampil bersih sebagai storefront modern saat diakses pengunjung publik.

---

## 2. ARSITEKTUR SISTEM & DESAIN PERANGKAT LUNAK

Platform mengadopsi pola arsitektur **Model-View-Controller (MVC)** kustom dengan alur permintaan terpadu (*single point of entry*):

```
                        [ Klien Peramban / Webhook Gateway ]
                                         |
                                         v
                                  [ index.php ]
                                         |
                   +---------------------+---------------------+
                   |                                           |
                   v                                           v
         [ Inisialisasi Sesi ]                       [ Error Handler ]
                   |                                           |
                   +---------------------+---------------------+
                                         |
                                         v
                                   [ App.php ]
                    (Routing Engine & Pemeliharaan Sistem)
                                         |
       +---------------------------------+---------------------------------+
       |                                 |                                 |
       v                                 v                                 v
[ Mode Pemeliharaan ]           [ URL Route Dispatcher ]          [ Filter Whitelist IP ]
       |                                 |
       v                                 v
[ maintenance.php ]           [ Controller Terpilih ]
                                         |
          +------------------------------+------------------------------+
          |                              |                              |
          v                              v                              v
  [ Auth & Keamanan ]            [ Model Layer ]                [ Helper Layer ]
  - Token CSRF                   - Transaksi Data               - Server Provisioning
  - Validasi Multi-Tenant        - Kueri Berparameter           - Registrar Proxy
  - Cek Sesi Aktif               - Business Logic               - Gateway Handler
          |                              |                              |
          +------------------------------+------------------------------+
                                         |
                                         v
                           [ Base Controller & View ]
                   - Render HTML Layouts (header / footer)
                   - Serialisasi JSON Response untuk API / AJAX
```

### Komponen Inti Arsitektur
1. **Core Router (`app/core/App.php`):**
   - Memproses segmentasi URL `$_GET['url']` secara aman.
   - Memetakan request ke Controller dan Method yang sesuai beserta parameter dinamisnya.
   - Mendeteksi status pemeliharaan situs (*Maintenance Mode*) secara dinamis dengan pengecualian IP whitelist admin.
2. **Base Controller (`app/core/Controller.php`):**
   - Mengabstraksi pemanggilan berkas tampilan (`view`), instansiasi model (`model`), dan respon API (`jsonResponse`).
   - Menerapkan isolasi tata letak antarmuka secara adaptif.
3. **Database Wrapper (`app/core/Database.php`):**
   - Menggunakan pola Singleton untuk mengelola koneksi PDO ke database.
   - Seluruh kueri wajib menggunakan prepared statements dengan binding tipe data parameter eksplisit untuk mencegah celah SQL Injection.

---

## 3. RINGKASAN MODUL & FITUR UTAMA

Platform YoHost terbagi ke dalam empat modul ekosistem terpadu:

```
+-----------------------------------------------------------------------------------+
|                            EKOSISTEM PLATFORM YOHOST                              |
+-----------------------------------------------------------------------------------+
| 1. STOREFRONT & PUBLIK       | 2. CLIENT AREA (PORTAL KLIEN)                      |
| - Katalog Cloud Hosting      | - Dashboard 4 Kolom Metrik                         |
| - Pencarian Domain Cepat     | - Actionable Expiry & Renewal Alert (<= 14 Hari)   |
| - Discovery Cart Hub         | - DNS Propagation & Health Checker Mandiri         |
| - Onboarding 6 Langkah       | - Centralized Auto-Renewal Manager (AJAX Toggle)   |
| - Pusat Pengetahuan (KB)     | - Audit Keamanan Sesi & Remote Logout Multi-Device |
| - Pelacakan Afiliasi         | - cPanel One-Click Single Sign-On (SSO)            |
| - Mobile Quick Menu          | - Manajemen Domain, Nameserver & DNS Zone Editor   |
+------------------------------+----------------------------------------------------+
| 3. TRANSAKSI & CHECKOUT      | 4. SUPERADMIN CONTROL PANEL                        |
| - Multi-Item Cart Builder    | - Analitik Finansial & Metrik MRR                  |
| - Mesin Kupon Fleksibel      | - Manajemen Klaster Server WHM/cPanel              |
| - Kalkulasi Pajak PPN 11%    | - Matriks Margin Harga Domain TLD (Modal vs Jual)  |
| - Pembayaran Multi-Gateway   | - Dispatcher Tiket Bantuan & Respon Cepat          |
| - Dompet Saldo Digital       | - Template Email Transaksional & Live Preview      |
| - Provisi Akun Otomatis      | - Pengaturan Sistem Terpusat & Mode Pemeliharaan   |
+-----------------------------------------------------------------------------------+
```

---

## 4. DEEP-DIVE FITUR CLIENT AREA (PORTAL PENGGUNA)

Portal pengguna dirancang agar pelanggan dapat mengelola seluruh infrastruktur web mereka secara mandiri (*self-service*) tanpa ketergantungan konstan pada staf bantuan:

### 4.1. Dashboard Utama & Widget Statistik 4 Kolom
- Menampilkan 4 kartu ringkasan status akun secara proporsional:
  - **Hosting Aktif:** Total akun cloud hosting yang berjalan normal pada klaster server.
  - **Domain Terdaftar:** Portofolio nama domain aktif milik pengguna.
  - **Saldo Deposit:** Saldo dompet digital internal yang siap digunakan untuk transaksi dan auto-renew.
  - **Tagihan Belum Bayar:** Jumlah faktur yang membutuhkan pelunasan beserta tombol aksi langsung.

### 4.2. Actionable Expiry & Renewal Alert
- Widget peringatan dinamis yang otomatis aktif ketika sistem mendeteksi ada layanan hosting atau domain yang masa aktifnya tersisa $\le 14$ hari atau baru kedaluwarsa dalam 7 hari terakhir.
- Dilengkapi badge hitung mundur (`H-X Hari` atau `Kedaluwarsa X hari lalu`) dan tombol satu klik untuk langsung memproses perpanjangan layanan.

### 4.3. DNS Propagation & Health Checker Mandiri
- Diagnostik kesehatan DNS mandiri di dalam dashboard (`/dashboard/dns-check`).
- Memeriksa 4 record DNS utama secara real-time via AJAX:
  - **A Record (IPv4):** Memverifikasi apakah domain mengarah ke server hosting yang sah.
  - **NS Record:** Memvalidasi konfigurasi server nama (*nameservers*).
  - **MX Record:** Memeriksa rute server pengiriman dan penerimaan email.
  - **TXT Record:** Memeriksa record SPF, DKIM, dan verifikasi kepemilikan.
- Menyajikan status kesimpulan propagasi global secara transparan.

### 4.4. Manajemen Perpanjangan Otomatis (Auto-Renewal Center)
- Panel pengelolaan terpusat pada halaman penagihan (`/dashboard/billing`).
- Merangkum seluruh hosting dan domain aktif dalam tabel rapi dengan switch toggle interaktif.
- Perubahan status auto-renewal langsung tersimpan via AJAX tanpa perlu memuat ulang halaman.

### 4.5. Audit Jejak Keamanan & Manajemen Sesi Multi-Perangkat
- Mencatat riwayat setiap aktivitas login berhasil (merekam alamat IP, peramban, sistem operasi, tipe perangkat `Desktop`/`Mobile`, dan session ID).
- Menandai sesi peramban yang sedang aktif digunakan dengan badge penanda "Sesi Ini (Aktif)".
- Menyediakan tombol **"Keluar dari Semua Perangkat Lain"** untuk memutuskan sesi di perangkat lain secara instan saat terindikasi aktivitas mencurigakan.

### 4.6. Pengelolaan Cloud Hosting & cPanel One-Click SSO
- Menampilkan grafik pemakaian ruang penyimpanan disk dan alokasi transfer data bulanan.
- Fitur **Login cPanel Satu Klik** yang memanfaatkan token sesi SSO sekali pakai, memungkinkan pelanggan masuk ke dasbor cPanel tanpa harus memasukkan kata sandi manual.
- Pengaturan reset password cPanel dan panduan koneksi FTP/Database/Email langsung dari halaman layanan.

### 4.7. Pengelolaan Domain & DNS Zone Editor
- **Nameserver Manager:** Mengubah delegasi hingga 4 server DNS dengan validasi sintaks.
- **DNS Zone Editor:** Menambah dan menghapus record DNS (A, CNAME, MX, TXT) yang otomatis tersinkronisasi ke server DNS registrar.
- **Registrar Lock:** Mengaktifkan atau menonaktifkan proteksi transfer domain (*ClientTransferProhibited*).
- **EPP Code:** Mengambil kode rahasia otorisasi transfer domain secara aman.

---

## 5. DEEP-DIVE FITUR E-COMMERCE & KERANJANG BELANJA

### 5.1. Discovery Cart Hub
- Menghadirkan antarmuka keranjang belanja yang modern dan adaptif di `/cart`:
  - **Kondisi Kosong:** Menampilkan banner hero selamat datang, form pencarian domain instan dengan tombol cepat ekstensi populer (`.com`, `.id`, `.net`, dll), 3 rekomendasi paket hosting unggulan, dan 4 kartu garansi layanan resmi.
  - **Kondisi Terisi:** Menampilkan rincian item, konfigurasi domain terhubung, siklus langganan, input kupon promo, kalkulasi PPN 11%, dan pemilihan metode bayar.

### 5.2. Navigasi Mobile Ergonomis (Menu Pintas Dropdown)
- Pada perangkat layar ponsel (`max-width: 768px`), tombol-tombol aksi sekunder yang padat diringkas ke dalam satu tombol trigger elegan **"Menu Pintas"** berikon `layout-grid`.
- Membuka panel dropdown melayang bergaya glassmorphism yang memuat akses cepat ke Tiket Bantuan, Keranjang Belanja, dan Notifikasi beserta badge penghitung aktif (*live counter*).

### 5.3. Mesin Kupon Diskon Dinamis
- Mendukung pemotongan diskon dalam bentuk persentase (`%`) maupun nilai nominal tetap (`Rp`).
- Pembatasan lingkup kupon yang fleksibel: berlaku untuk semua produk, hanya hosting, hanya domain, atau terbatas pada kategori paket tertentu.
- Validasi syarat minimal total pesanan dan batas maksimal frekuensi penggunaan.

---

## 6. DEEP-DIVE FITUR SUPERADMIN DASHBOARD

Panel Superadmin (`/admin`) memberikan kendali mutlak atas seluruh aspek operasional bisnis:

| Modul Admin | Deskripsi Fungsionalitas |
| :--- | :--- |
| **Finansial & MRR** | Grafik pertumbuhan omset, pendapatan berulang bulanan (MRR), total faktur lunas, dan tagihan tertunda. |
| **Paket Hosting** | Membuat dan mengubah paket, alokasi kuota disk/bandwidth, pemetaan nama paket WHM, dan struktur harga multi-siklus. |
| **Klaster Server** | Pendaftaran node server fisik baru, pemantauan kapasitas kuota akun, dan pengujian konektivitas API. |
| **Matriks TLD Domain** | Penetapan harga modal registrar vs harga jual ritel untuk kalkulasi otomatis margin keuntungan (markup profit). |
| **Katalog Kategori** | Pengaturan hierarki kategori dan subkategori dinamis lengkap dengan slug URL ramah SEO. |
| **Manajemen Pengguna** | Audit data pelanggan, penyesuaian saldo dompet (kredit/debit), penangguhan akun, dan fitur *Login as Client*. |
| **Tiket Bantuan** | Pusat disposisi tiket bantuan teknis, penentuan prioritas, dan template balasan cepat (*canned responses*). |
| **Template Email** | Kustomisasi kode HTML dan subjek email transaksional dengan antarmuka live preview interaktif. |
| **Pengaturan Global** | Konfigurasi SEO metadata, kredensial payment gateway, SMTP mailer, dan tombol saklar mode pemeliharaan website. |

---

## 7. OTOMASI SISTEM & BACKGROUND TASKS (CRON JOBS)

YoHost dirancang untuk berjalan secara otonom tanpa memerlukan intervensi manual untuk tugas-tugas rutin. Seluruh automasi dijalankan melalui controller background task:

```
+--------------------------------------------------------------------------------+
|                          JADWAL OTOMASI BACKGROUND TASK                        |
+--------------------------------------------------------------------------------+
| Waktu Eksekusi | Perintah Tugas             | Tindakan Sistem                  |
+----------------+----------------------------+----------------------------------+
| 00:30 WIB      | cron generate_invoices     | Menerbitkan tagihan perpanjangan |
|                |                            | otomatis H-14 masa aktif habis.  |
| 01:00 WIB      | cron process_auto_renew    | Mendebit saldo dompet pelanggan  |
|                |                            | untuk faktur berstatus auto-renew|
| 02:00 WIB      | cron suspend_overdue       | Menangguhkan akun cPanel di WHM  |
|                |                            | untuk layanan yang menunggak bayar|
| 04:00 WIB      | cron sync_domains          | Sinkronisasi masa aktif & status |
|                |                            | domain langsung ke registrar.    |
| Setiap 5 Menit | cron check_uptime          | Memeriksa keterjangkauan port    |
|                |                            | server (HTTP, SSH, cPanel, MySQL)|
| Minggu 03:00   | cron terminate_expired     | Menghapus akun cPanel menunggak  |
|                |                            | yang melewati toleransi akhir.   |
+----------------+----------------------------+----------------------------------+
```

---

## 8. KEAMANAN, PRIVASI & INTEGRITAS DATA

### 8.1. Pencegahan Insecure Direct Object References (Anti-IDOR)
Setiap permintaan modifikasi atau peninjauan data spesifik (layanan hosting, detail domain, faktur, tiket) diikat secara ketat pada `user_id` yang tersimpan dalam sesi autentikasi server. Akses silang antar pengguna dicegah secara mutlak pada lapisan controller.

### 8.2. Proteksi SQL Injection & XSS
- Seluruh komunikasi basis data wajib menggunakan PDO Prepared Statements dengan parameter binding bertipe data eksplisit.
- Seluruh data masukan yang ditampilkan kembali ke peramban disanitasi menggunakan fungsi penyandi entitas HTML berstandar `UTF-8`.

### 8.3. Proteksi CSRF & Hashing Kriptografis
- Setiap formulir mutasi data (POST/PUT/DELETE) menyertakan token CSRF unik yang divalidasi ketat sebelum pemrosesan logika bisnis.
- Kata sandi pengguna diamankan menggunakan algoritma **BCRYPT** dengan faktor biaya (*cost factor*) standar industri.

### 8.4. Isolasi Komunikasi API (Server-Side Proxy)
Seluruh komunikasi dengan API registrar eksternal, server klaster cPanel/WHM, dan gerbang pembayaran berlangsung secara murni dari backend server PHP. Tidak ada kunci rahasia, token akses, atau URL pihak ketiga yang dikirimkan ke peramban pengguna.

---

## 9. PANDUAN DEPLOYMENT & KONFIGURASI LINGKUNGAN

### 9.1. Persyaratan Server Minimal
- **Sistem Operasi:** Linux (Ubuntu 20.04/22.04 LTS, AlmaLinux 8/9, Rocky Linux) atau Windows Server.
- **Web Server:** Apache 2.4+ (dengan `mod_rewrite` aktif) atau Nginx 1.20+ (dengan `php-fpm`).
- **PHP Version:** PHP 8.1, 8.2, atau 8.3.
- **Database:** MySQL 8.0+ atau MariaDB 10.4+ (Mesin InnoDB, Charset `utf8mb4`).
- **Ekstensi PHP Wajib:** `pdo`, `pdo_mysql`, `curl`, `openssl`, `mbstring`, `json`, `sockets`, `gd` / `imagick`, `zip`.

### 9.2. Format Konfigurasi Lingkungan
Salin berkas template konfigurasi pada direktori aplikasi dan sesuaikan parameter berikut:

```php
<?php
// Konfigurasi Basis Data
define('DB_HOST', 'localhost');
define('DB_NAME', 'nama_database_anda');
define('DB_USER', 'username_database_anda');
define('DB_PASS', 'kata_sandi_database_rahasia');

// Konfigurasi Aplikasi & URL
define('BASE_URL', 'https://domain-anda.com');
define('APP_NAME', 'Nama Brand Hosting Anda');
define('APP_ENV', 'production'); // 'development' untuk debugging lokal, 'production' untuk server rilis

// Kunci Enkripsi Sesi & Keamanan
define('ENCRYPTION_KEY', 'buat_kunci_acak_kriptografi_32_karakter_di_sini');
```

### 9.3. Konfigurasi Penjadwalan Crontab Linux
Tambahkan entri berikut pada crontab user web server (`crontab -e`):

```bash
# Penerbitan Tagihan Otomatis H-14 (Setiap hari pukul 00:30)
30 0 * * * /usr/bin/php /jalur/ke/proyek/anda/index.php cron generate_invoices > /dev/null 2>&1

# Pemotongan Saldo Auto-Renew (Setiap hari pukul 01:00)
0 1 * * * /usr/bin/php /jalur/ke/proyek/anda/index.php cron process_auto_renew > /dev/null 2>&1

# Suspensi Layanan Menunggak (Setiap hari pukul 02:00)
0 2 * * * /usr/bin/php /jalur/ke/proyek/anda/index.php cron suspend_overdue > /dev/null 2>&1

# Sinkronisasi Domain Registrar (Setiap hari pukul 04:00)
0 4 * * * /usr/bin/php /jalur/ke/proyek/anda/index.php cron sync_domains > /dev/null 2>&1

# Pengecekan Kesehatan Port Server (Setiap 5 menit)
*/5 * * * * /usr/bin/php /jalur/ke/proyek/anda/index.php cron check_uptime > /dev/null 2>&1
```

---

## 10. HISTORI PENGEMBANGAN & LOG RILIS

Rincian lengkap perjalanan rilis teknis dari Bab 01 hingga Bab 34 terdokumentasi secara terperinci pada berkas **[NEW_FEATURE_LIST.md](NEW_FEATURE_LIST.md)**. 

### Rangkuman Pembaruan Terkini:
- **v3.4.2 (12 September 2026):**
  - Redesain komprehensif halaman keranjang belanja (`/cart`) menjadi Discovery Conversion Hub dengan form pencarian domain langsung dan kartu jaminan garansi.
  - Penyelarasan tata letak adaptif `/cart` (Client Area mode vs Storefront Publik).
  - Optimasi header mobile via tombol dropdown **"Menu Pintas"** (`layout-grid`).
  - Pembersihan total seluruh referensi vendor pihak ketiga demi integritas **100% White-Label Registrar**.
  - Peniadaan total emoji keyboard bawaan (*Zero Keyboard Emojis Rule*) digantikan oleh pustaka vektor SVG resmi Lucide.
  - Perbaikan fatal error method alias `getUserDomains()` dan penyesuaian parameter dinamis linter PHP.

---

## 11. HAK CIPTA & KEPEMILIKAN

Platform ini merupakan perangkat lunak berlisensi komersial independen yang dikembangkan dan dipelihara oleh:

**YoHost Cloud Technologies Inc.**  
Hak Cipta (c) 2026 Seluruh Hak Dilindungi Undang-Undang.  
Setiap penggandaan, distribusi ulang, atau pemanfaatan tanpa izin resmi dilarang keras.
