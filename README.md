# JSON Server untuk Aplikasi Telekomunikasi

Proyek ini adalah implementasi JSON Server yang disesuaikan untuk menyediakan API REST palsu untuk aplikasi telekomunikasi. Server ini menggunakan data dari file `fixtures/db.json` yang berisi informasi tentang pengguna, nomor telepon, provider, paket data internet, dan transaksi.

## Fitur

- **API REST Lengkap**: Mendukung operasi CRUD (Create, Read, Update, Delete) untuk semua resource.
- **Hot Reload**: Server akan otomatis reload ketika file database diubah.
- **CORS Support**: Mendukung Cross-Origin Resource Sharing untuk pengembangan frontend.
- **Static Files**: Menyajikan file statis dari direktori `public`.
- **Snapshot Database**: Kemampuan untuk membuat snapshot database saat runtime.

## Struktur Data

Database terdiri dari beberapa resource utama:

### User
- `id`: ID unik pengguna
- `email`: Email pengguna
- `password`: Kata sandi (dalam format plain text untuk demo)
- `name`: Nama pengguna
- `role`: Peran pengguna
- `balance`: Saldo pengguna

### Phone Number
- `id`: ID unik nomor telepon
- `userId`: ID pengguna pemilik
- `number`: Nomor telepon
- `provider`: Provider telekomunikasi (telkomsel, xl, dll.)
- `label`: Label untuk nomor (contoh: "Modem", "No Pribadi")
- `internetLabel`: Label paket internet yang aktif
- `expDate`: Tanggal kadaluarsa paket

### Provider
- `id`: ID unik provider
- `provider`: Nama provider (telkomsel, xl, smartfren, axis, tri)

### Internet Data
- `id`: ID unik paket data
- `providerId`: ID provider
- `label`: Nama paket
- `normalPrice`: Harga normal
- `quota`: Kuota data
- `discPrice`: Harga diskon
- `content`: Deskripsi paket
- `detail`: Detail kuota harian/mingguan
- `exp`: Masa berlaku

### Transaction Data Internet & Transaction Wallet
Array untuk menyimpan data transaksi (saat ini kosong dalam fixture).

## Instalasi

Pastikan Anda memiliki Node.js versi 18.3 atau lebih tinggi terinstal.

1. Clone repositori ini:
   ```bash
   git clone <url-repositori>
   cd json-server-main
   ```

2. Install dependensi:
   ```bash
   npm install
   ```

## Penggunaan

### Menjalankan Server

Untuk menjalankan server dengan file database default:

```bash
npm run dev
```

Atau jalankan langsung dengan:

```bash
npx json-server fixtures/db.json
```

Server akan berjalan di `http://localhost:3000` secara default.

### Opsi Command Line

- `-p, --port <port>`: Set port (default: 3000)
- `-H, --host <host>`: Set host (default: localhost)
- `-w, --watch`: Watch file database, restart server saat file berubah
- `-s, --static <static>`: Set direktori file statis
- `-d, --delay <delay>`: Tambah delay pada response (ms)
- `--id <id>`: Set property ID database (default: id)
- `-q, --quiet`: Suppress log messages
- `--read-only`: Hanya izinkan request GET
- `--no-cors`: Disable CORS
- `--snapshots <snapshots>`: Set direktori snapshots

Contoh:

```bash
npx json-server fixtures/db.json --port 4000 --watch --delay 1000
```

## API Endpoints

Server menyediakan endpoint REST standar untuk setiap resource:

### GET /:resource
Mengambil semua item dari resource.

**Contoh:**
```
GET /user
GET /phoneNumber
GET /provider
GET /internetData
```

**Query Parameters:**
- `_start`, `_end`: Pagination
- `_limit`: Limit jumlah hasil
- `_page`, `_per_page`: Pagination alternatif
- Filter berdasarkan field: `?field=value`

### GET /:resource/:id
Mengambil item spesifik berdasarkan ID.

**Contoh:**
```
GET /user/00002
GET /phoneNumber/2
```

### POST /:resource
Membuat item baru.

**Body:** JSON object dengan data item.

**Contoh:**
```json
POST /user
{
  "email": "baru@example.com",
  "password": "123456",
  "name": "Pengguna Baru",
  "role": "user",
  "balance": "0"
}
```

### PUT /:resource/:id
Update item lengkap berdasarkan ID.

### PATCH /:resource/:id
Update sebagian item berdasarkan ID.

### DELETE /:resource/:id
Menghapus item berdasarkan ID.

## Home Page

Kunjungi `http://localhost:3000/` untuk melihat halaman home yang menampilkan semua data dalam format HTML.

## Testing

Jalankan test dengan:

```bash
npm test
```

## Build

Untuk build production:

```bash
npm run build
```

## Lisensi

Lihat file LICENSE untuk informasi lisensi.

## Kontribusi

Lihat CONTRIBUTING.md untuk panduan kontribusi.
