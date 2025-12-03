# Project DAE
* C14220004 - Bryan Mogens Warren
* C14220011 - Christoper Bintang Augurius

# Laporan Analisis Data Sereal (Project DAE)

## 1. Pendahuluan
Laporan ini merangkum hasil analisis terhadap dataset `Cereals.csv` menggunakan pendekatan End-to-End Data Analytics (sesuai logika workflow KNIME). Tujuan utama analisis ini adalah memahami faktor-faktor nutrisi yang mempengaruhi Rating (penilaian konsumen/kualitas) pada produk sereal.

## 2. Deskripsi Hasil Utama Analisa

### A. Persiapan & Statistik Data
* **Penanganan Data Hilang:** Ditemukan nilai kosong pada kolom `carbo`, `sugars`, dan `potass`. Nilai-nilai ini telah diimputasi menggunakan nilai median agar distribusi data tetap terjaga.
* **Segmentasi Target:** Variabel target adalah `rating`.
    * **Median Rating:** 40.4
    * Data dibagi menjadi dua kelas klasifikasi:
        * **High Rating:** Rating > 40.4
        * **Low Rating:** Rating ≤ 40.4

### B. Analisis Korelasi (Hubungan Antar Variabel)
Analisis korelasi menunjukkan faktor mana yang paling kuat mempengaruhi rating:
* **Korelasi Negatif Kuat (`sugars` vs `rating`):** Nilai korelasi sebesar -0.76. Ini menunjukkan bahwa semakin tinggi kandungan gula, rating sereal cenderung turun drastis.
* **Korelasi Positif (`fiber` vs `rating`):** Nilai korelasi sebesar 0.58. Sereal dengan kandungan serat tinggi memiliki kecenderungan mendapatkan rating yang lebih baik.

### C. Performa Model (Decision Tree)
Model Decision Tree digunakan untuk memprediksi kategori rating berdasarkan komposisi nutrisi.
* **Akurasi Model:** Mencapai ~83% pada data pengujian.
* **Fitur Paling Berpengaruh (Feature Importance):**
    1.  **Sugars (Gula):** Tingkat kepentingan 76% (Sangat Dominan).
    2.  **Vitamins:** Tingkat kepentingan 8%.
    3.  **Potass (Kalium) & Sodium:** Tingkat kepentingan ~5%.

---

## 3. Insight Bisnis & Produk

Berikut adalah wawasan mendalam yang diperoleh dari pola data dan model prediksi:

### Insight 1: Kesehatan adalah Faktor Utama Penilaian
Rating sereal dalam dataset ini sangat mencerminkan profil kesehatan produk, bukan semata-mata rasa. Produk yang dikategorikan "enak tapi manis" (tinggi gula/kalori) justru mendapatkan skor rendah. Konsumen atau sistem rating ini memprioritaskan nilai gizi (serat tinggi, rendah gula).

### Insight 2: Aturan "7.5 Gram Gula"
Berdasarkan struktur Decision Tree, ditemukan ambang batas (threshold) kritis untuk memprediksi kualitas sereal:
> **Rule of Thumb:** Jika kandungan gula (sugars) dalam satu sajian adalah 7.5 gram atau kurang, peluang sereal tersebut masuk kategori High Rating sangat besar.

Sebaliknya, jika gula di atas 7.5 gram, sereal tersebut hampir pasti masuk kategori Low Rating, kecuali jika memiliki kandungan serat (fiber) yang sangat tinggi (> 4.5 gram).

### Insight 3: Benchmarking Produsen (Manufacturer)
Terdapat perbedaan signifikan rata-rata rating antar produsen:
* **Top Performer (Nabisco - 'N'):** Rata-rata rating 67.9. Unggul karena portofolio produk yang sangat rendah gula dan kalori.
* **Low Performer (General Mills - 'G'):** Rata-rata rating 34.4. Tertinggal karena produk cenderung memiliki profil gula dan kalori yang lebih tinggi.

---

## 4. Rekomendasi Strategis

1.  **Reformulasi Produk:** Untuk meningkatkan rating produk ke kategori "High", prioritas utama adalah menurunkan kadar gula hingga di bawah 7.5g per sajian.
2.  **Marketing:** Tonjolkan kandungan Serat (Fiber) dalam pemasaran, karena data menunjukkan korelasi positif yang konsisten antara serat dan persepsi kualitas (rating).
3.  **Pengembangan Produk Baru:** Hindari kombinasi "Rendah Serat + Tinggi Gula" karena model memprediksi kombinasi ini memiliki probabilitas 100% untuk mendapatkan rating rendah.
