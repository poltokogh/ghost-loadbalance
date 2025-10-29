# **Ghost CMS Load Balancer Deployment**

Repositori ini berisi konfigurasi untuk **Ghost CMS** yang dijalankan dengan **HAProxy** sebagai *load balancer*, serta integrasi **Cloudflare Origin SSL Certificate** dan **Cloudflare Zero Trust Tunnel**.  
Tujuannya adalah membuat setup Ghost CMS yang **aman (HTTPS)**, **terdistribusi (multi-container)**, dan **mudah diakses melalui Cloudflare**.

---

## ⚙️ **1. Persiapan Awal**

### **Kebutuhan Sistem**
Pastikan kamu sudah memiliki:
- Domain aktif yang dikelola melalui **Cloudflare**
- **Docker** & **Docker Compose** telah terinstal
- Port 80 dan 443 terbuka di server
- File repo sudah di-*clone* ke server:
  ```bash
  git clone https://github.com/poltokogh/ghost-loadbalance.git
  cd ghost-loadbalance

## ☁️ **2. Konfigurasi Sertifikat Cloudflare**

1. Masuk ke Cloudflare Dashboard
2. Pilih domain kamu
3. Buka tab SSL/TLS → Origin Server
4. Klik Create Certificate, pilih opsi RSA
5. Unduh dua file yang dihasilkan:
   - origin.pem
   - origin-key.pem
6. Gabungkan kedua file menjadi satu sertifikat:
   ```bash
   cat origin.pem origin-key.pem > ~/ghost-loadbalance/haproxy/haproxy-origin.pem

## 📂 **3. Struktur Direktori HAProxy**

Pastikan folder *haproxy/* memiliki struktur seperti ini:
  ```markdown
  haproxy/
  ├── Dockerfile
  ├── haproxy-origin.pem
  └── haproxy.cfg
  ```

## 🚀 **4. Menjalankan Deployment**

Jalankan perintah berikut untuk membangun dan menjalankan seluruh layanan:
  ```bash
    docker compose build
    docker compose up -d --scale ghost=3
  ```

## 🛜 **5. Konfigurasi Cloudflare Zero Trust**

Tambahkan konfigurasi berikut ke dalam file _config.yaml_ di Cloudflare Tunnel:
```yaml
tunnel: <tunnel-id>
credentials-file: /etc/cloudflared/<tunnel-id>.json

ingress:
  - hostname: ghost.fajarawan.online
    service: https://172.23.12.104
    originRequest:
      noTLSVerify: true
  - service: http_status:404
```
