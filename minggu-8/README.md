# Laporan Konfigurasi Web Server dan FTP Server

### Dosen pengampu: Dr. Ferry Astika Saputra. S.T, M.Sc.

### 1. Vanessa Florentina Patricia (3121600001)

### 2. Achmad Zahir Wajdi (3121600012)

### 3. M. Naufal Ikrom (3121600019)

### Kelas : 2 D4 Teknik Informatika A

## 1. Web Server, php, dan database

### 1.1 Instalasi package web server, php, dan database

Masukkan perintah dibawah untuk menginstall webserver (apache2), php dan database(mariadb-server)

```console
sudo apt install apache2 php php-mysql phpmyadmin mysql-server
```

![instalasi package](assets/WhatsApp%20Image%202023-04-27%20at%2011.57.13.jpeg)

kemudian `enter` dan tunggu proses instalasi. Setelah itu akan muncul tampilan untuk mengatur webserver yang akan digunakan untuk phpmyadmin

![phpmyadmin_config](assets/WhatsApp%20Image%202023-04-27%20at%2011.57.14.jpeg)

pilih `apache2` dengan tekan spasi, kemudian enter. Kemudian akan diarahkan lagi untuk mengatur

![configure_database_for_phpmyadmin](<assets/WhatsApp%20Image%202023-04-27%20at%2011.57.14%20(1).jpeg>)

pilih yes dan enter dan tunggu sampai selesai.

Untuk mengecek apakah webserver sudah terinstall, masukkan perintah `sudo systemctl status apache2`

![apache_service](assets/WhatsApp%20Image%202023-04-27%20at%2011.57.15.jpeg)

### 1.2 mariadb-server

Pada langkah sebelumnya mariadb sudah berhasil terinstall, namun belum ada konfigurasi. Masukkan perintah dibawah untuk mengkonfigurasi

```console
sudo mysql_secure_installation
```

Setelah di enter, maka akan dihadapkan beberapa pilihan konfigurasi seperti password dan lain-lain. Kemudian tunggu sampai proses selesai

![mariadb_config](assets/Screenshot%202023-04-27%20130754.png)

### 1.3 Login User sebagai Root

Pertama masuk ke root user dengan perintah

```console
sudo mysql -u root password
```

![login_user](assets/WhatsApp%20Image%202023-04-27%20at%2011.55.37.jpeg)

### 1.4 .htaccess

Jika diperlukan konfigurasi .htaccess, buka file `apache2.conf` dengan perintah di bawah

```console
sudo nano /etc/apache2/apache2.conf
```

Cari baris kode `AccessFileName .htaccess`. Jika di depannya ada tanda pagar (#) silakan dihapus.

Kemudian temukan baris kode dengan script di bawah ini.

```console
<Directory /var/www/>
     Options Indexes FollowSymLinks
     AllowOverride None
     Require all granted
</Directory>
```

Kemudian ganti kata “None” menjadi “All”

`AllowOverride All`

Selanjutnya aktifkan ModRewrite dengan mengetikkan perintah.

```console
sudo a2enmod rewrite
```

Terakhir restart apache server

```console
sudo service apache2 restart
```

## 2. FTP Server

### 2.1 Install Package Proftpd

lakukan instalasi package Proftpd dengan menggunakan perintah berikut :

```console
sudo apt-get install proftpd
```

![update](assets/WhatsApp%20Image%202023-04-27%20at%2008.22.01.jpeg)

### 2.2 Melakukan backup

Sebelum mengedit file anda perlu melakukan backup paa file `proftpd.conf` dengan mengetikan perintah berikut.

```console
sudo cp /etc/proftpd/proftpd.conf /etc/proftpd/proftpd.conf.backup
```

![update](assets/WhatsApp%20Image%202023-04-27%20at%2008.22.02.jpeg)

### 2.3 Melakukan edit pada file proftpd.conf

Untuk mengedit file proftpd.conf dengan mengetikan perintah berikut.

```console
sudo nano /etc/proftpd/proftpd.conf
```

![update](<assets/WhatsApp%20Image%202023-04-27%20at%2008.22.02%20(1).jpeg>)

setelah itu akan terbuka file `proftpd.conf`. anda hanya perlu menganti beberapa baris untuk settingan default.

Ubah UseIPv6 yang awalnya on menjadi off, dan kemudian Ubah Domain sesuai dengan nama Domain Anda. Disini Nama Domain saya adalah `kampus-06.takehome.com`.

![update](assets/WhatsApp%20Image%202023-04-27%20at%2008.22.15.jpeg)

Setelah itu uncommand `DefaultRoot` di bagian bawah file.

![update](<assets/WhatsApp%20Image%202023-04-27%20at%2008.22.15%20(1).jpeg>)

Setelah itu anda dapat menekan `"Ctrl+X"` untuk keluar dan tekan `"Y"` untuk konfirmasi dan kemudian tekan `"Enter"`.

### 2.4 Membuat user

Masukkan perintah `sudo adduser [namauser]` untuk membuat user, kemudian tekan `y`

Anda dapat mengubah `namauser` dengan nama yang ingin anda berikan pada user. kemudian isi data yang muncul di layar. untuk yang wajib di isi adalah.

```console
New password :
Retype new password :
```

Kemudian tekan `Y` untuk konfirmasi.

![update](assets/WhatsApp%20Image%202023-04-27%20at%2008.22.16.jpeg)

### 2.5 Ujicoba Access FTP

Anda bisa menggunakan file exploler pada windows atau dengan file exploler lainnya.

jika anda menggunakan file exploler pada windows, anda dapat mengetikan alamat ip servic seperti berikut

![update](assets/WhatsApp%20Image%202023-04-27%20at%2008.22.38.jpeg)

Kemudian tekan `Enter` dan anda akan di arahkan untuk melakukan login dengan memasukkan username dan password.

![update](assets/WhatsApp%20Image%202023-04-27%20at%2008.22.39.jpeg)

Setelah itu masukan Username and Password anda lalu tekan Log On. dan selamat anda sudah dapat melakukan Upload file pada server.
