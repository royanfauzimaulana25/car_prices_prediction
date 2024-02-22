# Laporan Proyek Machine Learning - Muh Royan Fauzi Maulana

## Domain Proyek
___
Transportasi merupakan kebutuhan setiap orang saat ini untuk memudahkan bepergian dari suatu tempat ke tempat lainnya dengan lebih cepat memanfaatkan sebuah kendaraan. salah satu kendaraan yang banyak digunakan di Indonesia adalah Mobil. Mobil memiliki  model bervariasi yang diproduksi oleh berbagai produsen didalam maupun luar negeri. Tiap tahun nya produsen mobil acap kali mengeluarkan model terbaru mobil mereka untuk dapat bersaing dengan kompetitior dan mengikuti perkembangan zaman.

Harga mobil biasanya ditentukan berdasarkan tahun keluaran, brand mobil dan model mobilnya. Mobil dengan keluaran terbaru biasanya memiliki harga yang relatif tinggi dibandingkan keluaran sebelumnya [1]. Oleh karena itu sebagian orang memilih opsi mobil bekas keluaran tahun sebelumnya sebagai alternatif kendaraanya.

Kebutuhan akan mobil bekas untuk menjadi opsi kendaraan dengan harga yang relatif terjangkau bagi sebagian orang menjadi peluang bisnis bagi perusahaan jual beli mobil. Dalam hal menentukan harga mobil bekas tersebut variabel tambahan yang menentukan antara lain adalah tahun keluaran, jarak yang sudah ditempuh mobil, dan kondisi mobil. 

Dalam hal menentukan harga mobil tersebut dengan berbagai faktor atau variabel tentunya pemiliki showroom / perusahaan jual beli mobil bekas harus memiliki metode yang tepat untuk memberikan harga idealnya untuk menghindari kerugian atau peluang kehilangan harga tinggi [2]. Oleh karena itu dibutuhkan suatu metode yang dapat memprediksi harga suatu mobil. Salah satu metode yang dapat digunakan ialah machine learning. 

Machine Learning merupakan sub bidang dari kecerdasan buatan yang mampu memprediksi suatu data kedepan berdasarkan data dan algoritma komputer. machine learning dapat membantu menentukan prediksi harga kedepan selayakanya manusia berpikir dari data yang tersedia. 

Berdasarkan uraian diatas, maka dilakukan penelitian tentang prediksi harga mobil bekas menggunakan metode machine learning. Harapanya perusahaan dapat menentukan harga mobil bekas secara tepat dan ideal sehingga dapat menghindari kerugian dan kehilangan peluang. 

## Business Understanding
___
### Problem Statements

Berdasarkan uraian latar belakang diatas, permasalahan yang dapat diselesaikan pada proyek ini ialah:
- Berdasarkan fitur yang tersedia, fitur manakah yang paling berpengaruh terhadap harga jual mobil bekas?
- Bagaimana  model machine learning yang dapat memprediksi harga mobil bekas dengan baik sehingga perusahaan dapat mendapatkan keuntungan ideal dan tidak kehilangan peluang untuk mendapatkan harga yang sesuai?

### Goals

Tujuan proyek ini dibuat adalah sebagai berikut:
- Mendapatkan analisa yang cukup terkait data harga mobil bekas.
- Memprediksi harga mobil bekas secara akurat dengan nilai error (mean square error) <5%.

### Solution statements
Solusi yang dapat diterapkan untuk menyelesaikan permasalahan tersebut adalah :
- Melakukan analisa data terkait data harga mobil bekas dengan menerapkan Exploratory data analysis (EDA) seperti teknik visualisasi. Adapun analisa yang dapat dilakukan ialah 
    - Menangani missing value.
    - mengeksplor korelasi variabel atau data fitur terhadap variabel target yaitu harga.
    - Menangani outlier.
    
- Melakukan persiapan data, seperti : 
    - Encoding fitur kategori.
    - Reduksi dimensi.
    - Spliting data.
    - Menormalisasi data.

- Menerapkan teknik Grid Search untuk mendapatkan parameter-parameter dengan performa terbaik pada masing-masing model.

## Data Understanding
Dataset yang digunakan pada proyek machine learning ini menggunakan data riwayat harga mobil dari tahun ke tahun yang dapat diunduh di website kaggle : [Car Prices Data](https://www.kaggle.com/datasets/mrsimple07/car-prices-prediction-data/data?select=CarPricesPrediction.csv).

berdasarkan analisa pada data, didapatkan informasi sebagai berikut : 
- format dataset yaitu CSV (Comma Separeted Value).
- Jumlah kolom pada dataset berjumlah 7 Kolom, antara lain: no, make, model, year, Mileage, Condition, Price.
- Fitur Target Merupakan kolom Prices.
- Terdapat 1000 sample data didalam dataset.
- Terdapat 2 kolom data yang memiliki tipe data integer yaitu (Milleage dan Year).
- Terdapat 3 Kolom data yang memiliki tipe data object atau string yaitu (Make, Model, Condition).
- Terdapat 1 Kolom data yang memiliki tipe data float64 yaitu (Price).
- Terdapat 1 kolom tidak bernama yang tidak memiliki makna apapun pada kolom pertama (akan dihapus).
- tidak terdapat missing value pada dataset.


### Variabel-variabel pada Car Prices dataset adalah sebagai berikut:
- Make: Produsen brand mobil (Chevrolet, Toyota, Ford, Honda, dan Nissan).
- Model: model / seri mobil (Altima, Camry, Silverado, F-150, Civic).
- Year: Tahun pembuatan mobil (2010 - 2022).
- Mileage: Jarak yang telah ditempuh mobil dalam mil (10K - 150K).
- Condition: kondisi mobil dari terbaik ke terburuk (Excellent, Good, Fair)
- Price: Harga Mobil dalam dolar.

Data akan dianalisa terlebih dahulu sebelum dilakukan pemrosesan data seperti korelasi antar fitur dan target dan outlier. 
Berikut visualisasi data yang menunjukan outlier dan korelasi antar fitur :
- Outlier
Berdasarkan visualisasi boxplot pada ketiga fitur numerical, outlier tidak ditemukan pada dataset, sehingga tidak diperlukannya penanganan pada nilai outlier. Tidak adanya outlier akan mempercepat proses pelatihan model dan tidak akan mempengaruhi model untuk mendapat akurasi tinggi.

    ![gambar outlier mieage](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/boxplot_Mileage.png)
    Gambar 1. Analisa Boxplot untuk fitur Numerical Mileage

    ![gambar outlier mieage](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/boxplot_price.png)
     Gambar 2. Analisa Boxplot untuk fitur Numerical Price

    ![gambar outlier mieage](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/boxplot_yearsofmanufacture.png)
     Gambar 3. Analisa Boxplot untuk fitur Numerical Years of Manufacture

- Univariate Analysis
    - Categorical Features
        Berdasarkan ketiga grafik dibawah, dapat disimpulkan bahwa fitur Make tidak akan berpengaruh signifikan pada akurasi model. Sedangkan fitur Model dan Condition memiliki sebaran data yang tidak merata yang dapat berpengaruh pada generalisasi model pada data baru. 

        ![gambar univariate categorical make](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/univariate_categorical_Make.png)
        Gambar 4. Grafik Jumlah tiap fitur Make pada dataset

        Berdasarkan grafik diatas, fitur terbesar ialah chevrolet. Namun bila dilihat secara keseluruhan jumlah fitur **Make** satu sama lain tidak terlalu jauh atau hampir sama rata.

        ![gambar univariate categorical make](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/univariate_categorical_Model.png).
        Gambar 5. Grafik Jumlah tiap fitur Model pada dataset
        
        Berdasarkan grafik diatas, sebagian besar fitur didominasi oleh model Altima dan Camry.
        
        ![gambar univariate categorical make](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/univariate_categorical_condition.png)
        Gambar 6. Grafik Jumlah tiap fitur Model pada dataset
        
        Berdasarkan grafik diatas, kualitas mobil didominasi dengan fitur Excelent yang merupakan grade terbaik.

    - Numerical Features
        Fitur target pada dataset ini adalah fitur Price, sehingga analisa berfokus pada korelasi pada data feature tersebut. 
        ![gambar univariate numerical](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/univariate_numerical.png)
        Gambar 7. Grafik Histogram Fitur Numerical
        
        Berdasarkan grafik histogram diatas, pada fitur prices diperoleh informasi sebagai berikut :

        - Sample data memusat disekitar median data. dimana dapat dilihat bahwa median data yaitu 22500 menjadi pusat sebaran data.
        - sebagian besar mobil berada pada harga direntang 17500 - 25000 dollar.
        - Distribusi mendekati distribusi normal, namun tetap tidak terkonsentrasi dimedian data untuk menjadikan distribusi normal (Aaimetris). Hal ini akan berdampak pada model.


- Multivariate Analysis
    - Categorical Features
        ![gambar multivariate categorical make](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/rata%20rata%20price%20relatif%20make.png)
        Gambar 8. Grafik Bar Chart pengaruh fitur Make pada rata rata Price

        ![gambar multivariate categorical model](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/rata%20rata%20price%20relatif%20model.png)
        Gambar 9. Grafik Bar Chart pengaruh fitur Model pada rata rata Price
        
        ![gambar multivariate categorical condition](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/rata%20rata%20price%20relatif%20condition.png)
        Gambar 10. Grafik Bar Chart pengaruh fitur Conditon pada rata rata Price
        
        Berdasarkan grafik pengaruh fitur kategorik terhadap price didapatkan insight sebagai berikut :
        - Ketiga fitur yaitu Make, Model dan Contiditon memiliki rata rata harga cenderung mirip yaitu pada kisaran diatas 20.000 Dollar keatas
        - Kesimpulan akhir ketiga fitur berpengaruh rendah pada fitur target harga.

    - Numerical Features
        ![gambar multivariate numerical](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/multivariate_numerical.png)
        Gambar 11. Grafik Pengaruh fitur numerik pada fitur target Price. 
        
        - Correlation Score
        ![gambar corr score](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/corr_score.png)
        Gambar 12. Score Heatmap Pengaruh fitur numerik pada fitur target Price. 
        
        Berdasarkan grafik diatas, pada baris ketiga didapatkan insight sebagai berikut :

        - bahwa fitur mileage memiliki pola menurun seriring bertambahnya sumbu x terhadap harga (prices). Sehingga dapat disimpulkan bahwa fitur mileage ** berkorelasi negatif** pada fitur target.
        - sedangkan fitur Years of Manufacture memiliki pola menaik seiring bertambahnya sumbu x terhadap y . Dapat disimpulkan fitur ini berkorelasi positif pada fitur target.
        - Skor korelasi pada Mileage mendekati negative 1 yaitu -0.45 yang menandakan fitur tersebut berpengaruh negatif pada fitur target price. Fitur Year berpengaruh karena skor yang paling mendekati satu, yaitu 0.88.
        - Berdasarkan haris analisas multivariate analisis ini, fitur Year of Manufacture akan menjadi fitur yang paling berpengaruh pada model. 


## Data Preparation
Pada tahapan ini akan dilakukan tahapan persiapan data, yaitu :    
- Encoding Fitur Kategori 
- Reduksi Dimensi dengan PCA
- Spliting Data
- normalisasi data 

### Tahapan encoding fitur kategori 
Fungsi encoding fitur kategori ialah untuk mengubah fitur menjadi fitur numerik yang dapat diolah oleh komputer. Encoding fitur kategori akan membuat proses pelatihan dan konvergensi model menjadi lebih cepat dan efesien.

### Reduksi Dimensi dengan PCA
Reduksi dimensi akan mengurangi jumlah fitur yang akan dilatih kedalam model tanpa mengurangi informasi fitur itu sendiri dengan membuat fitur dimensi baru.Berkurang nya fitur yang dimasukan akan membuat model tidak terlalu kompleks dan terhindar dari overffting. 
Berdasarkan gambar dibawah, Dikarenakan fitur numerik year dan mileage tidak memiliki informasi yang sama dan kedua fitur tersebut tidak memiliki korelasi sehingga tidak perlu reduksi dimensi pada fitur tersebut. Dengan kata lain fitur tersebut independen.
![gambar pca](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/pca_corr.png)
Gambar 13. Korelasi antar fitur numerikal 

### Spliting Data
Membagi dataset menjadi data latih (train) dan data uji (test). Membagi dataset tersut bertujuan untuk mengukur performa model yang dilatih dengan data latih dan diuji dengan data uji (test) Proporsi pembagian dataset pada proyek ini menggunakan proporsi pembagian 90:10 yang berarti sebanyak 90% merupakan data latih dan 10% persen merupakan data uji.

### Normalisasi Data
Normalisasi data bertujuan untuk mempermudah dan mempercepat model mencapai konvergen dan mengurangi cost computation model. Data diubah menjadi pada rentang 0 - 1. 

## Modeling
Prediksi harga mobil bekas merupakan kasus regresi yang menentukan nilai selanjutnya berdasarkan fitur fitur lainya.
Algoritma machine learning yang dapat digunakan untuk regresi yaitu K-Nearest Neigbor, Random Forest dan Support Vector Regression (SVR). Selanjutnya ketiga model tersebut akan diuji coba pada dataset untuk menemukan model terbaik untuk memprediksi harga mobil bekas secara akurat.

### K-Nearest Neighbor
merupakan algoritma machine learning dengan pendekatan supervised learning atau terawasi. Algoritma ini bekerja dengan menghitung kemiripin data disekitarnya sejumlah data (k) menjadi data baru. Dapat digunakan untuk klasifikasi dan regresi. Parameter yang digunakan pada algoritma ini ialah `n_neigbours` (jumlah teteangga). 

Keunggulan K-Nearest Neighbours:
- Sangat sederhana dan mudah dipahami
- Sangat mudah diterapkan
- Dapat digunakan dalam proses klasifikasi maupun regresi.
- Sangat mudah jika akan dilakukan penambahan data
- Parameter yang diperlukan sedikit, yaitu hanya jumlah tetangga yang dipertimbangkan (K), dan metode perhitungan jaraknya (distance metrik)

Kelemahan K-Nearest Neighbours:
- Perlu menentukan nilai K yang tepat.
- biaya komputasi yang tinggi
- Waktu pemrosesan yang lama jika datasetnya sangat besar.
- Tidak cukup bagus jika diterapkan pada high dimensional data
- Sangat sensitif pada data yang memiliki banyak noise (noisy data), banyak data yang hilang (missing data), dan pencilan (outliers).

### Random Forest
Merupakan kumpulan algoritma decision tree yang disatukan. Biasa disebut sebagai algoritma ensemble atau gabungan. Algoritma ini dapat menyelesaikan kasus klasifikasi dan regresi. Parameter yang digunakan ialah :
- n_estimator: jumlah trees (pohon) di forest. Parameter ini diset sebesar n_estimator=50.
- max_depth: kedalaman atau panjang pohon. Ia merupakan ukuran seberapa banyak pohon dapat membelah (splitting) untuk membagi setiap node ke dalam jumlah pengamatan yang diinginkan.

kelebihan random forest:
- algoritma random forest merupakan algoritma machine learning paling akurat yang tersedia
- berjalan efisien pada data besar
- dapat menangani ribuan variable atau fitur inputan

kekurangan random forest :
- mudah overfiting bilang data memiliki noise

### Support Vector Regresion (SVR)
merupakan algoritma yang menggunakan prinsip yang sama seperti support vector machine. perbedaan nya ialah svm digunakan pada kasus klasifikasi. svm bekerja dengan menentukan atau mencari hyperlane paling optimal yang memisahjkan dua data. Adapun parameter yang digunakan pada algoritma ini ialah :

- `kernel` = rbf. Parameter ini merupakan metode yang digunakan untuk mengambil data sebagai input dan mengubahnya menjadi bentuk pemrosesan data yang diperlukan.
- `gamma` = 0.003. Secara intuitif, parameter gamma menentukan seberapa jauh pengaruh satu contoh pelatihan mencapai, dengan nilai rendah berarti 'jauh' dan nilai tinggi berarti 'dekat'. Parameter gamma dapat dilihat sebagai kebalikan dari radius pengaruh sampel yang dipilih oleh model sebagai vektor pendukung.
- `C (parameter Regularisasi)` = 100000. Parameter C menukar klasifikasi yang benar dari contoh pelatihan terhadap maksimalisasi margin fungsi keputusan.

keunggulan svr :
- SVR efektif pada data berdimensi tinggi.
- SVR efektif pada kasus di mana jumlah fitur pada data lebih besar dari jumlah sampel.

kelemahan svr : 
- sulit dipakai pada skala besar yaitu jumlah sample yang terlalu banyak.

### Hyperparameter Tuning (Grid Search)
Hyperparameter Tuning (Grid Search) Hyperparameter tuning adalah cara untuk mendapatkan parameter terbaik dari algoritma dalam membangun model. Salah satu teknik dalam hyperparameter tuning yang digunakan dalam proyek ini adalah grid search. Berikut adalah hasil dari Grid Search pada proyek ini :

| **_model_** |                 **_best_params_**                 | **Prediksi_RF** |
|:-----------:|:-------------------------------------------------:|:---------------:|
|    _knn_    |                _{'n_neighbors': 1}_               |   3978.528277   |
|     _rf_    |      _{'n_estimators': 8, 'rmax_depth': 64}_      |    20.510112    |
|    _svr_    | _{'c: 8, 'n_estimators': 25, 'random_stste': 11}_ |     0.001544    |

## *Evaluation*
Metrik yang digunakan pada proyek machine learning yaitu *`Mean Squared Error (MSE)`*. Metrik tersebut mengukur seberapa dekat data prediksi dengan data aktualnya. Semakin kecil nilai MSE maka jarak antara hasil prediksi dan data aktual sangat mirip yang menjadikan model akurat untuk memprediksi data baru.

$$MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$

**Keterangan:**

* `MSE` adalah singkatan dari *Mean Squared Error*.
* `n` adalah jumlah data.
* `y_i` adalah nilai target variabel untuk data ke-i.
* `y_i^` adalah nilai prediksi model untuk data ke-i.

Setelah dilakukan evaluasi menggunakan metrik `mean squared error` didapatkan hasil pada data uji sebagai berikut : 
![gambar mse formula](https://raw.githubusercontent.com/royanfauzimaulana25/car_prices_prediction/main/visualization/train_test_eval_mse.png) 
Gambar 14. Grafik nilai *MSE* pada tiap model

berdasarkan grafik diatas *`Support Vector Regression (SVR)`* memiliki nilai kesalahan terendah pada data latih dan uji. sehingga dapat disimpulkan bahwa SVR merupakan model yang paling baik untuk kasus prediksi harga mobil bekas. 

Adapun hasil uji prediksi model adalah sebagai berikut :
Tabel 1. Nilai MSE pada ketiga model 
| **_train_** | **_test_** | **Prediksi_RF** |
|:-----------:|:----------:|:---------------:|
|    _KNN_    |     0.0    |   3978.528277   |
|     _RF_    |  6.185566  |    20.510112    |
|    _SVR_    |  0.002215  |     0.001544    |

Tabel 2. Hasil prediksi data uji pada model (USD)
|  y_true | prediksi_KNN | Prediksi_RF | Prediksi_SVR |
|:-------:|:------------:|:-----------:|:------------:|
| 23105.8 |    17986.5   |   23112.6   |    23105.9   |

# Kesimpulan
Berdasarkan serangkaian analisa yang telah dilaksanakan, model *Support Vector Regresssion (SVR)`* menjadi model terbaik untuk memprediksi harga mobil bekas dengan fitur *Years of Manufacture, Make, Model, Condition* dan *Mileage*. *SVR* dapat menjadi pilihan yang baik untuk kasus regresi ini, seperti karena dapat tahan pada dataset yang memiliki noise dan outlier. Namun, SVM memiliki beberapa kelemahan yang perlu dipertimbangkan, seperti waktu pelatihan yang lama dan kebutuhan untuk memilih kernel yang tepat.

# Referensi
[1] B. Kriswantara, K. Kurniawati, and H. F. Pardede, ‘Prediksi Harga Mobil Bekas dengan Machine Learning’, SLJIL, vol. 6, no. 5, p. 2100, May 2021, doi: 10.36418/syntax-literate.v6i5.2716.
[2] F. R. Amik, A. Lanard, A. Ismat, and S. Momen, ‘Application of Machine Learning Techniques to Predict the Price of Pre-Owned Cars in Bangladesh’, Information, vol. 12, no. 12, p. 514, Dec. 2021, doi: 10.3390/info12120514.
