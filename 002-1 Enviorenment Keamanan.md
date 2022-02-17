# Keamanan
Layanan OpenStack mendukung berbagai metode keamanan termasuk password, kebijakan, dan enkripsi. Selain itu, layanan pendukung termasuk server database dan perantara pesan (message broker) mendukung keamanan password.

Untuk memudahkan proses instalasi, panduan ini hanya mencakup keamanan kata sandi bila berlaku. Anda dapat membuat kata sandi yang aman secara manual, namun string koneksi database dalam file konfigurasi layanan tidak dapat menerima karakter khusus seperti "@". Sebaiknya Anda buat mereka menggunakan alat seperti pwgen, atau dengan menjalankan perintah berikut:

<pre>$ openssl rand -hex 10</pre>

Untuk layanan OpenStack, panduan ini menggunakan SERVICE_PASS untuk layanan referensi password akun dan SERVICE_DBPASS untuk referensi password database.

Tabel berikut daftar layanan yang membutuhkan password dan referensi terkait dalam panduan.

 <table align="center" border="1" cellpadding="10">
        <tr> 
          <th>Nama password</th> <th>Deskripsi</th>
        </tr> 
        <tr>
            <td>Password database (tidak ada variabel yang digunakan)</td>
            <td>Password root untuk database</td>
        </tr>
        <tr>
            <td>ADMIN_PASS</td>
            <td>Password ``admin` pengguna</td>
        </tr>
        <tr>
            <td>CINDER_DBPASS</td>
            <td>Password database untuk layanan Block Storage</td>
        </tr>
        <tr>
            <td>CINDER_PASS</td>
            <td>Password layanan Blok Storage cinder pengguna</td>
        </tr>
        <tr>
            <td>DASH_DBPASS</td>
            <td>Password database untuk Dashboard</td>
        </tr>
        <tr>
            <td>DEMO_PASS</td>
            <td>Password demo pengguna</td>
        </tr>
        <tr>
            <td>GLANCE_DBPASS</td>
            <td>Password database untuk layanan Image</td>
        </tr>
         <tr>
            <td>GLANCE_PASS</td>
            <td>Password layanan Image glance pengguna</td>
        </tr> <tr>
            <td>KEYSTONE_DBPASS</td>
            <td>Password database layanan Identity</td>
        </tr> <tr>
            <td>METADATA_SECRET</td>
            <td>Rahasia untuk proxy metadata</td>
        </tr> <tr>
            <td>NEUTRON_DBPASS</td>
            <td>Password database untuk layanan Networking</td>
        </tr> <tr>
            <td>NEUTRON_PASS</td>
            <td>Password layanan Networking neutron pengguna</td>
        </tr> <tr>
            <td>NOVA_DBPASS</td>
            <td>Password database untuk layanan Compute</td>
        </tr> <tr>
            <td>NOVA_PASS</td>
            <td>Password layanan Compute nova pengguna</td>
        </tr> <tr>
            <td>PLACEMENT_PASS</td>
            <td>Sandi pengguna layanan Placement placement</td>
        </tr> <tr>
            <td>RABBIT_PASS</td>
            <td>Password dari pengguna RabbitMQ openstack</td>
 </table>

OpenStack dan layanan pendukung memerlukan hak administratif selama instalasi dan operasi. Dalam beberapa kasus, layanan melakukan modifikasi pada host yang dapat mengganggu alat otomasi penyebaran seperti Ansible, Chef, dan Puppet. Sebagai contoh, beberapa layanan OpenStack menambahkan pembungkus root (root wrapper) ke `` sudo`` yang dapat mengganggu kebijakan keamanan. Lihat Compute service documentation for Pike, the Compute service documentation for Queens, atau the Compute service documentation for Rocky untuk informasi lebih lanjut.

Layanan Networking mengasumsikan nilai default untuk parameter jaringan kernel dan memodifikasi aturan firewall. Untuk menghindari sebagian besar masalah selama instalasi awal Anda, kami sarankan menggunakan pengerahan stok distribusi yang didukung pada host Anda. Namun, jika Anda memilih untuk mengotomatisasi pengerahan host Anda, tinjaulah konfigurasi dan kebijakan yang diterapkan kepada mereka sebelum melanjutkan lebih lanjut.
