TUGAS PROYEK PERTEMUAN 9 — BACKEND LARAVEL, POSTMAN & TESTING RESULTS

Nama kelompok: Grup C-Projek-Mobile (KANTINKU — aplikasi pre-order kantin kampus)
Anggota: (isi nama + NIM anggota grup)

URL repository backend: https://github.com/kantinkita-kelompok3i/kantin-api
URL Pull Request (feature/api-implementation → dev): (diisi setelah PR dibuat dari akun Arjuna)
Permalink testing_results.md: https://github.com/kantinkita-kelompok3i/kantin-api/blob/feature/api-implementation/docs/testing_results.md

Jumlah endpoint aktif: 26 endpoint dalam prefix /api/v1
- Publik: register, login, daftar & detail kategori, daftar & detail produk
- Token: logout, me, users/me (GET+PATCH), cart (GET, POST item, PATCH item, DELETE item),
  orders (GET, POST, GET detail, DELETE/cancel, status-history), pembayaran (POST, GET)
- Admin: CRUD kategori (POST/PATCH/DELETE), CRUD produk (POST/PATCH/DELETE),
  PATCH status pesanan, PATCH pembayaran lunas, GET admin/orders, GET admin/summary

Jumlah atomic commit: 8 commit (1 commit per lapis: bootstrap, migration, model, seeder,
form request, resource, controller+middleware, route; ditambah 1 commit dokumentasi testing).

Ringkasan 10 test Postman (semua PASS, bukti di docs/testing_results.md):
1. POST /auth/register — 201 + access_token
2. POST /auth/login — 200 + token (password salah → 401)
3. GET /auth/me — 200 data user dari token
4. GET /products?limit=3 — 200 list + meta pagination
5. GET /products/{id} — 200 detail; id tidak ada → 404
6. POST /orders (valid) — 201 order + total terhitung, stok berkurang
7. GET /orders — 200 hanya pesanan milik user login
8. POST /orders {"items":[]} — 422 + detail errors
9. GET /orders tanpa token — 401 Unauthorized
10. POST /auth/logout — 200 token dihapus

Bukti tambahan: docs/postman/KANTINKU_API_v1.postman_collection.json (37 request, 7 folder),
docs/postman/KANTINKU_Local.postman_environment.json, dan
docs/postman/run_tests.py yang mencetak ulang tabel hasil test (25/25 lulus).

Catatan teknis: seeder terverifikasi (6 kategori, 31 produk, 9 user, 9 order, 18 order_item,
9 payment — minimal 5 record per tabel utama). Semua response memakai format
{status, message, data, meta} dan error memakai {status, message, errors} tanpa
membocorkan password/remember_token. Database dev: SQLite (file DB tidak di-commit).

Catatan: backend ini yang jadi bahan Pertemuan 10 (integrasi Flutter ↔ Laravel).
Base URL dev: http://127.0.0.1:8000/api/v1
