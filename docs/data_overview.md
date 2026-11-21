# Data Overview

Ringkasan hasil dari notebook `01_data_understanding.ipynb`.

## 1. Data Loading

Dataset dimuat dari:

- `data/raw/train.csv`
- `data/raw/test.csv`
- `data/raw/sample_submission.csv`

## 2. Data Overview

### 2.1 Shape dan Kolom

| Dataset | Shape | Keterangan |
|---|---|---|
| Train | 594.194 baris x 21 kolom | Berisi 20 fitur dan target `Churn` |
| Test | 254.655 baris x 20 kolom | Berisi fitur tanpa target `Churn` |
| Sample submission | 254.655 baris x 2 kolom | Kolom `id` dan `Churn` |

### 2.2 Deskripsi Kolom Train

| Column | Type | Description |
|---|---|---|
| id | int64 | Identifier unik setiap pelanggan pada data train. |
| gender | str | Jenis kelamin pelanggan: Male atau Female. |
| SeniorCitizen | int64 | Status warga lanjut usia; 1 berarti senior citizen dan 0 berarti bukan. |
| Partner | str | Menunjukkan apakah pelanggan memiliki pasangan: Yes atau No. |
| Dependents | str | Menunjukkan apakah pelanggan memiliki tanggungan: Yes atau No. |
| tenure | int64 | Lama berlangganan pelanggan dalam bulan. |
| PhoneService | str | Menunjukkan apakah pelanggan menggunakan layanan telepon: Yes atau No. |
| MultipleLines | str | Status beberapa jalur telepon: Yes, No, atau No phone service. |
| InternetService | str | Jenis layanan internet: DSL, Fiber optic, atau No. |
| OnlineSecurity | str | Status layanan keamanan online: Yes, No, atau No internet service. |
| OnlineBackup | str | Status layanan pencadangan online: Yes, No, atau No internet service. |
| DeviceProtection | str | Status perlindungan perangkat: Yes, No, atau No internet service. |
| TechSupport | str | Status dukungan teknis: Yes, No, atau No internet service. |
| StreamingTV | str | Status layanan streaming TV: Yes, No, atau No internet service. |
| StreamingMovies | str | Status layanan streaming film: Yes, No, atau No internet service. |
| Contract | str | Jenis kontrak: Month-to-month, One year, atau Two year. |
| PaperlessBilling | str | Menunjukkan apakah pelanggan menggunakan tagihan tanpa kertas: Yes atau No. |
| PaymentMethod | str | Metode pembayaran pelanggan. |
| MonthlyCharges | float64 | Biaya bulanan yang dibayarkan pelanggan. |
| TotalCharges | float64 | Total biaya yang telah dibayarkan pelanggan. |
| Churn | str | Target prediksi; Yes berarti pelanggan berhenti berlangganan dan No berarti tidak berhenti. |

Test memiliki 20 kolom fitur dengan shape **254.655 x 20**. Test tidak memiliki kolom target `Churn`.

## 3. Missing Values

- Train: tidak ada missing value pada 594.194 baris dan 21 kolom.
- Test: tidak ada missing value pada 254.655 baris dan 20 kolom.
- Sample submission: tidak ada missing value pada kolom `id` dan `Churn`.

## 4. Duplicate

- Train: 0 baris duplikat.
- Test: 0 baris duplikat.
- Sample submission: 0 baris duplikat.

Setiap baris dapat diperlakukan sebagai observasi pelanggan unik.

## 5. Cardinality

- `id` memiliki 594.194 nilai unik pada train dan 254.655 nilai unik pada test.
- Tidak ada overlap ID antara train dan test.
- Kolom biner mayoritas memiliki 2 kategori: `gender`, `SeniorCitizen`, `Partner`, `Dependents`, `PhoneService`, dan `PaperlessBilling`.
- Kolom `MultipleLines`, `InternetService`, serta layanan tambahan seperti `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, dan `StreamingMovies` memiliki 3 kategori.
- `Contract` memiliki 3 kategori dan `PaymentMethod` memiliki 4 kategori.
- Target `Churn` memiliki 2 kategori.
- Pada train, `tenure` memiliki 72 nilai unik, `MonthlyCharges` memiliki 1.921 nilai unik, dan `TotalCharges` memiliki 31.910 nilai unik.

## 6. Target Distribution

| Churn | Jumlah | Persentase |
|---|---:|---:|
| No | 460.377 | 77,48% |
| Yes | 133.817 | 22,52% |

Dataset tidak seimbang: pelanggan yang tidak churn sekitar 3,44 kali jumlah pelanggan yang churn. Karena itu, akurasi saja tidak cukup sebagai metrik evaluasi utama.

## 7. Ringkasan Fitur Numerik

| Fitur | Rata-rata | Median | Minimum | Maksimum |
|---|---:|---:|---:|---:|
| tenure | 36,58 bulan | 35 bulan | 1 bulan | 72 bulan |
| MonthlyCharges | 65,87 | 74,10 | 18,25 | 118,75 |
| TotalCharges | 2.494,38 | 1.433,65 | 18,80 | 8.684,80 |

`SeniorCitizen` bertipe integer namun merupakan fitur kategorikal biner.

## 8. Konsistensi Train dan Test

- Train memiliki 594.194 baris dan 21 kolom.
- Test memiliki 254.655 baris dan 20 kolom fitur.
- Train dan test tidak memiliki overlap ID.
- Tipe dan kategori fitur test konsisten dengan train.
- Format prediksi mengikuti `sample_submission`: 254.655 baris dengan kolom `id` dan `Churn`.

## 9. Kesimpulan Data Understanding

- Data relatif lengkap tanpa missing value.
- Tidak ditemukan duplikasi pada train, test, maupun sample submission.
- Sebagian besar fitur adalah kategorikal bertipe string, sedangkan fitur numerik utama terdiri dari `tenure`, `MonthlyCharges`, dan `TotalCharges`.
- Target `Churn` tidak seimbang dan perlu dipertimbangkan dalam pemilihan metrik serta strategi validasi/model.
- Tahap berikutnya memerlukan feature engineering berupa encoding untuk fitur kategorikal dan, jika algoritma yang digunakan sensitif terhadap skala, scaling untuk fitur numerik.
