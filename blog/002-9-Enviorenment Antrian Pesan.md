# Antrian pesan untuk Ubuntu
   
OpenStack menggunakan antrian pesan untuk mengoordinasikan operasi dan informasi status di antara layanan. Layanan antrian pesan biasanya berjalan pada node controller. OpenStack mendukung beberapa layanan antrian pesan termasuk RabbitMQ , Qpid , dan ZeroMQ . Namun, sebagian besar distribusi yang mengemas OpenStack mendukung layanan antrian pesan tertentu. Panduan ini mengimplementasikan layanan antrian pesan RabbitMQ karena sebagian besar distribusi mendukungnya. Jika Anda lebih suka menerapkan layanan antrian pesan yang berbeda, lihat dokumentasi yang terkait dengannya.

Antrian pesan berjalan pada node controller.

Instal dan konfigurasikan komponen
Instal paket:

<pre> apt install rabbitmq-server</pre>
Tambahkan openstackpengguna:

<pre> rabbitmqctl add_user openstack RABBIT_PASS

Creating user "openstack" ...</pre>

Ganti RABBIT_PASSdengan kata sandi yang sesuai.

Izinkan akses konfigurasi, tulis, dan baca untuk openstackpengguna:

<pre> rabbitmqctl set_permissions openstack ".*" ".*" ".*"

Setting permissions for user "openstack" in vhost "/" ...</pre>
