# Panduan Instalasi Ubuntu Server 22.04 pada Mesin Virtual (VM)

## 1. Persiapan Awal
1. **Unduh ISO Ubuntu Server 22.04:**
   - Download file ISO dari [situs resmi Ubuntu](https://ubuntu.com/download/server).
2. **Siapkan software virtualisasi:**
   - Pilih **VirtualBox** atau **VMware Workstation/Player** dan instal di komputer Anda.
3. **Spesifikasi minimum:**
   - **CPU:** 1 GHz atau lebih.
   - **RAM:** 1 GB (direkomendasikan 2 GB).
   - **Disk space:** 10 GB (direkomendasikan 20 GB).

---

## 2. Membuat Mesin Virtual
### Di VirtualBox:
1. **Buka VirtualBox** dan klik `New`.
2. **Konfigurasi mesin virtual:**
   - **Name:** Masukkan nama (misalnya `UbuntuServer22`).
   - **Type:** Linux.
   - **Version:** Ubuntu (64-bit).
3. **Set RAM:** Minimal 1024 MB (rekomendasi 2048 MB).
4. **Buat hard disk virtual:**
   - Pilih `Create a virtual hard disk now` → klik `Create`.
   - Pilih `VDI` dan `Dynamically allocated` → set ukuran disk (20 GB direkomendasikan).
5. Setelah selesai, klik `Settings` pada VM baru:
   - Pilih **Storage** → Klik ikon CD → Pilih file ISO Ubuntu Server.

### Di VMware:
1. **Buka VMware** dan pilih `Create a New Virtual Machine`.
2. Pilih `Installer disc image file (ISO)` → Masukkan file ISO Ubuntu Server.
3. **Konfigurasi hardware:**
   - Pilih tipe sistem operasi `Linux` → Versi `Ubuntu 64-bit`.
   - Set RAM minimal 1 GB.
   - Pilih ukuran disk minimal 20 GB.

---

## 3. Proses Instalasi Ubuntu Server
1. **Start VM:**
   - Klik `Start` (VirtualBox) atau `Power on` (VMware).
2. **Pilih bahasa:**
   - Pilih `English` atau bahasa lain sesuai preferensi.
3. **Pilih keyboard layout:**
   - Pilih tata letak keyboard, biasanya `English (US)`.
4. **Jaringan:**
   - Konfigurasikan jaringan secara otomatis (pilih default `DHCP`).
5. **Disk setup:**
   - Pilih `Use entire disk` untuk memformat dan menggunakan seluruh disk.
6. **Profil pengguna:**
   - Masukkan nama pengguna, hostname, dan password sesuai kebutuhan.
7. **Paket tambahan:**
   - Anda bisa memilih untuk menginstal paket seperti `OpenSSH` (direkomendasikan untuk akses remote).
8. **Tunggu instalasi selesai.**
   - Setelah selesai, reboot VM.

---

## 4. Post-Install
1. **Login ke sistem:**
   - Masukkan username dan password yang telah dibuat.
2. **Update sistem:**
3. 
   ```bash
   sudo apt update && sudo apt upgrade -y
