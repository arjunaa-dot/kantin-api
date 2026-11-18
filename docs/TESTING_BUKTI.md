# Bukti Test Postman — KANTINKU API v1

Dijalankan dengan **newman** (runner resmi Postman) memakai file collection yang sama
yang ada di `docs/postman/`. Jadi angka di bawah identik dengan yang muncul kalau
collection dijalankan dari Postman Desktop.

```bash
npx newman run docs/postman/KANTINKU_API_v1.postman_collection.json
```

- Waktu: 18 November 2026, 21:53
- Requests: **47** — Failed: **0**
- Assertions: **94** — Failed: **0**
- Durasi: 2.6 detik
- Laporan HTML: `docs/screenshots/kantin-report.html`
- Screenshot ringkasan: `docs/screenshots/01-newman-summary.png`

## Ringkasan per folder

| Folder | Request | Semua assertion lulus |
|---|---|---|
| 0. Setup (token & id) | 3 | ya |
| 1. Auth | 4 | ya |
| 2. User Profile | 2 | ya |
| 3. Categories | 5 | ya |
| 4. Products | 10 | ya |
| 5. Cart | 6 | ya |
| 6. Orders | 11 | ya |
| 7. Payments | 5 | ya |
| 8. Logout | 1 | ya |

## Kenapa ini bukan sekadar "happy path"

Yang diuji bukan cuma sukses, tapi juga jalur gagal yang diminta rubrik:

- **422** — register email duplikat, kategori duplikat, produk invalid (`category_id` tidak ada,
  `price` negatif, nama kosong), order `items: []`, qty 0, status tidak dikenal, metode bayar tidak dikenal
- **401** — login password salah, `GET /orders` tanpa token
- **403** — customer mencoba `POST /products`
- **404** — produk/order/item keranjang yang tidak ada
- **500** — nol. Tidak ada satu pun response 5xx selama run.

Setiap request punya assertion yang mengecek **kode status** dan **bentuk response**
(`{status, message, data}` untuk sukses, `{status, message, errors}` untuk error),
bukan cuma "request terkirim".

## Cara reproduksi

```bash
php artisan migrate:fresh --seed      # database bersih
php artisan serve                     # terminal lain, port 8000
npx newman run docs/postman/KANTINKU_API_v1.postman_collection.json
```

Kalau tombol **Run** di Postman Desktop yang dipakai, hasilnya sama persis —
Postman Desktop menjalankan collection yang sama.
