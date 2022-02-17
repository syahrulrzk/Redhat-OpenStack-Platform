# Environment (lingkungan)
   
Bagian ini menjelaskan cara mengkonfigurasi controller node dan satu compute node menggunakan arsitektur contoh.

Meskipun sebagian besar lingkungan termasuk Identity, layanan Image, Compute, setidaknya satu layanan jaringan, dan Dashboard, layanan Object Storage dapat beroperasi secara independen. Jika use case Anda hanya melibatkan Object Storage, Anda bisa lewati

<ul>
  <li>Object Storage Installation Guide for Stein</li>
  <li>Object Storage Installation Guide for Rocky</li>
  <li>Object Storage Installation Guide for Queens</li>
  <li>Object Storage Installation Guide for Pike</li>
</ul>
  
setelah mengkonfigurasi node yang sesuai untuk itu.

Anda harus menggunakan akun dengan hak akses administratif untuk mengkonfigurasi setiap node. Baik menjalankan perintah sebagai pengguna root atau mengkonfigurasi utilitas sudo.

 <b>Catatan</b>

systemctl enable memanggil output openSUSE pesan peringatan ketika layanan menggunakan skrip SysV Init bukan file systemd asli. Peringatan ini bisa diabaikan.


Untuk performa terbaik, kami merekomendasikan bahwa lingkungan Anda memenuhi atau melebihi persyaratan hardware di Persyaratan hardware.

Persyaratan minimum berikut harus mendukung lingkungan proof-of-concept dengan layanan inti dan beberapa instance CirrOS:

<li>Controller Node: 1 prosesor, memori 4 GB, dan storage 5 GB</li>
<li>Controller Node: 1 prosesor, memori 2 GB, dan storage 10 GB</li>
<br>
Karena jumlah layanan OpenStack dan mesin virtual meningkat, begitu juga kebutuhan hardware untuk kinerja terbaik. Jika kinerja menurun setelah mengaktifkan layanan tambahan atau mesin virtual, pertimbangkanlah untuk menambahkan sumber daya perangkat keras untuk lingkungan Anda.

Untuk meminimalkan kekacauan dan menyediakan lebih banyak sumber daya untuk OpenStack, kami menyarankan instalasi minimal distribusi Linux Anda. Juga, Anda harus menginstal versi 64-bit dari distribusi Anda pada setiap node.

Sebuah partisi disk tunggal pada setiap node bekerja untuk kebanyakan instalasi dasar. Namun, Anda harus mempertimbangkan Logical Volume Manager (LVM) untuk instalasi dengan layanan opsional seperti Block Storage.

Untuk tujuan instalasi dan pengujian pertama kali, banyak pengguna memilih untuk membangun masing-masing host sebagai virtual machine (VM). Manfaat utama dari VMs meliputi berikut ini:

Satu server fisik dapat mendukung beberapa node, masing-masing dengan hampir semua jumlah antarmuka jaringan.

Kemampuan untuk mengambil periodik "snap shots" selama proses instalasi dan "roll back" ke konfigurasi berjalan ketika terjadi masalah.

Namun, VM akan mengurangi kinerja instance Anda, terutama jika hypervisor Anda dan/atau prosesor kekurangan dukungan untuk akselerasi hardware untuk nested VM.

<b>Catatan</b>

Jika Anda memilih untuk menginstal pada VM, pastikan hypervisor Anda menyediakan cara untuk menonaktifkan penyaringan MAC address pada antarmuka jaringan provider

Untuk informasi lebih lanjut tentang persyaratan sistem, lihat OpenStack Pike Administrator Guides, the OpenStack Queens Administrator Guides, atau the OpenStack Rocky Administrator Guides.
<ul>
  <li>Keamanan</li>
  <li>Host networking</li>
  <li>Network Time Protocol (NTP)</li>
  <li>Paket OpenStack</li>
  <li>SQL database</li>
  <li>Message queue (antrian pesan)</li>
  <li>Memcached</li>
  <li>Etcd</li>
</ul>
