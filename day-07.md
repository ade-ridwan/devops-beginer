
# Instalasi MySQL dan phpMyAdmin dengan Nginx di Ubuntu 22.04

## **1. Persiapan Sistem**

1. **Install Paket Pendukung:**
   ```bash
   sudo apt install wget curl unzip software-properties-common -y
   ```

---

## **2. Instalasi MySQL**
1. **Install MySQL Server:**
   ```bash
   sudo apt install mysql-server -y
   ```

2. **Amankan Instalasi MySQL:**
   Jalankan wizard untuk konfigurasi keamanan:
   ```bash
   sudo mysql_secure_installation
   ```
   Anda akan diminta untuk:
   - Menentukan sandi root MySQL.
   - Menonaktifkan login root jarak jauh.
   - Menghapus pengguna anonim dan basis data uji coba.

3. **Cek Status MySQL:**
   Pastikan MySQL berjalan:
   ```bash
   sudo systemctl status mysql
   ```

---

## **3. Instalasi Nginx**
1. **Install Nginx:**
   ```bash
   sudo apt install nginx -y
   ```

2. **Cek Status Nginx:**
   ```bash
   sudo systemctl status nginx
   ```

3. **Aktifkan Nginx untuk Start Otomatis:**
   ```bash
   sudo systemctl enable nginx
   ```

---

## **4. Instalasi PHP dan Modul PHP untuk Nginx**
1. **Tambahkan Repository PHP:**
   ```bash
   sudo add-apt-repository ppa:ondrej/php -y
   sudo apt update
   ```

2. **Install PHP dan Modulnya:**
   Install PHP (versi 8.1 atau sesuai kebutuhan) beserta modul pendukung:
   ```bash
   sudo apt install php-fpm php-mysql php-cli php-curl php-zip php-mbstring php-xml php-bcmath -y
   ```

3. **Konfigurasi PHP-FPM untuk Nginx:**
   Edit file konfigurasi PHP-FPM:
   ```bash
   sudo nano /etc/php/8.1/fpm/php.ini
   ```
   Cari dan ubah nilai berikut:
   ```ini
   cgi.fix_pathinfo=0
   ```

4. **Restart PHP-FPM:**
   ```bash
   sudo systemctl restart php8.1-fpm
   ```

---

## **5. Instalasi phpMyAdmin**
1. **Download phpMyAdmin:**
   ```bash
   wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.zip
   ```

2. **Ekstrak dan Pindahkan ke Direktori Web:**
   ```bash
   unzip phpMyAdmin-latest-all-languages.zip
   sudo mv phpMyAdmin-*-all-languages /usr/share/phpmyadmin
   ```

3. **Buat Direktori Temp:**
   ```bash
   sudo mkdir -p /usr/share/phpmyadmin/tmp
   sudo chmod 777 /usr/share/phpmyadmin/tmp
   ```

4. **Buat Konfigurasi Nginx untuk phpMyAdmin:**
   Buat file konfigurasi baru:
   ```bash
   sudo nano /etc/nginx/sites-available/phpmyadmin
   ```
   Tambahkan konfigurasi berikut:
   ```nginx
   server {
       listen 80;
       server_name your_domain_or_ip;

       root /usr/share/phpmyadmin;
       index index.php index.html index.htm;

       location / {
           try_files $uri $uri/ =404;
       }

       location ~ \.php$ {
           include snippets/fastcgi-php.conf;
           fastcgi_pass unix:/run/php/php8.1-fpm.sock;
           fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
           include fastcgi_params;
       }

       location ~ /\.ht {
           deny all;
       }
   }
   ```

5. **Aktifkan Konfigurasi dan Restart Nginx:**
   ```bash
   sudo ln -s /etc/nginx/sites-available/phpmyadmin /etc/nginx/sites-enabled/
   sudo nginx -t
   sudo systemctl restart nginx
   ```

---

## **6. Uji Instalasi**
1. **Akses phpMyAdmin:**
   Buka browser dan akses:
   ```
   http://your_domain_or_ip
   ```
   Masuk menggunakan kredensial MySQL Anda.

2. **Jika Mengalami Error Permission:**
   Pastikan direktori memiliki izin yang benar:
   ```bash
   sudo chown -R www-data:www-data /usr/share/phpmyadmin
   sudo chmod -R 755 /usr/share/phpmyadmin
   ```

---
