<p align="center">
  <img width="460" height="300" src="https://elgg.org/cache/1545410058/default/logo-full.svg">
</p>

# Overview
**Elgg** memungkinkan individu, kelompok, dan institusi untuk menciptakan web *social media* mereka sendiri. **Elgg**, mulai diluncurkan pada tahun 2004, adalah CMS (*content management system*) yang bersifat *open source*. Jika Anda mencari intranet sosial untuk menjalankan situs organisasi Anda, **Elgg** adalah pilihan yang tepat. Untuk informasi lebih lanjut, silahkan kunjungi [**Elgg**](https://elgg.org/).

# Installation
## Langkah 1 :Install Apache, MySQL, dan PHP

Elgg membutuhkan MySQL, PHP, dan sebuah *web server*. Sebelum menginstall Elgg, Hal yang terlebih dahulu dilakukan yaitu menginstall MySQL, dan PHP.

Update repository list.
```
apt-get update
```

Kemudian install apache web server.
```
apt-get install apache2 -y
```

Install MySQL.
```
apt-get install mysql-server -y
```

Selesaikan instalasi MySQL dengan menjalankan perintah berikut.
```
/usr/bin/mysql_secure_installation
```

Pada saat instalasi, anda akan ditanyakan untuk memasukkan root password. Masukkan password yang anda inginkan. Password tersebut akan digunakan untuk root password.
```
Would you like to setup VALIDATE PASSWORD plugin? [Y/N] N
New password: password
Re-enter new password: password
Remove anonymous users? [Y/N] Y
Disallow root login remotely? [Y/N] Y
Remove test database and access to it? [Y/N] Y
Reload privilege tables now? [Y/N] Y
```

Install PHP 7.2
```
apt-get install php7.2 libapache2-mod-php7.2 php7.2-common php7.2-sqlite3 php7.2-curl php7.2-intl php7.2-mbstring php7.2-xmlrpc php7.2-mysql php7.2-gd php7.2-xml php7.2-cli php7.2-zip -y
```

## Langkah 2 : Membuat Database MySQL untuk Elgg

Masuk ke console MySQL
```
mysql -u root -p
```
Setelah berhasil masuk dan masukkan password, Buat database baru.
```
CREATE DATABASE elgg;
```

Buat user MySQL baru dengan menggunakan perintah `GRANT ALL PRIVILEGES` pada database yang baru dibuat. `username` dan `password` dapat diganti sesuai keinginan.

```
GRANT ALL PRIVILEGES on elgg.* to 'username'@'localhost' identified by 'password';
FLUSH PRIVILEGES;
```

Kemudian keluar dari console MySQL
```
exit
```

# Configuration
- Untuk menentukan konfigurasi umum kita dapat membuka submenu `Administration` pada menu `Account` yang terletak di bagian kanan atas layar.
- Pada bagian `Configure`, terdapat tab `Upgrades`, `Appearence`, `Plugins`, `Settings`, dan `Utilities`.
- Tab `Upgrades` berfungsi untuk melakukan update **Elgg** versi terbaru (jika ada).
- Tab `Appearence` berfungsi untuk mengatur tampilan web seperti Menu Items dan Widget.
- Tab `Plugins` berfungsi untuk menambahkan sebuah program yang bisa diintegrasikan dengan **Elgg** untuk memberikan fungsi-fungsi lain yang belum tersedia pada instalasi standar.
- Tab `Settings` dapat digunakan untuk mengganti nama website, site URL, pengaturan log, dan lainnya.

# Maintenance
[]

# How to Use
[]

# Compared to Other CMS
[Dikma]
