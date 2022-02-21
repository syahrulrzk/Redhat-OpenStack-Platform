# Database SQL untuk RHEL dan CentOS
   
Sebagian besar layanan OpenStack menggunakan database SQL untuk menyimpan informasi. Basis data biasanya berjalan pada node pengontrol. Prosedur dalam panduan ini menggunakan MariaDB atau MySQL tergantung pada distribusinya. Layanan OpenStack juga mendukung database SQL lainnya termasuk PostgreSQL .

Instal dan konfigurasikan komponen
Instal paket:

<pre># yum install mariadb mariadb-server python2-PyMySQL</pre>

Buat dan edit /etc/my.cnf.d/openstack.cnffile (cadangkan file konfigurasi yang ada /etc/my.cnf.d/jika diperlukan) dan selesaikan tindakan berikut:

Buat [mysqld]bagian, dan atur bind-address kunci ke alamat IP manajemen dari node pengontrol untuk mengaktifkan akses oleh node lain melalui jaringan manajemen. Setel kunci tambahan untuk mengaktifkan opsi yang berguna dan rangkaian karakter UTF-8:

<pre>
[mysqld]
bind-address = 10.0.0.11

default-storage-engine = innodb
innodb_file_per_table = on
max_connections = 4096
collation-server = utf8_general_ci
character-set-server = utf8
</pre>

Selesaikan instalasi
Mulai layanan database dan konfigurasikan untuk memulai saat sistem melakukan booting:
<pre>
# systemctl enable mariadb.service
# systemctl start mariadb.service
</pre>
Amankan layanan database dengan menjalankan mysql_secure_installation skrip. Secara khusus, pilih kata sandi yang sesuai untuk rootakun database:

<pre># mysql_secure_installation</pre>
