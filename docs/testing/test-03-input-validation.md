\# Test 03 – Input Validation



\## Tujuan

Memastikan semua input dari pengguna divalidasi oleh sistem dan ditolak jika formatnya salah atau kosong.



\## Kriteria

Semua input pengguna harus melewati validasi sebelum diproses lebih lanjut.



\## File

server/src/routes/user.routes.ts



\## Fungsi

Endpoint POST /login-failed



\## Baris

Baris 40 - 41



\## Skenario Pengujian



| No | Skenario | Input (Body JSON) | Expected Result | Actual Result | Status |

| -- | -------- | ----------------- | --------------- | ------------- | ------ |

| 1 | Mengirim request tanpa field email | `{ "password": "123" }` | HTTP 400, pesan: "Email is required" | HTTP 400, pesan: "Email is required" | PASS |



\## Hasil Inspection

Berdasarkan pengecekan kode sumber dan pengujian manual menggunakan API Client, sistem sudah mengimplementasikan validasi input. Ketika endpoint diakses tanpa parameter `email` yang wajib, sistem otomatis menolak request dengan mengirimkan status HTTP 400.



\## Status

SESUAI



\## Evidence

(Paste Screenshot 03: Postman/Thunder Client di sini)



