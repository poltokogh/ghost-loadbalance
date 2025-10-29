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

