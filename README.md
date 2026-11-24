# SetaraBantu

**Sistem Informasi Penyaluran Bantuan Sosial Inklusif Berbasis Skor Prioritas**

SetaraBantu adalah aplikasi berbasis web untuk mendata warga penerima bantuan, memverifikasi pengajuan berdasarkan tingkat kerentanan, serta mengatur antrean penyaluran bantuan sosial secara lebih terstruktur. Proyek ini disusun untuk memenuhi tugas **Responsi 2 Praktikum Pemrograman Web I**, Jurusan Informatika, Fakultas Teknik, Universitas Jenderal Soedirman.

---

## Anggota Kelompok

| No | Nama Lengkap | NIM | Peran / Pembagian Tugas |
| --- | --- | --- | --- |
| 1 | *Fadillah Mauladi Yofiawan* | *H1D025015* | *Kategori rentan, program bantuan, dan pengajuan* |
| 2 | *Fatma Khoeruzdzikrina* | *H1D025038* | *Autentikasi, user & role, dan data penerima* |
| 3 | *Muhammad Fadilah Fikri* | *H1D025050* | *Verifikasi & prioritas, penyaluran, dan dashboard* |

---

## Latar Belakang dan Tujuan Proyek

### Latar Belakang
Penyaluran bantuan sosial di lapangan sering terkendala oleh pendataan warga yang kurang rapi dan urutan distribusi yang belum mempertimbangkan tingkat kerentanan keluarga. Akibatnya, kelompok yang sangat membutuhkan seperti penyandang disabilitas, lansia, atau kepala keluarga perempuan terkadang tertinggal dalam menerima bantuan.

### Tujuan dan Keterkaitan SDGs
Aplikasi SetaraBantu dibuat untuk membantu pencatatan dan penentuan prioritas penerima bantuan secara objektif, dengan mengacu pada dua tujuan **Sustainable Development Goals (SDGs)** berikut.

1. **SDG 1 (Tanpa Kemiskinan)** — Mempermudah pendataan warga prasejahtera dan pengelolaan program bantuan (sembako, tunai, alat bantu, beasiswa) agar meringankan beban ekonomi keluarga kurang mampu.
2. **SDG 10 (Berkurangnya Kesenjangan)** — Menerapkan perhitungan **Skor Prioritas** otomatis dari bobot kategori rentan, jumlah tanggungan, dan penghasilan per bulan sehingga kelompok rentan diprioritaskan pada urutan penyaluran.

---

## Daftar Fitur dan Modul

Aplikasi ini memiliki 3 peran aktif utama (**Admin**, **Petugas**, dan **Warga**) yang terintegrasi ke dalam **9 modul**.

1. **Autentikasi (`index.php`, `logout.php`)** — Login, logout, pengelolaan Session, fitur *Remember Me* (Cookie 30 hari), dan verifikasi hash password (`password_hash` / MD5).
2. **Manajemen User (`user.php`)** — Pengelolaan data akun pengguna dan pengaturan hak akses oleh Admin.
3. **Kategori Kelompok Rentan (`kategori.php`)** — Pengelolaan daftar kategori kerentanan beserta bobot skornya (Difabel, Lansia, Kepala Keluarga Perempuan, Anak Yatim/Piatu, Keluarga Biasa).
4. **Program Bantuan (`program.php`)** — CRUD jenis program bantuan (sembako, tunai, alat bantu, beasiswa) beserta kuota dan deskripsi.
5. **Profil Data Penerima (`penerima.php`)** — Formulir bagi warga untuk melengkapi alamat, penghasilan per bulan, jumlah tanggungan, dan kategori kelompok rentan.
6. **Pengajuan Bantuan (`pengajuan.php`)** — Formulir pengajuan program bantuan oleh warga sekaligus riwayat status pengajuan.
7. **Verifikasi dan Perhitungan Skor Prioritas (`verifikasi.php`)** — Persetujuan atau penolakan pengajuan oleh Petugas atau Admin yang otomatis menghitung Skor Prioritas dengan rumus berikut.
   ```text
   Skor Prioritas = Bobot Kategori + min(Jumlah Tanggungan × 5, 30) + max(0, 20 - floor(Penghasilan / 500.000))
   ```
8. **Antrean Penyaluran (`penyaluran.php`)** — Daftar antrean penyaluran yang otomatis diurutkan dari status *belum diterima*, skor prioritas tertinggi, lalu jadwal terdekat (H+3), lengkap dengan tombol konfirmasi penerimaan.
9. **Dashboard dan Ringkasan Data (`dashboard.php`)** — Statistik jumlah program, total pengajuan, pengajuan menunggu verifikasi, bantuan tersalurkan, grafik distribusi kelompok rentan (Chart.js), dan tabel pengajuan terbaru.

---

## Teknologi yang Digunakan

- **Bahasa Pemrograman** — PHP (Native), HTML5, JavaScript
- **Database** — MySQL / MariaDB (`setarabantu_db`)
- **Tampilan Antarmuka (UI)** — CSS3, Bootstrap 5, Bootstrap Icons, Chart.js, SweetAlert2
- **Web Server Lokal** — XAMPP (Apache & MySQL / PHP Built-in Server)

---

## Panduan Instalasi dan Konfigurasi

### Cara 1 — Otomatis Menggunakan Batch Script (Windows + XAMPP)
1. Pastikan **XAMPP** sudah terpasang di folder instalasi standar (`xampp`).
2. Clone atau download repository ini.
   ```bash
   git clone (https://github.com/Fikricraft/SetaraBantu)
   ```
3. Masuk ke folder proyek, lalu klik dua kali file `JALANKAN_WEBSITE.BAT`. Script ini otomatis menyalakan MySQL, membuat database `setarabantu_db`, mengimpor `database.sql`, dan menjalankan server lokal.

### Cara 2 — Manual via XAMPP dan phpMyAdmin
1. Clone atau ekstrak folder proyek ke direktori `htdocs/SetaraBantu` di dalam folder XAMPP.
2. Buka **XAMPP Control Panel**, lalu jalankan modul **Apache** dan **MySQL**.
3. Buka phpMyAdmin di browser (`http://localhost/phpmyadmin`), masuk ke tab **Import**, pilih file `database.sql`, lalu klik **Import**. Database `setarabantu_db` beserta seluruh tabel akan dibuat otomatis.
4. Jika konfigurasi MySQL lokal menggunakan password berbeda, sesuaikan pengaturan koneksi di file `koneksi.php`.
   ```php
   $conn = mysqli_connect("localhost", "root", "", "setarabantu_db");
   ```

---

## Panduan Menjalankan Aplikasi

1. Buka browser lalu akses `http://localhost:8000/` (jika dijalankan lewat `JALANKAN_WEBSITE.BAT`) atau `http://localhost/SetaraBantu/` (jika diletakkan di `htdocs` Apache XAMPP).
2. Masuk pada halaman login menggunakan salah satu akun bawaan berikut.

| Peran | Email | Password |
| --- | --- | --- |
| **Admin** | `admin@bantu.com` | `admin123` |
| **Petugas** | `petugas@bantu.com` | `petugas123` |
| **Warga** | `budi@bantu.com` | `budi123` |

3. Alur penggunaan singkat.
   - **Admin** mengelola data kategori rentan, program bantuan, dan akun pengguna.
   - **Warga** melengkapi data di menu **Profil Warga**, kemudian mengajukan bantuan di menu **Pengajuan**.
   - **Petugas** memverifikasi pengajuan di menu **Verifikasi** (skor prioritas terhitung otomatis), lalu mencatat penyerahan bantuan pada menu **Penyaluran**.
   - Ringkasan statistik dan grafik dapat dipantau pada menu **Dashboard**.

---

## Tautan Publikasi Proyek

- **Video Presentasi (YouTube)** — *([Isi link YouTube di sini](https://youtu.be/qwk2IYcPkJI?si=TLy8Xr6TM08WeLdG))*
- **Project Showcase Anggota 1** — *([Isi link Instagram / LinkedIn](https://lnkd.in/p/giGMxkEF))*
- **Project Showcase Anggota 2** — *([Isi link Instagram / LinkedIn](https://lnkd.in/p/gJvXHXZg))*
- **Project Showcase Anggota 3** — *([Isi link Instagram / LinkedIn](https://lnkd.in/p/gkA3m_XW))*
