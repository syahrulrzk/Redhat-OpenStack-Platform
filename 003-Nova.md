# OpenStack Compute (nova)

## Apa itu nova?
Nova adalah proyek OpenStack yang menyediakan cara untuk menyediakan instance komputasi (alias server virtual). Nova mendukung pembuatan mesin virtual, server baremetal (melalui penggunaan ironic), dan memiliki dukungan terbatas untuk wadah sistem. Nova berjalan sebagai satu set daemon di atas server Linux yang ada untuk menyediakan layanan itu.

Ini membutuhkan layanan OpenStack tambahan berikut untuk fungsi dasar:
<li><b>Keystone</b> : Ini memberikan identitas dan otentikasi untuk semua layanan OpenStack.</li>
<li><b>Glance</b>: Ini menyediakan repositori gambar komputasi. Semua instans komputasi diluncurkan dari gambar sekilas.</li>
<li><b>Neutron</b> : Ini bertanggung jawab untuk menyediakan jaringan virtual atau fisik yang terhubung dengan instans komputasi saat boot.</li>
<li><b>Placement</b>: Ini bertanggung jawab untuk melacak inventaris sumber daya yang tersedia di cloud dan membantu dalam memilih penyedia sumber daya mana yang akan digunakan saat membuat mesin virtuPlacement:l.</li>

Ini juga dapat berintegrasi dengan layanan lain untuk memasukkan: persistent block storage, encrypted disks, and baremetal compute instances.

## Arsitektur Sistem Nova
Nova terdiri dari beberapa proses server, masing-masing melakukan fungsi yang berbeda. Antarmuka yang menghadap pengguna adalah REST API, sementara komponen Nova secara internal berkomunikasi melalui mekanisme pengiriman pesan RPC.

Server API memproses permintaan REST, yang biasanya melibatkan pembacaan/penulisan basis data, secara opsional mengirim pesan RPC ke layanan Nova lainnya, dan menghasilkan respons terhadap panggilan REST. Pesan RPC dilakukan melalui perpustakaan oslo.messaging , sebuah abstraksi di atas antrian pesan. Nova menggunakan arsitektur "tidak berbagi apa-apa" berbasis pesan dan sebagian besar komponen nova utama dapat dijalankan di banyak server, dan memiliki manajer yang mendengarkan pesan RPC. Satu-satunya pengecualian utama adalah layanan komputasi, di mana satu proses berjalan pada hypervisor yang dikelolanya (kecuali saat menggunakan driver VMware atau Ironic). Manajer juga, secara opsional, memiliki tugas berkala. Untuk detail lebih lanjut tentang sistem RPC kami, lihat AMQP dan Nova .

Nova menggunakan database SQL tradisional untuk menyimpan informasi. Ini (secara logis) dibagi antara beberapa komponen. Untuk membantu pemutakhiran, database diakses melalui lapisan objek yang memastikan bidang kontrol yang ditingkatkan masih dapat berkomunikasi dengan node komputasi yang menjalankan rilis sebelumnya. Untuk memungkinkan hal ini, layanan yang berjalan pada basis data proxy node komputasi meminta melalui RPC ke manajer pusat yang disebut konduktor.

Untuk memperluas penyebaran Nova secara horizontal, kami memiliki konsep sharding penerapan yang disebut sel . Semua penerapan berisi setidaknya satu sel. Untuk informasi lebih lanjut, lihat Sel (v2) .
<p align="center"><img src="https://drive.google.com/uc?export=view&id=1WKpnHu-_GxAFd2bJ0-5udTLYMBRrRd9C"> </p>
<ul>
  <li>DB : Database SQL untuk penyimpanan data.</li>
  <li>API : Komponen yang menerima permintaan HTTP, mengubah perintah dan berkomunikasi dengan komponen lain melalui antrian oslo.messaging atau HTTP.</li>
  <li>Scheduler : Memutuskan host mana yang mendapatkan setiap instance.</li>
  <li>Compute : Mengelola komunikasi dengan hypervisor dan mesin virtual.</li>
  <li>Konduktor : Menangani permintaan yang memerlukan koordinasi (membangun/mengubah ukuran), bertindak sebagai proxy database, atau menangani konversi objek.</li>
  <li>:placement-doc:`Placement <>` : Melacak inventaris dan penggunaan penyedia sumber daya.</li>
</ul>
Meskipun semua layanan dirancang agar dapat diskalakan secara horizontal, Anda harus memiliki komputasi yang jauh lebih banyak daripada yang lainnya.

## For End User
Sebagai pengguna akhir nova, Anda akan menggunakan nova untuk membuat dan mengelola server dengan alat atau API secara langsung.
<ul>
  <li><b>Horizon</b> : UI web resmi untuk Proyek OpenStack.</li>
  <li><b>OpenStack Client</b> : CLI resmi untuk Proyek OpenStack. Anda harus menggunakan ini sebagai CLI Anda untuk banyak hal, ini tidak hanya mencakup perintah nova tetapi juga perintah untuk sebagian besar proyek di OpenStack.</li>
  <li><b>Nova Client</b> : Untuk beberapa fitur (atau perintah administratif) nova yang sangat canggih, Anda mungkin perlu menggunakan klien nova. Itu masih didukung, tetapi cli <b>openstack</b> direkomendasikan.</li>
</ul>
