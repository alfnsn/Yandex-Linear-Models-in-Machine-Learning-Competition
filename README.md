# Prediksi Waktu Tempuh Perjalanan – Ridge Regression

Repositori ini berisi solusi untuk kompetisi **Hackaton Digitalent × Yandex – Linear Models in Machine Learning**, dengan fokus memprediksi **waktu tempuh perjalanan (travel_time)** berdasarkan data perjalanan di Jakarta. Dataset mencakup rute, waktu, kondisi lalu lintas, cuaca, kepadatan, dan faktor-faktor lain yang memengaruhi durasi perjalanan.

---

## Deskripsi Singkat
Model dibangun menggunakan:
- **Exploratory Data Analysis (EDA)**
- **Feature Engineering lanjutan**
- **Preprocessing otomatis menggunakan ColumnTransformer**
- **Ridge Regression** sebagai model utama
- **GridSearchCV** untuk mencari nilai alpha terbaik
- Hasil akhir berupa file **submission.csv**

---

## Alur Penyelesaian

### 1. Exploratory Data Analysis (EDA)
- Mengecek ukuran dataset, tipe data, dan missing value  
- Visualisasi distribusi `travel_time` dan deteksi outlier  
- Korelasi antar fitur numerik  
- Perbandingan kategori seperti `start_point`, `end_point`, `weather`, `time_of_day` terhadap target  

---

### 2. Feature Engineering
Fitur tambahan yang digunakan untuk meningkatkan performa model:
- Kombinasi fitur:
  - `route` (start_point + end_point)
  - `day_time` (day_of_week + time_of_day)
  - `route_day_time`
- Interaction features:
  - `traffic_condition × historical_delay_factor`
  - `event_count × is_holiday`
  - Interaksi kepadatan (vehicle × population)
- Group-based traffic features
- Frequency encoding:
  - `route_freq`
  - `day_time_freq`
- Mean encoding:
  - `route_day_time_mean`
- Mapping kategori → numerik

---

### 3. Preprocessing
Dilakukan menggunakan `ColumnTransformer`:
- Imputasi: median & most_frequent  
- StandardScaler untuk semua fitur numerik  
- OneHotEncoder untuk fitur kategori  
- PolynomialFeatures:
  - Degree 4 untuk fitur penting
  - Degree 2 untuk fitur interaksi  

---

### 4. Modeling – Ridge Regression
Model utama menggunakan:
- Ridge Regression (max_iter=10000)  
- Tuning alpha (0.5 – 3)

## Output
File submission.csv berisi hasil prediksi.

## Struktur Repository
```
Data/
train_sample.csv
test_sample.csv
Ridge Regression.ipynb
submission.csv
README.md
```

## Cara Menjalankan
```
pip install -r requirements.txt
jupyter notebook "Ridge Regression.ipynb"
```

## Teknologi
Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn.
