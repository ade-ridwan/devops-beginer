# Konfigurasi VMWare dengan Ubuntu 22.04 dan Menjalankan Nginx pada Local IP

## 1. **Menyiapkan Virtual Machine**
1. **Buat Virtual Machine Baru:**
   - Buka VMWare Workstation/Player.
   - Pilih **Create a New Virtual Machine**.
   - Pilih opsi **Installer disc image file (ISO)**, lalu pilih file ISO Ubuntu 22.04.
     **Unduh ISO Ubuntu Server 22.04:**
   - Download file ISO dari [situs resmi Ubuntu](https://ubuntu.com/download/server).
2. **Siapkan software virtualisasi:**
   - Pilih **VirtualBox** atau **VMware Workstation/Player** dan instal di komputer Anda.
3. **Spesifikasi minimum:**
   - **CPU:** 1 GHz atau lebih.
   - **RAM:** 1 GB (direkomendasikan 2 GB).
   - **Disk space:** 10 GB (direkomendasikan 20 GB).

2. **Konfigurasi Virtual Machine:**
   - Pilih tipe OS: **Linux** > **Ubuntu 64-bit**.
   - Alokasikan resource:
     - **RAM**: Minimal 2GB (disarankan 4GB).
     - **Processor**: Minimal 2 core.
   - Buat disk virtual: Minimal 20GB.

3. **Konfigurasi Network Adapter:**
   - Pilih mode jaringan **Bridged** agar VM mendapatkan IP lokal di jaringan yang sama dengan host.

4. **Install Ubuntu:**
   - Ikuti langkah-langkah instalasi Ubuntu.
   - Saat selesai, reboot VM.

---

## 2. **Memasang Nginx di Ubuntu**
1. **Update dan Upgrade Paket:**
   Jalankan perintah berikut di terminal VM:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. **Install Nginx:**
   ```bash
   sudo apt install nginx -y
   ```

3. **Mulai dan Aktifkan Nginx:**
   ```bash
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

4. **Cek Status Nginx:**
   ```bash
   sudo systemctl status nginx
   ```

---

## 3. **Konfigurasi Firewall (Opsional)**
Jika firewall aktif, buka port HTTP (80) dan HTTPS (443):
```bash
sudo ufw allow 'Nginx Full'
sudo ufw enable
```

---

## 4. **Cek Local IP Ubuntu**
1. Jalankan perintah berikut untuk mengetahui IP lokal:
   ```bash
   ip addr show
   ```
   Cari IP pada interface seperti `eth0` atau `ens33`.

2. Contoh output:
   ```
   inet 192.168.1.100/24
   ```
   IP lokal VM adalah `192.168.1.100`.

---

## 5. **Akses Nginx dari Browser Host**
1. Buka browser di mesin host.
2. Masukkan IP lokal VM:
   ```
   http://192.168.1.100
   ```
3. Jika konfigurasi benar, Anda akan melihat halaman default Nginx.

---

## 6. **Konfigurasi Nginx (Opsional)**
Jika ingin membuat server blok baru:
1. Buat file konfigurasi baru:
   ```bash
   sudo nano /etc/nginx/sites-available/my-site
   ```

2. Tambahkan konfigurasi berikut:
   ```nginx
   server {
       listen 80;
       server_name 192.168.1.100;

       root /var/www/my-site;
       index index.html;

       location / {
           try_files $uri $uri/ =404;
       }
   }
   ```

3. Aktifkan konfigurasi:
   ```bash
   sudo ln -s /etc/nginx/sites-available/my-site /etc/nginx/sites-enabled/
   sudo nginx -t
   sudo systemctl reload nginx
   ```

4. Buat folder dan file `index.html`:
   ```bash
   sudo mkdir -p /var/www/my-site
   echo "<h1>Hello from Nginx</h1>" | sudo tee /var/www/my-site/index.html
   ```

---

## Troubleshooting
- **Nginx tidak berjalan:**
  ```bash
  sudo journalctl -xe
  ```
- **Firewall memblokir koneksi:**
  Pastikan port 80 terbuka di firewall host dan VM.

--- 

Dengan langkah-langkah ini, Nginx seharusnya sudah berjalan dan dapat diakses melalui IP lokal Ubuntu pada VMWare.
