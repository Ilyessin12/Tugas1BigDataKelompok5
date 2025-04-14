## Introductory
Project ini ditujukan untuk memenuhi Tugas 1 dari Mata Kuliah Big Data dengan Anggota kelompok sebagai berikut:
- Varrell Rizky Irvanni Mahkota (2306245)   
- Muhammad Hafidh Fadhilah (2305672)
- Muhammad Bintang Eighista Dwiputra (2304137)
- Muhammad Ichsan Khairullah (2306924)
- Lyan Nazhabil Dzuquwwa (2308428)

Tujuan utama dari project ini adalah untuk mempelajari cara untuk mengambil data dan melakukan proses Ingestion terhadap data yang sudah diambil ke MongoDB. Data yang diambil berasal dari 3 sumber, yaitu:
- yfinance API, data yang diambil berupa volume transaksi dari setiap emiten yang terdaftar di IDX
- https://www.IDX.com, data yang diambil berupa Laporan Keuangan dalam setahun terakhir untuk setiap emiten yang terdaftar
- https://www.iqplus.com, data yang diambil berupa berita terkait emiten pada saham
	

## Description
Project ini mengimplementasikan pipeline scraping dan ingestion data keuangan dari tiga sumber berbeda ke dalam database MongoDB. Proyek terdiri dari tiga modul utama yang bekerja secara independen untuk mendapatkan data dari sumber yang berbeda:

1. **Stock Price Data (yfinance)**: 
   - Mengumpulkan data historis saham selama periode 1 tahun untuk semiten yang terdaftar di IDX 
   - Menggunakan library yfinance untuk fetching data melalui API
   - Data mencakup Open, Close, High, Low, Volume transaksi, dan timestamps

2. **Laporan Keuangan (IDX)**:
   - Melakukan scraping laporan keuangan terbaru perusahaan dari situs IDX
   - Mengotomasi proses download file Instance.zip dan melakukan ekstraksi
   - Parsing file XML taksonomi untuk mendapatkan informasi laporan keuangan
   - Mendapatkan data keuangan perusahaan seperti Aset, Liabilitas, Ekuitas, dll.

3. **Berita Saham (iqplus)**:
   - Mengumpulkan berita terkait emiten dari situs IQ Plus
   - Data meliputi judul berita, tanggal publikasi, dan link berita
   - Data disimpan dalam beberapa batch file JSON

Setiap modul memiliki dua tahap utama:
- **Scraping**: Pengambilan data dari sumber dan penyimpanan dalam format JSON
- **Ingestion**: Memasukkan data ke MongoDB dengan mekanisme penanganan duplikat dan update data

Pipeline ini menggunakan teknik batch ingestion, bulk operations, dan indexing untuk optimasi kinerja, memastikan tidak ada data duplikat dan memudahkan kueri nantinya.


## Teknologi yang Digunakan
- **Python**: Bahasa pemrograman utama
- **Libraries**:
  - yfinance: Untuk mengakses data saham historis
  - Selenium: Untuk otomatisasi web scraping
  - Beautiful Soup: Untuk parsing HTML
  - PyMongo: Untuk koneksi dan operasi MongoDB
  - Pandas: Untuk manipulasi data
  - Zipfile, XML: Untuk mengekstrak dan parsing file XML
- **MongoDB Atlas**: Sebagai database untuk penyimpanan data
- **Jupyter Notebook**: Sebagai IDE dan dokumentasi proses

## Setup dan Penggunaan

1. Klon repositori ini
2. Buat file `.env` berdasarkan `.env.example` dengan konfigurasi MongoDB Anda
3. Install dependensi yang diperlukan:
```
pip install yfinance selenium beautifulsoup4 pymongo pandas python-dotenv webdriver-manager

```
4. Jalankan notebook secara berurutan untuk:
- Scraping daftar emiten (`pencarianemiten.ipynb`)
- Scraping dan ingestion data yfinance (`tugas1yfinance.ipynb`)
- Scraping dan ingestion laporan keuangan (`Laporan Keuangan.ipynb`)
- Scraping dan ingestion berita saham (`Scrapping.ipynb`)