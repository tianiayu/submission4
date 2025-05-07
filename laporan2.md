# **Sistem Rekomendasi Destinasi Wisata di Yogyakarta Menggunakan Metode Content-based Filtering dan Collaborative Filtering**
# Laporan Proyek Machine Learning - Tiani Ayu Lestari

## Project Overview

Yogyakarta adalah salah satu tujuan wisata utama di Indonesia yang memiliki berbagai tempat wisata dan menarik wisatawan dari berbagai kalangan. Namun, keberagaman tempat wisata yang ada juga dapat membuat wisatawan merasa kebingungan dalam memilih destinasi yang paling sesuai dengan minat dan kebutuhan mereka. Untuk mengatasi tantangan ini, hadirnya sistem rekomendasi menjadi solusi yang dapat membantu wisatawan dalam memilih tujuan wisata yang tepat. Metode yang akan digunakan dalam membangun sistem rekomendasi dalam permasalahan ini adalah:
- Content-based Filtering, yang mengandalkan informasi terkait destinasi wisata seperti kategori, lokasi, atau rating.
- Collaborative Filtering, yang memanfaatkan preferensi pengguna lain untuk memberikan rekomendasi.

Gabungan dari kedua metode ini dapat menghasilkan sistem rekomendasi yang lebih akurat dan sesuai dengan kebutuhan pengguna. Beberapa penelitian terkait penerapan sistem rekomendasi dalam sektor pariwisata menunjukkan efektivitas pendekatan ini dalam meningkatkan pengalaman pengguna. Menurut Adomavicius & Tuzhilin (2005), perkembangan sistem rekomendasi merupakan teknologi penting dalam membantu pengguna menemukan informasi atau produk yang relevan di tengah banyaknya pilihan di era digital. Kemudian pada buku yang ditulis oleh Ricci, Rokach, & Shapira menyatakan bahwa Content-based Filtering sangat berguna untuk memberikan rekomendasi berdasarkan karakteristik atribut yang ada pada objek atau destinasi. Dalam penelitian Burke (2002), Penulis memperkenalkan sistem rekomendasi hybrid bernama EntreeC, yang menggabungkan pendekatan knowledge-based dan collaborative filtering menggunakan metode cascade hybrid. Dalam sistem ini, knowledge-based recommender memberikan rekomendasi awal berdasarkan pengetahuan domain, kemudian collaborative filtering memperbaiki rekomendasi berdasarkan data preferensi pengguna lain.

Untuk mendukung pengembangan sistem ini, berikut referensi yang relevan dan dapat dijadikan acuan:
- **Adomavicius, G., & Tuzhilin, A.** (2005). Toward the next generation of recommender systems: A survey of the state-of-the-art and possible extensions. IEEE Transactions on Knowledge and Data Engineering, 17(6), 734–749.
- **Ricci, F., Rokach, L., & Shapira, B.** (2022). Recommender systems handbook. Springer.
- **Burke, R.** (2002). Hybrid recommender systems: Survey and experiments. User Modeling and User-Adapted Interaction, 12(4), 331–370.



## Business Understanding

Pada bagian ini, Anda perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah:
- Bagaimana cara membuat sistem rekomendasi destinasi wisata yang dapat menyarankan tempat berdasarkan rating dan ulasan pengguna?
- Bagaimana cara mengoptimalkan data tempat wisata, seperti kategori, harga, dan waktu, guna menyusun rekomendasi yang lebih sesuai dengan preferensi pengguna?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Jawaban pernyataan masalah 1
- Jawaban pernyataan masalah 2
- Jawaban pernyataan masalah n

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution approach (algoritma atau pendekatan sistem rekomendasi).

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
