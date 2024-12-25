Deploy Aplikasi Web Statis ke Google App Engine

Panduan ini menjelaskan langkah-langkah untuk mendeply aplikasi web statis (HTML, CSS, JS) ke Google App Engine menggunakan Cloud Shell.

🗁 Struktur Direktori

Pastikan aplikasi Anda memiliki struktur direktori berikut:

my-static-website/
├── app.yaml
├── index.html
├── assets/
    ├── css/
    ├── js/
    └── images/

🌐 Langkah-langkah

1. Pilih Proyek Google Cloud

Pilih proyek Google Cloud yang akan digunakan:

gcloud config set project [PROJECT_ID]

2. Aktifkan App Engine

Aktifkan App Engine di proyek Anda dengan perintah berikut:

gcloud app create --region=[REGION]

Catatan: Ganti [REGION] dengan lokasi App Engine yang diinginkan, seperti us-central atau asia-southeast1.

3. Upload File ke Cloud Shell

Di Google Cloud Console, buka tab File di sisi kiri layar Cloud Shell.

Upload file dan folder aplikasi Anda dengan drag-and-drop ke direktori Cloud Shell.

Pastikan struktur direktori tetap seperti ini:

my-static-website/
├── app.yaml
├── index.html
├── assets/
    ├── css/
    ├── js/
    └── images/

Masuk ke direktori aplikasi:

cd my-static-website

4. Konfigurasi app.yaml

Buat file app.yaml dengan isi berikut:

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

Penjelasan:

runtime: python39 menandakan runtime Python 3.9.

handlers digunakan untuk mengatur bagaimana file statis diakses:

url: / menunjukkan root URL akan memuat index.html.

url: /assets akan mengarah ke direktori assets/.

url: /.* memastikan semua URL lainnya diarahkan ke index.html (berguna untuk SPA).

5. Deploy Aplikasi

Deploy aplikasi ke App Engine dengan perintah berikut:

gcloud app deploy

Ketika diminta konfirmasi, ketik Y.

Tunggu hingga proses selesai.

6. Akses Aplikasi

Setelah berhasil deploy, aplikasi Anda dapat diakses di URL berikut:

https://[PROJECT_ID].appspot.com

Ganti [PROJECT_ID] dengan ID proyek Google Cloud Anda.

7. 🕵️ Periksa Log (Opsional)

Untuk memeriksa log aplikasi Anda, gunakan perintah berikut:

gcloud app logs tail -s default

🚀 Selamat Mencoba!

Jika ada kendala, pastikan untuk memeriksa kembali langkah-langkah di atas atau kunjungi dokumentasi resmi Google Cloud.

