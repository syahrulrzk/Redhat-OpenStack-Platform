# Configure network interfaces¶

<ul>
<li>Mengkonfigurasi interface pertama sebagai interface manajemen:
IP address: 10.0.0.11
Network mask: 255.255.255.0 (or /24)
  Default gateway: 10.0.0.1</li>

<li>Provider interface menggunakan konfigurasi khusus tanpa alamat IP yang ditugaskan untuk itu. Mengkonfigurasi interface kedua sebagai provider interface:
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

<ul><li>Reboot sistem untuk mengaktifkan perubahan.</li></ul>

