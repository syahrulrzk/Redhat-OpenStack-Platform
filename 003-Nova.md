# OpenStack Compute (nova)

## Apa itu nova? kan
Nova adalah proyek OpenStack yang menyediakan cara untuk menyediakan instance komputasi (alias server virtual). Nova mendukung pembuatan mesin virtual, server baremetal (melalui penggunaan ironic), dan memiliki dukungan terbatas untuk wadah sistem. Nova berjalan sebagai satu set daemon di atas server Linux yang ada untuk menyediakan layanan itu.

Ini membutuhkan layanan OpenStack tambahan berikut untuk fungsi dasar:
<li>Keystone : Ini memberikan identitas dan otentikasi untuk semua layanan OpenStack.</li>
<li>Glance: Ini menyediakan repositori gambar komputasi. Semua instans komputasi diluncurkan dari gambar sekilas.</li>
<li>Neutron : Ini bertanggung jawab untuk menyediakan jaringan virtual atau fisik yang terhubung dengan instans komputasi saat boot.</li>
<li>Placement: Ini bertanggung jawab untuk melacak inventaris sumber daya yang tersedia di cloud dan membantu dalam memilih penyedia sumber daya mana yang akan digunakan saat membuat mesin virtuPlacement:l.</li>
