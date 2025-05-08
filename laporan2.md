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

Dalam era digital, pariwisata tidak lagi hanya mengandalkan brosur atau rekomendasi dari mulut ke mulut. Pengambilan keputusan wisata kini bergeser ke arah platform online yang dapat menyarankan destinasi secara personal berdasarkan data dan preferensi pengguna. Kota Yogyakarta sebagai salah satu destinasi wisata unggulan di Indonesia memiliki banyak tempat menarik, tetapi pengguna sering kali kesulitan memilih destinasi yang sesuai dengan minat dan waktu mereka. Oleh karena itu, sistem rekomendasi menjadi solusi penting untuk membantu wisatawan dalam menentukan pilihan terbaik.

### Problem Statements

- Bagaimana cara membuat sistem rekomendasi destinasi wisata yang dapat menyarankan tempat berdasarkan rating dan ulasan pengguna?
- Bagaimana cara mengoptimalkan data tempat wisata, seperti kategori, harga, dan waktu, guna menyusun rekomendasi yang lebih sesuai dengan preferensi pengguna?

### Goals

- Mengembangkan sistem rekomendasi destinasi wisata berbasis Collaborative Filtering.
- Menerapkan pendekatan Content-based Filtering untuk menghasilkan rekomendasi berdasarkan atribut tempat wisata.

    ### Solution Approach
    - Content-Based Filtering
      Pendekatan ini merekomendasikan destinasi wisata berdasarkan kesamaan fitur antar tempat wisata yang pernah disukai oleh pengguna. Sistem akan menganalisis atribut tempat wisata seperti kategori (alam, budaya, hiburan), harga, lama waktu kunjungan, serta deskripsi tempat untuk menilai kemiripan antar destinasi.
    - Collaborative Filtering
      Collaborative Filtering merekomendasikan tempat wisata berdasarkan interaksi atau rating yang diberikan oleh pengguna lain dengan preferensi serupa. Model ini fokus pada hubungan antar pengguna dan tempat wisata yang mereka nilai.
      

## Data Understanding
Dataset yang digunakan dalam proyek ini merupakan kumpulan data destinasi wisata di beberapa kota besar di Indonesia, yaitu Yogyakarta, Jakarta, Bandung, Semarang, dan Surabaya. Data mencakup informasi tempat wisata, penilaian dari pengguna, komposisi paket wisata, dan profil pengguna. Dataset ini bersumber dari platform publik dan dapat diakses melalui: [Indonesia Tourism Destination Dataset – Kaggle.](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination)

### Struktur Dataset dan Kondisi Data
Dataset terdiri atas empat file utama berikut:
- package_tourism.csv:
Berisi daftar paket wisata yang mencakup hingga lima destinasi per paket, lengkap dengan informasi kota. Jumlah data 100. Variabel-variabel pada package_tourism.csv adalah sebagai berikut:
  - Package; ID atau nama paket wisata.
  - City; Kota tempat paket wisata ditawarkan (Yogyakarta, Jakarta, Bandung, Semarang, Surabaya).
  - Place_Tourism1–5; Daftar tempat wisata yang termasuk dalam paket.
    
- tourism_rating.csv:
Berisi data rating atau ulasan pengguna terhadap tempat wisata. Jumlah data 437. Variabel-variabel pada tourism_rating.csv adalah sebagai berikut:
  - User_Id; ID unik pengguna.
  - Place_Id; ID unik tempat wisata yang diberi rating.
  - Place_Ratings; Skor penilaian (biasanya dalam skala 1–5).

- tourism_with_id.csv:
Menyediakan informasi detail untuk setiap tempat wisata, seperti nama, kategori, lokasi, harga, dan estimasi waktu kunjungan. Jumlah data 437. Variabel-variabel pada tourism_with_id.csv adalah sebagai berikut:
  - Place_Id; ID unik dari tempat wisata.
  - Place_Name; Nama tempat wisata.
  - Description; Deskripsi tempat wisata.
  - Category; Jenis/kategori wisata (alam, budaya, hiburan, kuliner, dll).
  - City; Kota tempat wisata berada.
  - Price; Biaya untuk mengunjungi tempat tersebut.
  - Rating; Rata-rata rating yang diterima tempat wisata.
  - Time_Minutes; Perkiraan durasi kunjungan (dalam menit).
  - Coordinate / Lat / Long; Lokasi geografis tempat wisata.

- user.csv:
Memuat data pengguna yang memberikan rating, termasuk lokasi dan usia. Jumlah data 300. Variabel-variabel pada user.csv adalah sebagai berikut:
  - User_Id; ID unik pengguna.
  - Location; Kota asal atau domisili pengguna.
  - Age; Usia pengguna.

### EDA
- Distribusi Tempat Wisata berdasarkan Kota

![image](https://github.com/user-attachments/assets/c00c5981-4f97-4b8f-90cd-7adc26f5ee3a)

Kota Yogyakarta memiliki jumlah tempat wisata terbanyak dalam dataset, diikuti oleh Jakarta dan Bandung.

- Distribusi Kategori Tempat Wisata

![image](https://github.com/user-attachments/assets/80b267ca-d488-40b7-b7fb-5f71af85b9ab)

Tempat hiburan dengan kategori alam dan budaya mendominasi, menunjukkan bahwa daya tarik utama di berbagai kota adalah wisata alam dan edukatif.

- Distribusi Rating Tempat Wisata

![image](https://github.com/user-attachments/assets/50bf45c1-031d-4fe3-ae16-624170cfe3c8)

Sebagian besar tempat wisata memiliki rating tinggi di atas 4.0, menandakan tingkat kepuasan pengunjung cukup baik.

- Distribusi Usia Pengguna

![image](https://github.com/user-attachments/assets/207b9f05-722b-44fa-a33a-220e3134536e)

Mayoritas pengguna yang memberikan rating berada pada rentang usia 20–35 tahun, sesuai dengan kelompok usia yang paling aktif berwisata.


## Data Preparation
Pada tahap ini, dilakukan beberapa proses data preparation untuk memastikan bahwa data yang digunakan bersih, konsisten, dan sesuai dengan kebutuhan model rekomendasi yang akan dibangun. Teknik-teknik yang digunakan dilakukan secara berurutan sesuai dengan notebook. Berikut penjelasan detailnya:

- Menghapus Kolom yang Tidak Diperlukan
  
Kolom Unnamed: 11 dan Unnamed: 12 adalah kolom kosong atau tidak memiliki informasi penting, kemungkinan besar berasal dari hasil ekspor file CSV. Kolom ini dihapus agar tidak mengganggu proses analisis dan pemodelan.

- Menangani Nilai Kosong (Missing Values)

  - Pada data packagetourism, nilai kosong diisi dengan string 'None' sebagai penanda tidak tersedia. Ini penting agar tidak terjadi error saat proses gabungan atau analisis berbasis teks.
  - Untuk kolom Time_Minutes pada tourismwithid, digunakan nilai median karena tipe datanya numerik. Median dipilih untuk menghindari bias akibat nilai ekstrim (outlier) yang dapat terjadi jika menggunakan rata-rata (mean).

- Menggabungkan Data Rating dan Data User

Langkah ini bertujuan untuk memperkaya data rating dengan informasi pengguna yang relevan, seperti ID pengguna atau atribut lainnya jika ada.

- Menggabungkan Data Rating dengan Informasi Tempat Wisata

Data hasil penggabungan ini menjadi basis utama dalam proses pemodelan rekomendasi karena sudah mengandung informasi pengguna, tempat wisata, dan nilai rating.

-  Membatasi Data ke Kota Yogyakarta

Karena fokus penelitian adalah sistem rekomendasi wisata di Yogyakarta, maka data difilter agar hanya memuat entri wisata di kota tersebut. Ini juga membantu mengurangi kompleksitas dan ukuran data.

- Menggabungkan Fitur Deskripsi dan Kategori Tempat Wisata

Fitur combined_features dibuat untuk mendukung pendekatan Content-Based Filtering, di mana informasi tekstual tentang tempat wisata digunakan sebagai dasar dalam menghitung kemiripan antar tempat. Penggabungan deskripsi dan kategori akan memberikan representasi yang lebih kaya untuk tiap destinasi wisata.

Tahapan-tahapan ini penting dilakukan untuk memastikan data dalam kondisi optimal sebelum digunakan dalam proses training model, baik untuk pendekatan Content-Based Filtering maupun Collaborative Filtering.


## Modeling
Tahapan ini membahas mengenai model sistem rekomendasi yang dikembangkan untuk membantu pengguna menemukan tempat wisata yang sesuai dengan preferensinya. Dalam proyek ini, dua pendekatan berbeda digunakan untuk memberikan Top-N Recommendation, yaitu:

1. Content-Based Filtering

Pendekatan pertama menggunakan Content-Based Filtering, yang merekomendasikan tempat wisata berdasarkan kemiripan konten dengan tempat yang pernah disukai atau dicari oleh pengguna.
- Langkah-langkah:
  - Fitur teks seperti Category, City, dan deskripsi lainnya dikombinasikan menjadi satu kolom combined_features.
  - Dilakukan proses TF-IDF vectorization untuk mengubah teks menjadi representasi numerik.
  - Cosine similarity digunakan untuk menghitung kemiripan antar tempat wisata.
  - Output: sistem akan memberikan rekomendasi tempat yang mirip dengan tempat yang dimasukkan sebagai referensi.

- Output Rekomendasi:
  
![image](https://github.com/user-attachments/assets/20567eea-4cd9-440d-b3be-05f70a2643a5)

Pendekatan ini cocok ketika belum ada data rating pengguna, dan dapat berjalan baik hanya dengan informasi konten.

2. Collaborative Filtering

Pendekatan kedua menggunakan Collaborative Filtering berbasis model, di mana sistem belajar dari pola rating pengguna terhadap berbagai tempat wisata. Model yang digunakan dapat berupa deep learning atau matrix factorization.
- Langkah-langkah:
  - Data Preprocessing:
    - Setiap User_Id dan Place_Id di-encode ke dalam indeks numerik agar dapat digunakan dalam model embedding.
    - Data rating pengguna dinormalisasi ke rentang [0,1] karena model menggunakan fungsi aktivasi sigmoid pada output.
      
  - Model Arsitektur:
    - Terdiri dari dua embedding layers masing-masing untuk pengguna dan tempat wisata.
    - Representasi vektor dari pengguna dan tempat dikombinasikan menggunakan dot product.
    - Output akhir diproses melalui fungsi sigmoid untuk mengestimasi rating sebagai probabilitas kesukaan.
      
  - Training:
    - Data dipisah menjadi training dan testing (80:20).
    - Model dilatih menggunakan binary crossentropy dan dioptimasi dengan Adam Optimizer.
    - Performa dilihat dari metrik Root Mean Squared Error (RMSE) pada data training dan validasi.
 
- Proses Training:

![image](https://github.com/user-attachments/assets/45672969-b09c-42c3-8af3-c7a79ff57546)


- Output Rekomendasi:
![image](https://github.com/user-attachments/assets/216dab9f-039b-4089-8215-6f83f515daeb)



## Evaluation
Evaluasi dilakukan untuk menilai seberapa baik sistem rekomendasi bekerja dalam memprediksi tempat wisata yang relevan bagi pengguna. Karena proyek ini melibatkan dua pendekatan berbeda yaitu, Content-Based Filtering dan Collaborative Filtering berbasis Neural Network.

1. Evaluasi Model Content-Based Filtering

Untuk model berbasis konten, tidak dilakukan evaluasi kuantitatif seperti RMSE karena model ini tidak memprediksi rating, melainkan menghitung kemiripan antar item. Cosine similarity digunakan untuk mengukur tingkat kemiripan antara dua vektor fitur tempat wisata. Nilainya berkisar antara 0 (tidak mirip) hingga 1 (sangat mirip).

- Formula:

![image](https://github.com/user-attachments/assets/6658cd60-2c1a-4bed-af39-7039a3b6c872)

Model ini dinilai baik apabila rekomendasi yang diberikan relevan secara tematik dengan tempat awal yang dipilih oleh pengguna. Evaluasi dilakukan secara kualitatif berdasarkan hasil rekomendasi yang terlihat konsisten, seperti:
    - Input: "Nol Kilometer Jl.Malioboro"
    - Output: Tempat wisata dengan karakteristik mirip seperti pusat keramaian, sejarah, dan wisata belanja.

2. Evaluasi Model Collaborative Filtering (Neural Network)

Menggunakan metrik Root Mean Squared Error (RMSE) untuk mengukur selisih rata-rata kuadrat antara rating sebenarnya dan rating yang diprediksi oleh model. Semakin kecil nilai RMSE, semakin akurat prediksi sistem.
- Formula:

![image](https://github.com/user-attachments/assets/4de91d30-76ee-4aad-bccc-a756151691e3)

- Hasil dari grafik RMSE selama proses pelatihan:
  - RMSE Training menunjukkan bahwa model mampu mempelajari pola dari data dengan cukup baik.
  - RMSE Validation tetap stabil dan tidak mengalami overfitting, menunjukkan model dapat digeneralisasi ke data baru.

    
![image](https://github.com/user-attachments/assets/5406214d-1e56-48df-b3d2-3daf7cb599f5)

Berdasarkan metrik RMSE, hasil pelatihan model menunjukkan performa yang cukup baik, dengan nilai RMSE yang rendah pada data training dan validasi. RMSE yang kecil menunjukkan bahwa model dapat memprediksi rating pengguna dengan akurasi yang cukup tinggi, artinya rekomendasi yang diberikan berdasarkan rating yang diprediksi relatif sesuai dengan preferensi pengguna. Grafik pelatihan yang menunjukkan konvergensi RMSE selama proses pelatihan mengindikasikan bahwa model tidak mengalami overfitting dan dapat digeneralisasi dengan baik ke data yang tidak terlihat sebelumnya.
 
3. Kesimpulan Evaluasi

- Content-Based Filtering adalah solusi yang efektif untuk mengatasi cold-start problem, memberikan rekomendasi yang relevan berdasarkan kesamaan konten, tetapi cenderung terbatas dalam keragaman rekomendasi dan tidak memperhitungkan preferensi individu pengguna.

- Collaborative Filtering berbasis Neural Network memberikan rekomendasi yang lebih personal dan lebih akurat ketika ada cukup data interaksi pengguna, tetapi menghadapi cold-start problem yang lebih besar, dan memerlukan lebih banyak sumber daya komputasi.

Sebagai hasil akhir, pendekatan hybrid yang menggabungkan kedua metode ini bisa menjadi solusi yang sangat efektif dalam memberikan rekomendasi yang lebih kaya dan lebih personal kepada pengguna.
