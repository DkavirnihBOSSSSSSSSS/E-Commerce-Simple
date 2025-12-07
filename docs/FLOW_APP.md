# FLOW_APP – Tecart E-Commerce

## 1. User Journey

### 1.1. Customer

1. Customer membuka aplikasi di `http://localhost:3000`.
2. Jika belum punya akun:
   - Klik **Register** dan mengisi form (fname, lname, email, password).
3. Jika sudah punya akun:
   - Klik **Login** dan memasukkan email & password.
4. Setelah login sebagai **customer** (isAdmin = 0):
   - Melihat daftar produk (data dari `/api/products`).
   - Menambahkan produk ke keranjang (`POST /api/cart/add`).
   - Melihat isi keranjang (`GET /api/cart/:userId`).
   - Menekan tombol **Buy** / checkout (`POST /api/cart/buy/:id` atau flow terkait).
5. Customer dapat melihat pesanan yang pernah dilakukan (endpoint `/api/orders/myPastOrders/:id` jika digunakan).
6. Customer bisa logout dari aplikasi.

### 1.2. Admin

1. Admin login dengan akun yang memiliki `isAdmin = 1` di tabel `users`.
2. Setelah login:
   - Masuk ke halaman **Admin** (komponen `AdminContainer` di frontend).
   - Mengelola produk:
     - Melihat daftar produk (`GET /api/products`).
     - Menambahkan produk (`POST /api/products/create`).
     - Mengupdate produk (`POST /api/products/update`).
     - Menghapus produk (`DELETE /api/products/delete/:id`).
   - Melihat daftar order dan detail order (via endpoint `GET /api/orders`, `GET /api/orders/getProductsByOrder/:id`, dll).
3. Admin bisa logout dari aplikasi.

---

## 2. Arsitektur Aplikasi

Aplikasi menggunakan arsitektur **client–server** dengan MySQL sebagai database:

- **Frontend (`frontend/` – React)**

  - Menyediakan antarmuka untuk Customer & Admin.
  - Menggunakan Axios untuk memanggil REST API ke backend.
  - Menyimpan informasi user (termasuk apakah admin / customer) dan menggunakan ini untuk mengontrol tampilan (RBAC di sisi UI).

- **Backend (`backend/` – Express.js)**

  - File utama: `app.js`
  - Menggunakan:
    - `routes/userRoutes.js` untuk autentikasi (register, login).
    - `routes/productRoutes.js` untuk produk.
    - `routes/cartRoutes.js` untuk keranjang.
    - `routes/orderRoutes.js` untuk order.
    - `utils/token.js` untuk generate & verifikasi JWT.
  - Mengakses database melalui `database/connection.js`.

- **Database (MySQL)**
  - Skrip: `database/createTables.sql`.
  - Tabel utama:
    - `users` (userId, fname, lname, email, password, isAdmin, createdDate)
    - `product` (productId, name, description, price, createdDate)
    - `shopingCart` (userId, productId, quantity)
    - `orders` (orderId, userId, address, totalPrice, createdDate)
    - `productsInOrder` (orderId, productId, quantity, totalPrice)

Secara umum:
React (frontend) ⇄ Express API (backend) ⇄ MySQL (e_commerce)
