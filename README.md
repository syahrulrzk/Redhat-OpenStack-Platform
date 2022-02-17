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

### Controller¶
Node pengontrol menjalankan layanan Identity, layanan Image, layanan Placement, bagian manajemen Compute, bagian manajemen dari Networking, berbagai agen Networking, dan Dashboard. Ini juga termasuk layanan pendukung seperti database SQL, message queue, dan NTP.

Secara opsional, controller node menjalankan bagian dari layanan Block Storage, Object Storage, Orchestration, and Telemetry

Controller nodemembutuhkan minimal dua antarmuka jaringan.

### Komputasi¶
The menghitung node menjalankan: istilah: hypervisor porsi Compute yang beroperasi contoh. Secara default, Hitung menggunakan: istilah: KVM <berbasis kernel VM (KVM)> hypervisor. The menghitung node juga menjalankan agen layanan Jaringan yang menghubungkan contoh untuk jaringan virtual dan menyediakan layanan firewall untuk contoh melalui: istilah: kelompok keamanan <grup keamanan>.

Anda dapat menyebarkan lebih dari satu menghitung node. Setiap node membutuhkan minimal dua antarmuka jaringan.

### Block Storage¶
Opsional Block Storage node berisi disk bahwa Blok Storage dan bersama penyediaan layanan File System untuk contoh.

Untuk mempermudah, trafik layanan antara node komputasi dan node ini menggunakan jaringan manajemen. lingkungan produksi harus menerapkan jaringan penyimpanan terpisah untuk meningkatkan kinerja dan keamanan.

Anda dapat menyebarkan lebih dari satu node penyimpanan blok. Setiap node membutuhkan minimal satu antarmuka jaringan.

### Object Storage¶
Opsional Object Storage simpul berisi disk bahwa layanan Object Storage menggunakan piutang menyimpan, kontainer, dan benda-benda.

Untuk mempermudah, trafik layanan antara node komputasi dan node ini menggunakan jaringan manajemen. lingkungan produksi harus menerapkan jaringan penyimpanan terpisah untuk meningkatkan kinerja dan keamanan.

Layanan ini memerlukan dua node. Setiap node membutuhkan minimal satu antarmuka jaringan. Anda dapat menyebarkan lebih dari dua node penyimpanan objek.

## Networking¶
Pilih salah satu opsi jaringan virtual berikut.

### Jaringan Opsi 1: Jaringan Provider
Opsi jaringan penyedia menyebarkan layanan OpenStack Networking dengan cara paling sederhana mungkin dengan terutama layanan lapisan-2 (bridging / switching) dan VLAN segmentasi jaringan. Pada dasarnya, hal ini menjembatani jaringan virtual untuk jaringan fisik dan bergantung pada infrastruktur jaringan fisik untuk layanan lapisan-3 (routing). Selain itu, :term:`DHCP<Dynamic Host Configuration Protocol (DHCP)>`layanan memberikan informasi alamat IP untuk instance.

Pengguna OpenStack membutuhkan lebih banyak informasi tentang infrastruktur jaringan yang mendasarinya untuk menciptakan jaringan virtual agar sesuai dengan infrastruktur.
<p align="center"><img src="https://drive.google.com/uc?export=view&id=1tT1Le-V-dzL3x6wGPyb7er1FOdDsu1s1"></p>
   
## Jaringan Opsi 2: Jaringan self-service¶
Opsi jaringan self-service menambah opsi jaringan provider dengan layanan lapisan-3 (routing) yang mengaktifkan jaringan self-service menggunakan metode segmentasi overlay seperti VXLAN. Pada dasarnya, itu me-rute jaringan virtual ke jaringan fisik dengan menggunakan NAT. Selain itu, opsi ini memberikan landasan bagi layanan canggih seperti LBaaS dan FWaaS.

Pengguna OpenStack dapat membuat jaringan virtual tanpa sepengetahuan infrastruktur yang mendasarinya pada jaringan data. Ini juga bisa mencakup jaringan VLAN jika plug-in layer-2 dikonfigurasikan.
   
<p align="center"><img src="https://drive.google.com/uc?export=view&id=1tT1Le-V-dzL3x6wGPyb7er1FOdDsu1s1"></p>
