# Jurnal Mengajar (Google Apps Script)

Aplikasi jurnal guru: jadwal hari ini, jurnal mengajar, absensi siswa per jam pelajaran, input nilai, rekap kelas, dan dashboard kepala sekolah. Berjalan di Google Apps Script + Google Sheets, tanpa hosting.

## File
- `Code.gs`: logika server (login guru, jurnal, absensi, nilai, rekap, dashboard)
- `Index.html`: aplikasi guru (NIP + PIN)
- `Admin.html`: dashboard kepala sekolah / operator (`?page=admin`)
- `Css.html`: gaya, ikon, dan fungsi bersama
- `appsscript.json`: manifest

## Instalasi
1. Buat spreadsheet baru (https://sheets.new) lalu buka **Ekstensi > Apps Script**.
2. Tempel `Code.gs`. Buat file HTML `Index`, `Admin`, `Css` lalu tempel isinya.
3. Di Project Settings centang *Show "appsscript.json"* dan ganti isinya dengan file dari ZIP.
4. Jalankan fungsi `setup` dan berikan izin.
5. (Opsional) Jalankan `buatDataContoh` untuk melihat 6 guru (PIN `1234`), 96 siswa, jadwal, dan jurnal sebulan.
6. **Deploy > New deployment > Web app**: Execute as *Me*, Who has access *Anyone*.

## Sheet
- **Pengaturan**: nama sekolah, tahun ajaran, semester, `jam_pelajaran` (jam ke-1, ke-2, ... dipisah koma), `kkm`, `bobot_nilai` (misal `Tugas:30,UH:30,PTS:20,PAS:20`), `batas_isi_hari`, `password_admin` (wajib diganti).
- **Guru**: NIP, Nama, Mapel, No HP, PIN (hash, diatur dari dashboard), Aktif.
- **Siswa**: NIS, Nama, Kelas, L/P, Aktif.
- **Jadwal**: Hari (1 = Senin ... 6 = Sabtu), Jam Ke (`1-2`, `3-4`, atau `5`), Kelas, Mapel, NIP guru.
- **Jurnal**, **Absensi**, **Nilai**: terisi otomatis dari aplikasi.

## Alur
1. Guru membuka aplikasi, memilih jam di jadwal hari ini, mengisi materi dan absensi, lalu menyimpan.
2. Jurnal bisa diubah lagi (absensi ikut diperbarui, tidak dobel).
3. Nilai diinput per penilaian (jenis + judul); rekap menghitung nilai akhir berbobot dan ketuntasan.
4. Kepala sekolah memantau keterisian jurnal dan kehadiran, lalu mengingatkan guru lewat WhatsApp.

## Catatan keamanan
- PIN guru disimpan sebagai hash HMAC; mengganti PIN membatalkan sesi lama.
- Guru hanya bisa menulis jurnal dan nilai untuk kelas dan mapel di jadwalnya.
- Semua penulisan dibungkus LockService.
- Percobaan PIN dan password dibatasi.
- Mengganti password admin di sheet langsung membatalkan sesi dashboard.
- Ekspor CSV memberi tanda `'` pada sel yang diawali `= + - @`.
