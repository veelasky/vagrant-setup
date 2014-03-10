### Opo Kui Vagrant?

Vagrant adalah _virtual machine_ portable, yang bisa digunakan untuk proses _development_ sebuah aplikasi (dalam hal ini web application). 

Dengan vagrant kita bisa develop aplikasi kita dengan meniru secara tidak langsung _production server_, yang terkadang berbeda dengan _development environment_ yang kita gunakan ketika tahap _development_.

Apalagi dengan maraknya penggunaan `node.js` package manager, dan ruby `gem`.

### Catatan

Tutorial ini dimaksudkan kepada pengguna windows yang akan menginstall linux sebagai _guest OS_, dalam hal ini Ubuntu 12.04 `precise pangolin`.


### Install

> untuk memudahkan anda nantinya ketika setup vagrant, anda bisa lakukan instalasi di directory dimana anda biasa bekerja.

Untuk instalasi vagrant di windows pertama kita harus download [VirtualBox](https://www.virtualbox.org/) dan [Vagrant](http://www.vagrantup.com/downloads.html) dan install pada komputer.

Apabila semua berjalan lancar (setelah restart dan segala macamnya), kita bisa test dengan [windows command prompt](http://lmgtfy.com/?q=windows+command+prompt) dan jalankan

```
    C:\Users\wongganteng> vagrant --help
```

Selamat! anda sudah berhasil menginstall vagrant! :+1:


### Your First Box

Untuk membuat _virtual machine_ pertama anda, yang anda perlukan cuma ketikkan perintah dibawah ini:

```
    C:\Users\wongganteng> vagrant init development http://files.vagrantup.com/precise32.box
```

`development` merupakan nama dari _machine_ kita, dan kita akan install `precise pangolin` dari vagrant cloud.

> Anda mungkin mengalami error ketika pertama kali menjalankan perintah ini, kenapa?! pake modem usb sih downloadnya. :stuck_out_tongue:
> Just kidding, apabila anda mengalami error, download manual file precise32.box dari browser anda, dan simpan di tempat yang aman.
> Dan kembali jalankan perintah `vagrant init development tempat\yang\aman\precise32.box`