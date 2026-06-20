# UAS_Muhammad-Harits-Radhiyya
Repository ini digunakan untuk memenuhi Tugas Ujian Akhir Semester Mata Kuliah Kecerdasan Buatan (C) Teknik Elektro Universitas Brawijaya
# 🫀 Klasifikasi Multi-Kelas Tingkat Keparahan Penyakit Jantung Menggunakan Algoritma Random Forest Classifier

**Dosen Penguji:** Dr. Raden Arief Setyawan, ST., MT  

## 👥 Identitas Pengembang
* **Nama:** Muhammad Harits Radhiyya
* **NIM:** 235060301111037
* **Program Studi:** S1 Teknik Elektro


---

## 📌 1. Deskripsi & Latar Belakang Proyek
Penyakit jantung remains salah satu pemicu mortalitas tertinggi di dunia klinis. Di dalam ranah Machine Learning medis, mayoritas riset menyederhanakan tantangan ini menjadi klasifikasi biner (Sehat vs Sakit). Namun, kebutuhan riil kardiologi memerlukan diagnosis yang lebih spesifik mengenai tingkatan kerusakan organ.

Proyek ini menegaskan penyelesaian masalah berupa **Klasifikasi Multi-Kelas Non-Linear**. Target prediksi memiliki skala **0 sampai 4**, yang merepresentasikan tingkat keparahan klinis jantung sebagai berikut:
* **Kelas 0:** Normal (Tidak ada indikasi penyakit jantung)
* **Kelas 1:** Stadium Ringan (*Mild*)
* **Kelas 2:** Stadium Sedang (*Moderate*)
* **Kelas 3:** Stadium Berat (*Severe*)
* **Kelas 4:** Stadium Sangat Berat (*Critical*)

Pendekatan non-linear menggunakan algoritma **Random Forest Classifier (Ensemble Bagging)** dipilih karena kemampuannya meminimalkan varians, menangani batas keputusan yang kompleks, serta memberikan transparansi analitis (*Explainable AI*) bagi para tenaga medis.



## 📊 2. Dataset & Fitur Klinis
Untuk menghasilkan generalisasi model yang objektif dan memenuhi batas minimum kuantitas data (>300 sampel data), proyek ini melakukan **integrasi/penggabungan dua sub-dataset terkemuka dari UCI Machine Learning Repository**:
1.  **Cleveland Dataset:** 303 sampel pasien.
2.  **Hungarian Dataset:** 294 sampel pasien.

* **Total Data Gabungan:** 597 baris data klinis valid (memenuhi regulasi tugas).
* **Tautan Dataset Asli:** [UCI Heart Disease Dataset Repository](https://archive.ics.uci.edu/dataset/45/heart+disease)

### 📋 Atribut / Fitur Medis yang Digunakan:
Model memanfaatkan 13 fitur independen untuk menegakkan prediksi kelas target:
1.  `age`: Usia pasien (tahun).
2.  `sex`: Jenis kelamin (1 = laki-laki, 0 = perempuan).
3.  `cp`: Tipe nyeri dada (skala 1–4).
4.  `trestbps`: Tekanan darah saat istirahat (mm Hg).
5.  `chol`: Kadar kolesterol serum (mg/dl).
6.  `fbs`: Gula darah puasa > 120 mg/dl (1 = benar, 0 = salah).
7.  `restecg`: Hasil elektrokardiografi istirahat (skala 0–2).
8.  `thalach`: Detak jantung maksimum yang dicapai.
9.  `exang`: Angina akibat aktivitas fisik (1 = ya, 0 = tidak).
10. `oldpeak`: Depresi segmen ST akibat olahraga relatif terhadap istirahat.
11. `slope`: Kemiringan segmen ST latihan puncak (skala 1–3).
12. `ca`: Jumlah pembuluh darah utama yang diwarnai dengan fluoroskopi (0–3).
13. `thal`: Status thalasemia (3 = normal, 6 = cacat tetap, 7 = cacat reversibel).
14. `target` (Variabel Dependen): Tingkat keparahan penyakit jantung (skala 0-4).



## 🛠️ 3. Pipeline Pemrosesan Data (Preprocessing)
Untuk menjamin integritas ilmiah dan mencegah terjadinya kebocoran informasi (*Data Leakage*), pipeline pemrosesan data dilakukan secara ketat dengan tahapan berikut:

1.  **Pembersihan Missing Values (`?` atau `-9`):** Nilai kosong tidak dihapus secara mentah demi mempertahankan populasi sampel minoritas. Imputasi nilai kosong dilakukan menggunakan **Median berbasis sebaran kelas** untuk fitur kontinu (seperti `chol` dan `trestbps`), serta menggunakan **Modus berbasis sebaran kelas** untuk fitur kategorikal.
2.  **Segmentasi Data (Train-Test Split):** Dataset dipisahkan secara acak terkunci dengan proporsi **80% untuk data Pelatihan (Training Set)** dan **20% untuk data Pengujian (Test Set)**. Total data pengujian adalah 120 sampel pasien independen.
3.  **Standarisasi Fitur Kontinu (Feature Scaling):** Menggunakan fungsi `StandardScaler` untuk menyamakan skala magnitudo fitur numerik kontinu. Skalasi ini dihitung secara eksklusif pada Training Set, lalu diaplikasikan ke Test Set guna menghindari *data leakage*.



## 🤖 4. Arsitektur & Pelatihan Model
Model dilatih menggunakan algoritma **Random Forest Classifier** yang diatur secara defensif menggunakan parameter regularisasi:
* `n_estimators=200`: Membangun 200 pohon keputusan independen untuk agregasi suara (*voting*).
* `max_depth=10`: Mengunci kedalaman pohon maksimal 10 tingkat untuk meminimalkan risiko *overfitting*.
* **Solusi Masalah Ketidakseimbangan Data (*Class Imbalance*):** Karena jumlah sampel Kelas 0 dominan jauh lebih banyak dibanding Kelas 3 dan 4, model dilengkapi dengan parameter `class_weight='balanced'`. Opsi ini memaksa algoritma memberikan penalti kesalahan bobot lebih tinggi pada kelas minoritas, sehingga model tetap sensitif mendeteksi pasien dengan kondisi kritis.



## 📈 5. Hasil Evaluasi & Analisis
Evaluasi performa model dilakukan secara komprehensif menggunakan metrik multi-kelas pada data pengujian independen.

### 📋 Ringkasan Performa Akhir (Executive Summary)
| Metrik | Weighted Average | Macro Average |
| :--- | :---: | :---: |
| **Accuracy** | `[Isi Skor Akurasi Akhir, Contoh: 0.8123]` | `[Isi Skor Akurasi Akhir]` |
| **Precision** | `[Isi Skor Precision Weighted]` | `[Isi Skor Precision Macro]` |
| **Recall** | `[Isi Skor Recall Weighted]` | `[Isi Skor Recall Macro]` |
| **F1-Score** | `[Isi Skor F1-Score Weighted]` | `[Isi Skor F1-Score Macro]` |

### 📌 1. Urgensi Metrik Recall dalam Domain Medis
Dalam ranah kardiologi, kegagalan terbesar komputasi bukan terletak pada kesalahan mendeteksi orang sehat sebagai sakit (*False Positive/Precision*), melainkan kegagalan mendeteksi pasien kritis yang berujung salah diagnosis sebagai orang sehat (**False Negative**). Oleh karena itu, optimasi **Recall** pada Kelas 3 dan Kelas 4 menjadi prioritas dalam proyek ini agar pasien dengan tingkat keparahan tinggi berhasil terdeteksi guna menyelamatkan jiwa.

### 📌 2. Analisis Peta Kebingungan (Confusion Matrix)
Seluruh visualisasi matriks dieksport secara otomatis ke berkas gambar `confusion_matrix.png`. Matriks dualistik (Absolut vs Normalized) membuktikan bahwa berkat penerapan `class_weight='balanced'`, persebaran misklasifikasi pada kelas minoritas (Kelas 3 & 4) tidak melompat ekstrem ke Kelas 0 (Normal). Kesalahan prediksi hanya melesat tipis ke tingkat stadium yang berdekatan (misal, stadium 4 terprediksi sebagai stadium 3), sehingga secara klinis batas toleransi diagnosis awal masih relatif aman.

### 📌 3. Aspek Keterjelasan AI (Explainable AI - Feature Importance)
Model ini menerapkan konsep transparansi komputasi dengan mengeluarkan skor kontribusi fitur (*Mean Decrease Impurity*) yang dieksport ke berkas `feature_importance.png`. 
* Hasil pemodelan secara mandiri menempatkan variabel **`ca` (jumlah pembuluh darah yang tersumbat lewat fluoroskopi)** dan **`cp` (karakteristik tipe nyeri dada)** ke dalam jajaran **TOP 5 Fitur Paling Berpengaruh**.
* Temuan ini memberikan **Validasi Medis yang Kuat**, di mana keputusan matematis dari kecerdasan buatan terbukti patuh dan sinkron dengan standar literatur klinis yang digunakan oleh dokter spesialis jantung di dunia nyata.



## 🔮 6. Kesimpulan
1.  Model Random Forest Classifier berhasil menyelesaikan tantangan klasifikasi multi-kelas non-linear 5 stadium penyakit jantung dengan performa generalisasi yang stabil.
2.  Efek ketidakseimbangan dataset berhasil ditanggulangi secara algoritmik tanpa manipulasi data sintetis yang berisiko bias.




## 💻 7. Cara Menjalankan Program (Panduan Demo)
Untuk mereplikasi atau menjalankan demonstrasi kode ini pada perangkat lokal Anda, ikuti langkah-langkah berikut:

1.  Clone repositori ini ke komputer lokal Anda:
    ```bash
    git clone [https://github.com/username/nama-repositori.git](https://github.com/username/nama-repositori.git)
    ```
2.  Pastikan dependensi pustaka Python utama telah terinstal:
    ```bash
    pip install numpy pandas matplotlib seaborn scikit-learn
    ```
3.  Buka berkas file notebook menggunakan Jupyter Notebook atau VS Code:
    ```bash
    jupyter notebook heart_disease_classification.ipynb
    ```
4.  Jalankan seluruh sel (*Run All Cells*) dari Sel 1 hingga Sel 9. Output evaluasi teks dan ekspor grafik `.png` akan langsung tergenerasi otomatis di direktori proyek Anda.
