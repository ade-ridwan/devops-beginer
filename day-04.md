# Instalasi dan Konfigurasi GitHub CLI (`gh`) di Ubuntu 22.04

## 1. Instal GitHub CLI

1. **Tambahkan repositori GitHub CLI ke sistem:**

   ```bash
   type -p curl >/dev/null || sudo apt install curl -y
   curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
   sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
   sudo apt update
   ```

2. **Instal GitHub CLI:**

   ```bash
   sudo apt install gh -y
   ```

3. **Verifikasi instalasi:**
   ```bash
   gh --version
   ```

## 2. Login ke GitHub

1. Jalankan perintah:
   ```bash
   gh auth login
   ```
2. Pilih **GitHub.com** untuk login ke akun GitHub Anda.
3. Pilih metode otentikasi:

   - **Browser**: Anda akan diarahkan ke browser untuk login.
   - **Token Personal**: Buat token di [GitHub Personal Access Token](https://github.com/settings/tokens). [gunakan ini jika pakai ubuntu server]

4. Setelah login berhasil, terminal akan menampilkan pesan sukses.

## 3. Konfigurasi Git (Opsional)

Konfigurasi ini akan memastikan commit Anda dikaitkan dengan akun GitHub Anda:

1. Set nama dan email pengguna global:

   ```bash
   git config --global user.name "YourGitHubUsername"
   git config --global user.email "YourGitHubEmail@example.com"
   ```

2. Periksa hasil konfigurasi:
   ```bash
   git config --global --list
   ```

## 4. Operasi GitHub dengan `gh`

Gunakan perintah `gh` untuk mengelola repositori GitHub:

- **Clone repositori:**

  ```bash
  gh repo clone <username>/<repo-name>
  ```

- Untuk melihat dokumentasi lebih lengkap tentang `gh`:
  ```bash
  gh help
  ```
