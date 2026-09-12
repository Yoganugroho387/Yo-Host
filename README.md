# YOHOST ENTERPRISE CLOUD WEB HOSTING, DOMAIN AUTOMATION & BILLING PLATFORM

Dokumentasi Teknis Lengkap Arsitektur Sistem, Modul Bisnis, Skema Database, API Integrasi, dan Panduan Operasional

Versi Rilis: v3.4.2 (Production Stable)  
Pembaruan Terakhir: 12 September 2026  
Lisensi: Proprietary - YoHost Cloud Technologies Inc.  
Standar Antarmuka: Zero Keyboard Emojis (Vektor SVG Murni / Lucide Icons)  
Integritas Brand: 100% White-Label Independent Registrar & Cloud Infrastructure  

---

## DAFTAR ISI

1. IKHTISAR SISTEM DAN FILOSOFI PENGEMBANGAN
   1.1. Latar Belakang dan Tujuan Platform
   1.2. Pilar Utama Arsitektur Sistem
   1.3. Prinsip Desain: Zero Keyboard Emojis Rule
   1.4. Prinsip Privasi: 100% White-Label Vendor Masking

2. STACK TEKNOLOGI DAN DEPENDENSI
   2.1. Backend Core & Bahasa Pemrograman
   2.2. Manajemen Database & Mesin Penyimpanan
   2.3. Frontend & Desain UI/UX
   2.4. Integrasi Protokol & Eksternal APIs
   2.5. Persyaratan Server Minimal & Ekstensi PHP

3. ARSITEKTUR PERANGKAT LUNAK DAN ALUR DISPATCHING
   3.1. Pola Model-View-Controller (MVC) Kustom
   3.2. Lifecycle Request dan URL Routing Engine (App.php)
   3.3. Base Controller dan Abstraksi Render Layout
   3.4. Database Connection Wrapper (PDO Singleton)
   3.5. Mekanisme Pemeliharaan Sistem (Maintenance Mode Engine)

4. STRUKTUR DIREKTORI DAN ORGANISASI REPOSITORI
   4.1. Direktori Inti Aplikasi (/app)
   4.2. Direktori Aset Publik (/assets)
   4.3. Direktori Skrip Pemeliharaan & Pengujian (/scratch)
   4.4. Arsip Migrasi Database SQL (/sql)

5. SKEMA DATABASE DAN MODEL DATA (28 MODEL INTI)
   5.1. Manajemen Akun dan Identitas (UserModel, LoginLogModel)
   5.2. Layanan Hosting dan Server (SubscriptionModel, PlanModel, ServerModel, ServerStatusModel)
   5.3. Manajemen Domain dan TLD (DomainModel, DomainTldModel)
   5.4. E-Commerce, Transaksi, dan Keranjang (CartModel, OrderModel, InvoiceModel, CouponModel, PromotionModel)
   5.5. Pengelompokan Layanan (CategoryModel, SubcategoryModel)
   5.6. Bantuan, Komunikasi, dan Pengetahuan (TicketModel, LiveChatModel, KbModel, NotificationModel)
   5.7. Program Afiliasi dan Migrasi (ReferralModel, MigrationModel, WaitlistModel)
   5.8. Konfigurasi, Template, dan Audit (SettingModel, EmailTemplateModel, ApiLogModel, BannerModel, MaintenanceScheduleModel)

6. SUBSISTEM HELPER DAN INTEGRASI EKSTERNAL
   6.1. WHMHelper: Otomasi cPanel & Server Hosting Cluster
   6.2. DewabizHelper: Integrasi Registrar Server-Side Proxy
   6.3. PaymentHelper: Multi-Gateway Payment Processing
   6.4. MailHelper & cPanelMailHelper: Sistem Notifikasi Email
   6.5. AuthHelper: Otentikasi, Enkripsi, dan Manajemen Sesi
   6.6. TotpHelper: Two-Factor Authentication (2FA RFC 6238)
   6.7. UptimeHelper: Pemantauan Port Layanan Jaringan Real-Time
   6.8. WhoisHelper: Resolusi Protokol Port 43 Socket WHOIS
   6.9. SecurityHelper & ValidationHelper: Sanitasi Input & CSRF
   6.10. ToastHelper: Penanganan Notifikasi Flash Sesi

7. MODUL CLIENT AREA (PORTAL PENGGUNA)
   7.1. Dashboard Utama & Widget Statistik 4 Kolom
   7.2. Actionable Expiry & Renewal Alert (Masa Tenggang <= 14 Hari)
   7.3. DNS Propagation & Health Checker Mandiri
   7.4. Manajemen Perpanjangan Otomatis (Auto-Renewal Center)
   7.5. Audit Jejak Keamanan & Pemutus Sesi Jarak Jauh (Remote Logout)
   7.6. Pengelolaan Layanan Cloud Hosting & cPanel One-Click SSO
   7.7. Pengelolaan Domain, DNS Zone Editor, Nameserver & EPP Code
   7.8. Dompet Deposit Saldo (YoHost Wallet) & Riwayat Transaksi
   7.9. Modul Permintaan Migrasi Hosting Gratis
   7.10. Program Afiliasi, Referral Link, dan Pencairan Komisi
   7.11. Profil Pengguna, Profil Kontak WHOIS, dan Keamanan 2FA

8. MODUL E-COMMERCE, KERANJANG, DAN CHECKOUT
   8.1. Arsitektur Layout Adaptif /cart (Client Area vs Storefront Publik)
   8.2. Discovery Cart Hub pada Kondisi Keranjang Kosong
   8.3. Pencarian Domain Instan & Rekomendasi Ekstensi Populer
   8.4. Mesin Kupon Diskon Dinamis (Persentase, Nominal, Scope, Multi-Use)
   8.5. Kalkulasi Pajak PPN 11% dan Grand Total Otomatis
   8.6. Alur Checkout Multi-Metode Pembayaran
   8.7. Otomasi Aktivasi Layanan Instan Pasca Pembayaran Sukses

9. MODUL SUPERADMIN DASHBOARD (PUSAT KENDALI OPERASIONAL)
   9.1. Ringkasan Finansial, Metrik MRR, dan Grafik Pertumbuhan
   9.2. Manajemen Master Paket Hosting & Mapping Package WHM
   9.3. Manajemen Server Cluster & Pemantauan Kapasitas Kuota
   9.4. Manajemen Kategori dan Subkategori Dinamis
   9.5. Penetapan Harga Modal vs Harga Jual Domain TLD (Margin Profit)
   9.6. Manajemen Data Pengguna, Hak Akses, dan Penyesuaian Saldo
   9.7. Dispatcher Tiket Bantuan & Respon Cepat Pelanggan
   9.8. Kustomisasi Template Email Transaksional & Live Preview
   9.9. Pengaturan Global (SEO, Gateway Pembayaran, SMTP, Maintenance)

10. CRON JOBS, BACKGROUND TASKS, DAN AUTOMATION WORKFLOW
    10.1. Penagihan dan Penerbitan Invoice Otomatis (H-14, H-7, H-3)
    10.2. Pemotongan Saldo Otomatis (Auto-Debit Saldo Dompet)
    10.3. Penangguhan Otomatis Layanan Menunggak (Auto-Suspension)
    10.4. Penghapusan Layanan Kedaluwarsa Parah (Auto-Termination)
    10.5. Sinkronisasi Masa Aktif Domain & Status Registrar
    10.6. Pengecekan Rutin Uptime Server dan Port Jaringan

11. WEBHOOKS DAN INTEGRASI PAYMENT GATEWAY
    11.1. Arsitektur Webhook Tripay (Signature HMAC SHA256)
    11.2. Arsitektur Webhook Midtrans (Status Notification Verification)
    11.3. Arsitektur Webhook Xendit (Callback Token Validation)
    11.4. Penanganan Pembayaran Manual via Transfer Bank & Bukti Bayar
    11.5. Idempotency Handling: Pencegahan Duplikasi Eksekusi Pembayaran

12. STANDAR KEAMANAN, HARDENING, DAN AUDIT INTEGRITAS
    12.1. Mitigasi Insecure Direct Object References (IDOR Multi-Tenant)
    12.2. Pencegahan SQL Injection melalui PDO Parameterized Statements
    12.3. Perlindungan Cross-Site Scripting (XSS) & HTML Purifying
    12.4. Proteksi Cross-Site Request Forgery (CSRF Tokens)
    12.5. Hashing Sandi Tingkat Lanjut (BCRYPT Cost Factor 10)
    12.6. Isolasi Server-Side Proxy pada API Eksternal

13. PANDUAN INSTALASI, DEPLOYMENT, DAN KONFIGURASI SERVER
    13.1. Persiapan Database MySQL / MariaDB
    13.2. Konfigurasi Web Server Apache (.htaccess) & Nginx (vhost)
    13.3. Menjalankan Skrip Instalasi Web (/install)
    13.4. Konfigurasi Environment & Kredensial Sistem
    13.5. Penjadwalan Linux Crontab untuk Otomasi Penuh
    13.6. Penerbitan Sertifikat SSL Let's Encrypt / Cloudflare

14. PANDUAN PENGUJIAN DAN VERIFIKASI SISTEM
    14.1. Validasi Sintaks Kode PHP (php -l)
    14.2. Pengujian Koneksi WHM/cPanel API
    14.3. Pengujian API Registrar Domain
    14.4. Pengujian Simulasi Transaksi Pembayaran Webhook
    14.5. Pengujian Pengecekan DNS dan WHOIS Socket

15. CATATAN PERJALANAN RILIS & HISTORI FITUR (BAB 01 - BAB 34)
    15.1. Evolusi Fondasi Hosting dan Penagihan (Bab 01 - Bab 10)
    15.2. Otomasi Domain, TLD Margin, dan Gateway (Bab 11 - Bab 20)
    15.3. Pemeliharaan Sistem, DNS, dan Keamanan Sesi (Bab 21 - Bab 30)
    15.4. Onboarding, Alerting, Cart Hub, dan White-Label (Bab 31 - Bab 34)

---

## 1. IKHTISAR SISTEM DAN FILOSOFI PENGEMBANGAN

### 1.1. Latar Belakang dan Tujuan Platform
YoHost adalah platform komputasi awan tingkat lanjut yang dirancang khusus untuk memfasilitasi operasional penyedia web hosting, pendaftaran domain, dan penagihan otomatis berskala enterprise. Sistem ini dibangun secara mandiri (*custom-built*) menggunakan arsitektur PHP murni berkecepatan tinggi tanpa beban ketergantungan framework pihak ketiga yang membengkak, sehingga memberikan efisiensi eksekusi yang optimal, waktu respons server di bawah 100 milidetik, serta kendali penuh atas keamanan data.

Tujuan utama platform meliputi:
- Menyediakan automasi siklus hidup hosting secara menyeluruh: pemesanan, verifikasi pembayaran real-time, pembuatan akun cPanel instan di server cluster, pengiriman kredensial, suspensi keterlambatan, hingga terminasi otomatis.
- Menyediakan platform registrasi domain independen dengan integrasi registrar otomatis tanpa memperlihatkan identitas vendor backend kepada pengguna akhir.
- Memberikan antarmuka Client Area yang modern, intuitif, berestetika tinggi, dan ramah pengguna di semua perangkat.
- Menyajikan panel Superadmin terpusat yang komprehensif untuk tata kelola finansial, kupon promo, pengelolaan server cluster, tiket bantuan, dan diagnostik teknis.

### 1.2. Pilar Utama Arsitektur Sistem
Platform dibangun di atas lima pilar rekayasa perangkat lunak:
1. **High Performance & Low Latency:** Menghindari abstraksi ORM yang berat. Seluruh kueri basis data dioptimalkan menggunakan PDO Prepared Statements dengan indeks tabel yang terukur.
2. **Absolute Multi-Tenant Security:** Mengisolasi data pengguna secara ketat. Seluruh operasi manipulasi layanan (hosting, domain, tiket, invoice, profil) wajib menyertakan validasi kepemilikan ganda berbasis ID sesi terotentikasi.
3. **Full Automation Lifecycle:** Mengeliminasi intervensi manual dalam proses rutin. Penerbitan tagihan, perpanjangan otomatis dengan saldo dompet, pembuatan akun hosting WHM, dan pendaftaran domain berjalan secara otomatis melalui background cron tasks.
4. **Resilient Self-Healing Infrastructure:** Skema basis data dilengkapi mekanisme deteksi dan migrasi otomatis untuk kolom atau tabel baru yang hilang pada saat runtime, mencegah kegagalan fatal pada lingkungan produksi.
5. **Universal Device Accessibility:** Tampilan responsif murni yang didesain secara spesifik untuk pengalaman desktop, tablet, dan smartphone dengan navigasi ergonomis.

### 1.3. Prinsip Desain: Zero Keyboard Emojis Rule
Standar estetika YoHost mewajibkan peniadaan mutlak simbol emoji unicode keyboard bawaan sistem operasi (misalnya simbol roket, keranjang belanja, gembok, atau globe mentah). Seluruh elemen grafis, indikator status, dan ikon visual diwajibkan menggunakan vektor SVG resmi dari pustaka **Lucide Icons** dengan ketajaman rendering yang konsisten di semua peramban, kontras warna yang harmonis, dan skalabilitas resolusi layar tinggi (Retina/High-DPI).

### 1.4. Prinsip Privasi: 100% White-Label Vendor Masking
YoHost beroperasi sebagai entitas registrar domain dan cloud hosting mandiri. Seluruh vendor hulu (*upstream registrar* seperti Dewabiz) disterilkan secara total dari penglihatan pengguna akhir:
- Tidak ada teks brand vendor pada footer, profil WHOIS, judul modal, maupun keterangan halaman.
- Tidak ada flash message atau peringatan sistem yang menyebut nama vendor pihak ketiga.
- Seluruh interaksi API ke server upstream berlangsung murni di sisi backend server PHP (*Server-Side Proxy via cURL*). Browser pengguna tidak pernah melakukan kontak jaringan langsung ke server vendor, sehingga pada saat pemeriksaan *Inspect Element Network Tab*, tidak ada URL atau endpoint pihak ketiga yang bocor.
- Dokumentasi dan komunikasi klien menggunakan istilah resmi netral: "Registrar Domain Resmi", "Server DNS Domain", dan "ICANN / PANDI".

---

## 2. STACK TEKNOLOGI DAN DEPENDENSI

### 2.1. Backend Core & Bahasa Pemrograman
- **Bahasa Utama:** PHP 8.1 / 8.2 / 8.3 Native (Object-Oriented Programming).
- **Arsitektur:** Custom Light MVC (Model-View-Controller) dengan Single Point of Entry (`index.php`).
- **Penanganan Sesi:** PHP Native Session Management dengan konfigurasi aman (`cookie_httponly`, `use_strict_mode`, `cookie_samesite`).
- **Autentikasi:** Enkripsi kata sandi berbasis BCRYPT (`PASSWORD_BCRYPT`) dengan cost factor dinamis.
- **Dukungan 2FA:** Two-Factor Authentication berbasis RFC 6238 Time-Based One-Time Password (TOTP).

### 2.2. Manajemen Database & Mesin Penyimpanan
- **Sistem Manajemen Basis Data:** MySQL 8.0+ / MariaDB 10.4+.
- **Engine Tabel:** InnoDB (Mendukung ACID Compliance, Foreign Keys, dan Row-Level Locking).
- **Karakter Set:** `utf8mb4` dengan Collation `utf8mb4_unicode_ci` untuk kompatibilitas multibyte penuh.
- **Akses Data:** PHP Data Objects (PDO) dengan mode error exception aktif (`PDO::ATTR_ERRMODE_EXCEPTION`) dan prepared statements bawaan (`PDO::ATTR_EMULATE_PREPARES => false`).

### 2.3. Frontend & Desain UI/UX
- **Desain Kerangka Visual:** HTML5 Semantik dengan styling utility TailwindCSS.
- **Tipografi:** Google Fonts berlisensi terbuka (*Plus Jakarta Sans* untuk heading & teks modern, *Inter* untuk elemen data terstruktur).
- **Ikonografi:** Lucide Icons (Render SVG Client-Side & Embedded Vectors).
- **Palet Warna Identitas:**
  - Primary Brand: `#353893` (Deep Indigo)
  - Primary Dark: `#272a72`
  - Accent Color: `#19C37D` (Emerald Success Green)
  - Tertiary / Warning: `#FF7A21` (Vibrant Coral Orange)
  - Neutral Background: `#F8FAFC` / `#F4F6FB`
  - Border Line: `#E2E8F0`

### 2.4. Integrasi Protokol & Eksternal APIs
- **cPanel & WHM API v1:** Komunikasi REST JSON via HTTPS Port 2087 dengan token otentikasi Bearer API WHM.
- **Domain Registrar API:** REST JSON Client via HTTPS dengan Basic Authentication dan custom header token.
- **Tripay Payment Gateway:** REST API v2 dengan verifikasi signature HMAC SHA256.
- **Midtrans Payment Gateway:** Snap API & Core Notification Webhook.
- **Xendit Payment Gateway:** Invoice API & Webhook Verification Token.
- **Protokol Jaringan Socket:** Native PHP Socket (`fsockopen`) untuk kueri WHOIS Port 43 dan deteksi port server (Port 80 HTTP, 443 HTTPS, 22 SSH, 3306 MySQL, 25/587 SMTP).
- **SMTP Mailer:** Native socket / PHPMailer untuk pengiriman email transaksional dengan enkripsi TLS/SSL.

### 2.5. Persyaratan Server Minimal & Ekstensi PHP
- **Sistem Operasi:** Linux (Ubuntu 20.04/22.04 LTS, AlmaLinux 8/9, Rocky Linux) atau Windows Server (Laragon / IIS).
- **Web Server:** Apache 2.4+ (dengan modul `mod_rewrite`) atau Nginx 1.20+ (dengan `php-fpm`).
- **RAM Minimal:** 1 GB (Direkomendasikan 2 GB+ untuk lingkungan produksi aktif).
- **Ekstensi PHP Wajib:**
  - `pdo` dan `pdo_mysql` (Konektivitas basis data).
  - `curl` (Komunikasi API eksternal).
  - `openssl` (Enkripsi data, token CSRF, dan koneksi TLS).
  - `mbstring` (Pemrosesan karakter multibyte).
  - `json` (Serialisasi data API).
  - `sockets` (Kueri WHOIS port 43 dan port health-check).
  - `gd` atau `imagick` (Pemrosesan gambar profil, avatar, dan QR Code 2FA).
  - `zip` (Ekstraksi dan backup sistem).

---

## 3. ARSITEKTUR PERANGKAT LUNAK DAN ALUR DISPATCHING

### 3.1. Pola Model-View-Controller (MVC) Kustom
YoHost menggunakan implementasi pola arsitektur MVC yang ringkas namun tangguh:
- **Core Engine (`/app/core/`):** Menyediakan kerangka dasar yang mengontrol alur eksekusi aplikasi tanpa library eksternal. Terdiri dari `App.php`, `Controller.php`, `Database.php`, dan `Model.php`.
- **Model Layer (`/app/models/`):** Bertanggung jawab atas integritas logika bisnis, aturan validasi data, serta interaksi kueri basis data. Setiap model mewakili satu entitas data tabel utama.
- **View Layer (`/app/views/`):** Mengelola antarmuka pengguna yang disajikan ke browser. Terbagi ke dalam direktori publik, autentikasi, client dashboard, panel admin, pusat bantuan, dan tata letak bersama (*layouts*).
- **Controller Layer (`/app/controllers/`):** Menerima permintaan HTTP yang telah diuraikan oleh router, memverifikasi sesi dan hak akses, berkoordinasi dengan model dan helper, lalu merender view atau mengembalikan respon JSON.

### 3.2. Lifecycle Request dan URL Routing Engine (App.php)
Seluruh lalu lintas permintaan web masuk melalui berkas gerbang tunggal `index.php`. Berkas ini memicu inisialisasi kelas router `App.php` yang menjalankan alur kerja sistem:

```
[ HTTP Request Masuk ]
         |
         v
[ index.php (Inisialisasi Session, Error Handler, Config) ]
         |
         v
[ App.php Router Engine ]
         |--> 1. Pemeriksaan Mode Pemeliharaan (Maintenance Mode)
         |--> 2. Sanitasi & Penguraian Parameter URL ($_GET['url'])
         |--> 3. Resolusi Mapping Controller & File Existence Check
         |--> 4. Instansiasi Controller Terpilih
         |--> 5. Resolusi Nama Method / Aksi & Pengiriman Parameter Dinamis
         |
         v
[ Eksekusi Method Controller ]
         |--> Verifikasi Autentikasi / Sesi (AuthHelper)
         |--> Proteksi CSRF pada Operasi POST/PUT/DELETE
         |--> Pemanggilan Logika Model / Helper
         |
         v
[ Output Rendering: HTML View Layout atau JSON Response ]
```

Aturan default routing:
- URL kosong (`/`) diarahkan ke `HomeController@index`.
- URL satu segmen (misal `/cart`) diarahkan ke `CartController@index`.
- URL dua segmen (misal `/dashboard/domains`) diarahkan ke `DashboardController@domains`.
- URL tiga segmen dengan parameter dinamis (misal `/dashboard/domain/manage/15`) diarahkan ke `DashboardController@domainManage` dengan parameter `15`.
- URL rute admin (misal `/admin/plans/edit/2`) diarahkan ke `AdminController@plansEdit` dengan parameter `2`.

### 3.3. Base Controller dan Abstraksi Render Layout
Kelas dasar `Controller.php` menyediakan fungsionalitas inti yang diwarisi oleh semua controller:
- `view($viewPath, $data = [])`: Mengekstrak array asosiatif `$data` menjadi variabel lokal PHP dan memuat berkas view yang dituju.
- `model($modelName)`: Melakukan instansiasi model yang diminta secara dinamis dengan caching instansiasi jika diperlukan.
- `jsonResponse($data, $statusCode = 200)`: Mengirimkan header `Content-Type: application/json`, mengatur kode status HTTP, dan mengeluarkan payload JSON yang telah diserialisasi.
- `redirect($url)`: Mengirim header pengalihan `Location:` dan menghentikan eksekusi skrip seketika (`exit()`).

### 3.4. Database Connection Wrapper (PDO Singleton)
Kelas `Database.php` mengimplementasikan pola Singleton untuk memastikan koneksi basis data MySQL hanya dibuat satu kali per siklus permintaan (request lifecycle), menghemat alokasi memori dan mencegah saturasi sambungan basis data (*max connections limit*).

Fitur penting wrapper basis data:
- Mengonfigurasi atribut PDO untuk keamanan maksimal.
- Mengatur time zone koneksi basis data agar sinkron dengan waktu server lokal (`+07:00` WIB).
- Menyediakan metode pembantu kueri terparameterisasi:
  - `query($sql)`: Mempersiapkan statement SQL.
  - `bind($param, $value, $type = null)`: Menentukan tipe data parameter secara eksplisit (`PDO::PARAM_INT`, `PDO::PARAM_STR`, `PDO::PARAM_BOOL`, `PDO::PARAM_NULL`).
  - `execute()`: Menjalankan prepared statement.
  - `resultSet()`: Mengembalikan seluruh baris data sebagai array objek atau array asosiatif.
  - `single()`: Mengembalikan tepat satu baris data pertama.
  - `rowCount()`: Mengembalikan jumlah baris yang terpengaruh oleh operasi kueri.
  - `lastInsertId()`: Mengembalikan ID auto-increment dari data terakhir yang tersimpan.

### 3.5. Mekanisme Pemeliharaan Sistem (Maintenance Mode Engine)
YoHost dilengkapi subsistem proteksi mode pemeliharaan website yang dapat diaktifkan secara instan melalui panel Superadmin tanpa mematikan web server:
- Ketika `maintenance_mode = 1` di database, seluruh pengunjung publik otomatis dialihkan ke halaman pemeliharaan visual elegan di `app/views/public/maintenance.php`.
- **Whitelist IP Administrator:** Sistem mengizinkan alamat IP yang terdaftar pada tabel pengaturan untuk tetap dapat mengakses seluruh situs secara normal untuk keperluan inspeksi.
- **Akses Login Khusus Admin:** Terdapat jalur bypass autentikasi darurat di `/login?maintenance_bypass=1` yang memungkinkan administrator masuk dan menonaktifkan status pemeliharaan setelah pekerjaan selesai.

---

## 4. STRUKTUR DIREKTORI DAN ORGANISASI REPOSITORI

```
c:/laragon/www/hostyo/
|-- app/
|   |-- config/
|   |   `-- config.php                  # Kredensial Database, Base URL, Kunci Enkripsi
|   |-- controllers/
|   |   |-- AdminController.php         # Operasional Superadmin (126 KB, Modul Master)
|   |   |-- AuthController.php          # Login, Registrasi, Lupa Sandi, 2FA, Verifikasi
|   |   |-- BillingController.php       # Invoice, Pembayaran, Kwitansi PDF, Konfirmasi
|   |   |-- CartController.php          # Discovery Hub, Kupon, Kalkulasi PPN, Checkout
|   |   |-- CouponApiController.php     # Endpoint AJAX Validasi Kupon Diskon Real-Time
|   |   |-- CronController.php          # Otomasi Penagihan, Suspensi, Terminasi, Auto-Renew
|   |   |-- DashboardController.php     # Portal Client Area Lengkap (143 KB)
|   |   |-- HomeController.php          # Landing Page, Pricelist Domain, Syarat Ketentuan
|   |   |-- InstallationController.php  # Setup Wizard Instalasi Awal Sistem
|   |   |-- KbController.php            # Pusat Pengetahuan & Artikel Panduan
|   |   |-- LiveChatController.php      # Sesi Obrolan Langsung Pelanggan Real-Time
|   |   |-- SupportController.php       # Manajemen Tiket Bantuan & Lampiran Berkas
|   |   `-- WebhookController.php       # Respon Callback Gateway (Tripay, Midtrans, Xendit)
|   |-- core/
|   |   |-- App.php                     # Router Utama, Request Dispatcher & URL Parser
|   |   |-- Controller.php              # Abstraksi Base Controller & Renderer View
|   |   |-- Database.php                # PDO Wrapper Singleton & Parameter Binder
|   |   `-- Model.php                   # Abstraksi Model Dasar
|   |-- helpers/
|   |   |-- AuthHelper.php              # Pengendali Sesi, Token Remember, Audit Login
|   |   |-- ConfigHelper.php            # Pengambilan Nilai Pengaturan Ter-cache
|   |   |-- DewabizHelper.php           # API Registrar Domain (White-Label Server Proxy)
|   |   |-- EmailSecurityHelper.php     # Sanitasi Header & Proteksi Mail Injection
|   |   |-- MailHelper.php              # Pengirim Email SMTP Transaksional
|   |   |-- PaymentHelper.php           # Generator Signature & Gateway Invoicing
|   |   |-- SecurityHelper.php          # Sanitasi XSS & Token CSRF Generator
|   |   |-- ToastHelper.php             # Flash Message Berbasis Sesi
|   |   |-- TotpHelper.php              # RFC 6238 Generator & Verifier 2FA Authenticator
|   |   |-- UptimeHelper.php            # Monitor Port Server (HTTP, SSH, MySQL, cPanel)
|   |   |-- ValidationHelper.php        # Validasi Format Domain, Email, dan Telepon
|   |   |-- WHMHelper.php               # Otomasi cPanel API v1 (82 KB, Cluster Manager)
|   |   |-- WhoisHelper.php             # Resolusi Port 43 Socket WHOIS Domain
|   |   `-- cPanelMailHelper.php        # Integrasi Webmail & Akun Email Hosting
|   |-- models/
|   |   |-- AnnouncementModel.php       # Pengumuman Publik & Internal
|   |   |-- ApiLogModel.php             # Pencatatan Request & Response API Eksternal
|   |   |-- BannerModel.php             # Banner Promosi Beranda
|   |   |-- CartModel.php               # Penyimpanan Item Keranjang Pengguna & Sesi
|   |   |-- CategoryModel.php           # Master Kategori Layanan Hosting
|   |   |-- CouponModel.php             # Diskon, Kupon Promo, Batas Pemakaian
|   |   |-- DomainModel.php             # Data Domain Pengguna, Nameserver, Status Kunci
|   |   |-- DomainTldModel.php          # Penetapan Harga Modal vs Jual Ekstensi TLD
|   |   |-- EmailTemplateModel.php      # Master Template Email Transaksional (47 KB)
|   |   |-- InvoiceModel.php            # Faktur Tagihan, Item Rincian, Status Pembayaran
|   |   |-- KbModel.php                 # Artikel Knowledgebase & Kategori Bantuan
|   |   |-- LiveChatModel.php           # Log Percakapan Live Chat
|   |   |-- LoginLogModel.php           # Audit Trail Sesi Login, IP, Perangkat, Browser
|   |   |-- MaintenanceScheduleModel.php# Penjadwalan Pemeliharaan Server Terencana
|   |   |-- MigrationModel.php          # Antrian Permintaan Transfer Hosting Gratis
|   |   |-- NotificationModel.php       # Notifikasi In-App Pengguna & Administrator
|   |   |-- OrderModel.php              # Pesanan Layanan Baru & Riwayat Checkout
|   |   |-- PlanModel.php               # Paket Layanan Cloud Hosting, Kuota, Siklus Bayar
|   |   |-- PromotionModel.php          # Banner Promo Spesial
|   |   |-- ReferralModel.php           # Komisi Afiliasi, Riwayat Klik, Permintaan Cair
|   |   |-- ServerModel.php             # Master Server WHM, Kredensial Token, Kuota Akun
|   |   |-- ServerStatusModel.php       # Log Pemantauan Uptime Server Berkala
|   |   |-- SettingModel.php            # Kunci Konfigurasi Global Sistem
|   |   |-- SubcategoryModel.php        # Subkategori Layanan Dinamis
|   |   |-- SubscriptionModel.php       # Langganan Hosting Aktif, cPanel User, Auto-Renew
|   |   |-- TicketModel.php             # Tiket Dukungan Teknis & Balasan Diskusi
|   |   |-- UserModel.php               # Akun Pengguna, Saldo Dompet, Role, Hash Sandi
|   |   `-- WaitlistModel.php           # Daftar Tunggu Notifikasi Paket Habis
|   `-- views/
|       |-- admin/                      # Seluruh Tampilan Dashboard Superadmin
|       |-- auth/                       # Halaman Login, Register, Lupa Sandi, 2FA
|       |-- dashboard/                  # Seluruh Tampilan Client Area Pengguna
|       |-- install/                    # Tampilan Panduan Wizard Instalasi
|       |-- kb/                         # Tampilan Direktori Knowledgebase
|       |-- layouts/                    # Layout Bersama: header.php, footer.php
|       `-- public/                     # Landing Page, Syarat Ketentuan, Maintenance
|-- assets/                             # File CSS, JavaScript, Favicon, Vektor SVG
|-- scratch/                            # Alat Bantu Diagnostik & Pengemasan Rilis ZIP
|-- beda.html                           # Halaman Showcase Fitur Bergaya Play Store
|-- NEW_FEATURE_LIST.md                 # Rekam Jejak Dokumentasi Fitur Bab 01 - Bab 34
|-- README.md                           # Dokumentasi Komprehensif Sistem (Berkas Ini)
`-- index.php                           # Gerbang Utama Eksekusi Aplikasi
```

---

## 5. SKEMA DATABASE DAN MODEL DATA (28 MODEL INTI)

### 5.1. Manajemen Akun dan Identitas

#### UserModel (`users`)
Model fundamental yang menyimpan seluruh entitas pengguna, baik pelanggan reguler maupun superadmin.
- `id` (INT, Primary Key, Auto Increment): Pengenal unik akun.
- `name` (VARCHAR 100): Nama lengkap pengguna.
- `email` (VARCHAR 100, Unique Index): Alamat email terverifikasi untuk login dan korespondensi.
- `password` (VARCHAR 255): Hash kata sandi BCRYPT.
- `phone` (VARCHAR 20): Nomor telepon seluler atau WhatsApp.
- `role` (ENUM 'client', 'admin'): Penentu hak akses hak istimewa sistem.
- `balance` (DECIMAL 15,2, Default 0.00): Saldo dompet digital internal (*YoHost Wallet*).
- `status` (ENUM 'active', 'suspended', 'unverified'): Status operasional akun.
- `two_factor_secret` (VARCHAR 64, Nullable): Kunci rahasia Base32 untuk verifikasi TOTP Google Authenticator.
- `two_factor_enabled` (TINYINT 1, Default 0): Status proteksi keamanan 2FA aktif/nonaktif.
- `referral_code` (VARCHAR 32, Unique Index): Kode tautan unik program afiliasi pelanggan.
- `referred_by` (INT, Nullable): ID pengguna perujuk yang berhak menerima komisi.
- `created_at`, `updated_at` (DATETIME): Timestamp rekaman data.

#### LoginLogModel (`user_login_logs`)
Mencatat jejak audit keamanan seluruh aktivitas sesi masuk ke sistem. Dilengkapi skrip self-healing migration otomatis saat runtime.
- `id` (INT, Primary Key, Auto Increment).
- `user_id` (INT, Index): Relasi ke `users.id`.
- `ip_address` (VARCHAR 45): Alamat IP sumber (mendukung format IPv4 dan IPv6).
- `user_agent` (TEXT): String User-Agent lengkap dari peramban.
- `device_type` (VARCHAR 50): Klasifikasi perangkat (`Desktop`, `Mobile`, `Tablet`).
- `browser` (VARCHAR 100): Nama dan versi peramban (Chrome, Firefox, Safari, Edge).
- `platform` (VARCHAR 100): Sistem operasi (Windows, macOS, Linux, Android, iOS).
- `status` (VARCHAR 20): Status percobaan login (`success`, `failed`).
- `session_id` (VARCHAR 128, Index): ID sesi aktif PHP untuk keperluan terminasi jarak jauh.
- `created_at` (DATETIME, Index): Waktu terjadinya aktivitas autentikasi.

### 5.2. Layanan Hosting dan Server

#### SubscriptionModel (`subscriptions`)
Mengelola data instansi layanan hosting aktif yang terpasang pada klaster server cPanel/WHM.
- `id` (INT, Primary Key, Auto Increment).
- `user_id` (INT, Index): Relasi ke pemilik layanan.
- `plan_id` (INT, Index): Relasi ke master paket hosting `plans.id`.
- `server_id` (INT, Index): Relasi ke server fisik/VPS `servers.id`.
- `domain` (VARCHAR 150): Domain primer yang terhubung pada akun hosting.
- `username` (VARCHAR 16): Username akun cPanel pada server WHM.
- `status` (ENUM 'active', 'suspended', 'terminated', 'pending'): Status operasional layanan.
- `billing_cycle` (ENUM 'monthly', 'quarterly', 'semi-annually', 'annually', 'biennially', 'triennially').
- `price` (DECIMAL 15,2): Nilai nominal perpanjangan berkala.
- `auto_renew` (TINYINT 1, Default 1): Preferensi perpanjangan otomatis via saldo dompet.
- `start_date` (DATE): Tanggal aktivasi perdana layanan.
- `expiry_date` (DATE, Index): Tanggal jatuh tempo masa aktif hosting.
- `termination_date` (DATE, Nullable): Batas toleransi sebelum penghapusan data akun cPanel permanen.

#### PlanModel (`plans`)
Menyimpan konfigurasi paket web hosting yang ditawarkan kepada pelanggan.
- `id` (INT, Primary Key, Auto Increment).
- `category_id` (INT, Index): Relasi ke kategori layanan.
- `subcategory_id` (INT, Nullable, Index): Relasi ke subkategori layanan.
- `name` (VARCHAR 100): Nama paket (contoh: Cloud Starter, Turbo Enterprise).
- `slug` (VARCHAR 100, Unique): Slug URL ramah SEO.
- `description` (TEXT): Rincian keunggulan dan spesifikasi paket.
- `whm_package_name` (VARCHAR 100): Nama paket resmi yang terkonfigurasi di server WHM.
- `price_monthly`, `price_annually`, dll (DECIMAL 15,2): Matriks harga berdasarkan siklus tagihan.
- `disk_space` (INT): Alokasi ruang penyimpanan dalam satuan Megabyte (MB) atau 0 untuk unlimited.
- `bandwidth` (INT): Batas kuota transfer data bulanan dalam satuan Megabyte (MB).
- `is_featured` (TINYINT 1, Default 0): Penanda paket terpopuler pada antarmuka beranda.
- `status` (ENUM 'active', 'inactive'): Status keterlihatan paket pada storefront.

#### ServerModel (`servers`)
Menyimpan kredensial klaster server cPanel/WHM untuk alokasi otomatis akun hosting baru.
- `id` (INT, Primary Key, Auto Increment).
- `name` (VARCHAR 100): Nama identifikasi server (contoh: Node-01 SG, Node-02 JKT).
- `hostname` (VARCHAR 150): FQDN server (contoh: srv1.yohost.net).
- `ip_address` (VARCHAR 45): Alamat IP publik server.
- `whm_username` (VARCHAR 50): Username administrator WHM (biasanya `root`).
- `whm_api_token` (TEXT): Token API WHM yang terenkripsi untuk otentikasi API v1.
- `nameserver_1`, `nameserver_2` (VARCHAR 100): Nameserver bawaan server klaster.
- `max_accounts` (INT): Batas kuota maksimal akun cPanel sebelum dialihkan ke node server berikutnya.
- `current_accounts` (INT, Default 0): Jumlah akun aktif saat ini pada server.
- `status` (ENUM 'active', 'full', 'maintenance', 'disabled').

#### ServerStatusModel (`server_statuses`)
Merekam metrik historis kesehatan server dan pemantauan port layanan secara real-time.
- `id` (INT, Primary Key, Auto Increment).
- `server_id` (INT, Index): Relasi ke `servers.id`.
- `service_name` (VARCHAR 50): Nama layanan (HTTP, HTTPS, SSH, cPanel, MySQL, SMTP).
- `port` (INT): Nomor port yang dipantau (80, 443, 22, 2083, 3306, 587).
- `is_online` (TINYINT 1): Status ketercapaian koneksi (1 = Terhubung, 0 = Terputus).
- `response_time_ms` (INT): Waktu respon latensi jaringan dalam milidetik.
- `checked_at` (DATETIME, Index): Waktu eksekusi pengecekan.

### 5.3. Manajemen Domain dan TLD

#### DomainModel (`domains`)
Menyimpan portofolio nama domain milik pelanggan yang terdaftar di sistem.
- `id` (INT, Primary Key, Auto Increment).
- `user_id` (INT, Index): Relasi ke akun pemilik domain.
- `domain_name` (VARCHAR 150, Index): Nama domain lengkap (contoh: bisnisonline.com).
- `registration_period` (INT, Default 1): Durasi pendaftaran dalam tahun.
- `price` (DECIMAL 15,2): Nilai perpanjangan tahunan.
- `status` (ENUM 'active', 'pending', 'expired', 'transferred_out').
- `auto_renew` (TINYINT 1, Default 1): Status perpanjangan otomatis via saldo dompet.
- `registration_date` (DATE): Tanggal pendaftaran perdana di registrar.
- `expiry_date` (DATE, Index): Tanggal jatuh tempo kedaluwarsa domain.
- `nameserver_1` hingga `nameserver_4` (VARCHAR 150): Delegasi server DNS domain.
- `whois_privacy` (TINYINT 1, Default 0): Status perlindungan proteksi privasi WHOIS.
- `registrar_lock` (TINYINT 1, Default 1): Kunci proteksi transfer domain (*Transfer Lock*).
- `epp_code` (VARCHAR 100, Nullable): Kode otorisasi transfer domain.
- `whois_profile_id` (INT, Nullable): Relasi ke data profil kontak pendaftar resmi.

#### DomainTldModel (`domain_tlds`)
Mengatur penetapan harga modal dasar registrar versus harga jual konsumen serta margin profit untuk setiap ekstensi TLD.
- `id` (INT, Primary Key, Auto Increment).
- `tld` (VARCHAR 30, Unique Index): Ekstensi domain (contoh: `.com`, `.id`, `.co.id`, `.net`).
- `cost_price` (DECIMAL 15,2): Harga modal dasar yang dibebankan oleh upstream registrar.
- `selling_price` (DECIMAL 15,2): Harga jual ritel pendaftaran tahun pertama.
- `renewal_price` (DECIMAL 15,2): Harga jual ritel perpanjangan tahunan berikutnya.
- `transfer_price` (DECIMAL 15,2): Biaya transfer masuk domain dari provider lain.
- `is_popular` (TINYINT 1, Default 0): Tanda chip sorotan pada kotak pencarian cepat.
- `is_promo` (TINYINT 1, Default 0): Status pemberlakuan harga promosi spesial.
- `promo_price` (DECIMAL 15,2, Nullable): Harga khusus diskon terbatas.
- `status` (ENUM 'active', 'disabled').

### 5.4. E-Commerce, Transaksi, dan Keranjang

#### InvoiceModel (`invoices`) & OrderModel (`orders`)
Pusat pencatatan seluruh tagihan finansial, transaksi langganan, dan checkout produk.
- `id` (INT, Primary Key, Auto Increment).
- `invoice_number` (VARCHAR 50, Unique Index): Nomor faktur resmi (contoh: INV-202609-00821).
- `user_id` (INT, Index): Relasi ke akun pelanggan.
- `subtotal` (DECIMAL 15,2): Total nilai sebelum pemotongan diskon kupon.
- `discount` (DECIMAL 15,2, Default 0.00): Potongan nilai kupon promosi.
- `tax` (DECIMAL 15,2, Default 0.00): Nilai Pajak Pertambahan Nilai (PPN 11%).
- `total` (DECIMAL 15,2): Grand total kewajiban bayar yang sah.
- `payment_method` (VARCHAR 50): Saluran bayar (Tripay, Midtrans, Xendit, Wallet, Manual Transfer).
- `payment_channel` (VARCHAR 50): Kode kanal spesifik (BCAVA, BRIVA, QRIS, MANDIRIVA).
- `status` (ENUM 'unpaid', 'paid', 'expired', 'cancelled', 'refunded').
- `payment_reference` (VARCHAR 150, Index): ID referensi transaksi eksternal dari gateway.
- `checkout_payload` (LONGTEXT, Nullable): Serialisasi JSON data pesanan produk dan konfigurasi domain.
- `paid_at` (DATETIME, Nullable): Waktu penyelesaian pelunasan pembayaran.
- `due_date` (DATE, Index): Batas waktu toleransi pelunasan faktur.
- `created_at` (DATETIME, Index).

#### CartModel (`cart_items`)
Menyimpan state keranjang belanja sebelum transaksi di-checkout. Mendukung persistensi ganda: bound ke `user_id` untuk pengguna terotentikasi, atau bound ke `session_id` untuk tamu publik.
- `id` (INT, Primary Key, Auto Increment).
- `user_id` (INT, Nullable, Index).
- `session_id` (VARCHAR 128, Index).
- `type` (ENUM 'hosting', 'domain', 'addon').
- `item_id` (INT, Nullable): Relasi ke ID paket hosting `plans.id` atau ID TLD.
- `domain` (VARCHAR 150, Nullable): Nama domain yang dikonfigurasikan.
- `billing_cycle` (VARCHAR 50, Default 'annually').
- `price` (DECIMAL 15,2): Harga sewa item.
- `config_options` (TEXT, Nullable): Serialisasi JSON preferensi tambahan (SSL, IP Dedicated).
- `created_at` (DATETIME).

#### CouponModel (`coupons`)
Mengatur aturan pemotongan diskon promosi dengan validasi kombinasi ketat.
- `id` (INT, Primary Key, Auto Increment).
- `code` (VARCHAR 50, Unique Index): Kode voucher (contoh: HEMATMERDEKA, YOHOSTPROMO).
- `type` (ENUM 'percentage', 'fixed'): Tipe pemotongan (Persentase % atau Nominal Tetap Rp).
- `value` (DECIMAL 15,2): Nilai potongan diskon.
- `scope` (ENUM 'all', 'hosting_only', 'domain_only', 'category'): Pembatasan lingkup produk.
- `target_id` (INT, Nullable): ID target kategori atau paket tertentu.
- `min_order_amount` (DECIMAL 15,2, Default 0.00): Syarat belanja minimum.
- `max_uses` (INT, Default 0): Kuota kupon maksimal sistem (0 = Tanpa batas).
- `used_count` (INT, Default 0): Jumlah kupon yang telah berhasil ditebus pelanggan.
- `start_date`, `end_date` (DATETIME): Masa berlaku kupon promosi.
- `is_active` (TINYINT 1, Default 1).

### 5.5. Pengelompokan Layanan

#### CategoryModel (`categories`) & SubcategoryModel (`subcategories`)
Menyediakan hierarki katalog produk bertingkat dua dengan slug SEO ramah pengguna.
- `categories`: `id`, `name`, `slug`, `description`, `icon`, `sort_order`, `status`.
- `subcategories`: `id`, `category_id`, `name`, `slug`, `description`, `sort_order`, `status`.

### 5.6. Bantuan, Komunikasi, dan Pengetahuan

#### TicketModel (`tickets`, `ticket_replies`)
Manajemen tiket bantuan teknis pelanggan dengan alur percakapan threaded dan lampiran berkas.
- `tickets`: `id`, `ticket_number`, `user_id`, `department`, `priority` ('low', 'medium', 'high', 'urgent'), `service_type`, `subject`, `status` ('open', 'answered', 'customer-reply', 'closed'), `last_reply_at`, `created_at`.
- `ticket_replies`: `id`, `ticket_id`, `user_id`, `message`, `attachment_path`, `is_admin`, `created_at`.

#### LiveChatModel (`live_chat_sessions`, `live_chat_messages`)
Sistem komunikasi obrolan langsung real-time berbasis polling AJAX asinkronus antara pelanggan dan tim dukungan YoHost.

#### KbModel (`kb_categories`, `kb_articles`)
Manajemen pusat bantuan mandiri (Knowledgebase) lengkap dengan fitur pencarian teks lengkap, penghitung jumlah pembaca (*view counter*), dan penilaian kebergunaan artikel (*helpful votes*).

#### NotificationModel (`notifications`)
Notifikasi in-app real-time untuk memberitahukan peristiwa penting (invoice terbit, akun cPanel aktif, peringatan domain jatuh tempo, status tiket dibalas).

### 5.7. Program Afiliasi dan Migrasi

#### ReferralModel (`referrals`, `referral_payouts`)
Pengelolaan program mitra afiliasi YoHost:
- Pelacakan klik link afiliasi unik `?ref=KODE`.
- Penghitungan komisi otomatis saat pendaftar baru melakukan pelunasan invoice perdana.
- Modul permohonan penarikan dana komisi (*payout request*) ke rekening bank lokal pelanggan.

#### MigrationModel (`migrations`)
Alur kerja pemindahan hosting gratis dari penyedia lama ke server YoHost:
- Pengguna memasukkan kredensial login cPanel provider asal (URL cPanel, Username, Password).
- Staf teknis menerima antrian, memvalidasi cadangan full backup, merestorasi ke server YoHost, dan mengubah status migrasi menjadi 'completed'.

#### WaitlistModel (`waitlists`)
Mencatat antrian email pelanggan yang berminat pada paket hosting yang kuotanya sedang penuh. Sistem otomatis mengirimkan notifikasi email ketika kuota paket kembali tersedia.

### 5.8. Konfigurasi, Template, dan Audit

#### SettingModel (`settings`)
Menyimpan konfigurasi pasangan kunci-nilai (*key-value pairs*) untuk seluruh parameter sistem tanpa perlu mengubah baris kode program.

#### EmailTemplateModel (`email_templates`)
Master template email transaksional dengan antarmuka editor HTML interaktif, dukungan variabel dinamis `{user_name}`, `{invoice_number}`, `{domain_name}`, `{cpanel_user}`, `{expiry_date}`, serta fungsi uji kirim (*test email preview*).

#### ApiLogModel (`api_logs`)
Pencatatan rekam jejak komunikasi API eksternal (cURL requests/responses) untuk memudahkan investigasi kesalahan teknis, audit timeout, dan pemantauan gateway.

---

## 6. SUBSISTEM HELPER DAN INTEGRASI EKSTERNAL

### 6.1. WHMHelper: Otomasi cPanel & Server Hosting Cluster
Berkas [WHMHelper.php](file:///c:/laragon/www/hostyo/app/helpers/WHMHelper.php) (82 KB) adalah modul pengendali orkestrasi klaster server hosting. Seluruh panggilan memanfaatkan WHM API v1 via HTTPS port 2087 dengan otentikasi Bearer Token.

Fungsi utama WHMHelper:
- `createAccount($serverId, $userData, $planData)`: Memeriksa ketersediaan kuota server, menyeleksi node terbaik, lalu mengeksekusi pembuatan akun cPanel baru lengkap dengan penetapan limitasi ruang disk, bandwidth, akun email, database MySQL, dan alokasi domain.
- `suspendAccount($serverId, $username, $reason)`: Menangguhkan akses akun cPanel dan menampilkan halaman penangguhan bawaan jika pelanggan menunggak pembayaran tagihan.
- `unsuspendAccount($serverId, $username)`: Membuka kembali status penangguhan secara instan segera setelah pembayaran faktur perpanjangan terkonfirmasi.
- `terminateAccount($serverId, $username)`: Menghapus akun cPanel secara permanen dari server klaster jika masa tenggang terminasi terlampaui.
- `changePackage($serverId, $username, $newPackageName)`: Mengubah alokasi kuota paket cPanel saat pelanggan melakukan upgrade atau downgrade layanan secara instan tanpa downtime situs.
- `createCpanelUserSession($serverId, $username)`: Menghasilkan token sesi Single Sign-On (SSO) sekali pakai yang memungkinkan pelanggan masuk ke dasbor cPanel mereka secara langsung dari portal Client Area tanpa perlu mengetik kata sandi.

### 6.2. DewabizHelper: Integrasi Registrar Server-Side Proxy
Berkas [DewabizHelper.php](file:///c:/laragon/www/hostyo/app/helpers/DewabizHelper.php) bertindak sebagai *Server-Side Proxy Client* yang menghubungkan sistem YoHost dengan upstream registrar secara aman dan terisolasi.

Karakteristik penting DewabizHelper:
- **Zero Client Leak:** Tidak ada kredensial, URL registrar, atau ID reseller yang dikirimkan ke peramban pengguna. Semua permintaan dilakukan melalui fungsi cURL privat PHP di sisi server.
- **Dynamic Method Invocation:** Menghindari pemanggilan string literal pada opsi `CURLOPT_CUSTOMREQUEST` untuk menjamin kepatuhan linter PHP dan mengeliminasi false positive *call to unknown function*.
- **Fungsi Operasional Domain:**
  - `checkDomainAvailability($domain)`: Memeriksa status ketersediaan domain secara real-time.
  - `registerDomain($domain, $years, $whoisProfile, $nameservers)`: Mendaftarkan nama domain baru melalui API resmi registrar.
  - `renewDomain($domain, $years)`: Memperpanjang masa aktif pendaftaran domain.
  - `updateNameservers($domain, $nsArray)`: Mengubah delegasi server DNS domain.
  - `getDnsRecords($domain)`: Mengambil seluruh daftar DNS Zone Records domain dari server DNS registrar.
  - `addDnsRecord($domain, $recordData)`: Menambahkan record baru (A, CNAME, MX, TXT, AAAA, SRV).
  - `deleteDnsRecord($domain, $recordId)`: Menghapus record DNS tertentu.
  - `toggleRegistrarLock($domain, $status)`: Mengaktifkan atau menonaktifkan status kunci transfer domain (*ClientTransferProhibited*).
  - `getEppCode($domain)`: Mengambil kode otorisasi transfer EPP domain secara aman.

### 6.3. PaymentHelper: Multi-Gateway Payment Processing
Berkas [PaymentHelper.php](file:///c:/laragon/www/hostyo/app/helpers/PaymentHelper.php) mengabstraksikan pemrosesan transaksi pembayaran multi-gateway:
- **Tripay Integration:** Menghasilkan payload transaksi kanal Tertutup (*Closed Payment*) dengan signature keamanan `hash_hmac('sha256', $merchantCode . $merchantRef . $amount, $privateKey)`. Mengembalikan instruksi bayar, kode Virtual Account (VA), atau QRIS string.
- **Midtrans Snap:** Menghasilkan token transaksi Snap untuk antarmuka pembayaran popup terintegrasi.
- **Xendit Invoice:** Mengirimkan permintaan pembuatan faktur pembayaran online dengan redirect URL resmi.
- **YoHost Internal Wallet:** Memvalidasi kecukupan saldo dompet pengguna (`users.balance >= invoice.total`), melakukan pemotongan saldo secara atomik dengan database transaction lock, dan langsung menandai status faktur sebagai `paid`.

### 6.4. MailHelper & cPanelMailHelper: Sistem Notifikasi Email
- **MailHelper:** Memuat template email HTML dari basis data, menyuntikkan variabel dinamis kontekstual, dan mengirimkan pesan melalui protokol SMTP terenkripsi dengan penanganan error fallback.
- **cPanelMailHelper:** Mengintegrasikan pengelolaan kotak surat email domain (Webmail) yang terhubung ke cPanel, memungkinkan pembuatan akun email baru (`info@domainanda.com`), perubahan kuota kotak surat, dan reset sandi email langsung dari dashboard YoHost.

### 6.5. AuthHelper: Otentikasi, Enkripsi, dan Manajemen Sesi
Mengelola siklus hidup sesi pengguna:
- `login($userId, $remember = false)`: Mengenerasi ulang ID sesi baru (`session_regenerate_id(true)`) demi mencegah serangan *Session Fixation*, menetapkan data sesi penting, menginisialisasi cookie remember-me berbasis token kriptografi acak, dan memanggil `LoginLogModel` untuk mencatat metadata audit login perangkat.
- `logout()`: Menghapus seluruh variabel sesi, merotasi ID sesi, menghapus cookie remember-me di browser, dan mengakhiri sesi pengguna secara bersih.
- `logoutOtherSessions($userId)`: Memutuskan seluruh sesi login akun di peramban atau perangkat lain berdasarkan perbandingan `session_id`, mengamankan akun dari potensi pembajakan sesi jarak jauh.

### 6.6. TotpHelper: Two-Factor Authentication (2FA RFC 6238)
Mengimplementasikan algoritma otentikasi dua faktor standar industri:
- Menghasilkan kunci rahasia acak Base32 16-karakter.
- Menghasilkan URL format `otpauth://totp/YoHost:user@email?secret=...&issuer=YoHost` untuk dipindai oleh aplikasi otentikator (Google Authenticator, Microsoft Authenticator, Authy).
- Memverifikasi kode 6-digit dengan toleransi drift waktu $\pm 1$ langkah periode waktu (30 detik).

### 6.7. UptimeHelper: Pemantauan Port Layanan Jaringan Real-Time
Menguji keterjangkauan port jaringan server fisik secara asinkronus menggunakan koneksi socket murni dengan batas waktu timeout ketat (2 detik), memastikan dasbor pemantauan kesehatan server dapat menampilkan status online/offline setiap node tanpa membebani performa aplikasi.

### 6.8. WhoisHelper: Resolusi Protokol Port 43 Socket WHOIS
Melakukan kueri langsung ke server WHOIS resmi di port 43 (seperti `whois.verisign-grs.com` untuk `.com` atau `whois.pandi.id` untuk `.id`), mengurai teks keluaran mentah untuk memvalidasi tanggal kedaluwarsa, nameserver aktif, dan ketersediaan domain secara independen dari API komersial.

### 6.9. SecurityHelper & ValidationHelper: Sanitasi Input & CSRF
- **SecurityHelper:** Menyediakan token CSRF kriptografis unik berbasis sesi (`$_SESSION['csrf_token']`), memverifikasi kecocokan token pada setiap request POST non-webhook, serta melakukan sanitasi teks anti-XSS melalui `htmlspecialchars` dengan flag `ENT_QUOTES | ENT_HTML5`.
- **ValidationHelper:** Memvalidasi format sintaksis nama domain yang sah (panjang 3–63 karakter, alphanumeric, tanda hubung di tengah, TLD terdaftar), validasi nomor ponsel WhatsApp, dan validasi ekspresi reguler email RFC 5322.

### 6.10. ToastHelper: Penanganan Notifikasi Flash Sesi
Menyimpan dan mengambil pesan notifikasi sementara dalam sesi (`$_SESSION['toast_success']`, `$_SESSION['toast_error']`) yang otomatis ditampilkan dan dihapus setelah halaman selesai dimuat di browser.

---

## 7. MODUL CLIENT AREA (PORTAL PENGGUNA)

### 7.1. Dashboard Utama & Widget Statistik 4 Kolom
Halaman beranda portal pengguna (`/dashboard`) menyajikan pusat informasi performa akun dalam format grid responsif 4 kolom yang seimbang:
1. **Hosting Aktif (Ikon `server`):** Menampilkan jumlah langganan cloud hosting yang berstatus aktif dan terhubung ke klaster cPanel.
2. **Domain Terdaftar (Ikon `globe`):** Menampilkan total nama domain aktif milik akun yang dikelola pada sistem.
3. **Saldo Deposit (Ikon `wallet`):** Menampilkan saldo dompet digital pengguna saat ini, lengkap dengan tombol akses instan "Top Up Saldo".
4. **Tagihan Belum Bayar (Ikon `receipt`):** Menampilkan jumlah invoice berstatus unpaid yang memerlukan pelunasan beserta tombol aksi cepat menuju rincian tagihan.

### 7.2. Actionable Expiry & Renewal Alert (Masa Tenggang <= 14 Hari)
Sistem secara cerdas memindai seluruh layanan hosting dan domain milik pengguna. Jika terdapat item yang memiliki masa aktif $\le 14$ hari atau telah kedaluwarsa dalam 7 hari terakhir, dashboard otomatis memunculkan banner peringatan dinamis:
- Menampilkan rincian nama domain atau layanan hosting dengan ikon pembeda.
- Menampilkan badge waktu jatuh tempo proporsional (`H-X Hari` atau `Kedaluwarsa X hari lalu`).
- Menyediakan tombol aksi satu klik "Perpanjang" yang langsung mengarahkan pengguna ke alur pembuatan invoice perpanjangan instan.

### 7.3. DNS Propagation & Health Checker Mandiri
Fitur diagnostik mandiri di `/dashboard/dns-check` memungkinkan pengguna memeriksa propagasi DNS domain mereka secara instan tanpa membuka alat pihak ketiga:
- Pengguna dapat memilih domain aktif mereka melalui pill chips atau mengetikkan nama domain kustom.
- Sistem mengeksekusi kueri asinkronus via AJAX (`/dashboard/dns-check/lookup`) untuk 4 record kritis:
  - **A Record (IPv4):** Memverifikasi apakah domain sudah mengarah ke IP Server YoHost (`103.59.160.21`).
  - **NS Record:** Memeriksa kesesuaian delegasi Nameserver terhadap standar YoHost (`ns1.yohost.net`, `ns2.yohost.net`).
  - **MX Record:** Memeriksa rute server penanganan email domain.
  - **TXT Record:** Memeriksa konfigurasi verifikasi domain, SPF, dan DKIM.
- Menampilkan kesimpulan status propagasi instan (*Propagasi Sempurna* vs *Sedang Berlangsung*).

### 7.4. Manajemen Perpanjangan Otomatis (Auto-Renewal Center)
Halaman penagihan (`/dashboard/billing`) dilengkapi kartu pengelolaan Auto-Renewal terpusat:
- Merangkum seluruh hosting dan domain aktif dalam tabel interaktif.
- Dilengkapi tombol switch toggle AJAX (`/dashboard/auto-renew/toggle`) yang memperbarui preferensi auto-renew secara instan tanpa perlu memuat ulang halaman.
- Nilai preferensi (1/0) langsung tersimpan ke database pada tabel `subscriptions` maupun `domains`.

### 7.5. Audit Jejak Keamanan & Pemutus Sesi Jarak Jauh (Remote Logout)
Pada halaman profil pengguna (`/dashboard/profile`):
- Menampilkan daftar riwayat aktivitas login terbaru dengan detail alamat IP, jenis perangkat (Desktop, Mobile, Tablet dengan ikon spesifik), peramban, sistem operasi, dan waktu aktivitas relatif.
- Menandai sesi peramban yang sedang aktif dengan badge hijau "Sesi Ini (Aktif)".
- Menyediakan tombol keamanan darurat **"Keluar dari Semua Perangkat Lain"** (`/dashboard/profile/logout-other-sessions`) untuk memutus seluruh sesi login lain saat dicurigai ada akses tanpa izin.

### 7.6. Pengelolaan Layanan Cloud Hosting & cPanel One-Click SSO
Pada halaman detail hosting (`/dashboard/service/manage/{id}`):
- Menampilkan alokasi ruang penyimpanan disk dan kuota bandwidth dengan grafik visual.
- Tombol **"Login ke cPanel"** yang memanfaatkan API token SSO WHM untuk membuka sesi cPanel pengguna secara instan di tab baru tanpa input password manual.
- Penggantian kata sandi cPanel langsung dari antarmuka YoHost.
- Rincian informasi koneksi FTP, database MySQL, dan panduan konfigurasi email klien (Outlook, Thunderbird, Apple Mail).

### 7.7. Pengelolaan Domain, DNS Zone Editor, Nameserver & EPP Code
Pada halaman pengelolaan domain (`/dashboard/domain/manage/{id}`):
- **Nameserver Manager:** Mengubah delegasi 4 server nama DNS domain dengan validasi format FQDN.
- **DNS Zone Editor:** Menambah, melihat, dan menghapus record DNS (A, CNAME, MX, TXT) secara real-time yang tersinkronisasi ke server DNS registrar.
- **Registrar Lock Toggle:** Mengunci atau membuka status proteksi transfer domain.
- **EPP Code Request:** Menampilkan kode rahasia transfer domain untuk otorisasi perpindahan domain.
- **Profil WHOIS:** Memperbarui data kontak nama, alamat, nomor telepon, dan email pemilik domain.

### 7.8. Dompet Deposit Saldo (YoHost Wallet) & Riwayat Transaksi
Pengguna dapat mengisi ulang saldo dompet (*Top Up Balance*) melalui berbagai kanal pembayaran otomatis. Saldo dompet dapat digunakan untuk:
- Pembayaran instan invoice baru tanpa biaya admin tambahan gateway.
- Pemotongan otomatis tagihan perpanjangan (*Auto-Debit Renewal*) pada saat jatuh tempo layanan.

### 7.9. Modul Permintaan Migrasi Hosting Gratis
Pelanggan dapat mengajukan permintaan transfer data hosting dari penyedia lama melalui formulir `/dashboard/migration`. Sistem merekam URL login, username, dan password cPanel lama secara terenkripsi untuk diproses oleh teknisi YoHost.

### 7.10. Program Afiliasi, Referral Link, dan Pencairan Komisi
Setiap pelanggan memiliki tautan rujukan unik (`https://yohost.net/?ref=KODE`). Sistem merekam klik via cookie browser 30 hari. Ketika pengguna baru mendaftar dan membayar tagihan hosting, komisi persentase otomatis masuk ke saldo afiliasi pelanggan. Pelanggan dapat mengajukan penarikan dana (*withdraw*) ke rekening bank setelah mencapai ambang batas minimum.

### 7.11. Profil Pengguna, Profil Kontak WHOIS, dan Keamanan 2FA
Pengaturan lengkap akun pelanggan yang mencakup data diri, alamat penagihan, aktivasi proteksi Two-Factor Authentication (2FA) dengan pemindaian kode QR, dan perubahan kata sandi terotentikasi.

---

## 8. MODUL E-COMMERCE, KERANJANG, DAN CHECKOUT

### 8.1. Arsitektur Layout Adaptif /cart (Client Area vs Storefront Publik)
Sistem menerapkan rendering layout bersyarat (*conditional layout architecture*) pada berkas `header.php`, `footer.php`, dan `cart/index.php`:
- **Pengguna Terautentikasi (Logged-In User):** Halaman `/cart` otomatis menyatu dengan ekosistem Client Area penuh: memuat `dashboard/layout_header.php`, menampilkan sidebar portal klien, kontainer terstruktur, dan footer minimal dashboard. Navigasi publik dan footer raksasa landing page ditiadakan agar fokus transaksi tidak terganggu.
- **Pengunjung Publik (Guest):** Halaman `/cart` menyajikan tampilan storefront publik elegan: header navigasi publik, kontainer penuh terpusat (`max-w-6xl mx-auto`), dan footer publik lengkap.

### 8.2. Discovery Cart Hub pada Kondisi Keranjang Kosong
Menghilangkan tampilan lama yang polos dan menggantikannya dengan pusat konversi modern (*Discovery & Conversion Hub*):
- **Hero Banner Interaktif:** Berlatar gradien indigo lembut dengan ikon Lucide `shopping-bag` animasi pulse dan ajakan eksplorasi produk.
- **Form Pencarian Domain Terintegrasi:** Kotak pencarian domain instan langsung di halaman keranjang belanja yang mengarah ke `/domain-search`, lengkap dengan pill filter TLD terpopuler (`.com`, `.id`, `.net`, `.org`, `.biz.id`).
- **Pilihan Paket Hosting Unggulan (3 Kolom):** Rekomendasi paket Cloud Starter, Pro Business, dan Turbo Enterprise lengkap dengan rincian spesifikasi, badge harga transparan, dan tombol CTA "Pilih Paket".
- **Kartu Nilai Keunggulan (Trust Cards):** 4 jaminan layanan resmi dengan ikon Lucide: Garansi Uang Kembali 30 Hari (`award`), Aktivasi Instan 60 Detik (`zap`), Bantuan Teknis 24/7 (`headset`), dan Uptime SLA 99.9% (`shield-check`).

### 8.3. Pencarian Domain Instan & Rekomendasi Ekstensi Populer
Fitur pencarian domain publik dan dashboard yang terhubung ke kueri ketersediaan registrar. Jika domain incaran telah terdaftar, sistem secara otomatis memberikan alternatif ekstensi lain (.id, .net, .org, .xyz, .my.id) yang masih tersedia beserta rincian biaya registrasinya.

### 8.4. Mesin Kupon Diskon Dinamis
Pelanggan dapat memasukkan kode kupon diskon pada ringkasan pesanan keranjang belanja. Validasi dilakukan secara asinkronus via endpoint AJAX `/cart/apply-coupon`:
- Memeriksa tanggal kadaluwarsa kupon.
- Memeriksa batas kuota pemakaian global dan riwayat pemakaian akun.
- Memeriksa syarat minimal nominal transaksi belanja.
- Memeriksa lingkup produk (*scope*): hanya berlaku untuk hosting, domain, atau kategori tertentu.
- Menerapkan pemotongan persentase (%) atau nominal tetap (Rp) secara otomatis.

### 8.5. Kalkulasi Pajak PPN 11% dan Grand Total Otomatis
Sistem menghitung nilai subtotal pesanan, memotong diskon kupon yang valid, menghitung Pajak Pertambahan Nilai (PPN 11%) sesuai regulasi perpajakan yang berlaku, dan menetapkan grand total kewajiban bayar secara transparan.

### 8.6. Alur Checkout Multi-Metode Pembayaran
Saat pengguna menekan tombol "Lanjutkan ke Pembayaran":
- Sistem membuat rekaman data pada tabel `orders` dan menerbitkan nomor faktur resmi pada tabel `invoices`.
- Seluruh rincian item, nama domain, durasi paket, dan preferensi server disimpan ke dalam format serialisasi JSON terstruktur pada kolom `invoices.checkout_payload`.
- Pengguna dialihkan ke halaman pembayaran tagihan `/billing/invoice/{id}` untuk memilih metode pembayaran yang dikehendaki.

### 8.7. Otomasi Aktivasi Layanan Instan Pasca Pembayaran Sukses
Segera setelah notifikasi pembayaran diterima (baik via Webhook Tripay/Midtrans/Xendit maupun pembayaran saldo dompet internal):
- Status faktur diperbarui menjadi `paid`.
- Dispatcher otomatis menguraikan payload pesanan:
  - Jika pesanan mencakup akun hosting: Sistem memanggil `WHMHelper::createAccount()` untuk membuat akun cPanel di server klaster secara instan, menyusun data langganan di tabel `subscriptions`, dan mengirimkan email berisikan kredensial login akun cPanel ke email pelanggan.
  - Jika pesanan mencakup pendaftaran domain: Sistem memanggil `DewabizHelper::registerDomain()` untuk mengeksekusi registrasi domain resmi di registrar hulu, mengonfigurasi nameserver default, dan menyusun data kepemilikan di tabel `domains`.
  - Jika pengguna memiliki perujuk afiliasi: Sistem menghitung persentase komisi dan mengkreditkan saldo komisi ke akun perujuk.

---

## 9. MODUL SUPERADMIN DASHBOARD (PUSAT KENDALI OPERASIONAL)

### 9.1. Ringkasan Finansial, Metrik MRR, dan Grafik Pertumbuhan
Dasbor Superadmin (`/admin`) menyajikan metrik analitik bisnis tingkat tinggi:
- **Pendapatan Kotor Bulanan (MRR):** Total penerimaan kas dari seluruh transaksi faktur berstatus lunas.
- **Statistik Pertumbuhan Pengguna:** Grafik pendaftaran akun baru per minggu dan per bulan.
- **Rasio Utilisasi Klaster Server:** Total akun cPanel aktif dibandingkan batas kuota maksimal kapasitas server.
- **Antrian Tiket & Migrasi:** Indikator pekerjaan tertunda yang membutuhkan penanganan staf teknis.

### 9.2. Manajemen Master Paket Hosting & Mapping Package WHM
Pengelolaan katalog produk hosting (`/admin/plans`):
- Tambah, ubah, dan nonaktifkan paket hosting.
- Pemetaan nama paket cPanel resmi (*cPanel Package Name*) di server WHM.
- Penetapan kuota ruang penyimpanan disk, bandwidth, akun email, subdomain, dan database MySQL.
- Konfigurasi struktur harga multi-siklus (Bulanan, 3 Bulanan, 6 Bulanan, Tahunan, 2 Tahunan, 3 Tahunan).

### 9.3. Manajemen Server Cluster & Pemantauan Kapasitas Kuota
Pengelolaan klaster server cPanel/WHM (`/admin/servers`):
- Mendaftarkan node server baru dengan memasukkan IP, Hostname, dan Token API WHM.
- Menetapkan batas kapasitas maksimal akun cPanel per server.
- Pengujian konektivitas API server secara langsung (*Test Connection Button*).
- Menandai server yang sedang dalam pemeliharaan (*Maintenance Mode Server*).

### 9.4. Manajemen Kategori dan Subkategori Dinamis
Mengatur hierarki katalog layanan di `/admin/categories` dan `/admin/subcategories` lengkap dengan penataan urutan tampil (*sorting order*), ikon visual, dan slug URL.

### 9.5. Penetapan Harga Modal vs Harga Jual Domain TLD (Margin Profit)
Pengelolaan matriks harga domain (`/admin/domain-tlds`):
- Menetapkan harga modal hulu (*cost price*) dari registrar.
- Menetapkan harga jual ritel pendaftaran, perpanjangan, dan transfer masuk.
- Sistem secara otomatis menghitung estimasi margin keuntungan kotor (Rp dan %) untuk setiap ekstensi domain.
- Pengaturan status ekstensi populer (*Popular Chip*) dan status promosi terbatas.

### 9.6. Manajemen Data Pengguna, Hak Akses, dan Penyesuaian Saldo
Pengelolaan akun pengguna (`/admin/users`):
- Pencarian dan filter pengguna berdasarkan nama, email, role, atau status.
- Penyesuaian saldo dompet digital pelanggan secara manual (Kredit/Debit Saldo) dengan pencatatan alasan audit.
- Penangguhan akun yang melanggar ketentuan layanan (*Suspended User*).
- Masuk ke akun pelanggan sebagai administrator (*Impersonate Login / Login as Client*) untuk mempermudah investigasi masalah teknis.

### 9.7. Dispatcher Tiket Bantuan & Respon Cepat Pelanggan
Panel penanganan tiket bantuan (`/admin/support`):
- Menyaring tiket berdasarkan status (*Open, In Progress, Answered, Closed*) dan prioritas (*Urgent, High, Medium, Low*).
- Membalas pesan pelanggan dengan dukungan template jawaban cepat (*Canned Responses*).
- Menutup atau membuka kembali tiket bantuan yang telah terselesaikan.

### 9.8. Kustomisasi Template Email Transaksional & Live Preview
Pengelolaan master template email transaksional (`/admin/email-templates`):
- Mengedit subjek dan kode HTML template email untuk seluruh skenario notifikasi: Pembuatan Faktur Baru, Konfirmasi Pembayaran Berhasil, Kredensial Akun cPanel Baru, Peringatan Domain Jatuh Tempo, Tiket Bantuan Dibalas, dan Reset Kata Sandi.
- Fitur **Live Preview** interaktif yang merender tampilan template email secara nyata di layar.
- Fitur **Kirim Email Uji Coba** untuk menguji kompatibilitas rendering template pada klien email nyata (Gmail, Outlook).

### 9.9. Pengaturan Global (SEO, Gateway Pembayaran, SMTP, Maintenance)
Pengaturan terpusat sistem (`/admin/settings`):
- **General Settings:** Nama website, logo, favicon, mata uang, zona waktu server, dan format nomor tagihan.
- **SEO & Metadata:** Judul meta bawaan, deskripsi meta, kata kunci pencarian, dan OpenGraph Image.
- **Payment Gateway Credentials:** Kunci API, Merchant ID, dan Private Key untuk Tripay, Midtrans, dan Xendit, serta pengaturan rekening bank transfer manual.
- **SMTP Configuration:** Host SMTP, port, username, password, dan jenis enkripsi (SSL/TLS).
- **Maintenance Switch:** Mengaktifkan atau menonaktifkan mode pemeliharaan website publik beserta daftar whitelist IP administrator.

---

## 10. CRON JOBS, BACKGROUND TASKS, DAN AUTOMATION WORKFLOW

Untuk mengoperasikan automasi penuh tanpa intervensi manual, YoHost mengandalkan eksekusi berkala melalui controller khusus `CronController.php`.

### 10.1. Penagihan dan Penerbitan Invoice Otomatis (H-14, H-7, H-3)
Tugas: `php index.php cron generate_invoices` (Dijalankan setiap hari pukul 00:30 WIB)
- Memindai seluruh layanan hosting dan domain aktif yang tanggal kedaluwarsanya jatuh dalam kurun waktu 14 hari ke depan.
- Memeriksa apakah sudah ada invoice yang belum terbayar untuk periode perpanjangan yang sama guna mencegah duplikasi tagihan.
- Menerbitkan invoice perpanjangan baru dan mengirimkan pemberitahuan tagihan ke email pelanggan.

### 10.2. Pemotongan Saldo Otomatis (Auto-Debit Saldo Dompet)
Tugas: `php index.php cron process_auto_renew` (Dijalankan setiap hari pukul 01:00 WIB)
- Memeriksa seluruh invoice perpanjangan berstatus unpaid milik pelanggan yang mengaktifkan opsi `auto_renew = 1`.
- Memeriksa saldo dompet pengguna (`users.balance`). Jika saldo mencukupi, sistem langsung mendebit saldo, menandai faktur sebagai lunas (`paid`), dan memicu perpanjangan otomatis layanan di server WHM atau registrar.

### 10.3. Penangguhan Otomatis Layanan Menunggak (Auto-Suspension)
Tugas: `php index.php cron suspend_overdue` (Dijalankan setiap hari pukul 02:00 WIB)
- Memindai seluruh langganan hosting aktif yang telah melewati tanggal jatuh tempo (`expiry_date < CURRENT_DATE`) dan fakturnya belum dilunasi.
- Memanggil `WHMHelper::suspendAccount()` untuk menangguhkan akun cPanel terkait di server klaster dengan alasan keterlambatan pembayaran.
- Memperbarui status langganan di database menjadi `suspended` dan mengirimkan email pemberitahuan penangguhan layanan ke pelanggan.

### 10.4. Penghapusan Layanan Kedaluwarsa Parah (Auto-Termination)
Tugas: `php index.php cron terminate_expired` (Dijalankan setiap hari Minggu pukul 03:00 WIB)
- Memindai layanan hosting yang telah berstatus `suspended` selama lebih dari masa toleransi yang ditentukan (misalnya 30 hari pasca jatuh tempo).
- Memanggil `WHMHelper::terminateAccount()` untuk menghapus akun cPanel secara permanen dari server klaster guna membebaskan ruang disk server.
- Memperbarui status layanan menjadi `terminated`.

### 10.5. Sinkronisasi Masa Aktif Domain & Status Registrar
Tugas: `php index.php cron sync_domains` (Dijalankan setiap hari pukul 04:00 WIB)
- Melakukan sinkronisasi tanggal kedaluwarsa, status kunci transfer, dan status nameserver domain terdaftar terhadap data resmi registrar via API server-side proxy.

### 10.6. Pengecekan Rutin Uptime Server dan Port Jaringan
Tugas: `php index.php cron check_uptime` (Dijalankan setiap 5 menit)
- Memeriksa keterjangkauan port HTTP, HTTPS, SSH, cPanel, MySQL, dan SMTP pada seluruh node server fisik yang terdaftar.
- Mencatat riwayat keterjangkauan ke tabel `server_statuses` untuk keperluan grafik status sistem.

---

## 11. WEBHOOKS DAN INTEGRASI PAYMENT GATEWAY

Seluruh penerimaan notifikasi status pembayaran dari payment gateway eksternal ditangani secara terpusat oleh [WebhookController.php](file:///c:/laragon/www/hostyo/app/controllers/WebhookController.php).

### 11.1. Arsitektur Webhook Tripay (Signature HMAC SHA256)
- **Endpoint:** `POST /webhook/tripay`
- **Validasi Keamanan:**
  - Membaca header `X-Callback-Event` (hanya memproses event `payment_status`).
  - Mengambil raw JSON payload dari `php://input`.
  - Menghitung signature lokal: `hash_hmac('sha256', $rawJson, $privateKey)`.
  - Membandingkan signature lokal dengan header `X-Callback-Signature`. Jika tidak cocok, sistem menolak request dengan kode status `403 Forbidden`.
- **Eksekusi Status:**
  - Jika status pembayaran adalah `PAID`: Sistem memanggil prosedur penyelesaian faktur (`processInvoicePaid`), mengaktifkan layanan hosting/domain, dan mengembalikan respon JSON `{"success": true}`.

### 11.2. Arsitektur Webhook Midtrans (Status Notification Verification)
- **Endpoint:** `POST /webhook/midtrans`
- **Validasi Keamanan:**
  - Menghitung hash SHA512: `hash('sha512', $orderId . $statusCode . $grossAmount . $serverKey)`.
  - Membandingkan hasil hash terhadap parameter `signature_key` dari Midtrans.
- **Eksekusi Status:**
  - Memproses status transaksi: `settlement` atau `capture` (dengan status `accept`) ditandai sebagai `paid`. Status `cancel`, `expire`, atau `deny` ditandai sebagai `cancelled` atau `expired`.

### 11.3. Arsitektur Webhook Xendit (Callback Token Validation)
- **Endpoint:** `POST /webhook/xendit`
- **Validasi Keamanan:**
  - Membandingkan header `x-callback-token` dengan token verifikasi webhook yang tersimpan pada pengaturan sistem.
- **Eksekusi Status:**
  - Jika status invoice adalah `PAID` atau `SETTLED`, memicu aktivasi layanan terkait.

### 11.4. Penanganan Pembayaran Manual via Transfer Bank & Bukti Bayar
Untuk pelanggan yang memilih metode transfer bank manual:
- Pelanggan mengunggah berkas bukti transfer (*receipt image*) melalui portal tagihan.
- Faktur berubah status menjadi `pending_verification`.
- Superadmin menerima notifikasi di dashboard admin untuk memverifikasi keabsahan dana masuk pada mutasi rekening bank sebelum menekan tombol "Konfirmasi Lunas".

### 11.5. Idempotency Handling: Pencegahan Duplikasi Eksekusi Pembayaran
Seluruh metode webhook menerapkan proteksi **Idempotensi Transaksi**:
- Sebelum memproses aktivasi layanan, sistem memeriksa status faktur saat ini di basis data.
- Jika status faktur sudah berstatus `paid`, proses penyediaan layanan diabaikan dan webhook langsung mengembalikan respon sukses `200 OK`. Hal ini mencegah penggandaan pembuatan akun cPanel atau duplikasi komisi afiliasi akibat pengiriman ulang callback dari payment gateway.

---

## 12. STANDAR KEAMANAN, HARDENING, DAN AUDIT INTEGRITAS

### 12.1. Mitigasi Insecure Direct Object References (IDOR Multi-Tenant)
Seluruh endpoint mutasi dan tampilan data spesifik (misalnya detail hosting `/dashboard/service/manage/{id}`, detail domain `/dashboard/domain/manage/{id}`, atau detail invoice `/billing/invoice/{id}`) menerapkan validasi kepemilikan ganda:
```php
// Pola Wajib Pencegahan IDOR
$userId = $_SESSION['user_id'];
$service = $this->subscriptionModel->getByIdAndUserId($id, $userId);

if (!$service && !AuthHelper::isAdmin()) {
    ToastHelper::error('Akses ditolak: Anda tidak memiliki hak atas layanan ini.');
    $this->redirect('/dashboard');
    exit();
}
```
Pola ini menjamin seorang pelanggan tidak akan pernah dapat melihat atau memodifikasi konfigurasi milik pelanggan lain meskipun mereka menebak ID numerik pada parameter URL.

### 12.2. Pencegahan SQL Injection melalui PDO Parameterized Statements
Sistem melarang keras penggabungan string langsung (*string concatenation*) dalam pembentukan sintaks kueri basis data. Seluruh kueri wajib menggunakan prepared statements dengan binding parameter eksplisit:
```php
// Standar Kueri Aman YoHost
$this->db->query("SELECT * FROM users WHERE email = :email AND status = :status LIMIT 1");
$this->db->bind(':email', $sanitizedEmail, PDO::PARAM_STR);
$this->db->bind(':status', 'active', PDO::PARAM_STR);
$user = $this->db->single();
```

### 12.3. Perlindungan Cross-Site Scripting (XSS) & HTML Purifying
Seluruh keluaran data pengguna (*user-supplied data*) yang dirender ke antarmuka HTML wajib melewati sanitasi pengkodean entitas melalui fungsi `htmlspecialchars($data, ENT_QUOTES, 'UTF-8')`. Untuk data formulir yang menerima tag HTML terbatas (seperti deskripsi artikel pengetahuan atau template email), sistem memfilter tag berbahaya (`<script>`, `<iframe>`, `onload=`, `onerror=`) sebelum menyimpannya ke basis data.

### 12.4. Proteksi Cross-Site Request Forgery (CSRF Tokens)
Setiap formulir HTML yang melakukan mutasi data via metode HTTP POST, PUT, atau DELETE wajib menyertakan input tersembunyi `csrf_token`. Controller memvalidasi token tersebut terhadap token yang tersimpan pada sesi pengguna:
```php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    if (!SecurityHelper::validateCsrfToken($_POST['csrf_token'] ?? '')) {
        ToastHelper::error('Sesi keamanan telah berakhir. Silakan ulangi kembali.');
        $this->redirect($_SERVER['HTTP_REFERER'] ?? '/dashboard');
        exit();
    }
}
```

### 12.5. Hashing Sandi Tingkat Lanjut (BCRYPT Cost Factor 10)
Kata sandi pengguna di-hash menggunakan algoritma BCRYPT (`PASSWORD_BCRYPT`) dengan faktor biaya komputasi (*cost factor*) 10. Kata sandi mentah tidak pernah dicatat dalam berkas log maupun basis data dalam kondisi apa pun.

### 12.6. Isolasi Server-Side Proxy pada API Eksternal
Seluruh komunikasi dengan API registrar dan WHM cluster dieksekusi secara privat oleh backend server PHP. Token otorisasi, kunci rahasia, dan kredensial reseller disimpan pada tabel konfigurasi terenkripsi dan tidak pernah diekspos ke klien peramban.

---

## 13. PANDUAN INSTALASI, DEPLOYMENT, DAN KONFIGURASI SERVER

### 13.1. Persiapan Database MySQL / MariaDB
1. Buka antarmuka manajemen MySQL (phpMyAdmin atau terminal MySQL).
2. Buat basis data baru dengan character set `utf8mb4` dan collation `utf8mb4_unicode_ci`:
```sql
CREATE DATABASE `yohost_db` CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'yohost_user'@'localhost' IDENTIFIED BY 'PasswordSangatKuat_2026!';
GRANT ALL PRIVILEGES ON `yohost_db`.* TO 'yohost_user'@'localhost';
FLUSH PRIVILEGES;
```

### 13.2. Konfigurasi Web Server Apache (.htaccess) & Nginx (vhost)

#### Konfigurasi Apache (`.htaccess` di folder root):
```apache
<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /
    
    # Cegah akses langsung ke direktori sistem sensitif
    RewriteRule ^app/ - [F,L]
    RewriteRule ^sql/ - [F,L]
    RewriteRule ^scratch/ - [F,L]
    
    # Arahkan semua permintaan non-file ke index.php
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)$ index.php?url=$1 [QSA,L]
</IfModule>

# Pengamanan Header HTTP
<IfModule mod_headers.c>
    Header set X-Content-Type-Options "nosniff"
    Header set X-Frame-Options "SAMEORIGIN"
    Header set X-XSS-Protection "1; mode=block"
    Header set Referrer-Policy "strict-origin-when-cross-origin"
</IfModule>
```

#### Konfigurasi Nginx (`/etc/nginx/sites-available/yohost.conf`):
```nginx
server {
    listen 80;
    listen 443 ssl http2;
    server_name yohost.net www.yohost.net;
    root /var/www/yohost;
    index index.php index.html;

    # SSL Configuration (Let's Encrypt)
    ssl_certificate /etc/letsencrypt/live/yohost.net/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/yohost.net/privkey.pem;

    # Blokir akses ke direktori internal sensitif
    location ~ ^/(app|sql|scratch) {
        deny all;
        return 403;
    }

    # Penanganan file statis
    location ~* \.(jpg|jpeg|png|gif|ico|css|js|svg|woff|woff2|ttf|eot)$ {
        expires 30d;
        add_header Cache-Control "public, no-transform";
    }

    # Routing utama
    location / {
        try_files $uri $uri/ /index.php?url=$uri&$args;
    }

    # Eksekusi PHP-FPM
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.2-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

### 13.3. Menjalankan Skrip Instalasi Web (/install)
Jika basis data masih kosong, akses URL instalasi melalui peramban:
`http://domainanda.com/install`
1. **Pemeriksaan Persyaratan Server:** Sistem memeriksa versi PHP dan kelengkapan ekstensi wajib (PDO, cURL, OpenSSL, Mbstring, Sockets, GD, Zip).
2. **Konfigurasi Database:** Masukkan Host Database, Nama Database, Username, dan Password. Skrip akan menguji koneksi dan mengeksekusi skema database secara otomatis.
3. **Akun Administrator:** Masukkan Nama, Email, dan Password untuk akun Superadmin perdana.
4. **Selesai:** Sistem menulis berkas konfigurasi `app/config/config.php` dan mengunci akses direktori instalasi demi keamanan.

### 13.4. Konfigurasi Environment & Kredensial Sistem
Berkas konfigurasi utama terletak di [app/config/config.php](file:///c:/laragon/www/hostyo/app/config/config.php):
```php
<?php
define('DB_HOST', 'localhost');
define('DB_USER', 'yohost_user');
define('DB_PASS', 'PasswordSangatKuat_2026!');
define('DB_NAME', 'yohost_db');

define('BASE_URL', 'https://yohost.net');
define('APP_NAME', 'YoHost Cloud Technologies');
define('APP_ENV', 'production'); // 'development' atau 'production'
define('ENCRYPTION_KEY', 'kunci_acak_kriptografi_32_karakter_rahasia_anda');
```

### 13.5. Penjadwalan Linux Crontab untuk Otomasi Penuh
Buka editor crontab server dengan perintah `crontab -e` pada user web server (`www-data` atau `root`), lalu tambahkan baris jadwal berikut:
```bash
# Otomasi Penagihan Invoice (Pukul 00:30 WIB setiap hari)
30 0 * * * /usr/bin/php /var/www/yohost/index.php cron generate_invoices > /dev/null 2>&1

# Eksekusi Auto-Renewal Saldo Dompet (Pukul 01:00 WIB setiap hari)
0 1 * * * /usr/bin/php /var/www/yohost/index.php cron process_auto_renew > /dev/null 2>&1

# Penangguhan Akun Menunggak (Pukul 02:00 WIB setiap hari)
0 2 * * * /usr/bin/php /var/www/yohost/index.php cron suspend_overdue > /dev/null 2>&1

# Sinkronisasi Domain Registrar (Pukul 04:00 WIB setiap hari)
0 4 * * * /usr/bin/php /var/www/yohost/index.php cron sync_domains > /dev/null 2>&1

# Pemantauan Uptime Server & Port (Setiap 5 menit)
*/5 * * * * /usr/bin/php /var/www/yohost/index.php cron check_uptime > /dev/null 2>&1

# Terminasi Akun Kedaluwarsa Parah (Setiap Minggu pukul 03:00 WIB)
0 3 * * 0 /usr/bin/php /var/www/yohost/index.php cron terminate_expired > /dev/null 2>&1
```

---

## 14. PANDUAN PENGUJIAN DAN VERIFIKASI SISTEM

### 14.1. Validasi Sintaks Kode PHP (php -l)
Untuk memastikan tidak ada kesalahan sintaksis pada berkas PHP di lingkungan produksi, jalankan pengujian linting massal melalui terminal:
```bash
find app/ -name "*.php" -exec php -l {} \; | grep -v "No syntax errors detected"
```
Jika tidak ada keluaran teks, seluruh berkas kode terverifikasi bersih dari kesalahan sintaks PHP.

### 14.2. Pengujian Koneksi WHM/cPanel API
1. Masuk ke Superadmin Panel di `/admin/servers`.
2. Klik tombol **"Test Connection"** pada node server yang ingin diuji.
3. Sistem akan mengirim panggilan API `applist` ke server WHM port 2087. Respon sukses menandakan token API WHM valid dan siap digunakan untuk provisioning akun hosting baru.

### 14.3. Pengujian API Registrar Domain
1. Buka halaman pencarian domain publik di `/domain-search`.
2. Masukkan nama domain acak (misal: `domainujicoba123987.com`).
3. Pastikan sistem mengembalikan status ketersediaan "Tersedia" beserta rincian harga pendaftaran resmi.

### 14.4. Pengujian Simulasi Transaksi Pembayaran Webhook
Untuk menguji webhook Tripay di lingkungan pengembangan lokal tanpa pembayaran nyata:
Jalankan skrip scratch simulator pengiriman payload webhook dengan signature valid ke `http://localhost/hostyo/webhook/tripay`, lalu verifikasi apakah status faktur otomatis berubah menjadi `paid` dan layanan hosting langsung terbuat di database.

### 14.5. Pengujian Pengecekan DNS dan WHOIS Socket
Akses `/dashboard/dns-check`, pilih salah satu domain terdaftar, dan klik "Periksa Sekarang". Pastikan record A, NS, MX, dan TXT berhasil ditarik secara asinkronus tanpa pesan error socket timeout.

---

## 15. CATATAN PERJALANAN RILIS & HISTORI FITUR (BAB 01 - BAB 34)

### 15.1. Evolusi Fondasi Hosting dan Penagihan (Bab 01 - Bab 10)
- **Bab 01 - 03:** Pembangunan arsitektur MVC native, skema database dasar `users`, `subscriptions`, dan `invoices`. Implementasi enkripsi BCRYPT dan tata letak responsif.
- **Bab 04 - 07:** Integrasi WHM API v1 untuk provisi akun cPanel instan. Pembuatan panel Superadmin untuk manajemen paket hosting dan server klaster.
- **Bab 08 - 10:** Integrasi Payment Gateway Tripay dan Midtrans dengan verifikasi callback signature. Implementasi sistem tiket bantuan teknis pelanggan.

### 15.2. Otomasi Domain, TLD Margin, dan Gateway (Bab 11 - Bab 20)
- **Bab 11 - 14:** Penambahan modul domain mandiri, integrasi API registrar, pengatur delegasi nameserver, dan DNS Zone Editor.
- **Bab 15 - 17:** Penetapan harga modal vs harga jual domain TLD di admin, kalkulasi margin keuntungan kotor, dan integrasi keranjang belanja e-commerce multi-item.
- **Bab 18 - 20:** Implementasi sistem kupon diskon dinamis, kalkulasi PPN 11%, dan automasi siklus hidup cron jobs (suspensi keterlambatan & pembuatan faktur H-14).

### 15.3. Pemeliharaan Sistem, DNS, dan Keamanan Sesi (Bab 21 - Bab 30)
- **Bab 21 - 24:** Fitur mode pemeliharaan website instan (Maintenance Mode Engine) dengan whitelist IP admin dan bypass login darurat.
- **Bab 25 - 27:** Penambahan integrasi Two-Factor Authentication (2FA TOTP RFC 6238), sistem obrolan langsung (Live Chat), dan pusat pengetahuan (Knowledgebase).
- **Bab 28 - 30:** Pembaruan antarmuka onboarding interaktif (Tour Panduan Sistem 6 Langkah) dengan persetujuan syarat ketentuan layanan legal.

### 15.4. Onboarding, Alerting, Cart Hub, dan White-Label (Bab 31 - Bab 34)
- **Bab 31:** Penambahan kotak centang persetujuan ketentuan layanan (*Agreement Checkbox*) dengan validasi JavaScript dan penyimpanan preferensi lokal.
- **Bab 32:** Pembaruan widget metrik dashboard 4 kolom, Actionable Expiry Alert ($\le 14$ hari), DNS Propagation Checker mandiri, Auto-Renewal Center, dan Security Audit Sessions Manager (`user_login_logs`).
- **Bab 33:** Redesain komprehensif halaman keranjang belanja (`/cart`) menjadi *Discovery Hub* berorientasi konversi, unifikasi arsitektur layout (Client Area vs Storefront Publik), serta penataan ulang header mobile dengan tombol dropdown **Menu Pintas** (`layout-grid`).
- **Bab 34:** Penguatan privasi White-Label Registrar 100% dengan sterilisasi menyeluruh seluruh referensi nama vendor pihak ketiga, penyelesaian linter warning dynamic parameter `CURLOPT_CUSTOMREQUEST`, dan perbaikan fatal error method alias `getUserDomains()`.

---

Dokumentasi ini disusun dan dipelihara oleh Tim Rekayasa Perangkat Lunak YoHost Cloud Technologies.  
Hak Cipta (c) 2026 YoHost Cloud Technologies Inc. Seluruh hak cipta dilindungi undang-undang.
