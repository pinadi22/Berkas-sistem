# Ruang Lega

Aplikasi kecil untuk membantu mengurangi "Berkas sistem" yang membengkak di HP Xiaomi/Poco, tanpa root dan tanpa PC. Berjalan lewat [Shizuku](https://github.com/RikkaApps/Shizuku).

Yang dibersihkan hanya **cache** (berkas sementara) dan log. Foto, video, chat, data aplikasi, dan aplikasinya tidak dihapus.

> Dites di **Poco X3 Pro, Android 12, MIUI Global 13**. Di HP lain hasilnya bisa berbeda, jadi coba dengan hati-hati. Proyek hobi, gratis, tanpa iklan.

## Unduh

Buka halaman rilis terbaru lalu unduh `app-debug.apk` di bagian **Assets**:

**https://github.com/pinadi22/Berkas-sistem/releases/latest**

Pasang APK-nya. Kalau diminta, izinkan "pasang dari sumber ini". Play Protect mungkin memberi peringatan karena aplikasi ini tidak dari Play Store.

## Persiapan: Shizuku

Shizuku adalah "jembatan" supaya aplikasi bisa menjalankan perintah ADB dari HP sendiri. Video panduan: https://youtube.com/shorts/28SrSZjoXzk

Langkah tertulis (HP harus terhubung Wi-Fi):

1. Nyalakan Opsi Pengembang: Pengaturan > Tentang ponsel > ketuk "Versi MIUI" 7 kali.
2. Pengaturan > Pengaturan tambahan > Opsi pengembang > nyalakan **Wireless debugging**. Kalau muncul pertanyaan izin jaringan, pilih "Izinkan".
3. Pasang dan buka Shizuku, pilih **Start via Wireless debugging**, lalu **Pairing**.
4. Di Opsi pengembang, buka Wireless debugging > "Pasangkan perangkat dengan kode pairing". Akan muncul kode 6 angka.
5. Masukkan kode itu lewat kolom balasan di notifikasi Shizuku. Kalau kode hilang saat pindah aplikasi, pakai jendela mengambang atau layar terpisah.
6. Kembali ke Shizuku lalu tekan **Start**. Berhasil kalau tampil "Shizuku is running".

Yang sering bikin gagal:
- Wi-Fi putus atau pindah jaringan: Wireless debugging mati sendiri, ulangi dari langkah 2.
- HP habis restart: Shizuku harus dimulai lagi.
- Notifikasi pairing tidak muncul: pastikan izin notifikasi Shizuku aktif.

## Cara pakai

1. Buka **Ruang Lega**, tekan **Beri izin Shizuku**, lalu setujui.
2. Tekan **1. Analisis penyimpanan** untuk melihat aplikasi dan folder yang paling boros. Tidak ada yang dihapus di langkah ini.
3. Untuk tiap langkah pembersihan, tekan **Pratinjau saja** dulu. Aplikasi menampilkan apa yang akan dihapus beserta ukurannya, tanpa menghapus apa pun. Kalau sudah yakin, ulangi lalu tekan **Hapus**.
4. Log lengkap tersimpan otomatis di folder Download (`RuangLega-log-<tanggal>.txt`), atau tekan **Salin seluruh log**.

## Fitur

| Langkah | Fungsi |
|---|---|
| 1. Analisis penyimpanan | Hanya membaca. Aplikasi dengan data dan cache terbesar, serta folder terbesar |
| 2. Bersihkan cache semua aplikasi | `pm trim-caches`. Log menampilkan cache tiap aplikasi sebelum dan sesudah |
| 3. Bersihkan cache eksternal | Mengosongkan `/sdcard/Android/data/*/cache`. Log menampilkan folder dan berkas |
| 4. Bersihkan log MIUI | Mengosongkan `/sdcard/MIUI/debug_log` dan buffer logcat |
| 5. Reset dexopt | Mengembalikan hasil kompilasi aplikasi ke bawaan. Opsional, bisa beberapa menit, dan hasilnya biasanya kecil |

Saran urutan: langkah 2 dan 3 dulu. Langkah 4 boleh. Langkah 5 dilewati saja kecuali ruang masih kurang.

## Hal yang perlu diketahui

- Cache akan menggemuk lagi seiring pemakaian. Bersihkan seperlunya saja, tidak perlu tiap hari: aplikasi hanya akan mengunduh ulang gambar dan video, yang memakai kuota.
- Sebagian aplikasi menyimpan unduhan offline atau aset game di folder cache. Itu bisa ikut hilang dan perlu diunduh ulang.
- Tanpa root, sebagian "Berkas sistem" memang tidak bisa disentuh. Hasil di tiap HP bisa jauh lebih kecil dari di HP pengembang.
- Istilah "Berkas sistem" adalah tampilan MIUI. Langkah 4 (log MIUI) hanya berarti di Xiaomi.
- Butuh Android 11 ke atas agar Shizuku bisa dinyalakan lewat Wireless debugging dari HP.

## Alternatif

Kalau lebih nyaman dengan aplikasi yang sudah mapan dan ada di Play Store, SD Maid SE adalah pilihan yang baik. Silakan pilih yang paling cocok.

## Ada masalah?

Buka tab **Issues** di repositori ini, atau tulis di komentar postingan asalnya. Sertakan merek, tipe, versi Android, dan potongan log (tombol **Salin seluruh log**).

## Untuk pengembang

- Bahasa: Kotlin, tanpa dependensi UI tambahan. Memakai [Shizuku API](https://github.com/RikkaApps/Shizuku-API) 13.1.5. `minSdk` 26, `targetSdk` 34.
- Kode sumber ada di dalam `proyek.zip`.
- Build otomatis lewat GitHub Actions (`.github/workflows/build.yml`): tiap perubahan dibangun menjadi APK dan diterbitkan di halaman Releases.
- APK ditandatangani dengan kunci debug yang disertakan, jadi ini bukan rilis resmi yang aman dari pemalsuan. Unduh hanya dari repositori ini.
