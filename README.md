# Capstone Project 2 - Analisis Popularitas Listing Airbnb di Bangkok

## Langkah 0: Latar Belakang & Rumusan Masalah

Pasar properti di Bangkok menunjukkan tren peningkatan popularitas untuk penyewaan jangka pendek melalui platform seperti Airbnb. Namun, tidak semua listing memiliki performa yang sama. Beberapa listing sangat populer dan sering dipesan, sementara lainnya sepi peminat. Faktor-faktor seperti lokasi, harga, tipe ruang, dan aktivitas host menjadi penentu utama kesuksesan listing.

Sebagai seorang **data analyst** yang dikontrak oleh sekelompok **investor properti**, Anda diminta untuk menganalisis dataset Airbnb Listings Bangkok dan memberikan rekomendasi strategis mengenai properti seperti apa yang layak dijadikan investasi.

### Problem Statement

Investor ingin mengetahui **faktor-faktor apa saja yang mempengaruhi popularitas listing Airbnb di Bangkok**, agar dapat mengalokasikan modal investasi mereka secara optimal.

### Tujuan Analisis (Analytical Breakdown Questions):

1. Bagaimana sebaran listing berdasarkan `room_type` dan `neighborhood`?
2. Apakah listing dengan harga yang lebih tinggi memiliki tingkat okupansi (`availability_365`) yang rendah?
3. Karakteristik listing seperti apa yang mendapatkan lebih banyak review dalam 12 bulan terakhir?
4. Faktor-faktor apa yang paling mempengaruhi popularitas listing secara keseluruhan?
5. Apakah host dengan banyak listing cenderung memiliki listing dengan kualitas (review/okupansi) lebih rendah?

---

## Langkah 1: Data Understanding & Cleaning

Dataset yang digunakan adalah **Airbnb Listings Bangkok (tahun XXXX)** dengan fitur-fitur seperti:

- Identitas Listing (`id`, `name`)
- Informasi Host (`host_id`, `host_name`)
- Lokasi (`neighborhood`, `latitude`, `longitude`)
- Detail Properti (`room_type`, `price`, `minimum_nights`)
- Metrik Popularitas (`number_of_reviews`, `number_of_reviews_ltm`, `last_review`)
- Metrik Host & Ketersediaan (`calculated_host_listings_count`, `availability_365`)

### Data Cleaning Steps:

1. **Backup Raw Dataset:**

   - Backup dataset original sebelum melakukan cleaning.

2. **Overview & Diagnosis:**

   - Mengecek dimensi data, tipe data, dan jumlah missing values per kolom.

3. **Duplicate Handling:**

   - Memeriksa apakah terdapat baris duplikat dan menanganinya sesuai konteks.

4. **Data Type Correction:**

   - Membersihkan kolom `price` dari simbol mata uang dan mengkonversinya ke tipe data numerik.
   - Mengkonversi `last_review` menjadi tipe datetime.

5. **Missing Values Handling:**

   - Menentukan strategi handling kolom dengan missing values seperti `host_name` dan `last_review`.

6. **Outlier Detection & Handling:**

   - Mendeteksi outlier pada kolom numerik kritikal (price, minimum_nights) dan mengambil tindakan sesuai justifikasi.

7. **Feature Engineering:**

   - Membuat fitur baru seperti `days_since_last_review`, `host_type`, dan `estimated_revenue`.

---

## Langkah 2: Data Analysis (Exploratory Data Analysis)

Analisis dilakukan untuk menjawab 5 pertanyaan utama yang telah dirumuskan.

1. **Sebaran Listing berdasarkan Tipe Ruang & Neighborhood:**

   - Visualisasi: Bar chart & pie chart.
   - Insight: Lokasi dengan supply terbanyak & proporsi tipe ruang.

2. **Analisis Harga vs Okupansi:**

   - Visualisasi: Scatter plot antara `price` dan `availability_365`.
   - Insight: Identifikasi "sweet spot" harga yang optimal.

3. **Karakteristik Listing Populer (Banyak Review):**

   - Visualisasi: Boxplot perbandingan `price`, `room_type`, `minimum_nights` pada listing dengan review tinggi.

4. **Faktor-faktor yang Mempengaruhi Popularitas:**

   - Visualisasi: Heatmap korelasi antar variabel numerik.
   - Insight: Variabel apa yang berkorelasi kuat dengan popularitas.

5. **Analisis Host dengan Banyak Listing:**

   - Visualisasi: Bar chart atau boxplot perbandingan rata-rata review berdasarkan kategori `host_type`.

---

## Langkah 3: Insight & Rekomendasi

### Insight:

(Tempatkan hasil temuan utama setelah EDA selesai)

### Rekomendasi Strategis:

(Tempatkan saran actionable di sini. Contoh: 'Prioritaskan investasi pada Entire home/apt di Sukhumvit karena menunjukkan estimasi pendapatan tertinggi dengan tingkat ketersediaan terendah')

---

## Langkah 4: Visualisasi Tableau

Tautan ke dashboard Tableau interaktif akan disediakan setelah visualisasi selesai.

---

## Deliverables

1. Jupyter Notebook (file .ipynb)
2. Dashboard Tableau (link Tableau Public)
3. Slide Presentasi Capstone 2
4. README.md (dokumen ini)
