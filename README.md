<p align="center"><img src="https://drive.google.com/uc?export=view&id=1fHQYxNCcv79kbnA5Jamhag5ziuUn-w3T"></p>

# OpenStack!
Apa itu <b>OpenStack</b>? OpenStack adalah sistem operasi cloud yang mengontrol kumpulan besar sumber daya komputasi, penyimpanan, dan jaringan di seluruh pusat data, semuanya dikelola melalui dasbor yang memberi administrator kontrol sambil memberdayakan penggunanya untuk menyediakan sumber daya melalui antarmuka web.

Proyek OpenStack adalah platform komputasi awan sumber terbuka untuk semua jenis awan, yang bertujuan agar mudah diimplementasikan, dapat diskalakan secara besar-besaran, dan kaya fitur. Pengembang dan ahli teknologi komputasi awan dari seluruh dunia membuat proyek OpenStack.

OpenStack menyediakan solusi <b>Infrastructure-as-a-Service (IaaS)</b> melalui serangkaian layanan yang saling terkait. Setiap layanan menawarkan Antarmuka <b>Pemrograman Aplikasi (API)</b> yang memfasilitasi integrasi ini. Tergantung pada kebutuhan Anda, Anda dapat menginstal beberapa atau semua layanan.

## Arsitektur logis
   
Untuk merancang, menerapkan, dan mengkonfigurasi OpenStack, administrator harus memahami arsitektur logisnya.

Seperti yang ditunjukkan pada Arsitektur konseptual, OpenStack terdiri dari beberapa bagian independen, yang diberi nama layanan OpenStack. Semua layanan mengotentikasi melalui layanan Identity umum. Layanan perorangan berinteraksi satu sama lain melalui API publik, kecuali jika perintah administrator istimewa diperlukan.

Secara internal, layanan OpenStack terdiri dari beberapa proses. Semua layanan memiliki setidaknya satu proses API, yang mendengarkan permintaan API, melakukan preprocesses mereka dan meneruskannya ke bagian lain layanan. Dengan pengecualian layanan Identity, pekerjaan sebenarnya dilakukan dengan proses yang berbeda.

Untuk komunikasi antara proses satu layanan, broker pesan AMQP digunakan. Status layanan disimpan dalam database. Saat menggelar dan mengonfigurasi awan OpenStack Anda, Anda dapat memilih beberapa solusi broker dan database pesan, seperti RabbitMQ, MySQL, MariaDB, dan SQLite.

Pengguna dapat mengakses OpenStack melalui antarmuka pengguna berbasis web yang dilaksanakan oleh Horizon Dashboard, via command-line clients dan dengan mengeluarkan permintaan API melalui alat seperti plug-in browser atau curl. Untuk aplikasi, several SDKs tersedia. Pada akhirnya, semua metode akses ini mengeluarkan REST API panggilan ke berbagai layanan OpenStack.

Diagram berikut menunjukkan arsitektur yang paling umum namun tidak mungkin untuk awan OpenStack:
<p align="center"><img src="https://drive.google.com/uc?export=view&id=1WVuTUoZ6tfNtW776txyDV206R78uXH_3"></p>
