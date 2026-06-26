# 📊 Mini Project: E-Commerce Retail Analysis

Proyek eksplorasi data (EDA) untuk menganalisis perilaku transaksi pelanggan dan performa brand pada platform retail/e-commerce selama bulan **Desember 2019**, menggunakan Python, Pandas, dan Matplotlib.

> 🎯 Project ini dibuat sebagai latihan mandiri untuk memperdalam kemampuan *data wrangling* dan *data visualization* menggunakan studi kasus data transaksi retail.

---

## 🧰 Tools & Libraries

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-150458?logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C?logo=plotly&logoColor=white)

- **Python 3**
- **Pandas** — manipulasi dan agregasi data
- **Matplotlib** — visualisasi data (line chart, bar chart, histogram, scatter plot)

---

## 📁 Dataset

Dataset yang digunakan adalah `retail_raw_reduced.csv`, berisi data transaksi e-commerce dengan kolom utama:

| Kolom | Deskripsi |
|---|---|
| `order_date` | Tanggal transaksi |
| `customer_id` | ID unik pelanggan |
| `product_id` | ID unik produk |
| `brand` | Nama brand produk |
| `item_price` | Harga satuan produk |
| `quantity` | Jumlah barang yang dibeli |

Dataset diambil langsung dari URL publik:
```
https://dqlab-dataset.s3-ap-southeast-1.amazonaws.com/retail_raw_reduced.csv
```

Dua kolom tambahan dibuat untuk kebutuhan analisis:
- `order_month` → format `YYYY-MM`, untuk memfilter data per bulan
- `gmv` (*Gross Merchandise Value*) → hasil dari `item_price × quantity`

---

## 🔍 Alur Analisis & Insight

Analisis difokuskan pada data bulan **Desember 2019**.

### 1️⃣ Tren Harian Jumlah Pelanggan

![Daily Number of Customers](https://raw.githubusercontent.com/GilangPrasetyo/miniproject-ecommerce-retail-analysis/main/public/daily_number_of_customers.png)

Jumlah pelanggan harian berfluktuasi antara **19–40 pelanggan per hari** sepanjang Desember 2019. Beberapa pengamatan:
- Titik tertinggi terjadi di **awal bulan (1 Desember, ±40 pelanggan)** dan **akhir bulan (30 Desember, ±38 pelanggan)**.
- Titik terendah terjadi di **28 Desember (±19 pelanggan)**, tepat sebelum lonjakan menjelang akhir tahun.
- Pola naik-turun cukup tajam dari hari ke hari (tidak stabil), menunjukkan transaksi tidak merata — kemungkinan dipengaruhi hari kerja vs akhir pekan atau momen promo tertentu.

### 2️⃣ Tren Penjualan Harian per Brand (Top 5)

![Daily Sold Quantity Breakdown by Brand](https://raw.githubusercontent.com/GilangPrasetyo/miniproject-ecommerce-retail-analysis/main/public/daily_sold_quantity.png)

- **BRAND_P** mengalami **lonjakan penjualan paling signifikan** sekitar tanggal **8 Desember**, mencapai lebih dari **300 unit dalam sehari** — jauh di atas brand lain pada periode yang sama.
- **BRAND_S** dan **BRAND_R** juga menunjukkan beberapa lonjakan tajam (BRAND_S di awal bulan ±230 unit, BRAND_R di sekitar 19 Desember ±245 unit).
- **BRAND_A** dan **BRAND_C** cenderung lebih stabil dengan fluktuasi yang lebih kecil dibanding ketiga brand lainnya.
- Mendekati akhir bulan (29–30 Desember), hampir semua brand mengalami kenaikan penjualan bersamaan — mengindikasikan momentum belanja akhir tahun.

### 3️⃣ Jumlah Produk Terjual per Brand

![Number of Sold Products per Brand](https://raw.githubusercontent.com/GilangPrasetyo/miniproject-ecommerce-retail-analysis/main/public/number_of_sold_product_per_brands.png)

- **BRAND_S** memiliki variasi produk terjual paling banyak (~152 produk unik), disusul **BRAND_P** (~103) dan **BRAND_R** (~87).
- **BRAND_A** memiliki variasi produk paling sedikit (~68 produk unik), meskipun begitu (dari grafik sebelumnya) brand ini cukup konsisten dalam penjualan harian.

### 4️⃣ Segmentasi Produk: Laris vs Kurang Laris

![Number of Sold Products per Brand - Stacked](https://raw.githubusercontent.com/GilangPrasetyo/miniproject-ecommerce-retail-analysis/main/public/number_of_sold_product_per_brands2.png)

- Secara proporsi, **mayoritas produk di semua brand terjual di bawah 100 unit** (kategori `< 100`), termasuk brand dengan total penjualan tertinggi seperti BRAND_S dan BRAND_P.
- **BRAND_P** punya proporsi produk "laris" (`>= 100` unit) yang terlihat paling jelas dibanding brand lain — sejalan dengan lonjakan tajam yang ditemukan di grafik tren harian.
- Ini menunjukkan pola umum *long-tail*: penjualan didominasi oleh sedikit produk *best-seller*, sementara sebagian besar produk lain hanya terjual dalam jumlah kecil.

### 5️⃣ Distribusi Harga Median Produk

![Distribution of Price Median per Product](https://raw.githubusercontent.com/GilangPrasetyo/miniproject-ecommerce-retail-analysis/main/public/distribution_of_price_median_per_product.png)

- Mayoritas produk dari top 5 brand berada di rentang harga **Rp 0 – Rp 600.000**, dengan puncak terbanyak di kisaran **Rp 400.000 – Rp 600.000 (±125 produk)**.
- Semakin tinggi harga, jumlah produknya semakin sedikit dan menyebar — menunjukkan sebagian besar katalog top 5 brand ini berada di segmen harga menengah ke bawah, dengan sedikit produk premium (>Rp 1.000.000).

### 6️⃣ Korelasi Quantity vs GMV per Produk

![Correlation of Quantity and GMV per Product](https://raw.githubusercontent.com/GilangPrasetyo/miniproject-ecommerce-retail-analysis/main/public/correlation_of_quantity_and_GMV_per_product.png)

- Terlihat ada **korelasi positif** antara quantity terjual dan GMV — produk yang terjual lebih banyak unit cenderung menghasilkan GMV lebih besar, sesuai ekspektasi (GMV = harga × quantity).
- Namun korelasinya **tidak linear sempurna**: ada produk dengan quantity tinggi (>200 unit) tapi GMV-nya tidak setinggi produk lain dengan quantity lebih rendah — mengindikasikan **perbedaan harga satuan produk** ikut berperan besar terhadap GMV, bukan hanya volume penjualan.
- Sebagian besar produk justru terkonsentrasi di pojok kiri bawah (quantity rendah, GMV rendah) — kembali menegaskan pola *long-tail* yang ditemukan sebelumnya.

---

## 📂 Struktur Folder

```
.
├── MiniProject_G231210145.ipynb   # Script utama analisis
├── public/               # Hasil visualisasi (gambar untuk README)
└── README.md
```

---

## 📌 Catatan

Project ini dibuat untuk tujuan pembelajaran mandiri (*self-learning*) dalam mengasah kemampuan **data wrangling** dan **data visualization** menggunakan studi kasus data retail nyata. Dataset bersifat publik dan disediakan oleh DQLab untuk keperluan edukasi.
