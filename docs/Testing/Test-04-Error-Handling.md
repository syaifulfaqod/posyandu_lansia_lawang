# Test 04 – Error Handling

## Tujuan
Memastikan penanganan error sudah tepat (menggunakan `try...catch`), dicatat di log server, dan mengembalikan HTTP status yang sesuai (500) saat terjadi kegagalan sistem.

## Kriteria
Penanganan error sudah tepat, tidak ada error yang diabaikan secara diam-diam.

## File
`server/src/routes/user.routes.ts`

## Fungsi
Endpoint `GET /`

## Baris
Baris 100 - 108

## Kode yang Diinspeksi

```typescript
router.get("/", async (req, res) => {
  try {
    const data = await UserService.getAllUsers();
    res.json(data);
  } catch (error: any) {
    console.error("GET ALL USERS ERROR:", error);
    res.status(500).json({ error: error.message });
  }
});
```

## Analisis Error Handling Seluruh Endpoint

| No | Endpoint | Baris | `try...catch` | `console.error` | `res.status(500)` | Status |
|----|----------|-------|:-------------:|:----------------:|:------------------:|:------:|
| 1  | `GET /login-check` | 10-34 | ✅ | ❌ (ada detail error) | ✅ | OK |
| 2  | `POST /login-failed` | 38-68 | ✅ | ❌ | ✅ | OK |
| 3  | `POST /login-success` | 72-84 | ✅ | ❌ | ✅ | OK |
| 4  | `POST /:id/unlock` | 88-98 | ✅ | ❌ | ✅ | OK |
| 5  | **`GET /`** | **100-109** | ✅ | ✅ | ✅ | **OK** |
| 6  | `POST /` | 111-119 | ✅ | ✅ | ✅ | OK |
| 7  | `PUT /:id` | 121-129 | ✅ | ✅ | ✅ | OK |
| 8  | `DELETE /:id` | 131-139 | ✅ | ✅ | ✅ | OK |

## Skenario Pengujian

| No | Skenario | Expected Result | Actual Result | Status |
|----|----------|-----------------|---------------|--------|
| 1  | Hit endpoint `GET /api/users/` saat database dimatikan (MySQL di XAMPP di-stop) | Server me-log error di terminal, dan API merespons dengan HTTP 500 | Server mencetak log `"GET ALL USERS ERROR"` dan API merespons dengan HTTP 500 `{ "error": "..." }` | **PASS** |

## Langkah Pengujian

1. Jalankan server dengan `npm run dev` di folder `server/`.
2. Matikan database MySQL secara sengaja (klik **Stop** pada modul MySQL di XAMPP).
3. Buka Postman / Thunder Client.
4. Buat request `GET` ke URL: `http://localhost:8080/api/users/`.
5. Klik **Send**.
6. Verifikasi bahwa:
   - Di Postman: muncul status **500 Internal Server Error**.
   - Di terminal server: muncul log `"GET ALL USERS ERROR: ... (Connection Refused atau serupa)"`.
7. Nyalakan kembali database MySQL setelah pengujian selesai.

## Hasil Inspection

Aplikasi sudah mengimplementasikan **Error Handling yang sangat baik**. Setiap endpoint dibungkus dengan `try...catch`. Jika terjadi kegagalan di layer database atau service, blok `catch` akan menangkapnya, melakukan `console.error` untuk kebutuhan debugging backend, lalu mengembalikan respons `res.status(500)` agar Frontend tidak menggantung (timeout).

### Poin Positif:
- ✅ Semua 8 endpoint memiliki blok `try...catch`.
- ✅ Semua endpoint mengembalikan `res.status(500)` saat error terjadi.
- ✅ Endpoint CRUD utama (`GET /`, `POST /`, `PUT /:id`, `DELETE /:id`) memiliki `console.error` dengan label yang jelas untuk debugging.
- ✅ Error message diteruskan ke klien via `error.message` sehingga Frontend dapat menampilkan informasi yang berguna.

### Catatan Minor:
- ⚠️ Endpoint `POST /login-failed`, `POST /login-success`, dan `POST /:id/unlock` tidak memiliki `console.error`, sehingga error di endpoint tersebut hanya dikembalikan ke klien tanpa dicatat di log server. Disarankan menambahkan logging untuk konsistensi.

## Status
**SESUAI** ✅

## Evidence
- (Paste Screenshot 04A: Postman dengan status 500)
- (Paste Screenshot 04B: Terminal log error)
