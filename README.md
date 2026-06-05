# 📉 Customer Churn Prediction

Proyek **Machine Learning** untuk memprediksi pelanggan yang berpotensi **berhenti berlangganan (churn)** pada sebuah perusahaan layanan internet. Tujuannya: membantu tim retensi melakukan pencegahan lebih awal.

> **Jenis ML:** Supervised Learning · **Jenis masalah:** Classification (biner: churn / tidak)

---

## 🎯 Latar Belakang Bisnis

Sebuah perusahaan internet ingin tahu **pelanggan mana yang kemungkinan akan keluar**, sehingga bisa ditawarkan solusi/insentif sebelum benar-benar berhenti. Memprediksi churn lebih murah daripada mencari pelanggan baru.

- **Target:** `churn` → `0` = Tetap berlangganan, `1` = Berhenti
- **Metrik utama:** F1-Score, Recall, Precision, Confusion Matrix (bukan hanya Accuracy, karena data tidak seimbang)

---

## 📊 Dataset

`data/customer_churn_dummy.csv` — **10.000 baris**, 7 kolom (data sintetis untuk latihan).

| Kolom | Arti |
|---|---|
| `umur` | Umur pelanggan (tahun) |
| `lama_berlangganan` | Lama berlangganan (bulan) |
| `tagihan_bulanan` | Tagihan per bulan (Rupiah) |
| `jumlah_keluhan` | Jumlah keluhan yang diajukan |
| `jumlah_login` | Jumlah login ke aplikasi |
| `paket_premium` | Pakai paket premium (1) / tidak (0) |
| `churn` | **Target** — berhenti (1) / tetap (0) |

Catatan: kelas churn **tidak seimbang** (~71% churn vs ~29% tetap), sehingga evaluasi tidak boleh hanya bergantung pada Accuracy.

---

## 🗂️ Struktur Repo

```
.
├── data/
│   └── customer_churn_dummy.csv      # dataset
├── notebooks/
│   └── churn_prediction.ipynb        # notebook utama (EDA → model → evaluasi)
├── requirements.txt
├── .gitignore
└── README.md
```

---

## ⚙️ Cara Menjalankan

```bash
# 1. (opsional) buat virtual environment
python -m venv venv
venv\Scripts\activate          # Windows
# source venv/bin/activate     # macOS / Linux

# 2. install dependensi
pip install -r requirements.txt

# 3. buka notebook
jupyter notebook notebooks/churn_prediction.ipynb
```

---

## 🔬 Metodologi

1. **Data Understanding** — memahami struktur & distribusi data
2. **Data Cleaning** — cek missing value & duplikat
3. **EDA** — visualisasi distribusi, churn rate per fitur, korelasi
4. **Feature Engineering** — `tenure_group`, `rasio_keluhan_login`
5. **Preprocessing** — one-hot encoding + train/test split (stratified 80/20)
6. **Modeling** — Logistic Regression (baseline) → Random Forest
7. **Evaluasi** — Accuracy, Precision, Recall, F1, ROC-AUC, Confusion Matrix
8. **Insight Bisnis** — rekomendasi yang bisa ditindaklanjuti

---

## 📈 Hasil

Performa pada data uji (2.000 pelanggan), metrik untuk kelas **churn (1)**:

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | **0.882** | **0.919** | 0.915 | **0.917** | **0.960** |
| Random Forest | 0.878 | 0.914 | 0.915 | 0.915 | 0.953 |

> 💡 Menariknya, **Logistic Regression yang sederhana tampil setara — bahkan sedikit lebih unggul** — dibanding Random Forest. Pelajarannya: model kompleks tidak selalu lebih baik ketika pola datanya sudah jelas.

---

## 🔑 Insight Bisnis

1. **Jumlah keluhan adalah prediktor churn terkuat** (korelasi +0.71). Pelanggan dengan **8+ keluhan hampir pasti churn (~99%)**, sedangkan yang keluhannya sedikit (0–3) hanya ~16%.
2. **Rekomendasi:** bangun sistem *early warning* — saat pelanggan mencapai ambang keluhan tertentu (mis. 4+), tim retensi langsung menghubungi dan menawarkan solusi.
3. Memperbaiki kualitas penanganan keluhan = menurunkan churn.

---

## 🚀 Langkah Lanjutan

- Hyperparameter tuning (`GridSearchCV`)
- Teknik penyeimbang data (SMOTE / `class_weight`)
- Deploy model sederhana (Streamlit) agar bisa dipakai tim bisnis

---

## 🛠️ Tools

`Python` · `pandas` · `numpy` · `scikit-learn` · `matplotlib` · `seaborn` · `Jupyter Notebook`
