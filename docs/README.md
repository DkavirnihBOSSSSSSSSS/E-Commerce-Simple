Tecart E-Commerce adalah aplikasi toko online sederhana Fullstack Development. Aplikasi ini mendukung fitur:

- Registrasi & Login
- Manajemen produk (oleh Admin)
- Keranjang belanja
- Pemesanan (order)
- Penerapan Role-Based Access Control (RBAC) berbasis role **Admin** dan **Customer**

## Anggota Tim

- I Putu Doddy Eka Wiryana – Role: Softeng

## 🧰 Teknologi yang Digunakan

**Frontend:**

- React.js (Create React App)
- Axios
- JWT Decode
- CSS / SCSS

**Backend:**

- Node.js + Express.js (`app.js` sebagai entry point)
- MySQL (library `mysql`)
- JSON Web Token (JWT)
- bcryptjs untuk hashing password

**Database (folder `database/`):**

- MySQL
- Skrip: `database/createTables.sql`
  - Tabel: `users`, `product`, `shopingCart`, `orders`, `productsInOrder`

## Cara Menjalankan Project

1. Jalankan Database (MySQL)
   Start MySQL dari XAMPP.
   Buat database, misalnya: e_commerce
   Import file SQL (jika ada) ke database tersebut.

2. Setup & Jalankan Backend
   cd C:\Tugas\Semester 5\E-Commerce-Tecart\backend
   npm install
   npm start

3. Setup & Jalankan Frontend
   cd C:\Tugas\Semester 5\E-Commerce-Tecart\frontend
   npm install
   npm start
