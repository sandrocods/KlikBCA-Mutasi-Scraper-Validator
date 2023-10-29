
# KlikBCA Mutasi Scraper + Validator

Aplikasi Berbasis Web yang membantu anda mendapatkan informasi mutasi dari iBanking BCA dan melakukan Request Pembayaran otomatis validasi. Dapat diintegrasikan dengan API Request ke aplikasi anda untuk mempermudah validasi pembayaran otomatis.

Demo Aplikasi : [Video Demo Aplikasi](https://youtu.be/OyMMf0LfJgU)

Aplikasi ini bersifat tidak Publik di-host di repositori pribadi. Akses berbayar. akan mendapatkan benefit dukungan dasar untuk instalasi, konfigurasi, dan penggunaan. tersedia request fitur yang lainya

Anda dapat menghubungi saya di [Telegram](https://t.me/Sandroputraaa) untuk detailnya.




## Fitur

| Nama            | Deskripsi                   | Status
| ----------------- | ------------------------- | -------- | 
| Dashboard Admin | Digunakan untuk memantau transaksi | ✔
| API Request | Digunakan untuk integrasi ke aplikasi anda  | ✔
| Request Payment | Digunakan untuk melakukan permintaan pembayaran  | ✔
| Scheduler  | Digunakan untuk penjadwalan otomatis  | ✔
| Live Payment Page | Halaman pembayaran yang realtime  | ✔
| Auto Generate kode unik  | Digunakan untuk generate secara otomatis kode pembayaran  | ✔

#### Pada Fitur Scheduler berikut ini adalah proses yang dilakukan penjadwalan otomatis
- Otomatis mengambil history transaksi ( 5 menit )
- Otomatis mengubah pembayaran yang belum dibayarkan menjadi `failed` ( 30 menit )
- Otomatis Update Status Dashboard & Payment Page (*)

#### Pada Fitur Generate kode unik berikut ini adalah proses yang dilakukan
- Generate 2 digit
- Generate 3 digit




## Konfigurasi Aplikasi

```json
{
  "dashboard": {
    "keyAccess": "",
    "usernameAdmin": "",
    "passwordAdmin": ""
  },
  "bcaCredential": {
    "useridBCA": "",
    "passwordBCA": "",
    "accountNumberBCA": "",
    "nameAccountBCA": ""
  },
  "scrapOnStart": false,
  "scrapOn": false
}
```

| Parameter |  Deskripsi                |
| :-------- |  :------------------------- |
| `keyAccess` | Autentikasi API Request |
| `usernameAdmin` | Username login dashboard admin
| `passwordAdmin` | Autentikasi login dashboard admin
| `useridBCA` | Autentikasi login ibank BCA
| `passwordBCA` | Autentikasi login ibank BCA
| `accountNumberBCA` | Nomor rekening tujuan transfer 
| `nameAccountBCA` | A\n pemilik nomor rekening
| `scrapOnStart` | Menyalakan otomatis scrap pada saat aplikasi dijalankan 
| `scrapOn` | Menyalakan fitur scrap otomatis 

## Refrensi API
#### Index API 

Request :
```http
> GET /
```
Response :
```json
{
	"message": "Server Payment Gateway BCA is running 🚀",
	"status": true,
	"time": "2023-10-29 17:52:08"
}
```

#### Get All History Mutation
Akan menampilkan semua history mutasi transaksi

Request :
```http
> GET /api/historyMutation?key={keyAccess}
```

| Parameter |  Deskripsi                |
| :-------- |  :------------------------- |
| `keyAccess` | Autentikasi API Request |


Response :
```json
{
	"data": [
		{
			"amount": "5,004.00",
			"cab": "0000",
			"created_at": "Sun, 29 Oct 2023 18:05:51 GMT",
			"date": "PEND",
			"description": "BI-FAST CRTRANSFER   DR 501 Martinus Krisandro",
			"id": 1,
			"id_trx": 7,
			"last_balance": "9999,999.99",
			"status": "CR",
			"updated_at": "Sun, 29 Oct 2023 18:05:51 GMT"
		},
		{
			"amount": "5,075.00",
			"cab": "0000",
			"created_at": "Sun, 21 Oct 2023 18:11:21 GMT",
			"date": "PEND",
			"description": "BI-FAST CRTRANSFER   DR 501 Martinus Krisandro",
			"id": 2,
			"id_trx": 8,
			"last_balance": "9999,999.99",
			"status": "CR",
			"updated_at": "Sun, 21 Oct 2023 18:11:21 GMT"
		}
	],
	"message": "success",
	"status": true
}
```

#### Get All History Mutation Today
Akan menampilkan semua history mutasi transaksi yang dilakukan hari ini

Request :
```http
> GET /api/historyMutation/today?key={keyAccess}
```

| Parameter |  Deskripsi                |
| :-------- |  :------------------------- |
| `keyAccess` | Autentikasi API Request |


Response :
```json
{
	"data": [
		{
			"amount": "5,004.00",
			"cab": "0000",
			"created_at": "Sun, 29 Oct 2023 18:05:51 GMT",
			"date": "PEND",
			"description": "BI-FAST CRTRANSFER   DR 501 Martinus Krisandro",
			"id": 1,
			"id_trx": 7,
			"last_balance": "9999,999.99",
			"status": "CR",
			"updated_at": "Sun, 29 Oct 2023 18:05:51 GMT"
		},
		{
			"amount": "5,075.00",
			"cab": "0000",
			"created_at": "Sun, 29 Oct 2023 18:11:21 GMT",
			"date": "PEND",
			"description": "BI-FAST CRTRANSFER   DR 501 Martinus Krisandro",
			"id": 2,
			"id_trx": 8,
			"last_balance": "9999,999.99",
			"status": "CR",
			"updated_at": "Sun, 29 Oct 2023 18:11:21 GMT"
		}
	],
	"message": "success",
	"status": true
}
```

#### Check Transaction by Amount
Akan menampilkan transaksi berdasarkan jumlah transfer

Request :
```http
> GET /api/historyMutation/checkAmount?key={keyAccess}&amount={jumlahTransfer}
```

| Parameter |  Deskripsi                |
| :-------- |  :------------------------- |
| `keyAccess` | Autentikasi API Request |
| `amount` | Jumlah Transfer


Response :
```json
{
	"data": {
		"amount": "5,004.00",
		"cab": "0000",
		"created_at": "Sun, 29 Oct 2023 18:05:51 GMT",
		"date": "PEND",
		"description": "BI-FAST CRTRANSFER   DR 501 Martinus Krisandro",
		"id": 1,
		"id_trx": 7,
		"last_balance": "9999,999.99",
		"status": "CR",
		"updated_at": "Sun, 29 Oct 2023 18:05:51 GMT"
	},
	"message": "success",
	"status": true
}
```


#### Add Request Payment
Akan melakukan permintaan pembayaran

Request :
```http
> POST /api/requestPayment
| {
| 	"amount": "",
| 	"key": ""
| }
```

| Parameter |  Deskripsi                |
| :-------- |  :------------------------- |
| `key` | Autentikasi API Request |
| `amount` | Jumlah Permintaan Pembayaran |


Response :
```json
{
	"data": {
		"amount": 5330,
		"created_at": "Fri, 27 Oct 2023 02:56:55 GMT",
		"id_unique": "2ZOIFI7ZC3QHNPRCL8HX",
		"status": "pending",
		"updated_at": "Fri, 27 Oct 2023 02:56:55 GMT"
	},
	"message": "success",
	"status": true
}
```

#### Get All Status
Akan menampilkan informasi berupa `total credit mutasi` `total pending payment` `total success payment` `total failed payment`

Request :
```http
> GET /admin/ajax?keyAccess={keyAccess}
```

| Parameter |  Deskripsi                |
| :-------- |  :------------------------- |
| `keyAccess` | Autentikasi API Request |


Response :
```json
{
  "status": true,
  "total_cr_transaction": 2,
  "total_request_payment_failed": 1,
  "total_request_payment_pending": 0,
  "total_request_payment_success": 2
  "get_request_payment": [
    {
      "status": "success",
      "created_at": "Sun, 29 Oct 2023 17:56:43 GMT",
      "amount": "Rp 5,004",
      "updated_at": "Sun, 29 Oct 2023 18:06:00 GMT",
      "id_unique": "3G2N8Z3L5SOF1RTLZADS",
      "id": 1
    },
    {
      "status": "failed",
      "created_at": "Sun, 29 Oct 2023 18:07:33 GMT",
      "amount": "Rp 10,019",
      "updated_at": "Sun, 29 Oct 2023 18:28:10 GMT",
      "id_unique": "04X164HVUIOBAUUN2JAL",
      "id": 2
    },
    {
      "status": "success",
      "created_at": "Sun, 29 Oct 2023 18:07:42 GMT",
      "amount": "Rp 5,075",
      "updated_at": "Sun, 29 Oct 2023 18:11:30 GMT",
      "id_unique": "VM1KFCCSEIZFE0M1NJEX",
      "id": 3
    }
  ],
  "get_mutations": [
    {
      "status": "CR",
      "description": "BI-FAST CRTRANSFER   DR 501 Martinus Krisandro",
      "amount": "5,004.00",
      "created_at": "Sun, 29 Oct 2023 18:05:51 GMT",
      "updated_at": "Sun, 29 Oct 2023 18:05:51 GMT",
      "id": 1,
      "id_trx": 7,
      "date": "PEND",
      "cab": "0000",
	  "last_balance": "9999,999.99",
    },
    {
      "status": "CR",
      "description": "BI-FAST CRTRANSFER   DR 501 Martinus Krisandro",
      "amount": "5,075.00",
      "created_at": "Sun, 29 Oct 2023 18:11:21 GMT",
      "updated_at": "Sun, 29 Oct 2023 18:11:21 GMT",
      "id": 2,
      "id_trx": 8,
      "date": "PEND",
      "cab": "0000",
	  "last_balance": "9999,999.99",
    }
  ],
}
```


## Dashboard Admin

### Halaman Login
![image](https://github.com/sandrocods/KlikBCA-Mutasi-Scraper-Validator/assets/59155826/a59e3435-395f-426e-94b6-8dbd569fc5f9)

### Halaman Dashboard
![image](https://github.com/sandrocods/KlikBCA-Mutasi-Scraper-Validator/assets/59155826/e2207771-dcfc-4e93-b3ef-fef0023632b9)

### Halaman Permintaan Pembayaran
![image](https://github.com/sandrocods/KlikBCA-Mutasi-Scraper-Validator/assets/59155826/0aecf866-94f0-419d-9958-fc6b7a87af44)

### Halaman Data Request Pembayaran
![image](https://github.com/sandrocods/KlikBCA-Mutasi-Scraper-Validator/assets/59155826/741e18f9-7550-45ad-9a04-06c1f5c7c3cb)

### Halaman Live Status Pembayaran
![image](https://github.com/sandrocods/KlikBCA-Mutasi-Scraper-Validator/assets/59155826/aee02b2f-2d8e-4358-b9da-78599dd3268e)


### Halaman Pembayaran (Pending)
![image](https://github.com/sandrocods/KlikBCA-Mutasi-Scraper-Validator/assets/59155826/82d45ae6-20c6-4b46-b261-c3c881a83dfe)

### Halaman Pembayaran (Success)
![image](https://github.com/sandrocods/KlikBCA-Mutasi-Scraper-Validator/assets/59155826/9e3f1be4-301a-4510-8db9-f98e52f85882)


### Halaman Pembayaran (Failed)
![image](https://github.com/sandrocods/KlikBCA-Mutasi-Scraper-Validator/assets/59155826/eb39b3f5-dfd4-4c2b-8f1f-0ceb5289f1da)
## Support

Jika anda membutuhkan support dukungan aplikasi ini atau ingin membeli aplikasi ini dapat menghubungi saya via telegram [Telegram](https://t.me/Sandroputraaa) untuk detailnya.

