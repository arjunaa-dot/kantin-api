MILESTONE FORMATIF PERTEMUAN 9 — LAYER-BY-LAYER VERIFICATION

Kelompok: Grup C-Projek-Mobile
Commit hash terakhir: 3384cce (branch `feature/api-implementation`)
Jumlah endpoint aktif: **26** (`php artisan route:list --path=api/v1`)

| Lapis | Status | Bukti verifikasi |
|---|---|---|
| Migration | SELESAI | `php artisan migrate:status` → 13 migration Ran; `migrate:fresh --seed` bersih |
| Model + relasi | SELESAI | Category→products, Order→items/receipt, dicek via `php artisan tinker` |
| Seeder | SELESAI | categories 6, products 31, users 9, orders 9, order_items 18, payments 9 (semua ≥ 5) |
| Form Request | SELESAI | 11 Form Request; `POST /orders {"items":[]}` → 422 dengan detail errors |
| API Resource | SELESAI | response tidak memuat `password`/`remember_token`; field ikut `api_contract.md` |
| Controller + Route | SELESAI | `route:list` 26 endpoint; `GET /products`, `POST /orders`, `PATCH /orders/{id}/status` jalan |
| Postman | SELESAI | collection 37 request di `docs/postman/`, environment `baseUrl` + `token` otomatis |
| Git | SELESAI | 8 commit terpisah per lapis (lihat `git log main..HEAD`) |

Error tersulit yang sudah diselesaikan: `Auth guard [sanctum] is not defined` (HTTP 500
di semua endpoint ber-token). Penyebabnya bukan Sanctum, tapi `config/auth.php` yang
belum punya guard `sanctum` — skeleton config di repo lama tidak lengkap. Setelah guard
didaftarkan dan `php artisan optimize:clear`, 25/25 test lulus.
