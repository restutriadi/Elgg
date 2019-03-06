<p align="center">
  <img width="460" height="300" src="https://elgg.org/cache/1545410058/default/logo-full.svg">
</p>

[Overview](#overview) | [Installation](#installation) | [Configuration](#configuration) | [Maintenance](#maintenance) | [How to Use](#how-to-use) | [Compared to Other CMS](#compared-to-other-cms)
:---:|:---:|:---:|:---:|:---:|:---:

# Overview
**Elgg** memungkinkan individu, kelompok, dan institusi untuk menciptakan web *social media* mereka sendiri. **Elgg**, mulai diluncurkan pada tahun 2004, adalah CMS (*content management system*) yang bersifat *open source*. Jika Anda mencari intranet sosial untuk menjalankan situs organisasi Anda, **Elgg** adalah pilihan yang tepat. Untuk informasi lebih lanjut, silahkan kunjungi [**Elgg**](https://elgg.org/).

# Installation
### Kebutuhan Sistem :
- MySQL 5.0+
- PHP 5.5+
- Apache Web server

### Langkah 1: Install Apache, MySQL, dan PHP
**Elgg** membutuhkan MySQL, PHP, dan sebuah web server. Sebelum menginstall **Elgg**, Hal yang terlebih dahulu dilakukan yaitu menginstall MySQL, dan PHP

1. Update repository list.
    ```
    $ apt-get update
    ```

2. Kemudian install Apache web server.
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

5. Pada saat instalasi, Anda akan ditanyakan untuk memasukkan root password. Masukkan password yang Anda inginkan. Password tersebut akan digunakan sebagai root password.
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

### Langkah 2: Membuat Database MySQL untuk Elgg
1. Masuk ke console MySQL.
    ```
    $ mysql -u root -p
    ```
    
2. Setelah berhasil masuk, masukkan password dan buat database baru.
    ```
    $ CREATE DATABASE elgg;
    ```

3. Buat user MySQL baru dengan menggunakan perintah `GRANT ALL PRIVILEGES` pada database yang baru dibuat. `username` dan `password` dapat diganti sesuai keinginan.
    ```
    $ GRANT ALL PRIVILEGES on elgg.* to 'username'@'localhost' identified by 'password';
    $ FLUSH PRIVILEGES;
    ```

4. Kemudian keluar dari console MySQL.
    ```
    $ exit
    ```

### Langkah 3: Unduh dan Pasang Elgg
1. Unduh versi terbaru dari **Elgg**.
    ```
    $ cd /var/www/html
    $ rm -r index.html
    $ wget https://elgg.org/download/elgg-2.3.7.zip
    ```

2. Ekstrak file yang telah diunduh, kemudian pindahkan ke folder *root* dari Apache web server.
    ```
    $ apt install unzip
    $ unzip elgg-2.3.7.zip
    $ mv ./elgg-2.3.7/* . && rm elgg-2.3.7.zip && rm -r elgg-2.3.7
    ```

3. Membuat direktori data baru untuk **Elgg**.
    ```
    $ sudo mkdir -p /var/www/html/data
    ```

4. Atur *appropriate file permission*.
    ```
    $ sudo chown -R www-data:www-data /var/www/html/
    $ sudo chmod -R 755 /var/www/html/
    ```

### Langkah 4: Mengatur Apache untuk Elgg
1. **Elgg** memerlukan Apache untuk menulis ulang *module*.
    ```
    $ sudo a2enmod rewrite
    ```

2. Membuat file konfigurasi Apache untuk proses pemasangan **Elgg**.
    ```
    $ sudo nano /etc/apache2/sites-available/elgg.conf
    ```

3. *Paste* potongan berikut ke file tersebut, ganti `example.com` sesuai domain Anda.
    ```
    $ <VirtualHost *:80>
    $      DocumentRoot /var/www/html/
    $      ServerName example.com
    $      <Directory /var/www/html/>
    $           Options FollowSymlinks
    $           AllowOverride All
    $           Require all granted
    $      </Directory>
    $      ErrorLog ${APACHE_LOG_DIR}/error.log
    $      CustomLog ${APACHE_LOG_DIR}/access.log combined
    $ </VirtualHost>
    ```

4. *Enable* konfigurasi tersebut dan *restart* server Apache tersebut.
    ```
    $ sudo a2ensite elgg.conf
    $ sudo systemctl restart apache2.service
    ```

### Langkah 5: Selesaikan Pemasangan Elgg
1. Pada tahap ini, Anda dapat menyelesaikan pemasangan melalui browser. Buka browser di komputer Anda dan masuk ke *domain* yang telah dimasukkan. Kemudian akan muncul **Elgg browser installer**.
   
   ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/1.png)

2. Kemudian akan ada **Requirements check** dari server yang Anda buat terlebih dahulu.

   ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/2.png)

3. Lanjutkan pemasangan ke langkah `Database installation`. Di sini masukkan data yang telah Anda buat di **Langkah 2** dan lanjutkan ke tahap selanjutnya.
  
   ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/3fix.png)

4. Tahap selanjutnya, masukkan *site name* dan alamat email yang akan digunakan. Pada bagian `Site URL`, masukkan nama domain Anda. Pada bagian `Data Directory`, masukkan `/var/www/html/data` dan masuk ke langkah selanjutnya.

   ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/5fix.png)

5. Masukkan data untuk *administrator* Anda, dan klik `Next`. Sampai tahap ini, proses pemasangan telah selesai.

   ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/8.png)

6. Anda telah berhasil memasang **Elgg** pada Ubuntu 18.04 VPS dan dapat memulai mengatur jaringan sosial Anda.

   ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/9.png)
  
7. Untuk dapat masuk ke panel administrator, arahkan ke URL berikut.
    ```
    http://{your-domain-name}/admin
    ```

# Configuration
- Untuk menentukan konfigurasi umum kita dapat membuka submenu `Administration` pada menu `Account` yang terletak di bagian kanan atas layar.

  ![administration](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_administration.PNG)

- Pada bagian `Configure`, terdapat tab `Upgrades`, `Appearence`, `Plugins`, `Settings`, dan `Utilities`.

  ![configure](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_configure.PNG)

- Tab `Upgrades` berfungsi untuk melakukan update **Elgg** versi terbaru (jika ada).

  ![upgrade](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_upgrades.PNG)

- Tab `Appearence` berfungsi untuk mengatur tampilan web seperti Menu Items dan Widget.

  ![appearence](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_menuItems.PNG)
  
  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_widgets.PNG)  

- Tab `Plugins` berfungsi untuk menambahkan sebuah program yang bisa diintegrasikan dengan **Elgg** untuk memberikan fungsi-fungsi lain yang belum tersedia pada instalasi standar.

  ![plugin](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_plugins.PNG)  

- Tab `Settings` dapat digunakan untuk mengganti nama website, site URL, pengaturan log, dan lainnya.

  ![basic_setting](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_basicSettings.PNG)
  
  ![advance_setting](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_advancedSettings.PNG)
  
  ![log_setting](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_log.PNG)  

# Maintenance
Apabila kita ingin merubah atau melakukan perbaikan terhadap aplikasi web, kita dapat masuk ke dalam *maintenance mode*. Pada **Elgg**, *user* yang dapat masuk ke dalam website hanyalah admin. Langkah-langkah untuk masuk ke dalam *maintenance mode*, adalah sebagai berikut:
1. Login dengan menggunakan akun admin.
2. Klik submenu `Administration` pada menu `Account`.

   ![administration](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_administration.PNG)

3. Pada bagian `Administer` pilih tab `Utilities` > `Maintenance mode`.

   ![maintenance](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_maintenance.PNG)

4. Pilih **on** pada `Maintenance mode` untuk mengaktifkan *maintenance mode*.
5. Tuliskan pesan yang ingin disampaikan ketika ada orang yang membuka aplikasi saat sedang maintenance ke dalam field `Message displayed to users when maintenance mode is on:`
6. Klik tombol `Save` untuk menyimpan perubahan.

# How to Use
### Add User Account
1. Register
   - Pada halaman awal, pilih `Register`
   
     ![login](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_login.PNG)
     
   - Lengkapi identitas *user*, lalu pilih *Register*
     
     ![register](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_register.PNG)
   
   - Kemudian *user* harus melakukan validasi akun melalui alamat email yang sudah didaftarkan
   
     ![confirm](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_confirm.PNG)
   
2. Register by Admin
   - Admin dapat menambahkan *user* melalui `Administer` > `Users` > `Add New User`
   - Lengkapi identitas *user*, lalu pilih *Register*
   
     ![regist](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_registByAdmin.PNG)
   
   - *User* yang ditambahkan oleh admin, tidak perlu melakukan validasi melalui alamat email
   - Admin juga dapat memvalidasi akun *user* baru pada bagian `Administer` > `Users` > `Unvalidated`
   
     ![validate](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_validate.PNG)

### Add Blog Post
1. Pergi ke menu `Blogs`, lalu pilih *Add blog post*

   ![blogs](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_blog.PNG)

2. Buat post yang diinginkan. Pengguna dapat mengubah isi konten dengan menggunakan HTML (*Edit HTML*)

   ![post](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_addPost.PNG)

3. *User* dapat melihat *Preview* post yang dibuat. Jika post sudah siap di-*publish*, pilih *Save*

### Add Friends
1. Untuk menambahkan teman baru, pergi ke menu `More` > `Members`

   ![members](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_member.PNG)

2. Pada bagian ini, *user* dapat melihat akun *user* yang lain
3. Pilih akun yang ingin ditambahkan sebagai teman, lalu pilih *Add friend* yang berada di bagian bawah foto

   ![friend](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/elgg_profile.PNG)

# Compared to Other CMS

<p align="center">
  <img width="600" height="300" src="https://buddypress.org/media/text.png">
</p>

Dibandingkan dengan CMS *open source* sejenisnya seperti **BuddyPress**, CMS ini memiliki beberapa keunggulan dan kelemahan. Berikut adalah beberapa perbandingan antara kedua CMS ini:

- **Elgg** dapat di *customize* secara luas dan mendalam. Tidak seperti **BuddyPress** yang memiliki limitasi dalam pengembangannya.
- Karena base framework yang berbasis **WordPress**, **BuddyPress** lebih mudah digunakan oleh pengguna dibandingkan **Elgg**. Baik dari sisi *user* maupun dari sisi *administrator*.
- Pembelajaran bagi developer pemula lebih sulit jika menggunakan **Elgg**. Sebaliknya, **BuddyPress** lebih mudah dipahami oleh developer pemula.
