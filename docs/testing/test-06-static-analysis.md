# Test 06 – Kakas Bantu / Automated Static Testing

## Tujuan
Menganalisis source code menggunakan kakas bantu statis (Static Code Analysis) untuk menemukan potensi *syntax error* dan mengecek *code quality*.

## Kriteria
Project menggunakan kakas bantu seperti ESLint dan SonarQube untuk menjaga kualitas kode.

## File / Tools
- Tools: ESLint (Terdaftar di package.json, versi 9.39.5)

## Hasil Inspection
1. **ESLint**: Saat mencoba menjalankan pengujian statis dengan perintah `npm run lint`, eksekusi gagal (Fatal Error). Sistem memberikan peringatan: `ESLint couldn't find an eslint.config.(js|mjs|cjs) file.` Hal ini menunjukkan bahwa project telah menginstal ESLint versi 9, namun belum mengonversi atau memiliki file konfigurasi Flat Config yang diwajibkan oleh versi tersebut. Otomatis, *static testing* tidak dapat dilakukan.
2. **SonarQube**: Sama seperti ESLint, integrasi SonarQube belum dikonfigurasi di *environment* lokal (Out of Scope untuk environment saat ini).

## Status
TIDAK SESUAI (Gagal Eksekusi Kakas Bantu)

## Evidence
(Paste Screenshot 06: Terminal yang menunjukkan pesan Error ESLint di sini)

## Catatan
Ini adalah celah dalam *pipeline development*. Kakas bantu yang terdaftar di package.json harusnya bisa dijalankan langsung (Out-of-the-box).

## Rekomendasi
1. (Untuk ESLint): Segera buat file `eslint.config.js` dengan mengikuti *migration guide* ESLint v9, agar developer selanjutnya bisa melakukan pengecekan kualitas kode.
2. (Untuk SonarQube): Evaluasi penggunaan SonarCloud untuk diintegrasikan secara otomatis di repository GitHub (CI/CD).
