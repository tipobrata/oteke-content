+++
title = "Instalasi Lampp Server"
date = "2017-06-22T21:49:20+02:00"
tags = ["lmde", "linux"]
categories = ["linux"]
author = "tipobrata"
+++

Download xampp-linux-5.6.3-0-installer.run terlebih dahulu

# Cara Menjalankan Instalasi 

Ubah permission:

```
sudo chmod +x xampp-linux-5.6.3-0-installer.run
```

Install aplikasi:

```
sudo ./xampp-linux-5.6.3-0-installer.run
```

# Untuk menghentikan Xampp Service:

```
sudo /opt/lampp/lampp stop
```

# Untuk menjalankan Xampp service:

```
sudo /opt/lampp/lampp start
```

# Untuk menjalankan Xampp dalam versi GUI, bisa menggunakan printah berikut.

```
cd /opt/lampp
./manager-linux.run
```

Cara menjalankan aplikasi versi GUI, kamu lebih meudah untuk menjalankan service Apache, dan MySql. 

# Cara Menjalankan Yii2

copy folder project ke directory `/opt/lampp/httdoc/` dan tambahkan permission di bawah

``
sudo chmod -R 777 basic
```

buka `localhost/basic/web/`

# menjalankan mysql/mariaDB di terminal

masuk ke directory `/opt/lampp/bin`

```
$ cd /opt/lampp/bin $ 
```
jalankan command di bawah: 
```
./mysql -u root
```