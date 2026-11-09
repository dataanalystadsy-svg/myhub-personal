# MYHUB Real Data Edition v1.0

## Isi paket
- `index.html`, `styles.css`, `app.js`: aplikasi.
- `config.js`: tempat OAuth Web Client ID.
- `manifest.webmanifest`, `sw.js`, `icon.svg`: dukungan PWA/offline.
- Database lokal memakai IndexedDB. Tidak ada data contoh.

## Setup Google Drive (sekali saja)
1. Buka Google Cloud Console: https://console.cloud.google.com/
2. Buat project baru, misalnya `MYHUB Personal`.
3. Enable **Google Drive API**.
4. Configure OAuth consent screen / Google Auth Platform.
   - Audience: External (akun Gmail pribadi).
   - Tambahkan akun Google sendiri sebagai Test user jika aplikasi masih Testing.
5. Buat OAuth Client ID:
   - Application type: Web application.
   - Authorized JavaScript origins: masukkan origin HTTPS tempat MYHUB akan di-host, misalnya `https://USERNAME.github.io`.
   - Jangan masukkan path `/myhub-app/` pada origin; hanya scheme + host + port.
6. Salin Client ID (bukan Client Secret) ke `config.js`, ganti `PASTE_WEB_CLIENT_ID_HERE`.
7. Upload semua isi folder ini ke hosting HTTPS.
8. Buka URL MYHUB, masuk Pengaturan, lalu Hubungkan Google Drive.
9. Jika backup lama ditemukan, pilih restore atau pertahankan data lokal lalu upload.

## Catatan keamanan & batasan
- OAuth scope yang digunakan hanya `drive.appdata`, untuk area data aplikasi tersembunyi MYHUB; bukan akses seluruh Drive.
- Jangan pernah menaruh Client Secret di file frontend.
- Data utama berada di IndexedDB browser perangkat. Jangan hapus data situs/browser tanpa backup.
- Autosave lokal berlangsung saat data disimpan. Cloud backup otomatis berjalan sekitar 5 detik setelah perubahan ketika aplikasi terbuka, online, dan token Google masih aktif.
- Token akses Google hanya disimpan di memori sesi. Setelah membuka sesi baru, hubungkan Google Drive kembali. Browser tidak menjamin pekerjaan backup berjalan ketika aplikasi ditutup/diterminasi.
- Backup Google Drive bukan sinkronisasi multi-device real-time. Gunakan Restore secara sadar karena akan mengganti data lokal.
- Untuk pemakaian personal, biarkan OAuth app dalam mode Testing dan tambahkan akun sendiri sebagai test user. Untuk penggunaan lebih luas, lengkapi proses verifikasi OAuth sesuai kebijakan Google.

## Deploy tanpa GitHub (Netlify)
1. Buka https://app.netlify.com/drop dari komputer atau browser.
2. Ekstrak ZIP ini.
3. Seret folder `MYHUB_Real_Data` ke area upload Netlify Drop.
4. Netlify memberi URL HTTPS. Tambahkan domain tersebut sebagai Authorized JavaScript origin di Google Cloud Console.
5. Jika URL berubah, perbarui Authorized JavaScript origins.
