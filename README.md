#### **Deploy Aplikasi Web Statis ke Google App Engine** 📡

Panduan ini menjelaskan langkah-langkah untuk mendeply aplikasi web statis (HTML, CSS, JS) ke **Google App Engine** 

menggunakan **Cloud Shell**.

---

####  Langkah-langkah untuk Deploy

 1. Pilih Proyek Google Cloud
    
    Tentukan proyek Google Cloud yang akan digunakan
```
gcloud config set project [PROJECT_ID]
```
 2. Aktifkan App Engine
    
    Aktifkan App Engine di proyek Anda
```
gcloud app create --region=[REGION]
```

 Gantilah [REGION] dengan lokasi yang diinginkan, misalnya:
```
 us-central
 asia-southeast1
```

 3. Upload File ke Cloud Shell
    
     Di Google Cloud Console, buka tab "File" di sisi kiri layar Cloud Shell.
     Upload file dan folder aplikasi Anda dengan drag-and-drop ke direktori Cloud Shell.

##### Struktur direktori aplikasi:
```
 my-static-website/
 ├── app.yaml
 ├── index.html
 ├── assets/
     ├── css/
     ├── js/
     └── images/
```

 4. Masuk ke Direktori Aplikasi
```
cd my-static-website
```

 5. Konfigurasi app.yaml
```

# Buat file app.yaml dengan isi berikut:
cat <<EOL > app.yaml
runtime: python39
handlers:
  - url: /
    static_files: index.html
    upload: index.html
  - url: /assets
    static_dir: assets
  - url: /.*
    static_files: index.html
    upload: index.html
EOL
```

 Penjelasan:
 - runtime: python39 menandakan runtime Python 3.9.
 - handlers digunakan untuk mengatur bagaimana file statis diakses:
   - url: / untuk menampilkan index.html di root URL.
   - url: /assets mengarahkan ke direktori assets/.
   - url: /.* memastikan semua URL lainnya mengarah ke index.html (berguna untuk SPA).

 6. Deploy Aplikasi
    
    Deploy aplikasi ke App Engine dengan perintah:
```
gcloud app deploy
```

 Ketika diminta konfirmasi, ketik Y untuk melanjutkan.

 7. Akses Aplikasi
    Setelah berhasil deploy, aplikasi Anda dapat diakses di URL berikut:
```
 https://[PROJECT_ID].appspot.com
```
Gantilah [PROJECT_ID] dengan ID proyek Google Cloud Anda.

 8. Periksa Log Aplikasi (Opsional)
    
    Untuk memeriksa log aplikasi, gunakan perintah:
```
gcloud app logs tail -s default
```
