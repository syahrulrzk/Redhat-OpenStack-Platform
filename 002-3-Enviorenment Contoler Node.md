# Configure network interfaces¶
<ul>
<li>1. Mengkonfigurasi interface pertama sebagai interface manajemen:
IP address: 10.0.0.11
Network mask: 255.255.255.0 (or /24)
  Default gateway: 10.0.0.1</li>

<li>2. Provider interface menggunakan konfigurasi khusus tanpa alamat IP yang ditugaskan untuk itu. Mengkonfigurasi interface kedua sebagai provider interface:
Ganti INTERFACE_NAME dengan nama interface yang sebenarnya. Misalnya, *eth1 * atau *ens224 *.
  Untuk Ubuntu:</li>
</ul>

Untuk Ubuntu/Debian :
<li>Edit file /etc/network/interfaces berisi sebagai berikut:</li>
<pre>
# The provider network interface
auto INTERFACE_NAME
iface INTERFACE_NAME inet manual
up ip link set dev $IFACE up
down ip link set dev $IFACE down</pre>

Untuk RHEL/CENTOs
<li>Edit file /etc/sysconfig/network-scripts/ifcfg-INTERFACE_NAME mengandung berikut:
Jangan mengubah HWADDR dan UUID keys.</li>
<pre>
DEVICE=INTERFACE_NAME
TYPE=Ethernet
ONBOOT="yes"
BOOTPROTO="none"</pre>

<ul><li>3. Reboot sistem untuk mengaktifkan perubahan.</li></ul>

# Konfigurasi resolusi nama¶

<ul>
  <ol>1. Mengatur hostname dari node untuk controller.</ol>
  <ol>2. Mengedit file /etc/hosts memuat berikut</ol>
</ul>

<pre>
# controller
10.0.0.11       controller

# compute1
10.0.0.31       compute1

# block1
10.0.0.41       block1

# object1
10.0.0.51       object1

# object2
10.0.0.52       object2</pre>


# Compute node
   
Configure network interfaces¶
Mengkonfigurasi interface pertama sebagai interface manajemen:
<pre>
IP address: 10.0.0.31
Network mask: 255.255.255.0 (or /24)
Default gateway: 10.0.0.1
</pre>

 ==Catatan

Compute node tambahan harus menggunakan 10.0.0.32, 10.0.0.33, dan sebagainya.
Provider interface menggunakan konfigurasi khusus tanpa alamat IP yang ditugaskan untuk itu. Mengkonfigurasi interface kedua sebagai provider interface:
Ganti INTERFACE_NAME dengan nama interface yang sebenarnya. Misalnya, *eth1 * atau *ens224 *.

Untuk Ubuntu:
Edit file /etc/network/interfaces berisi sebagai berikut:

# The provider network interface
<pre>
auto INTERFACE_NAME
iface  INTERFACE_NAME inet manual
up ip link set dev $IFACE up
down ip link set dev $IFACE down
</pre>
Untuk RHEL atau CentOS:

Edit file /etc/sysconfig/network-scripts/ifcfg-INTERFACE_NAME mengandung berikut:
Jangan mengubah HWADDR dan UUID keys.
<pre>
DEVICE=INTERFACE_NAME
TYPE=Ethernet
ONBOOT="yes"
BOOTPROTO="none"
Untuk SUSE:
</pre>

Mengedit file /etc/sysconfig/network/ifcfg-INTERFACE_NAME mengandung berikut:
<pre>
STARTMODE='auto'
BOOTPROTO='static'
</pre>
Reboot sistem untuk mengaktifkan perubahan.

Konfigurasi resolusi nama¶
Mengatur hostname dari node untuk compute1.

Mengedit file /etc/hosts memuat berikut:

<pre>
# controller
10.0.0.11       controller

# compute1
10.0.0.31       compute1

# block1
10.0.0.41       block1

# object1
10.0.0.51       object1

# object2
10.0.0.52       object2</pre>

 ==Peringatan

Beberapa distribusi menambahkan sebuah entri asing di `` file / etc / hosts`` yang memecahkan hostname yang sebenarnya ke alamat IP loopback lain seperti `` 127.0.1.1``. Anda harus komentar atau bahkan menghapus entri ini untuk mencegah masalah resolusi nama. ** Jangan menghapus entri 127.0.0.1. **


 ==Catatan

Panduan ini mencakup entri host untuk layanan opsional untuk mengurangi kompleksitas harus Anda memilih untuk mengerahkan mereka.
