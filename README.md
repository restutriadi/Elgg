<p align="center">
  <img width="460" height="300" src="https://elgg.org/cache/1545410058/default/logo-full.svg">
</p>

# Overview
**Elgg** memungkinkan individu, kelompok, dan institusi untuk menciptakan web *social media* mereka sendiri. **Elgg**, mulai diluncurkan pada tahun 2004, adalah CMS (*content management system*) yang bersifat *open source*. Jika Anda mencari intranet sosial untuk menjalankan situs organisasi Anda, **Elgg** adalah pilihan yang tepat. Untuk informasi lebih lanjut, silahkan kunjungi [**Elgg**](https://elgg.org/).

# Installation
### Langkah 1: Install Apache, MySQL, dan PHP
Elgg membutuhkan MySQL, PHP, dan sebuah web server. Sebelum menginstall Elgg, Hal yang terlebih dahulu dilakukan yaitu menginstall MySQL, dan PHP

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

### Langkah 2: Membuat Database MySQL untuk Elgg
1. Masuk ke console MySQL.
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

4. Kemudian keluar dari console MySQL.
    ```
    $ exit
    ```

### Langkah 3: Unduh dan Pasang Elgg
1. Unduh versi terbaru dari Elgg.
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

3. Membuat direktori data baru untuk Elgg.
    ```
    $ sudo mkdir -p /var/www/html/data
    ```

4. Atur *appropriate file permission*.
    ```
    $ sudo chown -R www-data:www-data /var/www/html/
    $ sudo chmod -R 755 /var/www/html/
    ```

### Langkah 4: Mengatur Apache untuk Elgg
1. Elgg memerlukan Apache untuk menulis ulang *module*.
    ```
    $ sudo a2enmod rewrite
    ```

2. Membuat file konfigurasi Apache untuk proses pemasangan Elgg.
    ```
    $ sudo nano /etc/apache2/sites-available/elgg.conf
    ```

3. *Paste* potongan berikut ke file tersebut, ganti `example.com` sesuai domain anda.
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
1. Pada tahap ini, anda dapat menyelesaikan pemasangan melalui browser. Buka browser di komputer anda dan masuk ke *domain* yang telah dimasukkan. Kemudian akan muncul **Elgg browser installer**.

  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/1.png)

2. Kemudian akan ada **Requirements check** dari server yang anda buat terlebih dahulu.

  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/2.png)

3. Lanjutkan pemasangan ke langkah `Database installation`. Di sini masukkan data yang telah anda buat di **Langkah 2** dan lanjutkan ke tahap selanjutnya.
  
  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/3fix.png)

4. Tahap selanjutnya, masukkan *site name* dan alamat email yang akan digunakan. Pada bagian `Site URL`, masukan nama domain anda. Pada bagian `Data Directory`, masukan `/var/www/html/data` dan masuk ke langkah selanjutnya.

  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/5fix.png)

5. Masukan data untuk *administrator* anda, dan klik `Next`. Sampai tahap ini, proses pemasangan telah selesai.

  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/8.png)

6. Untuk dapat masuk ke panel administrator, arahkan ke URL berikut.
    ```
    http://{your-domain-name}/admin
    ```

7. Anda telah berhasil memasang Elgg pada Ubuntu 18.04 VPS dan dapat memulai mengatur jaringan sosial anda.

  ![alt text](https://raw.githubusercontent.com/restutriadi/Elgg/master/image/9.png)

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
