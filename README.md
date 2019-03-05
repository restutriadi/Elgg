<p align="center">
  <img width="460" height="300" src="https://elgg.org/cache/1545410058/default/logo-full.svg">
</p>

# Overview
**Elgg** memungkinkan individu, kelompok, dan institusi untuk menciptakan web *social media* mereka sendiri. **Elgg**, mulai diluncurkan pada tahun 2004, adalah CMS (*content management system*) yang bersifat *open source*. Jika Anda mencari intranet sosial untuk menjalankan situs organisasi Anda, **Elgg** adalah pilihan yang tepat. Untuk informasi lebih lanjut, silahkan kunjungi [**Elgg**](https://elgg.org/).

# Installation
## Langkah 1 :Install Apache, MySQL, dan PHP

Elgg membutuhkan MySQL, PHP, dan sebuah web server. Sebelum menginstall Elgg, Hal yang terlebih dahulu dilakukan yaitu menginstall MySQL, dan PHP.

1. Update repository list.
    ```
    $ apt-get update
    ```

2. Kemudian install apache web server.
    ```
    $ apt-get install apache2 -y
    ```

3. Install MySQL.
    ```
    $ apt-get install mysql-server -y
    ```

4. Selesaikan instalasi MySQL dengan menjalankan perintah berikut.
    ```
    $ /usr/bin/mysql_secure_installation
    ```

5. Pada saat instalasi, anda akan ditanyakan untuk memasukkan root password. Masukkan password yang anda inginkan. Password tersebut akan digunakan untuk root password.
    ```
    $ Would you like to setup VALIDATE PASSWORD plugin? [Y/N] N
    $ New password: password
    $ Re-enter new password: password
    $ Remove anonymous users? [Y/N] Y
    $ Disallow root login remotely? [Y/N] Y
    $ Remove test database and access to it? [Y/N] Y
    $ Reload privilege tables now? [Y/N] Y
    ```

6. Install PHP 7.2
    ```
    $ apt-get install php7.2 libapache2-mod-php7.2 php7.2-common php7.2-sqlite3 php7.2-curl php7.2-intl php7.2-mbstring php7.2-xmlrpc php7.2-mysql php7.2-gd php7.2-xml php7.2-cli php7.2-zip -y
    ```

## Langkah 2 : Membuat Database MySQL untuk Elgg

1. Masuk ke console MySQL
    ```
    $ mysql -u root -p
    ```
    
2. Setelah berhasil masuk dan masukkan password, Buat database baru.
    ```
    $ CREATE DATABASE elgg;
    ```

3. Buat user MySQL baru dengan menggunakan perintah `GRANT ALL PRIVILEGES` pada database yang baru dibuat. `username` dan `password` dapat diganti sesuai keinginan.
    ```
    $ GRANT ALL PRIVILEGES on elgg.* to 'username'@'localhost' identified by 'password';
    $ FLUSH PRIVILEGES;
    ```

4. Kemudian keluar dari console MySQL
    ```
    $ exit
    ```

# Configuration
- Untuk menentukan konfigurasi umum kita dapat membuka submenu `Administration` pada menu `Account` yang terletak di bagian kanan atas layar.

- Pada bagian `Configure`, terdapat tab `Upgrades`, `Appearence`, `Plugins`, `Settings`, dan `Utilities`.

  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_configure.PNG)

- Tab `Upgrades` berfungsi untuk melakukan update **Elgg** versi terbaru (jika ada).

  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_upgrades.PNG)

- Tab `Appearence` berfungsi untuk mengatur tampilan web seperti Menu Items dan Widget.

  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_menuItems.PNG)
  
  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_widgets.PNG)  

- Tab `Plugins` berfungsi untuk menambahkan sebuah program yang bisa diintegrasikan dengan **Elgg** untuk memberikan fungsi-fungsi lain yang belum tersedia pada instalasi standar.

  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_plugins.PNG)  

- Tab `Settings` dapat digunakan untuk mengganti nama website, site URL, pengaturan log, dan lainnya.

  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_basicSettings.PNG)
  
  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_advancedSettings.PNG)
  
  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_log.PNG)  

# Maintenance
[]

# How to Use
[]

# Compared to Other CMS
[Dikma]
