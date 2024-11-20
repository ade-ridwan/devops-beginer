## Setting MultiPort Nginx
---
### 1. Instalasi PHP
Tambahkan repository PHP dan instal versi yang dibutuhkan:
```bash
sudo add-apt-repository ppa:ondrej/php
sudo apt install php8.2-fpm
```

---

### 2. Konfigurasi Server Block
Masuk ke direktori `/etc/nginx/sites-available` dan edit file `default` untuk menambahkan dua server block:

#### Server Block untuk HTML
```nginx
server {
  listen 3344; # Port untuk HTML
  server_name localhost;

  root /var/www/magang/html;
  index index.html;

  location / {
    try_files $uri $uri/ /index.html;
  }
}
```

#### Server Block untuk PHP
```nginx
server {
  listen 1122; # Port untuk PHP info
  server_name localhost;

  root /var/www/magang/php;
  index index.php;

  location / {
    try_files $uri $uri/ /index.php;
  }

  location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/run/php/php8.2-fpm.sock;
  }
}
```

---

### 3. Periksa Sintaks dan Restart Nginx
Uji konfigurasi Nginx:
```bash
sudo nginx -t
```
Jika sintaks benar, restart Nginx:
```bash
sudo systemctl restart nginx
```

---

### 4. Buat File Konfigurasi Terpisah
Untuk pengelolaan yang lebih baik, pisahkan konfigurasi ke dalam dua file: `html.conf` dan `php.conf`.

1. Buat `html.conf` untuk server HTML.
2. Buat `php.conf` untuk server PHP.

---

### 5. Aktifkan File Konfigurasi Baru
Hapus file default di `sites-enabled` dan buat symlink:
```bash
ln -s /etc/nginx/sites-available/html.conf /etc/nginx/sites-enabled/
ln -s /etc/nginx/sites-available/php.conf /etc/nginx/sites-enabled/
```
Restart Nginx:
```bash
sudo systemctl restart nginx
```

---

## Verifikasi Setup
- **Halaman HTML**: Buka `localhost:3344`
- **PHP Info**: Buka `localhost:1122`
