# Sistem-Manajemen-Perpustakaan-Berbasis-Web

- Nama : Rizki Cahya Sulistian
- Nim : 23.83.0997
- Judul : Sistem Manajemen Perpustakaan Berbasis Web

## Spesifikasi Server
- Sistem Operasi: Ubuntu Server 20.04 LTS
- CPU: AMD Ryzen 5 3500U
- RAM: 8 GB
- Disk: SSD 256 GB


## Server
- Apache Web Server
- MySQL Database Server
- PHP
- Nginx
- Let's Encrypt

## tujuan projct
saya disini membuat project sistem management perpustakaan Project ini bertujuan untuk membangun sistem manajemen perpustakaan berbasis web yang dapat membantu pengelolaan koleksi buku, peminjaman, pengembalian, dan data anggota perpustakaan secara efisien. Sistem ini dirancang untuk mempermudah akses informasi dan proses administrasi perpustakaan, serta meningkatkan transparansi dan akuntabilitas.

## Operating System
Ubuntu Server 20.04 
https://releases.ubuntu.com/focal/ubuntu-20.04.6-live-server-amd64.iso

## Install Apache web server
```bash
#digunakan di sistem operasi berbasis Debian, seperti Ubuntu, untuk memperbarui daftar paket yang tersedia dan versi terbaru dari repositori perangkat lunak yang telah dikonfigurasi di sistem
sudo apt update
#Menginstal server web Apache2 
sudo apt install apache2
#Mengatur agar Apache2 otomatis dimulai saat sistem booting
sudo systemctl enable apache2
#Memulai layanan Apache2 secara manual 
sudo systemctl start apache2
# konfigurasi
sudo nano /etc/apache2/sites-available/Perpustakaan.conf
# konfigurasi seperti berikut
<VirtualHost *:80>
    ServerName Perpustakaan.com
    DocumentRoot /var/www/Perpustakaan/public
    <Directory /var/www/Perpustakaan/public>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
#aktifkan virtual host
sudo a2ensite Perpustakaan.conf
sudo systemctl restart apache2

```

## Install MySQL Database Server
```bash
#Menginstal server database MySQL
sudo apt install mysql-server
#Menjalankan skrip untuk mengamankan instalasi MySQL
sudo mysql_secure_installation
#Buat Database
mysql -u root -p
CREATE DATABASE perpustakaan_db;
#Buat User Database:
CREATE USER 'nama_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON [nama_database].* TO 'nama_user'@'localhost';
#- Berikan Izin:
FLUSH PRIVILEGES;

```

## Install  PHP
```bash
#digunakan untuk menginstal beberapa komponen penting yang diperlukan untuk menjalankan aplikasi web berbasis PHP di server Apache
sudo apt install php libapache2-mod-php php-mysql
#Aktifkan Modul PHP:
sudo a2enmod php
sudo systemctl restart apache2

```


![download](https://github.com/dword32bit/SysAdmin/assets/114817148/e3318239-a3a4-449d-bd86-79edc65c4b7f)
## Install Nginx
```bash
#digunakan untuk menginstal server web Nginx
sudo apt install nginx
#mengatur agar Nginx otomatis dimulai saat sistem booting.
sudo systemctl enable nginx
#digunakan untuk memulai layanan Nginx secara manual
sudo systemctl start nginx
#Konfigurasi Nginx sebagai Reverse Proxy:
sudo nano /etc/nginx/sites-available/[nama_virtual_host].conf
#Isi file konfigurasi Nginx seperti berikut:
server {
    listen 80;
    server_name [nama_domain_anda];

    location / {
        proxy_pass http://127.0.0.1:80;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

```

## Install Let's Encrypt
```bash
#digunakan untuk menginstal Certbot dan plugin Apache, yang diperlukan untuk mendapatkan dan mengelola sertifikat SSL/TLS dari Let's Encrypt.
sudo apt install certbot python3-certbot-apache
#digunakan untuk secara otomatis mengonfigurasi sertifikat SSL pada server Apache, termasuk mengatur pengalihan dari HTTP ke HTTPS.
sudo certbot --apache

```




  

