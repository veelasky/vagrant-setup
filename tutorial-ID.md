## Opo Kui Vagrant?

Vagrant adalah virtual machine portable yang biasa digunakan sebagai development environment ketika develop sebuah aplikasi (dalam hal ini web application).

##### Keuntungan memakai vagrant
- Flexibility: Anda bisa develop aplikasi anda dengan OS yang anda gunakan dengan editor favorit anda tanpa harus instalasi OS baru.
- Portability: Anda bisa dengan mudah membawa dev machine anda dan menjalankan dari mana saja.
- Stress Free: Dengan memakai vagrant machine, anda bisa develop dengan nyaman tanpa perlu mengkuatirkan apakah program aplikasi anda akan jalan di production server.
- Automation: Dengan `provision`, vagrant bisa automasi package yang anda butuhkan ketika menjalankan vagrant, tanpa harus instalasi paket satu persatu.

## Skenario

Untuk memudahkan pemahaman dalam membaca tutorial ini, berikut adalah skenario nya.

- OS Windows
- saya sedang develop sebuah aplikasi di path `D:/codebase/aplikasi/`
- saya ingin konfigurasi aplikasi saya agar bisa jalan di server linux dengan memakai full lamp stack.

## Instalasi

Sebelum memulai instalasi, anda akan membutuhkan beberapa software yang harus anda download

> WARNING: Bandwidth Killer!! Download dari kantor kalo bisa. :grin:

- [Vagrant](http://www.vagrantup.com/). duh?!
- [VirtualBox](https://www.virtualbox.org/). VM yang digunakan oleh vagrant untuk virtualisasi.
- [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html). digunakan untuk akses ssh kedalam virtual machine anda.
- [Ubuntu 12.04](http://files.vagrantup.com/precise32.box). OS yang kita gunakan untuk virtual machine kita, sebenarnya ada banyak sekali pilihan untuk OS yang bisa kita gunakan, tapi untuk tutorial ini kita gunakan Ubuntu 12.04.

Silahkan memulai instalasi vagrant dan virtual box di local komputer anda.

Untuk memudahkan pengorganisasian files pindahkan file `precise32.box` ke directory `D:\vagrant\boxes\` (kalo belum ada silahkan dibuat).

## Your Fist Box!

Setelah proses instalasi selesai kita bisa mulai melakukan initial setup untuk vagrant machine.

Karena kita sedang develop di `D:/codebase/aplikasi` kita akan buat `VagrantFile` pertama kita dari sana. Masuk ke dalam windows command prompt, dan pindahkan lokasi anda ke `D:/codebase/aplikasi/`.

Setelah anda berada di `D:/codebase/aplikasi` jalankan perintah sebagai berikut

```
    D:\codebase\aplikasi> vagrant init aplikasi ..\..\vagrant\boxes\precise32.box
```

> `aplikasi` adalah nama dari virtual machine anda,  sedangkan `../../vagrant/boxes/precise32.box` adalah path dimana anda menyimpan file Ubuntu 12.04 yang anda download ketika pertama kali instalasi.

Setelah ada konfirmasi bahwa `VagrantFile` telah dibuat, gunakan perintah `vagrant up` untuk boot virtual machine anda.

```
    D:\codebase\aplikasi> vagrant up
```

Sekarang anda bisa akses virtual machine anda dengan PuTTY, dengan konfigurasi

```
    Host: 127.0.0.1
    Port: 2222
    Username: vagrant
    Password: vagrant
    PrivateKey: C:\users\[your-window-username]\.vagrant.d\insecure_private_key
```

> Konfigurasi SSH Key pada putty ada pada `Connection - SSH - Auth`

Pada saat ini proses pembuatan virtual machine sudah selesai. Mudah bukan?!

Setiap kali kita melakukan perintah `vagrant init` vagrant akan membuat file bernama `VagrantFile` di tempat dimana anda bekerja sekarang (dari command prompt). File tersebut berisi konfigurasi specific dari virtual box anda, Anda bisa dengan mudah copy/paste file tersebut ke dalam root folder dari aplikasi yang anda buat dan langsung menjalankan `vagrant up`

## Konfigurasi

#### Sinkronisasi
Setelah kita berhasil membuat virtual machine kita yang pertama, selanjutnya kita akan membuat virtual machine kita mengenali folder dari windows kita, caranya sangat mudah, buka `VagrantFile` dan temukan baris:

```
    # config.vm.synced_folder "../data", "/vagrant"
```

Remark baris tersebut dan ganti parameter pertama dengan folder aplikasi kita (D:\codebase\aplikasi\, karena dalam hal ini `VagrantFile` berada dalam direktori tersebut kita akan representasikan dengan '.') dan ganti juga parameter kedua dengan alias `/aplikasi` sehingga akan menjadi seperti dibawah ini:

```
    config.vm.synced_folder ".", "/aplikasi"
```

Selanjut nya gunakan perintah `vagrant reload` untuk reload virtual machine anda.

> Setiap kali kita selesai merubah konfigurasi di `VagrantFile` kita akan melakukan perintah `vagrant reload` untuk load konfigurasi terbaru.

Login ke virtual machine anda dengan PuTTY dan ketikkan baris perintah sebagai berikut:

```
    ls aplikasi
```

Anda akan melihat folder anda sekarang sudah berada di virtual machine kita. Setiap kali kita melakukan perubahan file, virtual machine kita akan secara otomatis mengenali, sehingga memudahkan anda untuk develop dengan editor kesayangan anda.

#### Provisioning

Salah satu fitur vagrant yang sangat keren adalah provisioning, dalam bahasa awam bisa dikatakan sebagai automatisasi. Vagrant menyediakan berbagai macam cara untuk provisioning:

- `shell`: automatisasi menggunakan shell script
- `puppet`: automatisasi menggunakan [Puppet](http://puppetlabs.com/puppet/puppet-enterprise)
- `chef`: automatisasi menggunakan [Chef](http://www.getchef.com/chef/)

Untuk tutorial ini, kita akan menggunakan Chef sebagai sistem provisioning kita. 

