## Role & Hak Akses (RBAC)

- **Customer**

  - Registrasi & login sebagai customer
  - Melihat daftar produk
  - Menambahkan produk ke keranjang
  - Melakukan checkout / membuat pesanan

- **Seller**
  - Registrasi & Login sebagai seller
  - Menambah, mengubah, menghapus produk
  - Melihat daftar produk yang dimilikinya
  - Melihat daftar pesanan masuk

## Panduan Pengguna – Customer

Registrasi Akun
Klik tombol Register / Sign Up.

Isi form:
First Name (fname)
Last Name (lname)
Email
Password
Klik Register.

Login
Klik tombol Login.
Masukkan email dan password yang telah didaftarkan.
Jika benar, sistem akan:
Mengirim token JWT dari backend.
Mengarahkan ke halaman utama sebagai Customer.

Melihat Produk
Setelah login, user dapat melihat daftar produk yang diambil dari backend (/api/products).
Setiap kartu produk menampilkan:
Nama produk
Harga
Deskripsi singkat (jika ada)

Menambahkan ke Keranjang
Pada produk yang diinginkan, klik tombol Add to Cart / sejenisnya.
Sistem akan memanggil endpoint:
POST /api/cart/add
Produk akan masuk ke keranjang user (tabel shopingCart).

Melihat Keranjang
Klik menu atau ikon Cart / Keranjang.
Sistem akan memanggil:
GET /api/cart/:userId
Di halaman keranjang, user dapat melihat:
Daftar produk yang ada di keranjang.
Jumlah (quantity).
Subtotal harga.

Checkout / Buy
Di halaman keranjang, klik tombol Buy / Checkout.
Sistem akan memanggil endpoint:
POST /api/cart/buy/:id atau flow order terkait.
Data order akan disimpan di tabel orders dan productsInOrder.
Keranjang user akan dikosongkan sesuai implementasi.

Melihat Riwayat Pesanan
(Jika diimplementasikan di UI) user dapat membuka menu Orders / My Orders.
Sistem memanggil:
GET /api/orders/myPastOrders/:userId
Menampilkan daftar pesanan yang pernah dibuat user.

## Panduan Pengguna – Seller

Login sebagai Admin
Admin login melalui halaman yang sama dengan customer.
Akun admin dibedakan dengan kolom isAdmin = 1 di tabel users.
Setelah login, frontend akan mengecek isAdmin dan menampilkan menu Admin.

Mengelola Produk
Buka halaman Admin (komponen AdminContainer di frontend).
Di halaman ini Admin dapat:
Melihat daftar produk.
Menambahkan produk:
Mengisi nama, deskripsi, harga.
Mengirim ke endpoint POST /api/products/create.
Mengedit produk:
Mengubah field yang diperlukan.
Mengirim ke endpoint POST /api/products/update.
Menghapus produk:
Menekan tombol hapus.
Backend memanggil DELETE /api/products/delete/:id.

Melihat Order
Admin membuka halaman Orders (komponen Orders di frontend).
Sistem memanggil:
GET /api/orders
GET /api/orders/getProductsByOrder/:id untuk detail isi pesanan.
Admin dapat melihat pesanan yang dibuat oleh customer.

Logout
Baik Customer maupun Admin dapat melakukan logout melalui tombol Logout.
Setelah logout:
Token JWT dihapus dari frontend (state / storage).
User tidak bisa mengakses halaman yang memerlukan login sampai login kembali.

```

```
