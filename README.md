# 📊 Analisis Penjualan Retail Desember 2019 (Exploratory Data Analysis)

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

## 🔍 Alur Analisis

Analisis difokuskan pada data bulan **Desember 2019**, dengan tahapan sebagai berikut:

### 1️⃣ Tren Harian Jumlah Pelanggan
Melihat jumlah pelanggan unik (*unique customers*) yang bertransaksi setiap hari selama Desember 2019 untuk mengidentifikasi pola kunjungan/transaksi harian.

[<img width="856" height="526" alt="image" src="https://github.com/user-attachments/assets/1cf049ea-d994-4357-8a19-b4b263e28eb8" />
](https://github.com/GilangPrasetyo/miniproject-ecommerce-retail-analysis/blob/main/public/daily_number_of_customers.png)

### 2️⃣ Top 5 Brand Berdasarkan Quantity Terjual
Mengidentifikasi 5 brand dengan total kuantitas penjualan tertinggi, sebagai dasar untuk analisis lebih lanjut yang difokuskan hanya pada brand-brand terlaris ini.

### 3️⃣ Tren Penjualan Harian per Brand (Top 5)
Membandingkan tren kuantitas penjualan harian antar top 5 brand, termasuk anotasi pada titik yang menunjukkan adanya lonjakan penjualan signifikan.

![Quantity per Brand]([output/02_daily_quantity_per_brand.png](https://github.com/GilangPrasetyo/miniproject-ecommerce-retail-analysis/blob/main/public/daily_sold_quantity.png))

### 4️⃣ Jumlah Produk Terjual per Brand
Melihat seberapa banyak variasi produk (jumlah `product_id` unik) yang berhasil terjual dari masing-masing brand top 5.

![Products per Brand](output/03_products_per_brand.png)

### 5️⃣ Segmentasi Produk: Laris vs Kurang Laris
Mengelompokkan produk dalam tiap brand menjadi dua kategori berdasarkan total quantity terjual:
- **≥ 100 unit** (produk laris)
- **< 100 unit** (produk kurang laris)

Divisualisasikan dengan *stacked bar chart* untuk melihat proporsi produk laris di setiap brand.

![Products per Brand Stacked](output/04_products_per_brand_stacked.png)

### 6️⃣ Distribusi Harga Median Produk
Histogram distribusi median harga jual produk dari top 5 brand, untuk memahami di kisaran harga berapa mayoritas produk berada.

![Price Distribution](output/05_price_distribution.png)

### 7️⃣ Korelasi Quantity vs GMV
Scatter plot untuk melihat hubungan antara jumlah barang terjual (*quantity*) dan nilai transaksi (*GMV*) per produk.

![Correlation Quantity GMV](output/06_correlation_quantity_gmv.png)

### 8️⃣ Korelasi Harga vs Quantity
Scatter plot untuk melihat apakah ada hubungan antara harga produk dan jumlah unit yang terjual — umumnya digunakan untuk mengecek pola sensitivitas harga (*price sensitivity*).

![Correlation Price Quantity](output/07_correlation_price_quantity.png)

---

## 💡 Insight Umum yang Dicari

Dari rangkaian visualisasi di atas, project ini bertujuan menjawab pertanyaan-pertanyaan bisnis seperti:

- Kapan hari dengan jumlah pelanggan tertinggi/terendah di bulan Desember 2019?
- Brand mana yang paling dominan dari segi volume penjualan?
- Apakah ada lonjakan penjualan musiman (misalnya mendekati akhir tahun)?
- Brand mana yang punya variasi produk terbanyak vs paling sedikit?
- Apakah brand dengan banyak variasi produk juga punya banyak produk "laris"?
- Apakah produk dengan harga lebih murah cenderung terjual lebih banyak (dan sebaliknya)?
- Apakah quantity yang tinggi selalu berbanding lurus dengan GMV yang tinggi?

*(Isi insight spesifik — misal "tanggal X adalah hari dengan transaksi tertinggi" — bisa ditambahkan di sini setelah kamu menjalankan ulang script dan melihat hasil grafiknya.)*

---

## 🚀 Cara Menjalankan

1. Clone repository ini:
   ```bash
   git clone <url-repo-kamu>
   cd <nama-folder>
   ```

2. Install dependencies:
   ```bash
   pip install pandas matplotlib
   ```

3. Jalankan script:
   ```bash
   python retail_analysis.py
   ```

   Script akan otomatis menampilkan setiap grafik satu per satu dan menyimpannya ke folder `output/`.

---

## 📂 Struktur Folder

```
.
├── retail_analysis.py     # Script utama analisis
├── output/                 # Hasil visualisasi (auto-generated)
└── README.md
```

---

## 📌 Catatan

Project ini dibuat untuk tujuan pembelajaran mandiri (*self-learning*) dalam mengasah kemampuan **data wrangling** dan **data visualization** menggunakan studi kasus data retail nyata. Dataset bersifat publik dan disediakan oleh DQLab untuk keperluan edukasi.
