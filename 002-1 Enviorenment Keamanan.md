# Keamanan
Layanan OpenStack mendukung berbagai metode keamanan termasuk password, kebijakan, dan enkripsi. Selain itu, layanan pendukung termasuk server database dan perantara pesan (message broker) mendukung keamanan password.

Untuk memudahkan proses instalasi, panduan ini hanya mencakup keamanan kata sandi bila berlaku. Anda dapat membuat kata sandi yang aman secara manual, namun string koneksi database dalam file konfigurasi layanan tidak dapat menerima karakter khusus seperti "@". Sebaiknya Anda buat mereka menggunakan alat seperti pwgen, atau dengan menjalankan perintah berikut:

<pre>$ openssl rand -hex 10</pre>\

Untuk layanan OpenStack, panduan ini menggunakan SERVICE_PASS untuk layanan referensi password akun dan SERVICE_DBPASS untuk referensi password database.

Tabel berikut daftar layanan yang membutuhkan password dan referensi terkait dalam panduan.
