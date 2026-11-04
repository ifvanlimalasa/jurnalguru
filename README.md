# Jurnal Mengajar — Versi PWA (Offline)

Versi PWA dari aplikasi Jurnal Mengajar Guru (sebelumnya Google Apps Script + Google Sheets).
Tampilannya mengikuti aslinya (buku jurnal kertas bergaris), tapi berjalan sebagai aplikasi web mandiri:

- **Bisa di-install** di HP Android / iPhone / laptop seperti aplikasi biasa (ikon "Jurnal Guru").
- **Bekerja offline penuh** — setelah dibuka sekali, aplikasi dan datanya tersimpan di perangkat.
- **Data tersimpan lokal** di perangkat (localStorage), bukan di Google Sheets.
- Fitur sama seperti aslinya: login guru NIP + PIN, jadwal hari ini, isi jurnal + absensi siswa
  (H/S/I/A), input nilai (Tugas/UH/PTS/PAS), rekap kelas berbobot + ketuntasan KKM, riwayat,
  ekspor CSV, cadangan/pulihkan data (JSON).

## Cara mencoba langsung
Cukup buka `index.html` di browser. Untuk fitur PWA penuh (install + offline), jalankan lewat
server lokal atau hosting HTTPS, contoh:

```
python3 -m http.server 8080
```
lalu buka http://localhost:8080 — atau upload folder ini ke Netlify / Vercel / GitHub Pages /
hosting statis apa pun (semua file harus satu folder).

Di Chrome Android/desktop akan muncul tombol **Install aplikasi** (atau menu ⋮ → Install).
Di iPhone: Safari → Bagikan → Tambah ke Layar Utama.

## Data contoh
Sama seperti `buatDataContoh` di versi Apps Script:

- Sekolah: **SMP Negeri 2 Wonosobo**, TA 2026/2027, Semester Ganjil, KKM 75,
  bobot Tugas:30, UH:30, PTS:20, PAS:20.
- **6 guru, semua PIN `1234`** — ketuk nama guru di layar masuk untuk mengisi NIP otomatis:
  Sri Rahayu (Bahasa Indonesia), Bambang Hermawan (Matematika), Dewi Kurniasih (IPA),
  Ahmad Fauzi (IPS), Ratna Sari (Bahasa Inggris), Yoga Prasetya (PJOK).
- **96 siswa** di kelas 7A, 7B, 8A, 8B (24 per kelas).
- Jadwal Senin–Jumat (4 blok/hari/kelas), jurnal contoh ±4 minggu ke belakang,
  nilai contoh Tugas 1, Tugas 2, dan Ulangan Harian 1.

Jurnal hanya bisa diisi/diedit untuk hari ini sampai 3 hari ke belakang (sama seperti aslinya).
Di tab **Data & ekspor** ada tombol reset untuk memuat ulang data contoh dari awal.

## Catatan
- Karena data lokal per perangkat, versi ini cocok untuk pemakaian pribadi / demo.
  Untuk dipakai banyak guru dengan data terpusat, datanya perlu disambungkan ke backend
  (misalnya Google Sheets lewat Apps Script sebagai API) — itu langkah berikutnya bila diinginkan.
- PIN disimpan lokal di perangkat (bukan hash server seperti versi Apps Script),
  jadi jangan pakai PIN yang sama dengan akun penting.

## File
- `index.html` — seluruh aplikasi (tampilan + logika + data contoh)
- `manifest.webmanifest` — identitas PWA (nama, ikon, mode standalone)
- `sw.js` — service worker untuk cache offline
- `icon-*.png`, `favicon.png` — ikon aplikasi
