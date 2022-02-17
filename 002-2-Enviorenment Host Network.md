# Host Network
Setelah menginstal sistem operasi pada setiap node untuk arsitektur yang Anda pilih untuk digunakan, Anda harus mengkonfigurasi antarmuka jaringan. Sebaiknya nonaktifkan alat pengelolaan jaringan otomatis dan edit secara manual file konfigurasi yang sesuai untuk distribusi Anda. Untuk informasi lebih lanjut tentang cara mengkonfigurasi jaringan pada distribusi Anda, lihat dokumentasi.

Semua node membutuhkan akses internet untuk tujuan administratif seperti instalasi paket, update keamanan, DNS, dan NTP. Dalam kebanyakan kasus, node harus mendapatkan akses Internet melalui antarmuka jaringan manajemen. Untuk menyoroti pentingnya pemisahan jaringan, contoh arsitektur menggunakan private address space untuk jaringan manajemen dan menganggap dimana infrastruktur jaringan fisik menyediakan akses internet melalui NAT atau metode lainnya. Contoh arsitektur menggunakan ruang alamat IP routable untuk jaringan penyedia (eksternal) dan menganggap bahwa infrastruktur jaringan fisik menyediakan akses internet langsung.

Dalam arsitektur jaringan provider, semua instance berhubungan langsung ke jaringan provider. Di arsitektur jaringan self-service (private), instance dapat berhubungan ke jaringan self-service atau provider. Jaringan self-service dapat berada sepenuhnya dalam OpenStack atau memberikan beberapa tingkat akses jaringan eksternal menggunakan NAT melalui jaringan provider.

<p align="center"><img src="https://drive.google.com/uc?export=view&id=1kUSK8fXmmwZ3ncQSRHv8L7J-wthfkWAQ"></p>

Arsitektur contoh menganggap penggunaan jaringan berikut:

<ul>
<li>Manajemen pada 10.0.0.0/24 dengan gateway 10.0.0.1

Jaringan ini memerlukan gateway untuk menyediakan akses Internet untuk semua node untuk tujuan administratif seperti instalasi paket, update keamanan, DNS, dan NTP.</li>

<li>Provider pada 203.0.113.0/24 dengan gateway 203.0.113.1

Jaringan ini memerlukan gateway untuk menyediakan akses Internet untuk instance di lingkungan OpenStack Anda.</li>
</ul>
