# Technical Test - QA Automation Engineer Intern

Repositori ini berisi hasil pengerjaan Technical Test untuk posisi **QA Automation Engineer Intern** di **PT Tirtamas Coldstorindo Logistik**. Pengujian dilakukan pada JSONPlaceholder API.

## 🚀 Ringkasan Proyek
Proyek ini mencakup pembuatan skenario pengujian manual dan otomatisasi menggunakan Postman untuk memvalidasi fungsionalitas, keamanan, dan integritas data pada endpoint API `/posts`.

## 🛠️ Alat yang Digunakan
* **Postman**: Digunakan untuk eksekusi API, penulisan script automasi (JavaScript), dan validasi respon.
* **Markdown**: Digunakan untuk dokumentasi skenario pengujian.

## 📋 Pendekatan Pengujian (Testing Approach)
Saya menggunakan beberapa metode pengujian untuk memastikan reliabilitas API:
1. **Positive Testing**: Memastikan API berjalan sesuai fungsi normal.
2. **Negative Testing**: Memastikan API memberikan pesan error yang tepat pada input yang salah (Invalid ID, Malformed JSON).
3. **Edge Case & Security**: Menguji batas bawah/atas (BVA), simulasi XSS Injection, dan verifikasi tipe data ketat (*strict typing*).

## 📂 Struktur Repositori
* `TEST_SCENARIOS.md`: Tabel detail skenario pengujian (4x4 per endpoint).
* `QA_Tirtamas_Collection.json`: File koleksi Postman yang berisi request dan script automasi.
* `README.md`: Dokumentasi utama proyek.

## ⚙️ Cara Menjalankan Tes
1. Download file `QA_Tirtamas_Collection.json` dari repositori ini.
2. Buka aplikasi **Postman**.
3. Klik tombol **Import** dan pilih file JSON tersebut.
4. Klik kanan pada folder koleksi, lalu pilih **Run Collection**.
5. Lihat hasil di tab **Test Results** untuk melihat status pengujian (PASSED/FAILED).

## ⚠️ Temuan & Isu (Bugs/Issues)
Selama pengujian, ditemukan beberapa perilaku API yang perlu diperhatikan:
* **Data Persistence**: Data yang dibuat via `POST` tidak benar-benar tersimpan di server (GET 101 menghasilkan 404).
* **Missing Validation**: Endpoint `POST /posts` menerima payload kosong `{}` dan tetap memberikan status `201 Created`. Seharusnya mengembalikan `400 Bad Request`.

---
**Dikerjakan oleh:** Muhammad Akmal Hafizh
