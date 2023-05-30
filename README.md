# 🙂 Predict Customer Personality to Boost Marketing Campaign
<br>

**Tool** : Jupyter Notebook | [Link Notebook](https://github.com/faizns/Predict-Customer-Personality-to-Boost-Marketing-Campaign/blob/main/Predict%20Customer%20Personality.ipynb)<br>
**Programming Language** : Python <br>
**Libraries** : Pandas, NumPy, sklearn <br>
**Visualization** : Matplotlib, Seaborn, yellow-brick <br>
**Source Dataset** : Rakamin Academy <br>
<br>
<br>

**Table of Contents**
- [STAGE 0: Problem Statement]()
	- [Introduction]()
	- [Goal]()
	- [Objective]()
- [STAGE 1: Data Preparation]()
	- [Data Quality Asssessment]()
	- [Feature Engineering]()
- [STAGE 2: Data Exploration]()
	- [Conversion Rate by Income, Spending, and Age]()
	- [Income and Total Spending]()
- [STAGE 3: Data Modeling with K-Means Clustering]()
	- [Pre-processing]()
	- [Modeling]()
	- [Evaluation]()
- [STAGE 4: Customer Personality Analysis]()
- [STAGE 5: Business Recommendation]()
<br>
<br>

---

## 📂 **STAGE 0: Problem Statement**

### Introduction
Memahami bagaimana profil dan perilaku pelanggan dalam melakukan transaksi sangat penting untuk mengatur strategi penjualan produk dari sebuah perusahaan. Dengan memahami preferensi, kebutuhan, dan pola pembelian pelanggan, perusahaan dapat memberikan treatment yang tepat untuk setiap individu berdasarkan permasalahan yang dihadapinya. Dengan mempertimbangkan faktor-faktor ini, perusahaan dapat memberikan pengalaman yang lebih baik kepada pelanggan, meningkatkan kepuasan mereka dalam bertransaksi, dan pada akhirnya meningkatkan performa penjualan secara keseluruhan. Untuk menganalisis profil dan perilaku pelanggan, pendekatan clustering dapat digunakan untuk mengelompokkan pelanggan ke dalam segmen-segmen yang berbeda, yang kemudian dapat memberikan wawasan berharga dalam menyusun strategi penjualan yang lebih efektif dan memenuhi kebutuhan setiap kelompok pelanggan dengan lebih baik. Dengan demikian, memahami karakteristik pelanggan melalui analisis clustering merupakan langkah penting dalam mengoptimalkan strategi penjualan dan mencapai keberhasilan jangka panjang bagi perusahaan.<br>
<br>

### Goal
Tujuan dari analisis profil dan perilaku pelanggan dengan pendekatan clustering adalah untuk memahami pelanggan dengan lebih baik, menyediakan layanan yang lebih personal, meningkatkan performa penjualan, dan membangun hubungan yang kuat dengan pelanggan.<br>
<br>

### Objective
- Membuat model mechine learning yang dapat mengelompokkan pelanggan ke dalam segmen-segmen yang berbeda berdasarkan karakteristik dan perilaku mereka.
- Mengekstraksi insight yang lebih mendalam tentang profil dan perilaku pelanggan.
- Menentukan strategi bisnis yang efektif dari hasil clustering.<br>

<br>
<br>

---
## 📂 **STAGE 1: Data Preparation**
### Data Quality Asssessment
Dataset memiliki 2240 baris dan 30 fitur. Asesmen data dilakukan untuk memastikan bahwa data yang digunakan untuk analisis selanjutnya sudah siap dan sesuai dengan kebutuhan analisis. Hal yang dilakukan:
- Memeriksa missing value pada data
- Memeriksa duplikasi data
- Memeriksa tipe dan konsistensi nilai
- Memeriksa outlier atau data yang tidak biasa (anomali)

Tabel 1 — Hasil Data Quality Assessment
 **Data Assessment** | **Finding**  | **Cleaning** 
--------------------|--------------|--------------
Missing values | Tidak terdapat missing value | -
Duplikat | Tidak terdapat duplikat data | -
Fitur atau nilai yang tidak sesuai | Tipe data `Dt_Customer` sebaikkanya datettime | Mengubah tipe data menjadi datteime
Anomali atau outlier | Secara keseluruhan fitur memiliki outlier. Terlihat juga fitur `Income` dan `Year_Birth` memiliki nilai yang ekstrim  | Handling outlier menggunakan IQR.
<br>

### Feature Engineering
Pada tahap feature engineering, dilakukan pembuatan feature baru berdasarkan feature yang sudah ada dengan tujuan untuk membuat analisis menjadi lebih insightful. Feature baru ini dapat mengungkap informasi tambahan atau menggabungkan beberapa fitur yang saling berhubungan untuk membentuk fitur yang lebih kuat.

Tabel 2 — Feature Engineering
 **New Feature** | **Source** |
-----------------|--------------|
Membership Duration | 2023 - Dt_Customer  
Age_Categories | Age
Total_Children | Kidhome + Teenhome
Total_Transaction | NumDealsPurchases + NumWebPurchases + NumCatalogPurchases + NumStorePurchases
Total_Spending | MntCoke + MntFruits + MntMeatProducts + MntFishProducts + MntSweet
Total_Accepted_Campaign | AcceptedCmp1 + AcceptedCmp2 + AcceptedCmp3 + AcceptedCmp4 + AcceptedCmp5
CVR | Total_Transaction x NumWebVisitsMonth/100

<br>
<br>

## 📂 **STAGE 2: Data Exploration**
### Conversion Rate by Income, Spending, and Age
Pada tahap ini, dilakukan analisis konversi rate untuk mendapatkan wawasan tentang persentase pengunjung situs web dan tindakan yang dilakukan selama kunjungan mereka. Tujuan analisis ini adalah untuk melihat apakah tindakan pengunjung tersebut berujung pada transaksi pembelian atau tidak. Dengan demikian, perusahaan dapat memahami perilaku pengunjung dan mengidentifikasi peluang untuk meningkatkan tingkat konversi serta keberhasilan campaign pemasaran mereka.

<br>
<p align="center">
    <kbd> <img width="1000" alt="cvr" src="https://github.com/faizns/Predict-Customer-Personality-to-Boost-Marketing-Campaign/assets/115857221/cd694ce7-cb4f-409e-b8b5-3ae2272134dd"> </kbd> <br>
    Gambar 1 — Plot Korelasi Conversion Rate (CVR) dengan Pendapatan, Total Pengeluaran, dan Usia
</p>
<br>

Terdapat temuan bahwa **pendapatan dan total spending memiliki korelasi positif yang signifikan terhadap tingkat konversi**. Hal ini menunjukkan bahwa **semakin tinggi pendapatan dan total spending seseorang, semakin besar kemungkinan mereka melakukan pembelian**. Faktor-faktor seperti kemampuan finansial yang lebih baik dan persepsi nilai yang tinggi terhadap produk dapat menjadi penyebab korelasi positif ini. Oleh karena itu, perusahaan dapat memanfaatkan temuan ini untuk mengoptimalkan strategi pemasaran mereka. Mereka dapat fokus pada target audiens dengan pendapatan dan total spending yang lebih tinggi, dengan tujuan meningkatkan peluang konversi dan keberhasilan marketing campaign secara keseluruhan. Di sisi lain, **fitur usia cenderung tidak memiliki korelasi yang signifikan terhadap tingkat konversi**. Hal ini berarti usia tidak menjadi faktor dominan yang mempengaruhi keputusan konsumen dalam melakukan konversi atau pembelian. <br>
<br>

### Income and Total Spending
Analisis korelasi antara Income dan total spending penting dilakukan karena kedua fitur ini memiliki hubungan yang erat dalam konteks keuangan dan pengeluaran individu atau pelanggan. Dengan menganalisis korelasi antara kedua fitur ini, dapat dipahami sejauh mana tingkat pendapatan seseorang mempengaruhi pola pengeluaran mereka.

<br>
<p align="center">
    <kbd> <img width="500" alt="total spending income" src="https://github.com/faizns/Predict-Customer-Personality-to-Boost-Marketing-Campaign/assets/115857221/73d7c91c-9a00-4801-8e83-a7d300124827"> </kbd> <br>
    Gambar 2 — Plot Korelasi Pendapatan dengan Total Pengeluaran
</p>
<br>

Hubungan korelasi positif yang kuat antara Income dan total spending menunjukkan **adanya hubungan yang signifikan antara tingkat pendapatan seseorang dengan pola pengeluaran mereka**. Hal ini mengindikasikan bahwa **semakin tinggi pendapatan seseorang, kemungkinan besar mereka juga memiliki pengeluaran yang lebih tinggi**. Dalam konteks bisnis, pemahaman ini dapat membantu perusahaan dalam mengenali segmen pelanggan yang memiliki potensi pembelian yang lebih tinggi dan merancang strategi pemasaran yang tepat untuk meningkatkan keterlibatan dan kepuasan pelanggan.

<br>
<br>

---
## 📂 **STAGE 3: Data Modeling with K-Means Clustering**
### Pre-processing
Sebelum melakukan data modeling, terdapat beberapa tahap pre-processing data yang perlu dilakukan yaitu:
- **Fitur yang tidak diperlukan** untuk model akan **dihapus** agar data lebih terfokus. 
- Fitur kategorikal akan di-**encoding** agar dapat diolah oleh algoritma machine learning. 
- Dilakukan **standardisasi** fitur untuk memastikan skala data seragam dan menghindari bias dalam model.<br>
<br>

### Modeling
Setelah pre-processing data selesai, tahap berikutnya adalah menggunakan metode **Principal Component Analysis (PCA)**. PCA digunakan untuk mengurangi dimensi data dengan mempertahankan informasi yang signifikan. Dengan mengurangi dimensi data, dapat mengoptimalkan kinerja model dan mengatasi masalah multicollinearity antara fitur. Selanjutnya, langkah penting dalam proses ini adalah menentukan jumlah cluster terbaik. Dalam analisis ini, **Distortion Score dan Elbow Method** digunakan untuk memilih jumlah cluster yang optimal. Berdasarkan hasil analisis, **jumlah cluster terbaik yang ditemukan adalah 4**.

<br>
<p align="center">
    <kbd> <img width="600" alt="distortion" src="https://github.com/faizns/Predict-Customer-Personality-to-Boost-Marketing-Campaign/assets/115857221/176ddb7a-2357-49c0-8d06-1222973b0229"> </kbd> <br>
    Gambar 3 — Plot Distortion Scoce Elbow
</p>
<br>

Setelah menentukan jumlah cluster yang optimal, dilakukan **clustering menggunakan algoritma K-means**. Algoritma ini akan mengelompokkan data ke dalam cluster berdasarkan kesamaan fitur. Dengan melakukan clustering, dapat mengidentifikasi pola atau kelompok yang ada dalam data dan memahami karakteristik masing-masing cluster.

<br>
<p align="center">
    <kbd> <img width="600" alt="cluster" src="https://github.com/faizns/Predict-Customer-Personality-to-Boost-Marketing-Campaign/assets/115857221/dda584d5-8519-4775-92c9-f7519bee8c6f"> </kbd> <br>
    Gambar 4 — Hasil Clustering menggunakan K-means
</p>
<br>

Dari plot hasil pemodelan dan pengelompokan data menggunakan metode clustering, terlihat bahwa **cluster-cluster yang terbentuk terpisah dengan baik** dan mengelompokkan data ke dalam kelompok yang berbeda-beda. Hal ini menunjukkan bahwa algoritma clustering yang digunakan berhasil dalam membedakan dan menggolongkan data berdasarkan karakteristik yang dimiliki.<br>
<br>

### Evaluation

<p align="center">
    <kbd> <img width="400" alt="score" src="https://github.com/faizns/Predict-Customer-Personality-to-Boost-Marketing-Campaign/assets/115857221/1c6de7e4-aea2-4cfc-a6a8-402ab4a5b6c2"></kbd> <br>
    Gambar 5 — Hasil Evaluasi
</p>
<br>

Evaluasi hasil model menggunakan **Silhouette Score memberikan rekomendasi bahwa jumlah cluster terbaik adalah 4**. Hal ini didasarkan pada fakta bahwa nilai Silhouette Score pada jumlah cluster tersebut adalah yang tertinggi, yaitu 0.535. Silhouette Score merupakan metrik evaluasi yang menggambarkan seberapa baik objek-objek dalam satu cluster berada dalam kumpulan data mereka sendiri dibandingkan dengan cluster lainnya. Semakin tinggi nilai Silhouette Score, semakin baik cluster-cluster tersebut terpisah. <br>
<br>
<br>

---

## 📂 **STAGE 4: Customer Personality Analysis**
Customer Personality Analysis bertujuan untuk **memahami perbedaan dan kesamaan antara cluster-cluster tersebut, serta mengidentifikasi karakteristik unik yang mungkin dimiliki oleh setiap kelompok**. Dengan pemahaman yang lebih mendalam tentang karakteristik antar cluster, perusahaan dapat mengambil tindakan yang lebih tepat dan mengarahkan strategi bisnis yang lebih spesifik untuk setiap kelompok pelanggan.

<p align="center">
    <kbd> <img width="500" alt="income spending cluster" src="https://github.com/faizns/Predict-Customer-Personality-to-Boost-Marketing-Campaign/assets/115857221/d85e981b-615f-4ace-a07b-ddcd32cb4457"></kbd> <br>
    Gambar 6 — Plot Pendapatan dan Total Pengeluaran Berdasarkan Cluster
</p>
<br>

Berdasarkan plot korelasi antara pendapatan (Income) dan total pengeluaran (Total Spending), terlihat bahwa terdapat pembentukan cluster atau kelompok yang dapat dibedakan. Dalam hal ini, **cluster 0 dan 3 cenderung berada dalam satu kelompok yang menunjukkan adanya persamaan dan perbedaan karakteristik di antara kedua cluster tersebut**. Ketika dua cluster berada dalam satu kelompok, hal ini mengindikasikan bahwa terdapat kemiripan atau keterkaitan dalam pola pendapatan dan pengeluaran di antara anggota-anggota cluster tersebut. Secara visual, terlihat bahwa **kedua cluster tersebut mungkin memiliki tingkat pendapatan dan pengeluaran yang relatif mirip atau memiliki tren yang serupa**.

<p align="center">
    <kbd> <img width="1000" alt="meancluster" src="https://github.com/faizns/Predict-Customer-Personality-to-Boost-Marketing-Campaign/assets/115857221/2d66d306-a36d-46d2-a9f4-1f09f93abc1f"></kbd> <br>
    Gambar 6 — Plot Karakteristik Mayoritas/Rata-rata Total Transaksi, Pengeluaran, Pendapatan, Recency, dan Conversion Rate Berdasarkan Cluster
</p>
<br>

Berdasarkan hasil analisis yang lebih mendalam dapat diketahui karakteristik rata-rata/mayoritas dari setiap cluster berdasarkan pola transaksi pelanggan dan dapat dikelompokkan berdasarkan beberapa kategori.
- **Cluster 0**
    - Angka transaksi dan spending tertinggi yaitu mayoritas 25 transaksi dan Rp.1.116.000/bulan
    - Pendapatan cukup tinggi, mayoritas Rp.65.215.000/tahun
    - Conversion rate sedang, yaitu 4%
    - Kategori : **"*High-Transaction High-Spending Group*" - High Customer A** <br>
<br>

- **Cluster 1**
    - Angka transaksi dan spending terendah yaitu mayoritas hanya 7 transaksi dan Rp.58.000/bulan
    - Pendapatan terendah, mayoritas Rp.33.297.500/tahun
    - Conversion terendah, yaitu 1%
    - Kategori : **"*Low-Transaction Low-Spending Group*" - Low Customer** <br>
<br>
    
- **Cluster 2**
    - Angka transaksi dan spending cukup tinggi yaitu mayoritas 20 transaksi dan Rp.1.040.000/bulan
    - Pendapatan tertinggi, mayoritas Rp.71.488.000/tahun
    - Conversion rate tertinggi, yaitu 8%
    - Kategori : **"*High-Income High-Conversion Group*" - High Customer B** <br>
<br>

- **Cluster 3**
    - Angka transaksi dan spending sedang yaitu mayoritas 17 transaksi dan Rp.434.000/bulan
    - Pendapatan cukup sedang, mayoritas Rp.52.597.000/tahun
    - Conversion rate cukup sedang, yaitu 3%
    - Kategori : **"*Moderate-Transaction Moderate-Spending Group*" - Moderate Customer**<br>
<br>

Analisis distribusi beberapa fitur masing-masing cluster dilakukan juga dilakukan untuk mendapatkan wawasan yang lebih dalam. Melalui analisis ini, ditemukan beberapa insight menarik yang dapat memberikan pemahaman yang lebih baik tentang perilaku pengguna dalam setiap cluster, khususnya terkait kunjungan website dan respon terhadap campaign.

<p align="center">
    <kbd> <img width="900" alt="distri clus" src="https://github.com/faizns/Predict-Customer-Personality-to-Boost-Marketing-Campaign/assets/115857221/05707677-9a7e-47c2-b071-6f2d2c72c718"></kbd> <br>
    Gambar 7 — Plot Distribusi Berdasarkan Cluster
</p>
<br>

Berikut temuan yang menarik:
- **Low Customer (Cluster 1)** yang memiliki distribusi jumlah kunjungan website yang tinggi, namun memiliki total acceptance campaign yang rendah. Ini menunjukkan bahwa kelompok ini sangat **sering mengunjungi website perusahaan, tetapi tidak sepenuhnya menyadari atau tidak responsif terhadap campaign yang ditawarkan**. Mengingat kelompok ini memiliki populasi yang paling banyak, perusahaan perlu mengembangkan strategi yang tepat untuk menarik perhatian dan meningkatkan keterlibatan mereka. 
- Cluster yang **paling banyak merespon campaign adalah High Customer A (Cluster 0)** dengan tingkat konversi yang sedang. Ini menunjukkan bahwa mayoritas pelanggan dalam kelompok ini sangat responsif terhadap campaign yang ditawarkan oleh perusahaan. Hal ini dapat menjadi kesempatan yang baik untuk meningkatkan interaksi dan pembelian dari kelompok ini dengan meluncurkan campaign yang lebih menarik dan relevan sesuai dengan preferensi mereka.
- **High Customer B (Cluster 2)**, mayoritas pelanggannya tidak terlalu sering mengunjungi website perusahaan, namun memiliki distribusi konversi rate yang lebih tinggi dengan respon campaign yang sedang. Fenomena ini menunjukkan bahwa kelompok ini **memiliki kecenderungan pengeluaran yang tinggi dan cenderung merespons positif terhadap campaign yang ditawarkan, meskipun mereka tidak begitu aktif dalam kunjungan ke website**. Perusahaan dapat memanfaatkan informasi ini dengan mengoptimalkan saluran komunikasi lain seperti email, media sosial, atau platform online lainnya untuk efektif menjangkau kelompok ini.

<br>
<p align="center">
    <kbd> <img width="600" alt="percentage" src="https://github.com/faizns/Predict-Customer-Personality-to-Boost-Marketing-Campaign/assets/115857221/d7c0d96e-3d15-4d59-9ffc-b7afed8786a0"></kbd> <br>
    Gambar 8 — Plot Presentase Populasi Cluster 
</p>
<br>

Berdasarkan persentase populasi masing-masing cluster, ditemukan bahwa **50.22% dari keseluruhan pelanggan termasuk dalam kelompok Low Customer (Cluster 1)**. Meskipun kelompok ini memiliki angka transaksi dan pengeluaran yang rendah, namun karena populasi mereka yang besar. Perusahaan dapat fokus untuk menarik perhatian mereka. Sedangkan populasi **High Customer A (Cluster 0) dan B (Cluster 2) cenderung rendah**, namun memiliki potensi transaksi dan spending yang tinggi. Perusahaan dapat mempertimbangkan strategi pemasaran yang lebih personal dan eksklusif untuk menarik minat mereka.

<br>
<br>

---

## 📂 **STAGE 5: Business Recommendation**

Berdasarkan analisis yang telah dilakukan, dapat diidentifikasi personalitas atau karakteristik pelanggan berdasarkan cluster yang terbentuk. Mengetahui karakteristik ini sangat berharga dalam merancang strategi pemasaran yang lebih efektif. Dengan memahami preferensi, kebutuhan, dan perilaku konsumen dalam setiap cluster, perusahaan dapat menghasilkan campaign yang lebih relevan dan menarik bagi setiap kelompok pelanggan.

### High Customer A
Summary:
- Populasi 12.61%.
- High-Transaction High-Spending Group.
- Paling responsif terhadap campaign, dengan tingkat kunjungan website dan konversi ke pembelian sedang.

Rekomendasi:
- Mengingat kelompok High Customer A cenderung memiliki total transaksi dan total spending yang tinggi, perusahaan dapat memberikan **penawaran khusus dan insentif tambahan untuk mendorong pelanggan melakukan pembelian secara terus-menerus**. Perusahaan dapat menerapkan program diskon eksklusif, hadiah loyalitas, atau akses ke produk atau layanan khusus untuk kelompok ini.
- Perusahaan dapat meningkatkan **kualitas pengalaman pengguna dalam berselancar di website, mengingat tingkat kunjungan website yang sedang**. Perusahaan dapat memastikan tampilan yang menarik, customer journey yang efisien, dan lain sebagainya.
- Mengingat kelompok High Customer A sangat responsif terhadap campaign, memanfaatkan kepuasan mereka dengan memperkenalkan **program referral** dapat menjadi strategi yang efektif. Memberikan insentif kepada pelanggan untuk merekomendasikan produk atau layanan perusahaan kepada teman dan keluarga dapat membantu dalam memperluas jangkauan dan memperoleh pelanggan baru.
- Perusaan dapat **mingirimkan pesan yang dipersonalisasikan** seperti info promo atau diskon **berdasarkan preferensi** kelompok ini. Hal ini dilakukan untuk menjaga loyalitas pelanggan. <br>
<br>


### High Customer B
Summary :
- Populasi 13.42%.
- High-Income High-Conversion Group.
- Sama seperti High Customer B dalam segi income dan total spending, namun memiliki income paling tinggi.
- Tingkat konversi paling tinggi, respon terhadap campaign relatif sedang, kurang mengunjungi website secara aktif. 

Rekomendasi:
- Sama halnya dengan High Customer A, perusahaan dapat **memberikan penawaran khusus** seperti diskon, program loyalti, dan sebagainya agar pelanggan selalu tertarik untuk berbelanja terus menerus.
- Mengingat kelompok ini kurang aktif dalam kunjungan website, perusahaan dapat memanfaatkan **saluran komunikasi alternatif untuk campaign** seperti email, pesan teks, atau media sosial. Hal ini dapat membantu meningkatkan interaksi dan kesadaran pelanggan.
- Untuk meningkatkan respon pelanggan terhadap campaign, perusahaan dapat **memberikan campaign-campaign yang tertarget sesuai dengan preverensi dan kebutuhan pelanggan**.
- Mengingat pelanggan dalam kelompok High Customer B memiliki tingkat konversi yang tinggi, perusahaan dapat mempertimbangkan untuk meluncurkan **program loyalitas** yang memberikan insentif tambahan, penghargaan khusus, atau akses ke acara atau produk eksklusif dapat memperkuat loyalitas pelanggan. <br>
<br>


### Moderate Customer
Summmary:
- Populasi 23.75%.
- Moderate-Transaction Moderate-Spending Group
- Tingkat konversi, kunjungan website dan respon terhadap campaign relatif sedang.

Rekomendasi:
- Perusahaan dapat memberikan **penawaran khusus** dan diskon untuk mendorong pembelian lebih lanjut. Hal ini dapat memberikan insentif tambahan kepada pelanggan dalam kelompok ini untuk memilih produk atau layanan perusahaan dibandingkan dengan pesaing.
- Perusahaan dapat **mengirim pesan yang relevan dan menarik** kepada pelanggan untuk melakukan transaksi.
- **Memastikan pengalaman pengguna yang baik saat mengunjungi website** atau berinteraksi dengan produk atau layanan perusahaan.
- Membangun **program hadiah atau loyalitas** dapat membantu memperkuat keterikatan pelanggan. Seperti dengan memberikan poin, penghargaan, atau manfaat khusus kepada pelanggan setia, perusahaan dapat mendorong mereka untuk terus memilih dan membeli produk atau layanan perusahaan. <br>
<br>


### Low Customer
Summary:
- Populasi 50.22%, pelanggan didominasi oleh kategori ini.
- Low-Transaction Low-Spending Group.
- Tingkat konversi paling rendah, cenderung tidak merespon campaign, namun kategori ini paling sering mengunjungi website.

Rekomendasi:
- Mengingat kelompok Low Customer sering mengunjungi website, perusahaan dapat **memanfaatkan informasi kunjungan website untuk menyajikan konten yang personalisasi dan penawaran khusus yang sesuai dengan minat dan preferensi mereka**.
- Perusahaan dapat **melakukan retargeting campaign** dengan mengingatkan pelanggan dalam kelompok ini tentang produk atau layanan yang mereka telah kunjungi di website. Dengan menampilkan iklan yang disesuaikan di berbagai platform digital yang mereka gunakan, perusahaan dapat membangun kesadaran dan mendorong mereka untuk melanjutkan proses pembelian.
- Mengingat kelompok Low Customer memiliki tingkat konversi yang rendah dan cenderung tidak merespon campaign dengan baik, perusahaan dapat **menggunakan strategi konten yang lebih fokus pada edukasi dan informasi (softselling)**. Memberikan konten yang memberikan nilai tambah, memberikan solusi untuk masalah atau kebutuhan pelanggan, dan membantu mereka membuat keputusan yang lebih informatif dapat meningkatkan keterlibatan dan kepercayaan pelanggan dalam kelompok ini.
