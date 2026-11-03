# Pba5
KETENTUAN UMUM & REPOSITORY GITHUB
Sifat UTS : Open ALL Kecuali penggunaan AI
Nama Project: uts_nrp (Contoh: uts_c142300002)
Nama Package: uts.nrp.app (Ganti nrp dengan NRP lengkap Anda, contoh: uts.c142300002)
[WAJIB] GitHub Repository:
Buat Private Repository dengan nama yang sama dengan nama project (uts_nrp).
Tambahkan anitaforpetra@gmail.com sebagai collaborator.
Lakukan commit dengan pesan terstruktur sesuai tahapan fitur di bawah ini (Contoh format pesan commit: 1a - Desain Halaman Katalog).
Pastikan melakukan PUSH dan repo yang dikumpulkan adalah hasil commit terakhir.


KETENTUAN APLIKASI
Aplikasi yang harus Anda buat adalah Sistem Pesanan & Kalkulasi Kasir Cafe, yang terdiri dari 3 Halaman Utama (Halaman Katalog Menu, Halaman Pesanan, dan Halaman Daftar Pesanan).

Buat Desain per halaman sesuai dengan kebutuhan dan dapat di desain bebas (Desain akan diberikan penilaian tersendiri )


1. Halaman KATALOG MENU (Halaman Daftar)
(a) Item yang harus muncul pada setiap baris/card di daftar menu:

Nama Menu (Contoh: Caffe Latte, Matcha Frappe, Signature Tuna Bowl)

Harga Satuan Dasar (dalam format Rupiah)

(b) Aturan Interaksi:

Saat salah satu menu di-klik, user akan diarahkan ke Halaman Pesanan.

2. Halaman PESANAN
(a) Informasi yang harus ditampilkan/diinput:

Menampilkan Nama Menu dan Harga Satuan yang dipilih dari halaman sebelumnya.

Input Jumlah Qty

Pilihan Diskon Member: Checkbox atau RadioButton untuk menentukan apakah pembeli memiliki status "Member" (Diskon 10%).

(b) Total Harga akan dihitung otomatis saat ada perubahan :

Subtotal = Harga Satuan * Jumlah Porsi

Nilai Diskon = Jika berstatus Member, maka ada diskon 10%, jika tidak maka 0%.

Total Pembayaran Akhir = Subtotal - Nilai Diskon 

(c) Aturan Navigasi: 

Tombol "Konfirmasi Pesanan" akan menyimpan data transaksi dan meminta user input nama pemesan kemudian berpindah halaman ke Halaman Daftar Pesanan.
3. Halaman DAFTAR PESANAN
(a) Ketentuan Halaman:

Pesanan yang ada ditampilkan dalam bentuk daftar / List

Menampilkan rincian lengkap pesanan (Nama Pemesan, Nama Menu,  Rincian Perhitungan (Harga Satuan, Jumlah Porsi,  Diskon yang didapat, dan Grand Total Pembayaran)).

(b) Fitur Tambahan:

Saat salah satu daftar ditekan. aplikasi akan meminta user memasukkan Nama Pelanggan dan no HP, lalu membuka aplikasi SMS untuk mengirimkan pesanan yang dipilih itu ke no HP yang dimasukkan.

Isi SMS: Struk Pesanan - [Nama Menu] - [Nama Pelanggan]

Tambahkan Log SMS Berhasil disiapkan beserta datanya agar mudah di tracking
