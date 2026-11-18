# Testing Results — KANTINKU API

- Base URL: `http://127.0.0.1:8010/api/v1`
- Waktu eksekusi: 2026-11-18T21:15:42
- Hasil: **25/25 test lulus**
- Dijalankan dari `docs/postman/run_tests.py` (isi tabel = response asli, bukan tulisan tangan)

| # | Test | Request | Expected | Actual | Status |
|---|---|---|---|---|---|
| 1 | Register user baru | `POST /auth/register` | 201 | 201 | PASS |
| 2 | Login dan dapat token | `POST /auth/login` | 200 | 200 | PASS |
| 3 | Profil dari token | `GET /auth/me` | 200 | 200 | PASS |
| 4 | Daftar produk + pagination meta | `GET /products?limit=3` | 200 | 200 | PASS |
| 5 | Detail produk | `GET /products/15` | 200 | 200 | PASS |
| 6 | Buat pesanan valid | `POST /orders` | 201 | 201 | PASS |
| 7 | Daftar pesanan milik sendiri | `GET /orders` | 200 | 200 | PASS |
| 8 | Validasi: items kosong | `POST /orders` | 422 | 422 | PASS |
| 9 | Tanpa token | `GET /orders` | 401 | 401 | PASS |
| 10 | Logout | `POST /auth/logout` | 200 | 200 | PASS |
| 11 | Produk tidak ada | `GET /products/999999` | 404 | 404 | PASS |
| 12 | Login admin | `POST /auth/login` | 200 | 200 | PASS |
| 13 | Customer buat produk | `POST /products` | 403 | 403 | PASS |
| 14 | Admin buat produk | `POST /products` | 201 | 201 | PASS |
| 15 | Cari produk baru | `GET /products?search=Menu%20Uji%20211540` | 200 | 200 | PASS |
| 16 | Tambah item ke keranjang | `POST /cart/items` | 201 | 201 | PASS |
| 17 | Lihat keranjang | `GET /cart` | 200 | 200 | PASS |
| 18 | Buat pembayaran | `POST /orders/9/payments` | 201 | 201 | PASS |
| 19 | Detail pembayaran | `GET /orders/9/payment` | 200 | 200 | PASS |
| 20 | Admin ubah status | `PATCH /orders/9/status` | 200 | 200 | PASS |
| 21 | Riwayat status | `GET /orders/9/status-history` | 200 | 200 | PASS |
| 22 | Status tidak valid | `PATCH /orders/9/status` | 422 | 422 | PASS |
| 23 | Admin lihat semua pesanan | `GET /admin/orders` | 200 | 200 | PASS |
| 24 | Ringkasan dashboard | `GET /admin/summary` | 200 | 200 | PASS |
| 25 | Daftar kategori | `GET /categories` | 200 | 200 | PASS |

## Contoh Response

### Register user baru — POST `/auth/register`

```json
{
  "status": "success",
  "message": "Registrasi berhasil",
  "data": {
    "access_token": "7|x9be2k25L5lnS5H1hphtVgI9a72SS2uLHKhs1LWu9023be74",
    "token_type": "Bearer",
    "user": {
      "user_id": 9,
      "name": "Uji Coba 211540",
      "email": "uji211540@kantin.test",
      "role": "customer",
      "phone": null
    }
  }
}
```

### Login dan dapat token — POST `/auth/login`

```json
{
  "status": "success",
  "message": "Login berhasil",
  "data": {
    "access_token": "8|8LXzaiQPSILKezVSixgIbgMRzSuPAxsKFCk1nHUCeb751527",
    "token_type": "Bearer",
    "user": {
      "user_id": 2,
      "name": "Riska Dinar",
      "email": "riska@kantin.test",
      "role": "customer",
      "phone": "081200000002"
    }
  }
}
```

### Profil dari token — GET `/auth/me`

```json
{
  "status": "success",
  "message": "Data pengguna berhasil diambil",
  "data": {
    "user_id": 2,
    "name": "Riska Dinar",
    "email": "riska@kantin.test",
    "role": "customer",
    "phone": "081200000002"
  }
}
```

### Daftar produk + pagination meta — GET `/products?limit=3`

```json
{
  "status": "success",
  "message": "Produk berhasil diambil",
  "data": [
    {
      "product_id": 15,
      "category_id": 3,
      "product_name": "Air Mineral Dingin",
      "description": "Air Mineral Dingin siap disajikan di kantin kampus.",
      "price": 4000,
      "image_url": "/images/air-mineral-dingin.jpg",
      "stock": 60,
      "is_available": true,
      "category": {
        "category_id": 3,
        "category_name": "Minuman Dingin",
        "description": "Es teh, jus dan minuman kemasan"
      },
      "created_at": "2026-11-18T14:14:06+00:00"
    },
    {
      "product_id": 3,
      "category_id": 1,
      "product_name": "Ayam Geprek Sambal Bawang",
      "description": "Ayam Geprek Sambal Bawang siap disajikan di kantin kampus.",
      "price": 16000,
      "image_url": "/images/ayam-geprek-sambal-bawang.jpg",
      "stock": 18,
      "is_available": true,
      "category": {
        "category_id": 1,
        "category_name": "Makanan Berat",
        "description": "Nasi, mie, ayam dan lauk utama"
      },
      "created_at": "2026-11-18T14:14:06+00:00"
    },
    {
      "product_id": 28,
      "category_id": 6,
      "product_name": "Brownies Kukus",

```

### Detail produk — GET `/products/15`

```json
{
  "status": "success",
  "message": "Detail produk berhasil diambil",
  "data": {
    "product_id": 15,
    "category_id": 3,
    "product_name": "Air Mineral Dingin",
    "description": "Air Mineral Dingin siap disajikan di kantin kampus.",
    "price": 4000,
    "image_url": "/images/air-mineral-dingin.jpg",
    "stock": 60,
    "is_available": true,
    "category": {
      "category_id": 3,
      "category_name": "Minuman Dingin",
      "description": "Es teh, jus dan minuman kemasan"
    },
    "created_at": "2026-11-18T14:14:06+00:00"
  }
}
```

### Buat pesanan valid — POST `/orders`

```json
{
  "status": "success",
  "message": "Pesanan berhasil dibuat",
  "data": {
    "order_id": 9,
    "order_code": "KC-20261118-009",
    "order_status": "pending",
    "total_amount": 24000,
    "notes": null,
    "pickup_time": "2026-11-18T21:15:41+00:00",
    "ordered_at": "2026-11-18T14:15:42+00:00",
    "items": [
      {
        "order_item_id": 17,
        "product_id": 15,
        "product_name": "Air Mineral Dingin",
        "unit_price": 4000,
        "quantity": 2,
        "subtotal": 8000
      },
      {
        "order_item_id": 18,
        "product_id": 3,
        "product_name": "Ayam Geprek Sambal Bawang",
        "unit_price": 16000,
        "quantity": 1,
        "subtotal": 16000
      }
    ]
  }
}
```

### Daftar pesanan milik sendiri — GET `/orders`

```json
{
  "status": "success",
  "message": "Daftar pesanan berhasil diambil",
  "data": [
    {
      "order_id": 9,
      "order_code": "KC-20261118-009",
      "order_status": "pending",
      "total_amount": 24000,
      "notes": null,
      "pickup_time": "2026-11-18T21:15:41+00:00",
      "ordered_at": "2026-11-18T14:15:42+00:00",
      "items": [
        {
          "order_item_id": 17,
          "product_id": 15,
          "product_name": "Air Mineral Dingin",
          "unit_price": 4000,
          "quantity": 2,
          "subtotal": 8000
        },
        {
          "order_item_id": 18,
          "product_id": 3,
          "product_name": "Ayam Geprek Sambal Bawang",
          "unit_price": 16000,
          "quantity": 1,
          "subtotal": 16000
        }
      ]
    },
    {
      "order_id": 1,
      "order_code": "KC-20261118-001",
      "order_status": "pending",
      "total_amount": 28000,
      "notes": null,
      "pickup_time": "2026-11-18T15:00:00+00:00",
      "ordered_at": "2026-11-18T13:14:09+00:00",
      "items": [
        {
          "order_item_id": 1,
          "product_id": 1,
          "product_name": "Nasi Goreng Spesial Kampus",
          "unit_pric
```

### Validasi: items kosong — POST `/orders`

```json
{
  "status": "error",
  "message": "Data tidak valid",
  "errors": {
    "items": [
      "Minimal satu produk harus dipilih"
    ]
  }
}
```

### Tanpa token — GET `/orders`

```json
{
  "status": "error",
  "message": "Unauthenticated, token tidak valid atau tidak dikirim",
  "errors": {}
}
```

### Logout — POST `/auth/logout`

```json
{
  "status": "success",
  "message": "Logout berhasil",
  "data": null
}
```

### Produk tidak ada — GET `/products/999999`

```json
{
  "status": "error",
  "message": "Data tidak ditemukan",
  "errors": {}
}
```

### Login admin — POST `/auth/login`

```json
{
  "status": "success",
  "message": "Login berhasil",
  "data": {
    "access_token": "9|YVEQQBTe9KiI9WK7tli2ajJSFohMu7ey1P5rFGux42eb0811",
    "token_type": "Bearer",
    "user": {
      "user_id": 1,
      "name": "Admin Kantin",
      "email": "admin@kantin.test",
      "role": "admin",
      "phone": "081200000001"
    }
  }
}
```

### Customer buat produk — POST `/products`

```json
{
  "message": "Akses hanya untuk admin",
  "exception": "Symfony\\Component\\HttpKernel\\Exception\\HttpException",
  "file": "/Users/yogiprasetyasadewa/Desktop/KANTINKU/kantin-api/vendor/laravel/framework/src/Illuminate/Foundation/Application.php",
  "line": 1440,
  "trace": [
    {
      "file": "/Users/yogiprasetyasadewa/Desktop/KANTINKU/kantin-api/vendor/laravel/framework/src/Illuminate/Foundation/helpers.php",
      "line": 67,
      "function": "abort",
      "class": "Illuminate\\Foundation\\Application",
      "type": "->"
    },
    {
      "file": "/Users/yogiprasetyasadewa/Desktop/KANTINKU/kantin-api/app/Http/Middleware/EnsureUserIsAdmin.php",
      "line": 14,
      "function": "abort"
    },
    {
      "file": "/Users/yogiprasetyasadewa/Desktop/KANTINKU/kantin-api/vendor/laravel/framework/src/Illuminate/Pipeline/Pipeline.php",
      "line": 219,
      "function": "handle",
      "class": "App\\Http\\Middleware\\EnsureUserIsAdmin",
      "type": "->"
    },
    {
      "file": "/Users/yogiprasetyasadewa/Desktop/KANTINKU/kantin-api/vendor/laravel/framework/src/Illuminate/Routing/Middleware/SubstituteBindings.php",
      "line": 50,
      "function": "{closure:{closure:
```

### Admin buat produk — POST `/products`

```json
{
  "status": "success",
  "message": "Produk berhasil dibuat",
  "data": {
    "product_id": 31,
    "category_id": 1,
    "product_name": "Menu Uji 211540",
    "description": "Dibuat saat smoke test",
    "price": 12500,
    "image_url": "/images/uji.jpg",
    "stock": 10,
    "is_available": false,
    "category": {
      "category_id": 1,
      "category_name": "Makanan Berat",
      "description": "Nasi, mie, ayam dan lauk utama"
    },
    "created_at": "2026-11-18T14:15:42+00:00"
  }
}
```

### Cari produk baru — GET `/products?search=Menu%20Uji%20211540`

```json
{
  "status": "success",
  "message": "Produk berhasil diambil",
  "data": [
    {
      "product_id": 31,
      "category_id": 1,
      "product_name": "Menu Uji 211540",
      "description": "Dibuat saat smoke test",
      "price": 12500,
      "image_url": "/images/uji.jpg",
      "stock": 10,
      "is_available": true,
      "category": {
        "category_id": 1,
        "category_name": "Makanan Berat",
        "description": "Nasi, mie, ayam dan lauk utama"
      },
      "created_at": "2026-11-18T14:15:42+00:00"
    }
  ],
  "meta": {
    "page": 1,
    "per_page": 10,
    "total": 1,
    "last_page": 1
  }
}
```

### Tambah item ke keranjang — POST `/cart/items`

```json
{
  "status": "success",
  "message": "Item masuk keranjang",
  "data": {
    "cart_id": 1,
    "items": [
      {
        "cart_item_id": 1,
        "product_id": 31,
        "product_name": "Menu Uji 211540",
        "price": 12500,
        "quantity": 2,
        "subtotal": 25000
      }
    ],
    "total_items": 2,
    "total_amount": 25000
  }
}
```

### Lihat keranjang — GET `/cart`

```json
{
  "status": "success",
  "message": "Keranjang berhasil diambil",
  "data": {
    "cart_id": 1,
    "items": [
      {
        "cart_item_id": 1,
        "product_id": 31,
        "product_name": "Menu Uji 211540",
        "price": 12500,
        "quantity": 2,
        "subtotal": 25000
      }
    ],
    "total_items": 2,
    "total_amount": 25000
  }
}
```

### Buat pembayaran — POST `/orders/9/payments`

```json
{
  "status": "success",
  "message": "Pembayaran berhasil dibuat",
  "data": {
    "payment_id": 9,
    "order_id": 9,
    "payment_method": "qris",
    "payment_status": "pending",
    "transaction_reference": "TRX-KC-20261118-009",
    "paid_at": null
  }
}
```

### Detail pembayaran — GET `/orders/9/payment`

```json
{
  "status": "success",
  "message": "Detail pembayaran berhasil diambil",
  "data": {
    "payment_id": 9,
    "order_id": 9,
    "payment_method": "qris",
    "payment_status": "pending",
    "transaction_reference": "TRX-KC-20261118-009",
    "paid_at": null
  }
}
```

### Admin ubah status — PATCH `/orders/9/status`

```json
{
  "status": "success",
  "message": "Status pesanan berhasil diperbarui",
  "data": {
    "order_id": 9,
    "order_code": "KC-20261118-009",
    "order_status": "processing",
    "total_amount": 24000,
    "notes": null,
    "pickup_time": "2026-11-18T21:15:41+00:00",
    "ordered_at": "2026-11-18T14:15:42+00:00",
    "items": [
      {
        "order_item_id": 17,
        "product_id": 15,
        "product_name": "Air Mineral Dingin",
        "unit_price": 4000,
        "quantity": 2,
        "subtotal": 8000
      },
      {
        "order_item_id": 18,
        "product_id": 3,
        "product_name": "Ayam Geprek Sambal Bawang",
        "unit_price": 16000,
        "quantity": 1,
        "subtotal": 16000
      }
    ]
  }
}
```

### Riwayat status — GET `/orders/9/status-history`

```json
{
  "status": "success",
  "message": "Riwayat status berhasil diambil",
  "data": [
    {
      "status": "pending",
      "note": "Pesanan dibuat",
      "created_at": "2026-11-18T14:15:42+00:00"
    },
    {
      "status": "processing",
      "note": "Diproses dapur",
      "created_at": "2026-11-18T14:15:42+00:00"
    }
  ]
}
```

### Status tidak valid — PATCH `/orders/9/status`

```json
{
  "status": "error",
  "message": "Data tidak valid",
  "errors": {
    "status": [
      "Status tidak tersedia"
    ]
  }
}
```

### Admin lihat semua pesanan — GET `/admin/orders`

```json
{
  "status": "success",
  "message": "Semua pesanan berhasil diambil",
  "data": [
    {
      "order_id": 9,
      "order_code": "KC-20261118-009",
      "order_status": "processing",
      "total_amount": 24000,
      "notes": null,
      "pickup_time": "2026-11-18T21:15:41+00:00",
      "ordered_at": "2026-11-18T14:15:42+00:00",
      "customer": {
        "user_id": 2,
        "name": "Riska Dinar",
        "email": "riska@kantin.test",
        "role": "customer",
        "phone": "081200000002"
      },
      "items": [
        {
          "order_item_id": 17,
          "product_id": 15,
          "product_name": "Air Mineral Dingin",
          "unit_price": 4000,
          "quantity": 2,
          "subtotal": 8000
        },
        {
          "order_item_id": 18,
          "product_id": 3,
          "product_name": "Ayam Geprek Sambal Bawang",
          "unit_price": 16000,
          "quantity": 1,
          "subtotal": 16000
        }
      ]
    },
    {
      "order_id": 1,
      "order_code": "KC-20261118-001",
      "order_status": "pending",
      "total_amount": 28000,
      "notes": null,
      "pickup_time": "2026-11-18T15:00:00+00:00",
      "ordered_at": "2026-1
```

### Ringkasan dashboard — GET `/admin/summary`

```json
{
  "status": "success",
  "message": "Ringkasan dashboard berhasil diambil",
  "data": {
    "total_products": 31,
    "available_products": 31,
    "total_customers": 7,
    "total_orders": 9,
    "orders_by_status": {
      "cancelled": 1,
      "completed": 2,
      "pending": 1,
      "processing": 3,
      "ready": 2
    },
    "revenue": 78000
  }
}
```

### Daftar kategori — GET `/categories`

```json
{
  "status": "success",
  "message": "Kategori berhasil diambil",
  "data": [
    {
      "category_id": 6,
      "category_name": "Dessert",
      "description": "Puding, es krim dan kue",
      "products_count": 5
    },
    {
      "category_id": 1,
      "category_name": "Makanan Berat",
      "description": "Nasi, mie, ayam dan lauk utama",
      "products_count": 6
    },
    {
      "category_id": 2,
      "category_name": "Makanan Ringan",
      "description": "Gorengan, roti dan camilan",
      "products_count": 5
    },
    {
      "category_id": 3,
      "category_name": "Minuman Dingin",
      "description": "Es teh, jus dan minuman kemasan",
      "products_count": 5
    },
    {
      "category_id": 4,
      "category_name": "Minuman Hangat",
      "description": "Kopi, teh dan wedang",
      "products_count": 5
    },
    {
      "category_id": 5,
      "category_name": "Paket Hemat",
      "description": "Kombinasi makanan dan minuman",
      "products_count": 5
    }
  ]
}
```
