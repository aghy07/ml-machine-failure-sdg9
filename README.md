⚙️ Klasifikasi Kegagalan Mesin Berdasarkan Kondisi Operasional (Predictive Maintenance)

> **Case Project Mata Kuliah Kecerdasan Buatan**  
> **Program Studi Ilmu Komputer, Universitas Halu Oleo**  
> **Relevansi:** *Sustainable Development Goals* (SDG) 9 - Target 9.5

Proyek *Machine Learning* ini bertujuan untuk mengklasifikasikan status kegagalan mesin industri (*machine failure*) berdasarkan data historis kondisi operasional sensor fisik. Proyek ini mendemonstrasikan transisi dari *reactive maintenance* menuju *predictive maintenance* menggunakan analitik kecerdasan buatan.

---

📊 Dataset
Dataset yang digunakan adalah **AI4I 2020 Predictive Maintenance Dataset** yang bersumber dari [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/601/ai4i+2020+predictive+maintenance+dataset). 

*   **Total Observasi:** 10.000 baris
*   **Target Klasifikasi:** `Machine failure` (0 = Normal, 1 = Failure)
*   **Distribusi Kelas:** Sangat tidak seimbang (*Imbalanced Dataset*), dengan kelas normal mendominasi sebesar 96,6% dan kelas gagal hanya 3,4%.
*   **Fitur Operasional Fisik:** Kualitas Produk (`Type`), `Air temperature`, `Process temperature`, `Rotational speed`, `Torque`, dan `Tool wear`.

🛠️ Metodologi & Preprocessing
Eksperimen dilakukan secara *offline* menggunakan Python dengan tahapan sebagai berikut:
1. **Pencegahan Data Leakage:** Menghapus fitur indikator mode kegagalan spesifik (TWF, HDF, PWF, OSF, RNF) agar model murni belajar dari sensor operasional.
2. **Encoding & Scaling:** Menerapkan *One-Hot Encoding* pada fitur kategorikal kualitas produk dan `StandardScaler` pada fitur numerik.
3. **Train-Test Split:** Membagi data menjadi 80% *training* dan 20% *testing* dengan parameter `stratify` untuk menjaga proporsi *class imbalance*.

🤖 Pemodelan dan Hasil Evaluasi
Proyek ini membandingkan dua algoritma klasifikasi: **Logistic Regression** (sebagai *baseline model* linear) dan **Random Forest** (sebagai model *ensemble* non-linear). Mengingat dataset sangat tidak seimbang, metrik *Recall* dan *F1-Score* menjadi fokus utama untuk meminimalkan *False Negative* (mesin gagal namun diprediksi normal.

Tabel Hasil Evaluasi (Data Testing):**

| Model | Accuracy | Precision (Kelas 1) | Recall (Kelas 1) | F1-Score (Kelas 1) |
| :--- | :--- | :--- | :--- | :--- |
| **Logistic Regression** | 0.97 | 0.64 | 0.10 | 0.18 |
| **Random Forest** | 0.98 | 0.88 | **0.53** | **0.66** |

Kesimpulan Utama:** 
*   **Random Forest** jauh lebih unggul dalam mendeteksi kegagalan mesin (*Recall* 53%) dibandingkan Logistic Regression yang banyak melewatkan kerusakan (*Recall* 10%).
*   **Feature Importance:** Berdasarkan Random Forest, fitur yang memberikan kontribusi matematis terbesar terhadap prediksi kegagalan adalah `Torque [Nm]`, `Rotational speed [rpm]`, dan `Tool wear [min]`.

🚀 Rencana Pengembangan (Konsep)
*   Mengimplementasikan teknik penanganan *class imbalance* seperti **SMOTE** atau `class_weight='balanced'` untuk lebih menekan angka *False Negative*.
*   Membangun *pipeline deployment* melalui sistem *dashboard condition monitoring* untuk teknisi pemeliharaan di lantai produksi pabrik.

---

💻 Cara Menjalankan Proyek
Proyek ini dibangun menggunakan *Jupyter Notebook* (Google Colab). Library utama yang digunakan adalah `pandas`, `numpy`, `scikit-learn`, `matplotlib`, dan `seaborn`.

Tim Pengembang (Kelompok 9)

Aghy Hutama Prawira Sigit (F1G125023)
Mawar Putri Rabia (F1G125062)
Siti Munawara  (F1G125018)
