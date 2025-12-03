# Project DAE
* C14220004 - Bryan Mogens Warren
* C14220011 - Christoper Bintang Augurius

# Laporan Project Data Analytics: Analisis Faktor Penentu Rating Sereal

## 1. Latar Belakang
Dalam proyek ini, saya melakukan analisis terhadap dataset `Cereals.csv` untuk memahami variabel nutrisi apa saja yang paling berpengaruh terhadap penilaian (rating) produk sereal. Proses analisis dilakukan secara *end-to-end*, mulai dari pembersihan data hingga pembuatan model prediksi menggunakan algoritma Decision Tree.

## 2. Proses dan Hasil Analisis

### A. Preprocessing Data
Sebelum masuk ke pemodelan, saya melakukan beberapa tahapan persiapan data:
* **Handling Missing Values:** Terdapat beberapa data kosong (null) pada kolom `carbo`, `sugars`, dan `potass`. Agar data tidak bias, saya mengisi kekosongan tersebut menggunakan nilai tengah (median).
* **Penentuan Target:** Fokus analisis ini adalah kolom `rating`. Saya membagi data menjadi dua kelas klasifikasi berdasarkan nilai median-nya (40.4). Jadi, sereal dengan rating di atas 40.4 dikategorikan sebagai **High Rating**, dan sisanya **Low Rating**.

### B. Eksplorasi Hubungan Variabel (Korelasi)
Dari matriks korelasi, ditemukan pola hubungan yang sangat menarik:
* **Pengaruh Gula (Sugars):** Terdapat korelasi negatif yang cukup ekstrem (-0.76) antara gula dan rating. Artinya, semakin banyak gula, rating sereal justru makin anjlok.
* **Pengaruh Serat (Fiber):** Sebaliknya, serat memiliki korelasi positif (0.58). Sereal yang kaya serat cenderung mendapatkan rating yang lebih tinggi.

### C. Evaluasi Model Machine Learning
Saya menggunakan model Decision Tree untuk memprediksi apakah sebuah sereal akan mendapatkan rating tinggi atau rendah.
* **Akurasi:** Model berhasil memprediksi data uji dengan akurasi sekitar 83%.
* **Fitur Terpenting:** Berdasarkan *feature importance*, variabel **Sugars** menjadi penentu utama (76%), jauh mengungguli variabel lain seperti Vitamins (8%) dan Potass (5%).

---

## 3. Insight Utama

Dari hasil pengolahan data di atas, ada beberapa poin penting yang bisa disimpulkan:

1.  **Rating = Indikator Kesehatan**
    Ternyata, rating sereal dalam dataset ini mencerminkan seberapa "sehat" produk tersebut. Konsumen atau sistem penilaian tampaknya memberikan hukuman skor rendah untuk produk yang hanya menang di rasa manis (tinggi gula) tetapi minim nutrisi.

2.  **Ambang Batas Gula (The 7.5g Rule)**
    Saat melihat struktur *Decision Tree*, terlihat adanya pola "aturan main" yang jelas:
    * Jika kandungan gula per sajian **di bawah atau sama dengan 7.5 gram**, peluang produk tersebut masuk kategori **High Rating** sangat besar.
    * Jika gula **di atas 7.5 gram**, produk tersebut hampir pasti jatuh ke kategori **Low Rating**, kecuali jika dibantu dengan kandungan serat yang sangat tinggi (> 4.5 gram).

3.  **Perbandingan Produsen**
    Dari segi *brand*, Nabisco (N) menjadi juara dengan rata-rata rating tertinggi (67.9) karena produk mereka konsisten rendah gula. Sementara itu, General Mills (G) memiliki rata-rata terendah (34.4) karena profil produknya yang cenderung tinggi gula dan kalori.

---

## 4. Kesimpulan dan Saran

Berdasarkan analisis ini, kesimpulan utamanya adalah menurunkan kadar gula adalah cara paling efektif untuk menaikkan rating. Jika saya harus memberikan rekomendasi strategi produk, saran saya adalah:

1.  **Reformulasi Resep:** Pastikan kadar gula per sajian ditekan hingga di bawah 7.5 gram agar bisa masuk ke segmen "High Rating".
2.  **Strategi Pemasaran:** Highlight kandungan serat pada kemasan, karena data membuktikan serat berbanding lurus dengan persepsi kualitas produk.
3.  **Hindari Kombinasi Fatal:** Jangan membuat produk yang rendah serat sekaligus tinggi gula, karena model memprediksi produk seperti ini pasti akan gagal mendapatkan rating yang baik.
