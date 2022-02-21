# Basis data SQL untuk Ubuntu
   
Sebagian besar layanan OpenStack menggunakan database SQL untuk menyimpan informasi. Basis data biasanya berjalan pada node pengontrol. Prosedur dalam panduan ini menggunakan MariaDB atau MySQL tergantung pada distribusinya. Layanan OpenStack juga mendukung database SQL lainnya termasuk PostgreSQL .

Pada Ubuntu 20.04, instal paket-paket:

<pre> apt install mariadb-server python3-pymysql</pre>

Pada Ubuntu 18.04 atau 16.04, instal paket:

<pre> apt install mariadb-server python-pymysql</pre>

Buat dan edit ```/etc/mysql/mariadb.conf.d/99-openstack.cnffile``` dan selesaikan tindakan berikut:

Buat [mysqld]bagian, dan atur bind-address kunci ke alamat IP manajemen dari node pengontrol untuk mengaktifkan akses oleh node lain melalui jaringan manajemen. Setel kunci tambahan untuk mengaktifkan opsi yang berguna dan rangkaian karakter UTF-8:

<pre>
[mysqld]
bind-address = 10.0.0.11</pre>

<pre>
default-storage-engine = innodb
innodb_file_per_table = on
max_connections = 4096
collation-server = utf8_general_ci
character-set-server = utf8
</pre>

Selesaikan instalasi
Mulai ulang layanan basis data:

<pre> service mysql restart<pre>
Amankan layanan database dengan menjalankan mysql_secure_installation skrip. Secara khusus, pilih kata sandi yang sesuai untuk rootakun database:

<pre> mysql_secure_installation</pre>
