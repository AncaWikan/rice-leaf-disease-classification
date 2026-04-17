# 🌾 Klasifikasi Penyakit Daun Padi Berbasis Deep Learning (CNN & Transfer Learning)

Proyek ini bertujuan untuk membangun sistem *machine learning* yang mampu mendeteksi dan mengklasifikasikan tiga jenis penyakit utama pada daun padi melalui gambar. Proyek ini juga mendemonstrasikan bagaimana teknik *Transfer Learning* dapat digunakan untuk mengatasi masalah *overfitting* yang ekstrem pada *dataset* berukuran sangat kecil.

## 📌 Latar Belakang & Masalah
Penyakit pada tanaman padi dapat menurunkan hasil panen secara signifikan jika tidak dideteksi dan ditangani secara dini. Dengan memanfaatkan teknologi pengolahan citra digital (*Computer Vision*), proses identifikasi visual yang biasanya dilakukan secara manual oleh pakar dapat diotomatisasi.

Tantangan utama dalam eksperimen ini adalah **keterbatasan data**. Bagaimana cara membuat model cerdas yang mampu menggeneralisasi pola penyakit dengan baik, meskipun hanya dilatih menggunakan puluhan gambar saja?

## 📊 Informasi Dataset
Dataset yang digunakan berasal dari Kaggle dan terdiri dari **120 gambar** yang seimbang (*perfectly balanced*), terbagi ke dalam 3 kelas:
1. `Bacterial leaf blight` (40 gambar)
2. `Brown spot` (40 gambar)
3. `Leaf smut` (40 gambar)

*Dataset dibagi menjadi 80% data latih (96 gambar) dan 20% data validasi (24 gambar).*

## 🔬 Metodologi & Eksperimen Model

### Eksperimen 1: Custom CNN (Baseline)
Sebagai standar awal, sebuah arsitektur *Convolutional Neural Network* (CNN) dibangun dari awal. 
* **Hasil:** Model berhasil menghafal data latih, namun mengalami **Overfitting** yang sangat parah. Akurasi validasi terhenti pada kisaran **~41%** ketika dihadapkan pada gambar ujian yang belum pernah dilihat sebelumnya.

### Eksperimen 2: Transfer Learning (MobileNetV2)
Untuk mengatasi masalah keterbatasan data dan *overfitting*, pendekatan diubah menggunakan arsitektur **MobileNetV2** yang telah dilatih sebelumnya (pre-trained weights dari *ImageNet*).
* **Modifikasi:** Membekukan (*freeze*) bobot konvolusi dasar MobileNetV2, dan menambahkan lapisan klasifikasi khusus yang terdiri dari `GlobalAveragePooling2D`, `Dense` layer, dan `Dropout (20%)` sebagai langkah regularisasi.
* **Hasil:** Overfitting berhasil diatasi. Grafik pergerakan Akurasi dan Loss (*Loss Curve*) menunjukkan pola yang konvergen dan stabil secara bersamaan antara fase latih dan validasi.

## 📈 Kinerja & Evaluasi Akhir

Penerapan *Transfer Learning* sukses meroketkan performa model secara drastis:
* **Akurasi Validasi Keseluruhan:** **92%** (Lompatan jauh dari 41%)
* **F1-Score Makro:** **89%**
* **Highlight Metrik:**
  * Model mencapai nilai **Precision 100%** untuk deteksi *Bacterial leaf blight* dan *Leaf smut* (Model tidak pernah salah menuduh penyakit lain sebagai dua penyakit ini).
  * Model mencapai nilai **Recall 100%** untuk deteksi *Brown spot* (Tidak ada satu pun gambar *Brown spot* yang gagal terdeteksi oleh model).

*(Silakan lihat folder `images/` untuk detail visual Confusion Matrix dan Grafik Pergerakan Metrik).*

## 📂 Struktur Repositori

```text
├── images/
│   ├── accuracy_loss_plot.png     # Grafik pergerakan evaluasi saat training
│   └── confusion_matrix.png       # Detail matriks tebakan model
├── notebook/
│   └── Rice_Leaf_Classification.ipynb  # Kode sumber lengkap (Google Colab)
└── README.md
