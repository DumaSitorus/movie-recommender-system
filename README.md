# Laporan Proyek Machine Learning - Duma Mora Arta Sitorus

## Project Overview

Layanan streaming film seperti yang dimiliki oleh perusahaan Netflix, Disney , Warner dan masih banyak lagi terus meningkat jumlah penggunanya terutama para pecinta video, film maupun series (Lund et al., 2018). Pada tahun 2024, Netflix tercatat memiliki 301,6 juta pelanggan dan Disney memiliki 178,2 juta pelanggan. Pada tahun 2025, Netflix mengalami jumlah peningkatan pemasukan sebesarat 44.5 juta dolar (Szalai, 2025). Hal ini tentu mendorong perusahaan streaming ini untuk terus meningkatkan kualitas aplikasi mereka demi mempertahankan kesetiaan pelanggan. Salah satu solusi yang dapat mencapai hal tersebut adalah penerapan sistem rekomendasi.

Sistem rekomendasi berguna untuk menyediakan saran kepada para pengguna. Saran dapat berupa barang untuk dibeli, musik untuk didengar, film untuk ditonton dan bahkan keputusan untuk diambil serta bentuk saran lainnya (Abuein et al., 2017). Pengembangan sistem rekomendasi dapat dilakukan dengan pendekatan content based filtering, collaborative filtering, dan hybrid system. Tujuan proyek ini yaitu mengembangkan sistem rekomendasi film menggunakan dua pendekatan yaitu content-based filtering dan collaborative filtering.

Pendekatan pertama yang digunakan yaitu content-based filtering yang memampukan sistem memberikan rekomendasi item yang serupa dengan item yang sebelumnya berinteraksi dengan pengguna (Reddy et al., 2019). Dalam hal ini merekomendasikan film kepada pengguna berdasarkan kesamaan genre. Kemudian terdapat collaborative filtering yang merekomendasikan item dengan menganalisis perilaku dan preferensi pengguna untuk memprediksikan item berdasarkan kesamaan dengan pengguna lain (Wu et al., 2018). 

Melalui penerapan kedua pendekatan ini dapat diterapkan sistem rekomendasi yang mampu menyediakan rekomendasi film yang lebih personal, relevan dan akurat. Solusi ini diharapkan mampu meningkatkan pengalaman pengguna dan mempertahankan kepuasan serta loyalitas di tengah persaingan industri streaming film yang semakin ketat.



## Reference

Abuein, Q., Shatnawi, A., & Al-Sheyab, H. (2017). Trusted recommendation system based on level of trust (TRS_LoT). In 2017 International Conference on Engineering and Technology (ICET) (pp. 1–5). IEEE. https://doi.org/10.1109/ICEngTechnol.2017.8308148

Lund, J., & Ng, Y.-K. (2018). Movie Recommendations Using the Deep Learning Approach. 2018 IEEE International Conference on Information Reuse and Integration (IRI). doi:10.1109/iri.2018.00015 

Reddy, S., Nalluri, S., Kunisetti, S., Ashok, S., Venkatesh, B. (2019). Content-Based Movie Recommendation System Using Genre Correlation. In: Satapathy, S., Bhateja, V., Das, S. (eds) Smart Intelligent Computing and Applications . Smart Innovation, Systems and Technologies, vol 105. Springer, Singapore. https://doi.org/10.1007/978-981-13-1927-3_42

Szalai, G. (2025). Streaming profit report: Netflix leads Disney, Warner Bros. The Hollywood Reporter. https://www.hollywoodreporter.com/business/business-news/streaming-profit-report-netflix-leads-disney-warner-bros-1236184451/. Diakses pada 7 Mei 2025 pukul 21.00 WIB

Wu, C.-S. M., Garg, D., & Bhandary, U. (2018). Movie recommendation system using collaborative filtering. In 2018 IEEE 9th International Conference on Software Engineering and Service Science (ICSESS) (pp. 11–15). IEEE. https://doi.org/10.1109/ICSESS.2018.8663822

## Business Understanding

### Problem Statements

Permasalahan yang perlu diselesaikan melalui projek ini yaitu:
1. Bagaimana membangun sistem yang merekomendasikan film berdasarkan kemiripan antar film?
2. Bagaimana membangun sistem yang merekomendasikan film berdasarkan preferensi pengguna?
3. Bagaimana mengevaluasi performa sistem rekomendasi agar hasil yang diberikan optimal dan relevan?

### Goals

Tujuan dari projek ini antara lain:
1. Mengembangkan sistem rekomendasi yang memberikan saran film berdasarkan kemiripan antar film.
2. Mengembangkan sistem rekomendasi yang memberikan saran film berdasarkan preferensi pengguna.
3. Melakukan evaluasi terhadap sistem rekomendasi menggunakan metrik yang sesuai untuk memastikan kualitas dan relevansi hasil yang diberikan.

### Solution statements

1. Menerapkan pendekatan content-based filtering dengan menggunakan perhitungan TF-IDF dan cosine similarity untuk menghitung kemiripan antar film berdasarkan fitur seperti judul atau genre.
2. Menggunakan pendekatan collaborative filtering berbasis model (model-based) dengan memanfaatkan data interaksi historis antara pengguna dan film, berupa rating, untuk mempelajari preferensi pengguna.
3. Menghasilkan rekomendasi film dari masing-masing sistem (content-based dan collaborative), kemudian melakukan mendapatkan hasil rekomendasi yang diberikan.
4. Menerapkan metrik evaluasi yang sesuai untuk masing-masing pendekatan, seperti Root Mean Squared Error (RMSE) untuk collaborative filtering dan precision untuk content based filtering guna memastikan efektivitas dan akurasi sistem rekomendasi.

## Data Understanding

Dataset yang digunakan pada pembangunan sistem rekomendasi film ini diperoleh dari publik repository [Kaggle](https://www.kaggle.com/) yang dapat diakses melalui tautan [Movie Recommender System Dataset](https://www.kaggle.com/datasets/gargmanas/movierecommenderdataset). 
Dataset movie recommender terdiri dari atas 2 file terpisah yaitu movie dan rating. data movie terdiri dari 3 fitur dan 9742 baris data, sedangkan rating terdiri dari 4 fitur dan 100836 baris data. Untuk lebih detail mengenai pengenalan dataset ini akan dilakukan univariate exploratory data analysis untuk data movie dan rating.

### Univariate Exploratory Data Analysis untuk Data Movie

Informasi data:

<img width="215" alt="info-movie" src="https://github.com/user-attachments/assets/78d84435-a65f-4980-8fa4-f3264c3d37c0" />

Sample data:

<img width="433" alt="sample-movie" src="https://github.com/user-attachments/assets/5ba40afd-bfa6-4592-8776-4eb61f7950a2" />

Data `movie` terdiri dari tiga buah kolom yaitu:
1. `movieId`
    - kolom ini berisikan nomor identifikasi unik yang membedakan setiap data movie.
     - kolom `movieId` bertipe integer dan tidak memiliki *missing value*

2. `title`
    - kolom ini berisikan data judul film yang tersusun oleh `judul + (tahun tayang)`
    -  kolom `title` bertipe object dan tidak memiliki *missing value*

3. `genres`
    - kolom ini berisikan data berupa genre atau jenis film atau movie.
    -  kolom `genres` bertipe object dan tidak memiliki *missing value*
    - terdapat 951 data genre unik pada data movie dengan berbagai kombinasi dari 20 genre film yang ada. yaitu `action`, `adventure`, `animation`, `children`, `comedy`, `crime`, `documentary`, `drama`, `fantasy`, `film`, `horror`, `imax`, `musical`, `mystery`, `noir`, `romance`, `Sci-Fi`, `thriller`, `war`, `western`
    - terdapat film dengan genre yang tidak memiliki nilai tetapi diisi dengan teks `(no genres listed)`

Berdasarkan hasil analisis tersebut, diperlukan perbaikan untuk data movie sebagai berikut:
1. Data pada kolom `title` perlu dipisahkan antara judul dengan tahun tayang agar tidak memberikan representasi yang berbeda pada dua atau lebih film yang sama dengan tahun tayang yang berbeda ketika diterapkan TF-IDF.

2. Perlu perbaikan pada salah satu genre yaitu Sci-Fi yang merujuk pada genre Science Fiction. Penggunaan tanda hubungan (karakter '-') dapat memberikan representasi yang berbeda pada dua kata yaitu Sci dan Fi pada saat penggunaan TF-IDF yang menganggap karakter '-' sebagai pemisah antar kata.

3. Diperlukan penanganan pada data movie dengan genre yang kosong atau berikan `(no genres listed)`. Solusi yang dapat diberikan dapat berupa drop data jika data tidak terlalu banyak.

### Univariate Exploratory Data Analysis untuk Data Rating

Informasi data:

<img width="236" alt="info-rating" src="https://github.com/user-attachments/assets/9046bf0e-dc14-4f31-be0f-e695529459cc"/>

Sample data:

<img width="253" alt="sample-rating" src="https://github.com/user-attachments/assets/0385f56b-0586-4194-b74c-fb5d9fda6bb9"/>

Data `rating` terdiri dari empat buah kolom yaitu:
1. `userId`
    - kolom ini berisikan nomor identifikasi pengguna yang memberikan rating pada film
    - kolom `userId` bertipe integer dan tidak memiliki *missing value*
    - terdapat total 610 pengguna yang memberikan rating terhadap film

2. `movieId`
    - kolom ini berisikan nomor identifikasi film yang telah diberikan rating oleh pengguna
    -  kolom `movieId` bertipe integer dan tidak memiliki *missing value*
    - terdapat 9724 film yang telah diberikan rating oleh pengguna

3. `rating`
    - kolom ini berisikan data rating pengguna terhadap film
    -  kolom `rating` bertipe float dan tidak memiliki *missing value*
    - kolom `rating` memiliki nilai dari 0.5 hingga 5. sehingga terdapat 10 nilai unik untuk rating.
    - total keseluruhan aktivitas rate film yang tercatat pada data berjumlah 100836

4. `timestamp`
    - kolom ini berisikan data berupa timestamp atau waktu ketika data dimasukkan kedalam basis data.
    -  kolom `timestamp` bertipe integer dan tidak memiliki *missing value*

Berdasarkan hasil analisis tersebut, tidak terdapat permasalahan dalam data rating sehingga tidak perlu dilakukan penanganan apapun pada tahap preprocessing.

## Data Preparation
Tahap data preparation bertujuan untuk mempersiapkan data agar lebih bersih dan siap untuk digunakan dalam membangung sistem rekomendasi. Berikut adalah langkah yang dilakukan pada tahapan data preparation:
1. Merging dan cleaning data movie dan rating

Menggabungkan tabel rating dengan tabel movie berdasarkan movieId ke dalam sebuah dataframe bernama `df`. `df` kini memiliki 6 buah fitur yaitu `userId`, `movieId`, `rating`, `timestamp`, `title` dan `genres`. Jumlah data pada dataframe ini sebanyak 100836 buah data.
Setelah memperoleh dataframe yang memuat informasi rating pengguna terhadap film, dilakukan pengecekan apakah terdapat missing value, duplikasi data, maupun invalid data dalam dataframe tersebut. 
Data set cukup bersih dimana tidak terdapat missing value dan juga duplikasi data. Namun pada kolom genre terdapat data dengan nilai `(no genres listed)` sebanyak 47 buah data. Value ini tidak memberikan informasi apapun untuk genre sebuah film sehingga sebenarnya dapat dianggap sebagai missing value. Penanganan yang dilakukan yaitu drop data. Teknik ini dipilih karena mengingat data tersebut cukup sedikit dibandingkan jumlah keseluruhan data sehingga tidak mengganggu pola dalam data.

<img width="626" alt="merging" src="https://github.com/user-attachments/assets/9e3044ce-8d6b-4e8b-b36e-68b402a1b16a" />

2. Penanganan kolom `title`

Berdasarkan hasil analisis pada tahap exploratory data, kolom title memiliki struktur `Judul film + (tahun tayang)`. Sehingga perlu untuk memisahkan kedua bagian tersebut dengan menggunakan *Regular Expression*. Hasil penanganan kolom `title` akan menyimpan `Judul film` dalam kolom title dan tahun tayang dimuat pada kolom `year`. Tahapan ini menjadi penting agar data tidak memberikan representasi yang berbeda pada dua atau lebih film yang sama dengan tahun tayang yang berbeda ketika diterapkan TF-IDF.
    
<img width="535" alt="re-title" src="https://github.com/user-attachments/assets/fc670917-848a-48b4-86d5-238f0b281f0d" />

3. Penanganan kolom `genre`

Terdapat dua hal yang akan ditangani pada kolom genres yaitu penanganan karakter '|' dan genre value 'Sci-Fi'. Teknik yang digunakan dalam penanganan permasalahan ini yaitu *Regular Expression*. *Regular Expression* akan menemukan karakter atau teks dan diganti dengan nilai yang diinginkan.
Karakter '|' digunakan sebagai pemisah antara genre dari film dalam data. karakter '|' akan diganti dengan karakter space (' ') sebagai pemisah antar data genre tersebut.
Teks 'Sci-Fi' akan diganti nilainya menjadi 'SciFi' hal ini karena teks semula akan memberikan representasi yang berbeda karena akan dianggap sebagai 2 kata yaitu 'Sci' dan 'Fi' yang mana ini pastinya akan mempengaruhi perhitungan dalam menghasilkan rekomendasi berdasarkan kemiripan genre film.
Hasil dari tahapan ini dapat dilihat pada gambar berikut.

<img width="536" alt="re-genre" src="https://github.com/user-attachments/assets/ffe6a581-58e1-48aa-a4f5-792aeaf5f9ef" />

4. Cleaning Data Movie

Data movie akan digunakan pada pembangunan sistem rekomendasi dengan pendekatan content based filtering. Sehingga dilakukan cleaning data movie dengan berbagai teknik yaitu drop data pada kolom genre yang bernilai `(no genres listed)` dan menggunakan *regular expression* untuk memisahkan judul dengan tahun,  mengganti karakter '|' dan teks 'Sci-Fi'. Alasan cleaning data movie dan penggunaan teknik preparation tersebut sama dengan pada poin sebelumnya saat menangani data hasil merging.

## Modeling and Result

Tahapan ini membahas mengenai model sistem rekomendasi yang dikembangkan beserta top-n hasil rekomendasi film menggunakan pendekatan content based filtering dan collaborative filtering. 

### Pengembangan Sistem Rekomendasi dengan Content based Filtering

Content-Based Filtering (CBF) adalah pendekatan dalam sistem rekomendasi yang menggunakan karakteristik atau fitur dari item serta profil preferensi pengguna untuk memberikan rekomendasi. Item-item direkomendasikan kepada pengguna berdasarkan kesamaan antara item yang ada dan item yang disukai pengguna sebelumnya. Ini berarti jika seorang pengguna menyukai film tertentu, sistem akan mencoba merekomendasikan film lain yang memiliki fitur atau karakteristik yang mirip dengan item yang disukai tersebut baik melalui aktor yang berperan maupun genre film tersebut.
![ilustrasi-dicoding](https://assets.cdn.dicoding.com/original/academy/dos-619b3f2f34202af2c22998bd0dddc92420240625163549.jpeg)

Pada proyek ini, sistem rekomendasi dengan content based filtering dibangun dengan tahapan sebagai berikut:
1. Menyiapkan Data

Data yang digunakan pada pengembangan sistem rekomendasi ini akan mengambil data yang telah dibersihkan pada tahap preparation data dan menyimpannya ke dalam dataframe bernama `data`. Data ini dipilih untuk digunakan karena kita ingin mempertimbangkan rekomendasi film berdasarkan kemiripan genres antar film.

<img width="454" alt="cbf-prep-data" src="https://github.com/user-attachments/assets/524bf4ed-aa30-4d0c-88e6-f8d18139c23d" />

2. TF-IDF Vectorizer

TF-IDF Vectorizer dilakukan terhadap data movie untuk menghasilkan matriks bobot untuk setiap kata penting. 

Term Frequency (TF) mengukur seberapa sering suatu genre muncul dalam deskripsi atau atribut konten sebuah film. Genre yang lebih sering disebut atau terkait dalam suatu film diberikan bobot lebih tinggi, karena dianggap lebih representatif terhadap isi film tersebut.

![TF-Dicoding](https://assets.cdn.dicoding.com/original/academy/dos-b4564ae6e41e656876e253554497585c20240630154540.jpeg)

Inverse Document Frequency (IDF) mengukur seberapa jarang suatu genre muncul di seluruh koleksi film. Genre yang muncul di lebih sedikit film dianggap lebih spesifik atau unik, dan diberikan bobot lebih tinggi karena lebih informatif dalam membedakan film satu dengan yang lain.

![IDF-Dicoding](https://assets.cdn.dicoding.com/original/academy/dos-0b50bfccabb18a7f280a9058df732f8020240630154739.jpeg)

Sehingga secara keseluruhan perhitungan TF-IDF dirumuskan sebagai berikut:
![TF-IDF-Dicoding](https://assets.cdn.dicoding.com/original/academy/dos-4732aee49bbc9a24fb49616c916d98d720240630154923.jpeg)

Perhitungan TF-IDF dalam sistem rekomendasi film yang dikembangkan diterapkan dengan menggunakan `TfidfVectorizer()` sehingga dapat menghasilkan matriks TF-IDF dan disimpan ke dalam dataframe yang dapat dilihat pada gambar berikut.

<img width="1132" alt="matrix-tfidf" src="https://github.com/user-attachments/assets/e47bab2a-cbdd-4abe-8a9e-e6256534b93e" />

Output diatas merupakan hasil matriks tf-idf yang dihitung sebelumnya. baris mewakili item atau film sedangkan kolom berisikan kata-kata unik dari genres. Nilai yang terdapat pada baris dan kolom tertentu merupakan representasi seberapa penting genre dalam sebuah film. Jadi intinya hasil perhitungan TF-IDF memberikan representasi numerik yang mengindikasikan pentingnya kata-kata dalam judul atau genre secara relatif.

3. Cosine Similarity

Cosine similarity mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Ia menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity.  Cosine similarity dirumuskan sebagai berikut.
![Cos-Sim-Dicoding](https://assets.cdn.dicoding.com/original/academy/dos:784efd3d2ba47d47153b050526150ba920210910171725.jpeg)

Dalam proyek ini, Cosine similarity akan menggunakan hasil dari perhitungan TF-IDF untuk menghasilkan matriks numerik berdimensi `jumlah film x jumlah genre unik`. Setiap baris merepresentasikan sebuah film dan setiap kolom menunjukkan bobot TF-IDF dari masing-masing genre pada film tersebut. Matriks ini berfungsi sebagai representasi fitur konten dari setiap film dalam bentuk vektor.

<img width="619" alt="cos-sim" src="https://github.com/user-attachments/assets/9c89c5dc-bf12-4d05-9e4c-4e08125cfc1f" />

Hasil cosine similarity ini digunakan sebagai dasar untuk merekomendasikan film-film lain yang paling mirip secara konten terhadap film yang sedang dilihat pengguna.

4. Mendapatkan Rekomendasi

Setelah dilakukan proses perhitungan kemiripan antar film dengan TF-IF dan Cosine Similarity, maka berikutnya adalah mengimplementasikan cara untuk mendapatkan daftar rekomendasi film yang mirip dengan sebuah film.

Pertama, akan dibuat fungsi `movie_recommendations` dengan beberapa parameter sebagai berikut:
movie_title : Judul Film (index kemiripan dataframe).
Similarity_data : Dataframe mengenai similarity yang telah kita definisikan sebelumnya.
Items : Nama dan fitur yang digunakan untuk mendefinisikan kemiripan, dalam hal ini adalah ‘movie_title’ dan ‘genres’.
k : Banyak rekomendasi yang ingin diberikan.

Setelah fungsi berhasil diimplementasikan, maka dapat langsung digunakan untuk menghasilkan rekomendasi film serupa. Berikut adalah hasil rekomendasi yang dihasilkan oleh fungsi.

<img width="419" alt="cbf-rec-result" src="https://github.com/user-attachments/assets/3aa8ea60-912a-4efa-9a76-15855c70899a" />

Hasil rekomendasi film diperoleh dengan terlebih dahulu memanggil fungsi `movie_recommendations('Kung Fu Panda')` yang akan mengembalikan top-N recommendation yang mirip dengan judul movie yang diinputkan. Fungsi juga akan melakukan Drop movie title yang diinputkan pada fungsi agar judul movie yang dicari tidak muncul dalam daftar rekomendasi. Top-5 hasil rekomendasi telah berhasil dikembalikan oleh fungsi dimana hasil tersebut memiliki genre yang sangat mirip dengan film 'Kung Fu Panda'.

Adapun kelebihan dan kekurangan yang dapat dipertimbangkan dalam pemilihan pendekatan content based filtering adalah sebagai berikut:
**1. Kelebihan**
- Teknik ini baik dipakai ketika skala user yang besar.
- Teknik ini dapat menemukan ketertarikan spesifik dari seorang user dan dapat merekomendasikan item yang jarang disukai orang lain.

**2. kekurangan**
- Karena kita yang menentukan meta feature sendiri, kualitas dari rekomendasi tergantung kualitas dari meta feature itu sendiri.

### Pengembangan Model Rekomendasi dengan Collaborative Filtering
Collaborative filtering merupakan sebuah pendekatan yang menggunakan informasi dari aktivitas pengguna untuk memberikan rekomendasi. CF mencoba menemukan pola dan hubungan antara pengguna dan item. Terdapat 2 metode yang digunakan pada pendekatan ini yaitu model based (metode berbasis model machine learning) dan memory based (metode berbasis memori).
![CF-dicoding](https://assets.cdn.dicoding.com/original/academy/dos:756ce41a29e4e7b511a355fee284110320210910165836.jpeg)

Pada pengembangan sistem rekomendasi film yang akan dikembangkan pada proyek ini menggunakan model based CF. Sehingga akan dilakukan pelatihan model untuk belajar representasi pengguna dan item. Adapun tahapan yang dilakukan yaitu:
1. Data Preparation
Data yang digunakan pada pengembangan sistem rekomendasi akan menggunakan data yang telah dibersihkan pada tahap preparation data yaitu `df`. Data ini dipilih karena kita akan menggunakan historis interaksi (rating) pengguna terhadap item (film).
Data `df` memiliki fitur userId dan movieId dalam bentuk integer yang tidak berurutan karena telah melalui tahapan preprocessing dan preparation. Sehingga perlu dilakukan tahapan encoding agar data tersebut terindeks dengan baik. Hasil encoding data adalah sebagai berikut:

Data hasil encoding tersebut dimuat ke dalam kolom baru di data frame sebagai `user` dan `movie` menggunakan teknik mapping.  Dengan dapat dilakukan perhitungan jumlah pengguna, jumlah movie, rating tertinggi dan terendah.
- Number of User: 610
- Number of movie: 9724
- Min Rating: 0.5 
- Max Rating: 5.0'

Melalui tahapan persiapan ini, data semakin siap untuk masuk ke tahapan modeling.

2. Data Splitting

Tahapan ini bertujuan untuk melakukan pembagian data menjadi data training dan validasi. Namun, terlebih dahulu akan dilakukan pengacakan data agar distribusinya menjadi random. Hal ini membantu model untuk lebih handal dalam menemukan pola pada data.
Pada tahapan data splitting akan dilakukan dengan rangkaian langkah berikut:
    - memetakan (mapping) data user dan movie menjadi satu value terlebih dahulu
    - membuat rating dalam skala 0 sampai 1 agar mudah dalam melakukan proses training. 
    - pembagian data train dan validasi dengan komposisi 80:20.

Hasil pembagian akan tampak sebagai berikut:

<img width="551" alt="split-data" src="https://github.com/user-attachments/assets/f94c07e4-19b2-4e64-849e-ea20fd45006d" />

    
keseluruhan data akan dibagi menjadi X dan y. X yaitu vektor pertama akan berisi data user dan movie sedangkan y yaitu vektor kedua akan berisi berisi data rating pengguna terhadap movie. Pembagian data train dan test menggunakan rasio 80/20.

3. Modelling

Pada tahap ini, akan dibuat model yang akan menghitung skor kecocokan antara pengguna dan movie dengan teknik embedding. Pertama, akan dilakukan proses embedding terhadap data user dan movie. Selanjutnya, lakukan operasi perkalian dot product antara embedding user dan movie. Selain itu, dapat ditambahkan bias untuk setiap user dan resto. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi sigmoid.
Pada Proyek ini akan dibuat kelas `RecommenderNet(tf.keras.Model)`.

Setelah fungsi telah berhasil diimplementasikan, dilakukan proses compile terhadap model dengan kode berikut:
    
    model = RecommenderNet(num_users, num_movie, 50) # inisialisasi model
    
    # model compile
    model.compile(
        loss = tf.keras.losses.BinaryCrossentropy(),
        optimizer = keras.optimizers.Adam(learning_rate=0.001),
        metrics=[tf.keras.metrics.RootMeanSquaredError()]
    )
    
Model tersebut menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation. Langkah selanjutnya adalah proses training model yang dilakukan dengan kode berikut:
    
    # training
    history = model.fit(
        x = x_train,
        y = y_train,
        batch_size = 32,
        epochs = 15,
        validation_data = (x_val, y_val),
    )

Output dari pelatihan tersebut adalah sebagai berikut.

<img width="971" alt="training-history" src="https://github.com/user-attachments/assets/989d3468-761e-424d-8613-d9558744aa66" />

4. Plot RMSE

Untuk melihat visualisasi proses training maka dapat melakukan plot hasil perhitungan RMSE dengan library matplotlib. Hasil plot adalah sebagai berikut:

![plot-rmse](https://github.com/user-attachments/assets/73d87014-664c-47db-8cde-08d65e6f76a0)

5. Mendapatkan Rekomendasi

Pada tahapan ini, dilakukan percobaan untuk memperoleh hasil rekomendasi untuk sampel user. Hasil rekomendasi akan memberikan judul film yang pernah di rating dengan nilai tinggi oleh user tersebut sebagai film yang paling diminati, kemudian menampilkan rekomendasi film berdasarkan preferensi dan rating para pengguna. Rekomendasi film yang akan diberikan merupakan daftar film yang belum pernah di rating oleh pengguna.

Film yang belum pernah ditonton (dalam hal ini belum pernah diberikan rating) oleh pengguna sebelumnya akan disimpan dalam movie_not_watched yang diperoleh dengan menggabungkan operator bitwise (~) pada movie_watched_by_user atau film yang pernah ditonton oleh user.
Selanjutnya, untuk memperoleh rekomendasi film maka digunakan fungsi `model.predict()` dari library Keras untuk memprediksi film rekomendasi berdasarkan interaksi pengguna (rating).

Berikut adalah hasil Top-N salah satu hasil rekomendasi yang diberikan untuk user 230.

Dari hasil tersebut, terlihat bahwa model telah berhasil memberikan daftar rekomendasi beberapa film yang belum pernah ditonton oleh pengguna berdasarkan rating pengguna terhadap film sebelumnya.

Adapun kelebihan dan kekurangan yang dapat dipertimbangkan dalam pemilihan pendekatan collaborative filtering adalah sebagai berikut:
**1. Kelebihan**
- Teknik ini tidak memerlukan informasi konten seperti genre dan fitur sejenis lainnya, cukup dengan data interaksi (rating, like, pembelian) antar user dan item. Sehingga rekomendasi disesuaikan berdasarkan histori unik tiap pengguna, bukan hanya berdasarkan fitur item.
- Pendekatan ini memampukan sistem untuk menemukan pola tersembunyi yang tidak terlihat secara eksplisit

**2. kekurangan**
- Cold start problem. Terjadi saat pengguna baru atau item baru belum punya cukup interaksi sehingga tidak bisa direkomendasikan secara akurat.
- Kebutuhan terhadap data dengan jumlah yang banyak untuk analisis interaksi histori


## Evaluation
Pada bagian ini, sistem rekomendasi yang telah berhasil dikembangkan akan dievaluasi menggunakan metrik pengukuran yang sesuai dengan pendekatan yang digunakan. Berikut adalah tahap evaluasi untuk setiap pendekatan.

### Evaluasi Sistem Rekomendasi Content Based Filtering
Evaluasi untuk sistem rekomendasi dengan content based filtering dapat dilakukan dengan menggunakan berbagai macam metrik yang antara lain:
1.  Precision@K

Metrik ini akan mengukur apakah hasil rekomendasi yang diberikan benar-benar relevan dengan input dari segi kesamaan genre.

<img width="586" alt="precision" src="https://github.com/user-attachments/assets/024affcd-0b3e-4286-bbd1-058fc87c5ae3" />

- Pembilang: Jumlah film dalam rekomendasi dan memiliki genre yang sama dengan film input
- Penyebut (K): Jumlah film yang direkomendasikan (misal: top-5)

2.  Recall@K

Metrik ini akan melakukan pengukuran seberapa banyak item (film) yang relevan (genre sama) yang direkomendasikan. Sesuai konteks projek ini Recall dapat dirumuskan sebagai berikut:

<img width="568" alt="recall" src="https://github.com/user-attachments/assets/1522815e-2d43-4675-8a6b-467641d75db7" />

- K = Jumlah film yang direkomendasikan (misal: top-5)



3.  F1-Score@K

Metrik ini akan melakukan pengukuran dengan hasil kombinasi dari precision dan recall. 

<img width="279" alt="F1-score" src="https://github.com/user-attachments/assets/a109a904-04ea-47a5-a132-8b1ed8445991" />

- K = Jumlah film yang direkomendasikan (misal: top-5)

Metrik pengukuran yang dapat diterapkan dalam evaluasi untuk kasus ini adalah Precision@K.
Dalam kasus ini, metrik Recall@K kurang relevan karena tidak dapat diimplementasikan tanpa mengetahui data semua item yang relevan untuk direkomendasikan. Karena metrik recall sebelumnya kurang relevan, maka F1-Score juga secara otomatis menjadi tidak dapat diukur karena ketersediaan akan seluruh data yang relevan atau dapat direkomendasikan tidak tersedia.

Sehingga precision@K dipilih sebagai metrik evaluasi karena sesuai dengan konteks sistem rekomendasi berbasis genre yang dikembangkan. Berikut adalah evaluasi sistem rekomendasi film dengan pendekatan content based filtering menggunakan precision@K.

Dari data rekomendasi yang diberikan untuk film yang serupa dengan film input yaitu 'Kung Fu Panda', terdapat 5 buah film yang dapat kita hitung jumlah genre yang sesuai.
- Jumlah film dalam rekomendasi dan memiliki genre yang sama dengan film input adalah 5. Keseluruhan rekomendasi memiliki minimal 1 genre yang sama dengan film input.
- K = 5
- Maka Precision@5 = 5/5 = 1.0
- Precision@5 = 1.0 atau 100%, karena semua film yang direkomendasikan memiliki genre yang sama dengan film yang diminta.

### Evaluasi Sistem Rekomendasi collaborative Filtering
RMSE (Root Mean Squared Error) adalah metrik evaluasi regresi yang mengukur rata-rata akar kuadrat dari selisih antara nilai yang diprediksi dan nilai sebenarnya. RMSE mengukur seberapa jauh prediksi sistem dari nilai rating sebenarnya. Formula perhitungan RMSE adalah sebagai berikut.

<img width="219" alt="rmse" src="https://github.com/user-attachments/assets/45cc011d-09da-47e0-b986-c9cf0cba1309" />

Keterangan:
- n = Jumlah pasangan (user, film) yang sudah memberikan rating sebenarnya. Misalnya: 10.000 interaksi user-film.
- yi = Rating asli yang diberikan user ke film tertentu.
- y^i = Rating yang diprediksi oleh model Collaborative Filtering oleh User tertentu.

Untuk evaluasi pada model sistem rekomendasi film dengan pendekatan collaborative filtering yang telah dikembangkan dapat dihitung pada saat proses pelatihan untuk evaluasi. Hasil perhitungan dibuat ke dalam plot berikut:

![plot-rmse](https://github.com/user-attachments/assets/73d87014-664c-47db-8cde-08d65e6f76a0)
    
Berdasarkan hasil plot tersebut, terlihat bahwa nilai Root Mean Square Error terus menurun seiring bertambahnya epoch dengan nilai error  akhir sebesar 0.1867 untuk pelatihan dan 0.1994 untuk test.

# Conclusion
Pada proyek pengembangan sistem rekomendasi film ini, saya telah berhasil membuat sistem rekomendasi dengan pendekatan Content based Filtering dan Collaborative Filtering. Sistem rekomendasi dengan pendekatan Content based Filtering telah berhasil memberikan top-5 saran film berdasarkan kemiripan antar film.

Kemudian, untuk dengan pendekatan Collaborative Filtering telah berhasil melatih model yang mampu memberikan rekomendasi film berdasarkan preferensi pengguna seperti rating terhadap film.

Sistem rekomendasi baik yang dikembangkan dengan Content based Filtering telah dievaluasi menggunakan perhitungan precision yang mampu menghitung persentase kesesuaian genre antar film yang diinputkan dengan daftar film yang direkomendasikan.
Sedangkan model rekomendasi dengan pendekatan collaborative filtering telah dievalusi dengan menghitung nilai Root Mean Squared Error pada setiap epoch untuk melihat perkembangan kemampuan model dalam mengurangi kesalahan dalam memprediksikan untuk menghasilkan rekomendasi film.

Konsep pada proyek ini dapat diimplementasikan dengan menyesuaikan data mengingat industri film terus mereproduksi film setiap waktu sehingga perlu penyesuaian dataset.
