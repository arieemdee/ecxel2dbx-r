# Panduan Penggunaan — Excel to DBF Converter

Aplikasi ini membantu Anda mengubah data dari file Excel/CSV menjadi:
- **File DBF** (untuk diimpor ke aplikasi Clipper)
- **Tabel MySQL**
- **File SQLite**

Tidak perlu kemampuan teknis khusus — cukup upload file, cek sebentar, lalu klik Convert.
- **[Download](https://github.com/arieemdee/api-mdengine/releases/latest/download/Excel2dbf.zip)**
---

## Daftar Isi

1. [Membuka Aplikasi](#1-membuka-aplikasi)
2. [Halaman Utama](#2-halaman-utama)
3. [Upload & Analisa File](#3-upload--analisa-file)
4. [Mengatur Pemetaan Kolom](#4-mengatur-pemetaan-kolom)
5. [Template Mapping (Simpan Pengaturan untuk Dipakai Lagi)](#5-template-mapping-simpan-pengaturan-untuk-dipakai-lagi)
6. [Memilih Tujuan Convert](#6-memilih-tujuan-convert)
7. [Proses Convert & Progress Bar](#7-proses-convert--progress-bar)
8. [Halaman Hasil](#8-halaman-hasil)
9. [Riwayat Convert](#9-riwayat-convert)
10. [Masa Trial & Aktivasi Lisensi](#10-masa-trial--aktivasi-lisensi)
11. [Mengatasi Masalah Umum](#11-mengatasi-masalah-umum)

---

## 1. Membuka Aplikasi

Cukup **double-click** file aplikasinya (`.exe`). Browser akan terbuka
otomatis menampilkan halaman utama. Kalau browser tidak terbuka sendiri,
buka browser manual (Chrome/Edge) lalu ketik alamat yang tertulis di
jendela hitam (command prompt) yang muncul — biasanya:

```
http://localhost:3210/convert
```

**Penting:** biarkan jendela hitam (command prompt) itu tetap terbuka
selama memakai aplikasi. Kalau jendela itu ditutup, aplikasinya ikut mati.

---

## 2. Halaman Utama

Di halaman utama Anda akan melihat:

- **Kotak upload file** — tempat memilih file Excel/CSV yang mau di-convert
- **📜 Lihat Riwayat Convert** — link ke daftar semua proses convert yang pernah dilakukan
- **Badge status trial** (kalau masa trial belum habis) — menunjukkan sisa hari trial

---

## 3. Upload & Analisa File

1. Klik kotak file, pilih file **Excel (.xlsx)** atau **CSV** dari komputer Anda.
2. Klik tombol **"Analisa File"**.
3. Aplikasi akan membaca file tersebut dan otomatis:
   - Mendeteksi nama-nama kolom (dari baris pertama file)
   - Menyarankan nama field, tipe data, dan lebar kolom yang cocok

> **Syarat file:** baris pertama di file harus berisi nama-nama kolom
> (judul), bukan data. Contoh baris pertama yang benar: `Kode, Nama, Alamat`

---

## 4. Mengatur Pemetaan Kolom

Setelah file dianalisa, Anda akan melihat tabel seperti ini:

| Kolom Excel | Nama Field | Tipe | Lebar | Desimal |
|---|---|---|---|---|
| Nama Pelanggan | NAMA_PELA | C - Teks | 40 | - |
| Harga | HARGA | N - Angka | 10 | 0 |

Semua kolom **sudah diisi otomatis** — kalau memang sudah pas, tidak perlu
diubah apa-apa. Tapi Anda bisa mengubahnya kalau perlu:

- **Nama Field**: nama kolom di file hasil (maksimal 10 karakter untuk DBF)
- **Tipe**:
  - **C - Teks** → untuk teks biasa, kode, atau angka yang ada nol di
    depan (misalnya NIK `0081234567`) — **paling aman**, gunakan ini
    kalau ragu
  - **N - Angka** → untuk angka murni yang mau dijumlahkan/dihitung
    (harga, jumlah, dll)
  - **D - Tanggal**
  - **L - Ya/Tidak**
- **Lebar**: berapa karakter maksimal muat di kolom itu
- **Desimal**: khusus tipe Angka, berapa angka di belakang koma

> ⚠️ **Penting soal kode/NIK dengan angka nol di depan:** JANGAN ubah
> jadi tipe Angka, karena angka nol di depan akan hilang (misalnya
> `0081234567` jadi `81234567`). Biarkan sebagai tipe Teks.

---

## 5. Template Mapping (Simpan Pengaturan untuk Dipakai Lagi)

Kalau Anda sering convert file dengan **struktur kolom yang sama**
berulang-ulang (misalnya laporan bulanan), tidak perlu atur ulang dari
nol setiap kali.

### Menyimpan Template
1. Atur pemetaan kolom seperti biasa.
2. Di bagian bawah tabel, isi nama di kotak **"Simpan Pemetaan Ini
   sebagai Template"** (contoh: "Laporan Outlet Bulanan").
3. Klik **"Simpan Template"**.

### Memakai Template
1. Upload file baru → Analisa File.
2. Di atas tabel pemetaan, pilih template yang sesuai dari dropdown
   **"Muat dari Template Mapping"**.
3. Klik **"Terapkan"** — kolom yang namanya cocok akan otomatis terisi
   sesuai template.

### Menghapus Template
Pilih template di dropdown, klik tombol **🗑**, lalu konfirmasi.

---

## 6. Memilih Tujuan Convert

Ada 3 pilihan, pilih salah satu sesuai kebutuhan:

### 🗂 File DBF (untuk Clipper)
- **Nama File**: maksimal 8 karakter (tanpa `.DBF`, ditambahkan otomatis)
- **Encoding**: pilih **CP850** (paling umum untuk aplikasi Clipper).
  Kalau nanti hasil di Clipper hurufnya aneh, coba ganti ke CP1252.
- **Folder Tujuan**: klik "Pilih Folder..." untuk memilih lokasi simpan
- **Timpa file kalau sudah ada**: centang kalau memang mau mengganti
  file lama dengan nama yang sama

### 🗄 Tabel MySQL
- Isi **Host**, **Port**, **User**, **Password**, **Nama Database**,
  **Nama Tabel**
- Klik **"Test Koneksi"** dulu untuk memastikan datanya benar sebelum
  convert sungguhan
- Tabel dibuat otomatis kalau belum ada
- **Kosongkan dulu isi tabel**: centang kalau mau data lama di tabel
  itu dihapus dulu sebelum data baru masuk (kalau tidak dicentang,
  data baru akan ditambahkan)

### 📦 File SQLite
- Isi **Nama File** (tanpa `.db`), **Nama Tabel**, dan **Folder Tujuan**
- Kalau file `.db` dengan nama sama sudah ada, tabel baru akan
  ditambahkan ke file itu (bukan menimpa)
- Sama seperti MySQL, ada opsi **kosongkan dulu isi tabel**

---

## 7. Proses Convert & Progress Bar

Setelah klik tombol **Convert**, akan muncul halaman dengan progress bar
yang menunjukkan berapa baris data sudah diproses. Tunggu sampai selesai
— untuk data ribuan baris biasanya hanya perlu beberapa detik.

**Jangan tutup jendela browser** selama proses ini berjalan.

---

## 8. Halaman Hasil

Setelah selesai, akan muncul halaman konfirmasi berisi:
- Jumlah baris data yang berhasil di-convert
- Lokasi file (untuk DBF/SQLite) atau nama tabel & database (untuk MySQL)
- Struktur field yang ditulis

Klik **"Convert File Lain"** untuk mulai proses baru.

---

## 9. Riwayat Convert

Klik **"📜 Lihat Riwayat Convert"** di halaman utama untuk melihat
daftar semua proses convert yang **berhasil** dilakukan sebelumnya —
lengkap dengan waktu, nama file sumber, tujuan, dan jumlah baris.

Ada tombol **"Hapus Semua Riwayat"** kalau ingin mengosongkan daftar ini.

---

## 10. Masa Trial & Aktivasi Lisensi

Aplikasi ini punya masa **trial 30 hari**. Selama trial, akan muncul
badge kecil di halaman utama menunjukkan sisa hari.

### Kalau Masa Trial Sudah Habis
Fitur Analisa & Convert akan diblokir, dan muncul halaman berisi:
- **Machine ID** — kode unik komputer Anda
- Kotak untuk memasukkan **Kode Lisensi**

**Cara mengaktifkan:**
1. Salin **Machine ID** yang tertampil di layar
2. Kirim Machine ID tersebut ke penyedia aplikasi (untuk minta kode
   lisensi, biasanya terkait perpanjangan/pembayaran)
3. Setelah menerima **Kode Lisensi**, paste ke kotak yang tersedia
4. Klik **"Aktifkan"**

Setelah aktivasi berhasil, aplikasi bisa dipakai normal tanpa batas
waktu lagi, dan tidak akan diminta aktivasi ulang.

---

## 11. Mengatasi Masalah Umum

| Masalah | Kemungkinan Penyebab | Solusi |
|---|---|---|
| "File sudah ada di folder tersebut" | Nama file DBF/SQLite yang dipilih sudah ada sebelumnya | Centang "Timpa file jika sudah ada", atau ganti nama file |
| "Folder tujuan tidak valid" | Folder belum dipilih atau sudah tidak ada | Klik "Pilih Folder..." dan pilih ulang |
| Error `EPERM`/`ENOENT`/`EBUSY` saat convert | File sedang dibuka program lain, atau drive USB/jaringan terputus sesaat | Tutup program yang mungkin memakai file itu, pastikan drive tersambung, coba convert ulang (aplikasi sudah otomatis mencoba ulang beberapa kali) |
| Koneksi MySQL gagal | Host/port/user/password/database salah, atau server MySQL mati | Klik "Test Koneksi" untuk lihat pesan error yang lebih jelas |
| Kode/NIK kehilangan angka nol di depan | Kolom tersebut diatur sebagai tipe Angka | Ubah tipe kolom itu jadi **C - Teks** |
| Data di Clipper muncul karakter aneh | Encoding tidak cocok | Coba ganti encoding dari CP850 ke CP1252 (atau sebaliknya), lalu convert ulang |
| Masa trial habis, tidak bisa convert | Trial 30 hari sudah lewat | Hubungi penyedia aplikasi dengan Machine ID Anda untuk mendapat kode lisensi |

---

*Ada pertanyaan lain seputar penggunaan aplikasi ini? Hubungi penyedia
aplikasi Anda.*
