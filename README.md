# Compose-ci-cd-Minggu11
# Tugas Minggu 11: CI untuk Repo Compose

![CI](https://github.com/satnurz85-web/Compose-ci-cd-Minggu11/actions/workflows/compose-check.yml/badge.svg)


**Nama:** Nadya Shafwah Mujahidin
**NIM:** 202557201048
**Mata kuliah:** Teknologi Open Source

## Deskripsi
Workflow ini memvalidasi sintaks file docker-compose.yml (stack WordPress + MariaDB) secara otomatis. Workflow berjalan setiap ada push ke branch main dan setiap ada Pull Request.

## Isi repositori
- .github/workflows/compose-check.yml : workflow CI
- docker-compose.yml : stack WordPress + MariaDB (tugas minggu 10)
- .env.example : contoh variabel lingkungan tanpa rahasia asli
- .gitignore : mengabaikan .env

## Cara kerja workflow
Pemicunya adalah event push ke branch main dan pull_request. Workflow punya satu job bernama validate yang berjalan di runner ubuntu-latest. Job ini punya tiga step: 
(1) checkout untuk mengambil kode repo ke runner 
(2) menyalin .env.example menjadi .env karena file .env asli tidak ada di repo 
(3) menjalankan docker compose config -q untuk memeriksa sintaks file Compose tanpa menjalankan container.
(4) docker compose up -d untuk menjalankan stack
(5) docker compose ps untuk menampilkan status container
(6) docker compose down -v untuk mematikan stack. 
Step 4 sampai 6 adalah step bonus.

## Bukti
1. Run hijau di tab Actions
   ![Run hijau](bukti/1-run-hijau.png)
2. Pull Request dengan check gagal (merah)
   ![PR merah](bukti/2-pr-merah.png)
3. Badge status di README
   ![Badge](bukti/3-badge.png)
4. Run bonus (up, ps, down) hijau
   ![Bonus](bukti/4-bonus-hijau.png)

Tautan Pull Request (sudah hijau dan di-merge): https://github.com/satnurz85-web/Compose-ci-cd-Minggu11/pull/1 

## Kendala dan cara mengatasinya


## Refleksi singkat
CI membuat kesalahan pada file Compose ketahuan beberapa menit setelah push, sebelum digabung ke main. Dengan begitu saya tidak perlu mengandalkan ingatan untuk memeriksa file secara manual. Hasil hijau atau merah juga terlihat jelas di PR, sehingga perubahan yang rusak tidak ikut ter-merge.
