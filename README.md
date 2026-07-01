# SnapAbsen — Sistem Absensi Karyawan

Aplikasi absensi karyawan berbasis web yang terintegrasi dengan Firebase Firestore. Dirancang untuk digunakan melalui browser HP maupun desktop, tanpa perlu install aplikasi.

---

## 🔗 Demo

- **Panel Admin:** [ptidssby199.github.io/admin-snapabsen/admin-1.html](https://ptidssby199.github.io/admin-snapabsen/admin-1.html)
- **Halaman Utama:** [ptidssby199.github.io/admin-snapabsen](https://ptidssby199.github.io/admin-snapabsen)

---

## ✨ Fitur

| Fitur | Keterangan |
|---|---|
| Dashboard | Ringkasan absensi harian (hadir, terlambat, izin) |
| Absensi Manual | Input atau koreksi absensi karyawan oleh admin |
| Laporan Absensi | Rekap per bulan, export ke Excel |
| Manajemen User | Tambah, edit, nonaktifkan akun karyawan |
| Jadwal Kerja | Atur jadwal shift per karyawan |
| Template Shift | Buat template shift yang bisa digunakan ulang |
| Radius Absen | Batas lokasi GPS untuk absensi |
| Sinkronisasi | Sinkron data ke SQL Server (opsional) |
| Firebase Config | Konfigurasi koneksi Firebase langsung dari browser |

---

## 🛠️ Teknologi

- **Frontend:** HTML, CSS, JavaScript (Vanilla)
- **Database:** Firebase Firestore
- **Auth:** Firebase Authentication
- **Storage:** Firebase Storage
- **Deploy:** Netlify (auto-deploy dari GitHub)
- **Library:** Font Awesome, Firebase SDK 9.23.0

---

## 🚀 Cara Deploy

### 1. Clone / Fork repo ini

```bash
git clone https://github.com/username/snapabsen.git
```

### 2. Siapkan Firebase

1. Buka [Firebase Console](https://console.firebase.google.com)
2. Buat project baru
3. Aktifkan **Firestore**, **Authentication (Email/Password)**, dan **Storage**
4. Salin konfigurasi Firebase (apiKey, authDomain, dll)

### 3. Deploy ke GitHub Pages

1. Buka repo di GitHub → klik **Settings**
2. Pilih menu **Pages** di sidebar kiri
3. Pada **"Branch"**, pilih `main` dan folder `/ (root)`
4. Klik **Save**
5. Tunggu 1-2 menit → site live di `https://ptidssby199.github.io/admin-snapabsen`

### 4. Konfigurasi Firebase di Aplikasi

1. Buka URL admin: `yoursite.netlify.app/admin-1.html`
2. Masuk ke menu **Firebase Config**
3. Isi semua field konfigurasi Firebase
4. Klik **Simpan & Hubungkan**

---

## 👤 Setup Akun Admin Pertama

Setelah Firebase terhubung, buat akun admin pertama:

1. Buka **Firebase Console → Authentication** → Tambah user (email + password)
2. Buka **Firestore → Collection `users`** → Tambah dokumen baru
3. Isi field berikut:

```
uid        : (UID dari Firebase Auth)
name       : Nama Admin
email      : email@domain.com
userRole   : admin
nik        : (opsional)
```

---

## 📁 Struktur File

```
snapabsen/
├── index.html          # Halaman utama karyawan (absen masuk/pulang)
├── admin-1.html        # Panel admin lengkap
├── README.md           # Dokumentasi ini
├── .gitignore          # File yang dikecualikan dari Git
└── netlify.toml        # Konfigurasi Netlify (opsional)
```

---

## 🔐 Role User

| Role | Akses |
|---|---|
| `admin` | Akses penuh ke panel admin |
| `karyawan` | Hanya bisa absen masuk/pulang di halaman utama |
| `nonaktif` | Tidak bisa login |

---

## 📋 Struktur Firestore

### Collection: `users`
| Field | Tipe | Keterangan |
|---|---|---|
| uid | string | UID Firebase Auth |
| name | string | Nama lengkap |
| email | string | Email login |
| userRole | string | `admin` / `karyawan` / `nonaktif` |
| nik | string | Nomor induk karyawan |

### Collection: `absensi`
| Field | Tipe | Keterangan |
|---|---|---|
| uid | string | UID karyawan |
| userName | string | Nama karyawan |
| date | string | Format `YYYY-MM-DD` |
| type | string | `masuk` / `pulang` |
| time | string | Format `HH:MM` |
| lat / lng | number | Koordinat GPS |
| keterangan | string | `hadir` / `izin` / `sakit` / `cuti` / `alpha` |
| editedByAdmin | boolean | `true` jika diinput manual |
| editedBy | string | Nama admin yang menginput |

---

## 📄 Lisensi

Project ini dibuat untuk kebutuhan internal. Bebas dimodifikasi sesuai kebutuhan.
