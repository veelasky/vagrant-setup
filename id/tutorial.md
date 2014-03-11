### Opo Kui Vagrant?


Vagrant adalah _virtual machine_ portable, yang bisa digunakan untuk proses _development_ sebuah aplikasi (dalam hal ini web application). 

Dengan vagrant kita bisa develop aplikasi kita dengan meniru secara tidak langsung _production server_, 
yang terkadang berbeda dengan _development environment_ yang kita gunakan ketika tahap _development_.

### Catatan

Tutorial ini dimaksudkan kepada pengguna windows yang akan menginstall linux sebagai _guest OS_, dalam contoh ini kita memakai Ubuntu 12.04 `precise pangolin`.


### Install

> untuk memudahkan anda nantinya ketika setup vagrant, anda bisa lakukan instalasi di directory dimana anda biasa bekerja.

Untuk instalasi vagrant di windows pertama kita harus download [VirtualBox](https://www.virtualbox.org/) dan [Vagrant](http://www.vagrantup.com/downloads.html) dan install pada komputer.

Apabila semua berjalan lancar (setelah restart dan segala macamnya), kita bisa test dengan [windows command prompt](http://lmgtfy.com/?q=windows+command+prompt) dan jalankan

```
    C:/Users/wongganteng> vagrant --help
```

Selamat! anda sudah berhasil menginstall vagrant! :+1:


### Your First Box

Untuk membuat _virtual machine_ pertama anda, yang anda perlukan cuma ketikkan perintah dibawah ini:

```
    C:/Users/wongganteng> vagrant init development http://files.vagrantup.com/precise32.box
```

`development` merupakan nama dari _box_ kita, dan kita akan install `precise pangolin` dari vagrant cloud.

> Anda mungkin mengalami error ketika pertama kali menjalankan perintah ini, kenapa?! pake modem usb sih downloadnya. :stuck_out_tongue:
> Just kidding, apabila anda mengalami error, download manual file precise32.box dari browser anda, dan simpan di tempat yang aman.
> Dan kembali jalankan perintah `vagrant init development tempat\yang\aman\precise32.box`

Setelah berhasil membuat _box_ pertama anda, sekarang saat nya untuk bermain dengan _box_ yang sudah kita buat, gunakan [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) untuk akses ssh ke dalam server anda, dengan konfigurasi sebagai berikut:

```
    Host: 127.0.0.1
    Port: 2222
    Username: vagrant
    Password: vagrant
    PrivateKey: [Lokasi Private Key Anda] (kalo di saya: C:/Users/wongganteng/.vagrant.d/insecure_private_key
```

> Apabila anda tidak tahu cara menggunakan PuTTY anda bisa lihat tutorial nya [di sini](http://lmgtfy.com/?q=how+to+use+putty).

Nah saat ini anda sudah masuk kedalam _virtual machine_ anda, gimana?! keren kan?! :grin:

Setiap kali anda melakukan `vagrant init` anda akan membuat satu `VagrantFile` di tempat anda menjalankan perintah (dalam contoh ini: `C:/users/wongganteng/`), `VagrantFile` merupakan konfigurasi dari _box_ yang baru saja anda buat.

Di dalam, `VagrantFile` ada konfigurasi untuk mount disk anda ke dalam development environtment. Buka `VagrantFile` anda dan edit baris ini:

```
    config.vm.synced_folder "../data", "/codebase"
```

`../data` merupakan path windows anda yang akan anda baca di _development box_ anda, sedangkan `/codebase` merupakan mount alias yang akan kita baca di _development box_.

Setelah merubah file tersebut gunakan perintah `vagrant reload` untuk restart vagrant machine dan load new configuration. Setelah menyala kembali vagrant machine anda, gunakan PuTTY untuk kembali login ke _development box_ anda.

Ketikkan perintah:
```
    ls codebase
```
Dan anda akan melihat  file anda sudah terbaca dalam _development box_ anda!! HOW COOL IS THAT?!

### Lanjutan

-- To Be Continued --