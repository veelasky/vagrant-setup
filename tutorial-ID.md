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
- [Ubuntu 12.04](https://opscode-vm.s3.amazonaws.com/vagrant/opscode_ubuntu-12.04_chef-11.2.0.box). OS yang kita gunakan untuk virtual machine kita, sebenarnya ada banyak sekali pilihan untuk OS yang bisa kita gunakan, tapi untuk tutorial ini kita gunakan Ubuntu 12.04.

Silahkan memulai instalasi vagrant dan virtual box di local komputer anda.

Untuk memudahkan pengorganisasian files pindahkan file `opscode_ubuntu-12.04_chef-11.2.0.box` ke directory `D:\vagrant\boxes\` (kalo belum ada silahkan dibuat).

## Your Fist Box!

Setelah proses instalasi selesai kita bisa mulai melakukan initial setup untuk vagrant machine.

Karena kita sedang develop di `D:/codebase/aplikasi` kita akan buat `VagrantFile` pertama kita dari sana. Masuk ke dalam windows command prompt, dan pindahkan lokasi anda ke `D:\codebase\aplikasi\`.

Setelah anda berada di `D:/codebase/aplikasi` jalankan perintah sebagai berikut

```
    D:\codebase\aplikasi> vagrant init aplikasi ../../vagrant/boxes/opscode_ubuntu-12.04_chef-11.2.0.box
```

> `aplikasi` adalah nama dari virtual machine anda,  sedangkan `../../vagrant/boxes/opscode_ubuntu-12.04_chef-11.2.0.box` adalah path dimana anda menyimpan file Ubuntu 12.04 yang anda download ketika pertama kali instalasi.

