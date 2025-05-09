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
Dataset yang digunakan dalam proyek ini merupakan kumpulan data destinasi wisata dari beberapa kota besar di Indonesia, yaitu Yogyakarta, Jakarta, Bandung, Semarang, dan Surabaya. Dataset ini mencakup informasi tentang tempat wisata, penilaian dari pengguna, komposisi paket wisata, serta profil pengguna. Data bersumber dari platform publik dan dapat diakses melalui:[Indonesia Tourism Destination Dataset – Kaggle.](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination)

### Struktur Dataset dan Kondisi Data
Dataset terdiri atas empat file utama, yaitu:
1.  package_tourism.csv:
- Jumlah data 100 baris × 7 kolom. Dataset ini mencakup informasi tentang paket-paket wisata yang berisi kombinasi tempat wisata dalam satu kota.
- Variabel-variabel pada package_tourism.csv adalah sebagai berikut:
  - Package: ID atau nama dari paket wisata.
  - City: Kota tempat paket wisata ditawarkan. Hanya mencakup lima kota: Yogyakarta, Jakarta, Bandung, Semarang, Surabaya.
  - Place_Tourism1: Tempat wisata pertama dalam paket. Kolom ini selalu terisi.
  - Place_Tourism2: Tempat wisata kedua dalam paket.
  - Place_Tourism3: Tempat wisata ketiga dalam paket.
  - Place_Tourism4: Tempat wisata keempat dalam paket.
  - Place_Tourism5: Tempat wisata kelima dalam paket.
- Kondisi Data:
  - Kolom Place_Tourism3, Place_Tourism4, dan Place_Tourism5 mengandung missing values karena tidak semua paket terdiri dari lima tempat wisata.
  - Tidak ditemukan duplikat.
    
2. tourism_rating.csv:
- Jumlah data 437 baris × 3 kolom. Dataset ini mencatat penilaian pengguna terhadap tempat wisata tertentu.
- Variabel-variabel pada tourism_rating.csv adalah sebagai berikut:
  - User_Id: ID unik pengguna.
  - Place_Id: ID unik dari tempat wisata yang diberi rating.
  - Place_Ratings: Skor rating yang diberikan (dalam skala 1–5).
- Kondisi Data:
  - Tidak ditemukan missing values.
  - Terdapat kemungkinan duplikat entri (pengguna yang memberikan penilaian lebih dari satu kali ke tempat yang sama).

3. tourism_with_id.csv:
- Jumlah data 437 baris × 13 kolom. Dataset ini berisi informasi rinci tentang tempat-tempat wisata yang terdapat di kota-kota dalam cakupan data.
- Variabel-variabel pada tourism_with_id.csv adalah sebagai berikut:
  - Place_Id: ID unik dari tempat wisata.
  - Place_Name: Nama tempat wisata.
  - Description: Deskripsi singkat tentang tempat wisata, biasanya berupa ringkasan karakteristik, keunikan, atau aktivitas yang bisa dilakukan.
  - Category: Jenis atau kategori wisata, misalnya alam, budaya, hiburan, kuliner, dll.
  - City: Kota tempat wisata tersebut berada.
  - Price: Biaya atau tarif masuk ke tempat wisata (dalam satuan tidak disebutkan, kemungkinan dalam Rupiah).
  - Rating: Rata-rata rating atau penilaian dari pengguna (dalam skala 1–5).
  - Time_Minutes: Estimasi waktu kunjungan (dalam satuan menit). Kolom ini memiliki banyak nilai missing (hanya 205 dari 437 entri yang terisi).
  - Coordinate: Lokasi geografis tempat wisata dalam format string gabungan latitude,longitude.
  - Lat: Latitude dari tempat wisata dalam format desimal.
  - Long: Longitude dari tempat wisata dalam format desimal.
  - Unnamed: 11: Kolom kosong sepenuhnya, seluruh nilainya missing (null). Kemungkinan merupakan kolom sisa dari proses ekspor.
  - Unnamed: 12: Kolom berisi angka yang tidak diberi label. Belum jelas maknanya, namun semua nilainya terisi (437 non-null). Nilai-nilainya berupa integer, dan perlu eksplorasi lebih lanjut untuk memahami maknanya.
- Kondisi Data:
  - Kolom Time_Minutes memiliki missing values sebanyak 232 entri dari 437.
  - Kolom Unnamed: 11 kosong seluruhnya, bisa dihapus saat praproses.
  - Kolom Unnamed: 12 tidak diketahui fungsinya dan membutuhkan pemeriksaan lebih lanjut.
  - Tidak ditemukan duplikat.

4. user.csv:
- Jumlah data 300 baris × 3 kolom. Dataset ini berisi informasi dasar tentang pengguna yang memberikan penilaian pada tempat wisata.
- Variabel-variabel pada user.csv adalah sebagai berikut:
  - User_Id: ID unik pengguna.
  - Location: Kota tempat tinggal pengguna.
  - Age: Usia pengguna.
- Kondisi Data:
  - Tidak ditemukan missing values eksplisit, tetapi nilai Age mengandung beberapa nilai ekstrem.
  - Tidak ditemukan duplikat.

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
Pada tahap ini dilakukan serangkaian proses untuk mempersiapkan data agar siap digunakan dalam pembangunan model sistem rekomendasi. Proses dilakukan secara bertahap dan sistematis agar data bersih, relevan, dan terstruktur untuk dua pendekatan yang digunakan yaitu, Content-Based Filtering dan Collaborative Filtering. Berikut adalah tahapan yang dilakukan:

1. Menghapus Kolom yang Tidak Diperlukan
  - Kolom Unnamed: 11 dan Unnamed: 12 adalah kolom kosong atau tidak memiliki informasi penting, kemungkinan besar berasal dari hasil ekspor file CSV. Kolom ini dihapus agar tidak mengganggu proses analisis dan pemodelan.

2. Menangani Nilai Kosong (Missing Values)
  - Pada package_tourism.csv, kolom Place_Tourism3, Place_Tourism4, dan Place_Tourism5 yang memiliki nilai kosong diisi dengan string 'None'. Ini bertujuan untuk menjaga konsistensi format teks saat digabungkan atau diproses lebih lanjut.
  - Pada tourism_with_id.csv, kolom Time_Minutes memiliki banyak nilai kosong. Nilai-nilai ini diisi menggunakan nilai median dari kolom tersebut. Pemilihan median menghindari pengaruh outlier, yang bisa terjadi jika menggunakan mean.

3. Menggabungkan Data Rating dan Data User
  - Dataset tourism_rating.csv digabungkan dengan user.csv menggunakan kolom User_Id.
  - Hasil penggabungan ini memperkaya informasi rating dengan atribut pengguna, seperti lokasi dan usia, yang berpotensi digunakan dalam segmentasi atau analisis lanjutan..

4. Menggabungkan Data Rating dengan Informasi Tempat Wisata
  - Dataset hasil langkah sebelumnya kemudian digabungkan dengan tourism_with_id.csv melalui Place_Id.
  - Hasil akhir adalah data yang telah berisi informasi pengguna, tempat wisata, dan skor penilaian, serta fitur-fitur deskriptif tempat wisata (nama, kategori, harga, waktu, lokasi, dll).

5.  Menyaring Data Berdasarkan Kota Yogyakarta
  - Karena fokus penelitian adalah membangun sistem rekomendasi wisata khusus di Kota Yogyakarta, seluruh dataset difilter agar hanya mencakup entri wisata dengan City = Yogyakarta.
  - Penyaringan ini juga membantu mengurangi kompleksitas data dan memastikan model berfokus pada konteks geografis yang spesifik.

6. Membuat Fitur combined_features untuk Content-Based Filtering
  - Untuk pendekatan Content-Based Filtering, dibuat fitur baru bernama combined_features dengan cara menggabungkan kolom Description dan Category.
  - Penggabungan ini bertujuan untuk memperkaya informasi tekstual mengenai tempat wisata agar bisa digunakan dalam analisis kemiripan antar destinasi.

7. Ekstraksi Fitur dengan TF-IDF Vectorization
  - Setelah combined_features disiapkan, dilakukan transformasi teks menggunakan teknik TF-IDF (Term Frequency - Inverse Document Frequency).
  - Proses ini mengubah data teks menjadi matriks numerik yang mencerminkan pentingnya setiap kata dalam konteks seluruh dokumen (tempat wisata).
  - Hasilnya digunakan untuk menghitung similarity score antar tempat wisata berdasarkan konten deskriptifnya.

8. Persiapan Data untuk Collaborative Filtering
  - Untuk pendekatan Collaborative Filtering, data disusun menjadi user-item matrix dengan:
    - Baris mewakili User_Id
    - Kolom mewakili Place_Id
    - Nilai mewakili Place_Ratings
  - Matriks ini menjadi dasar bagi algoritma untuk mengidentifikasi pola preferensi antar pengguna.
  - Jika terdapat nilai kosong dalam matriks, ini merepresentasikan tempat yang belum diberi rating oleh pengguna, dan akan diisi atau diprediksi oleh model rekomendasi.

9. Mapping ID Pengguna dan Tempat Wisata ke Format Numerik
  - Karena model pembelajaran mesin membutuhkan input numerik, dilakukan pemetaan (encoding) terhadap ID pengguna (User_Id) dan ID tempat wisata (Place_Id) ke indeks numerik:
    - user2user_encoded: memetakan setiap User_Id ke integer unik
    - place2place_encoded: memetakan setiap Place_Id ke integer unik
  - Hasil pemetaan ini digunakan untuk membuat dua kolom baru:
    - user: hasil encode dari User_Id
    - place: hasil encode dari Place_Id
   
10. Menyusun Data Training
  - Fitur input X terdiri dari pasangan (user, place)
  - Label target y adalah nilai Place_Ratings, yang dinormalisasi ke rentang 0–1 karena fungsi aktivasi output yang digunakan adalah sigmoid, sehingga:
![image](https://github.com/user-attachments/assets/8dba9046-9dbe-4427-ad83-2e9b954ca958)

11. Membagi Data ke dalam Train dan Test Set
  - Dataset dibagi ke dalam data pelatihan dan data pengujian dengan rasio 80:20 menggunakan train_test_split dari Scikit-learn.
![image](https://github.com/user-attachments/assets/1494479d-4bf9-46a6-9081-60cc33b34f39)

12. Membuat Arsitektur Model Collaborative Filtering
  - Model yang digunakan adalah RecommenderNet, yaitu arsitektur berbasis embedding dan dot product:
    - Layer embedding dibuat untuk representasi pengguna dan tempat wisata dalam ruang vektor berdimensi 50.
    - Output dari model adalah skor prediksi kesukaan (dalam rentang 0–1), dihitung menggunakan dot product antara vektor embedding pengguna dan tempat.

13. Melatih Model
  - Model dilatih menggunakan binary crossentropy sebagai fungsi loss, karena target sudah dinormalisasi ke skala 0–1.
  - Optimizer yang digunakan adalah Adam, dengan metrik evaluasi berupa Root Mean Squared Error (RMSE).
  - Pelatihan dilakukan selama 10 epoch dengan batch size 64 dan disertai validasi terhadap data test:
![image](https://github.com/user-attachments/assets/a91487ef-585f-4b09-9a83-5503741805a4)




## Modelling dan Results
Pada bagian ini dijelaskan sistem rekomendasi yang dikembangkan untuk membantu pengguna menemukan tempat wisata sesuai preferensinya. Dua pendekatan utama digunakan, yaitu Content-Based Filtering dan Collaborative Filtering, yang masing-masing memiliki mekanisme kerja dan keunggulan tersendiri.

1. Content-Based Filtering

Content-Based Filtering adalah pendekatan yang merekomendasikan item (dalam hal ini tempat wisata) yang mirip dengan item yang telah disukai atau dikunjungi oleh pengguna sebelumnya, berdasarkan kemiripan konten.
- Cara Kerja Sistem:
  - Setiap tempat wisata direpresentasikan berdasarkan fitur-fitur tekstual seperti:
    - Category: jenis wisata (alam, budaya, dll.)
    - City: kota tempat wisata
    - Description: deskripsi tempat wisata
  - Fitur-fitur tersebut digabungkan ke dalam satu kolom combined_features.
  - Representasi teks diubah menjadi vektor numerik menggunakan teknik TF-IDF (Term Frequency-Inverse Document Frequency).
  - Kemiripan antar tempat wisata dihitung menggunakan cosine similarity antar vektor.
  - Sistem kemudian mengurutkan dan merekomendasikan tempat-tempat wisata yang paling mirip dengan tempat referensi yang diberikan pengguna.

- Kelebihan Pendekatan:
  - Tidak memerlukan data interaksi pengguna lain (cocok untuk cold-start user).
  - Memungkinkan rekomendasi berbasis deskripsi kaya dari item.

- Hasil Rekomendasi:
Sistem berhasil memberikan daftar rekomendasi tempat wisata yang kontennya serupa dengan tempat input. Misalnya, jika pengguna menyukai tempat bertema alam di Yogyakarta, maka sistem akan merekomendasikan tempat alam lain di kota tersebut dengan konten serupa.
  
![image](https://github.com/user-attachments/assets/20567eea-4cd9-440d-b3be-05f70a2643a5)

2. Collaborative Filtering

Collaborative Filtering bekerja dengan memanfaatkan pola interaksi dan penilaian antar pengguna terhadap tempat wisata, tanpa perlu mengetahui konten dari tempat tersebut. Pendekatan ini bekerja berdasarkan asumsi bahwa "pengguna yang menyukai tempat A juga cenderung menyukai tempat B".

- Cara Kerja Sistem:
  - Setiap pengguna (User_Id) dan tempat wisata (Place_Id) diubah menjadi indeks numerik, lalu dimasukkan ke dalam layer embedding.
  - Model pembelajaran mendalam (deep learning) digunakan untuk mempelajari representasi vektor pengguna dan tempat wisata.
  - Representasi ini dikombinasikan menggunakan dot product untuk memprediksi skor kesukaan.
  - Output dari model adalah skor probabilistik (antara 0 dan 1) yang mewakili seberapa besar kemungkinan pengguna menyukai suatu tempat.

- Arsitektur Model:
  - Dua layer embedding: satu untuk pengguna dan satu untuk tempat wisata.
  - Kombinasi antar vektor dilakukan dengan layer dot product.
  - Aktivasi akhir menggunakan sigmoid agar output berada dalam rentang 0–1.
  - Model dioptimasi menggunakan binary crossentropy loss dan Adam optimizer.
  - Evaluasi dilakukan menggunakan metrik Root Mean Squared Error (RMSE) pada data training dan validasi.

- Hasil Rekomendasi:
Setelah model dilatih, sistem dapat merekomendasikan tempat wisata yang belum pernah dikunjungi oleh pengguna, fungsi recommend_places() digunakan untuk menghasilkan rekomendasi personalized bagi masing-masing pengguna.


 
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
