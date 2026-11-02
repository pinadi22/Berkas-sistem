# Berkas Sistem (Poco X3 Pro, Android 12, MIUI 13)

Aplikasi kecil yang berjalan lewat Shizuku untuk menganalisis dan membersihkan penyimpanan. Tanpa root, tanpa PC.

## Yang bisa dilakukan
1. **Analisis penyimpanan**: hanya membaca. Menampilkan aplikasi dengan data dan cache terbesar, serta folder terbesar.
2. **Bersihkan cache semua aplikasi** (pm trim-caches).
3. **Bersihkan cache eksternal** (/sdcard/Android/data/*/cache).
4. **Bersihkan log MIUI** (/sdcard/MIUI/debug_log dan buffer logcat).
5. **Reset dexopt** (cmd package compile --reset -a), memakan beberapa menit.

Aplikasi tidak menghapus data pribadi, foto, atau aplikasi.

## Log dan pratinjau (baru di versi 1.1)
- Langkah 2 sampai 5 menampilkan dialog dengan tombol **Pratinjau saja**: hanya menampilkan apa yang akan dihapus, tanpa menghapus apa pun. Disarankan dipakai dulu.
- Tiap aplikasi atau folder yang dibersihkan dicatat dengan ukurannya. Langkah 2 menampilkan cache tiap aplikasi sebelum dan sesudah, jadi yang tercatat adalah yang benar-benar hilang.
- Langkah 3 dan 4 mencatat jalur folder dan nama berkas yang dihapus (daftar berkas lengkap ada di berkas log).
- Layar menampilkan 30 teratas. Rincian lengkap tersimpan otomatis di `Download/BerkasSistem-log-<tanggal>.txt`, atau tekan **Salin seluruh log**.
- Tiap langkah menutup dengan ruang bebas sebelum dan sesudah.

Catatan jujur: tanpa root, aplikasi hanya bisa menyentuh sebagian "Berkas sistem". Bagian di /data/system atau partisi sistem tidak terjangkau.

## Cara build dari HP lewat GitHub
1. Buka github.com di browser HP, buat akun, lalu buat repositori baru (misalnya `berkas-sistem`), boleh private.
2. Di repositori: **Add file > Create new file**. Pada kolom nama ketik `.github/workflows/build.yml` (garis miring otomatis membuat folder). Tempel seluruh isi file `build.yml`, lalu **Commit changes**.
3. **Add file > Upload files**, pilih `proyek.zip` (jangan diekstrak), lalu **Commit changes**. Kalau sudah ada `proyek.zip` lama, unggah dengan nama yang sama untuk menimpa.
4. Buka tab **Actions**. Build jalan otomatis, sekitar 3 sampai 6 menit. Kalau tidak jalan, pilih "Build APK" lalu **Run workflow**.
5. Setelah centang hijau, buka run tersebut, turun ke bagian **Artifacts**, unduh `BerkasSistem-apk` (berupa zip), ekstrak, lalu pasang `app-debug.apk`. Izinkan "pasang dari sumber ini" jika diminta.

**Update dari versi 1.0:** copot dulu aplikasi lama sekali saja (tidak ada data yang hilang), karena kunci penanda tangannya berbeda. Mulai versi 1.1 kuncinya tetap, jadi update berikutnya bisa langsung menimpa.

Kalau build gagal (silang merah), buka run-nya, salin pesan error di langkah "Build debug APK", dan kirim ke Claude.

## Cara pakai
1. Pasang Shizuku, buka, lalu mulai lewat **Wireless debugging** (butuh terhubung ke Wi-Fi).
2. Buka Berkas Sistem, tekan **Beri izin Shizuku** dan setujui.
3. Jalankan **Analisis**, lalu tiap langkah pembersihan: pakai **Pratinjau saja** dulu, baru **Hapus**.
