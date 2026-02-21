# MBA-Perbadingan-Pembelian-Produk-Toko-XYZ-Tahun-2016-dan-2017-Menggunakan-Algoritma

**Dataset:** https://www.kaggle.com/code/rahmi21/02-association-rule-mining-on-real-data/input

**by:** Rahmi21

## 🔬 Metodologi Penelitian

**🔷 1. Sumber dan Karakteristik Dataset**
- Dataset diperoleh dari Kaggle dengan judul “Association Rule Mining on Real Data”.
- Total data awal: 21.293 entri transaksi.
- Terdiri dari 4 kolom utama:
  - Date (tanggal transaksi)
  - Time (waktu transaksi)
  - Transaction (ID transaksi unik)
  - Item (nama produk)
- Data mencakup periode transaksi tahun 2016–2017.
- Setelah pembersihan data, tersisa 20.507 entri valid.

**🔷 2. Alur Kerja Penelitian**

**📌 a. Exploratory Data Analysis (EDA)**
- Identifikasi nilai tidak valid (Item = "NONE" sebanyak 786 data).
- Analisis distribusi frekuensi produk.
- Identifikasi produk terpopuler:
  - 2016 → Coffee, Bread, Tea
  - 2017 → Coffee, Bread, Tea (meningkat signifikan)
- Analisis ini menjadi dasar pembentukan aturan asosiasi.

**📌 b. Pre-processing**
- Tahapan krusial untuk memastikan kualitas data:
- Menghapus item dengan nilai "NONE"
- Memisahkan dataset berdasarkan tahun (2016 & 2017)
- Menghitung frekuensi tiap produk
- Mengelompokkan item berdasarkan Transaction ID
- Mengonversi item dalam satu transaksi menjadi bentuk list
- Hasil:
  - 2016 → 3.987 transaksi
  - 2017 → 5.478 transaksi

**📌 c. Encoding Data**
- Menggunakan TransactionEncoder (mlxtend)
- Menerapkan One-Hot Encoding (True/False)
- Mengubah transaksi menjadi matriks biner:
  - Baris → 1 transaksi
  - Kolom → 1 produk
  - Nilai → True (dibeli), False (tidak dibeli)
Tahap ini mempersiapkan data untuk algoritma Apriori.

**📌 d. Penerapan Algoritma Apriori**
- Diterapkan secara terpisah untuk 2016 dan 2017.
- Menghasilkan frequent itemsets beserta nilai support.
- Itemset disortir berdasarkan support tertinggi.

**📌 e. Association Rule Mining**
- Menggunakan fungsi association_rules dari mlxtend.
- Metrik evaluasi:
  - Support → Frekuensi kemunculan kombinasi item
  - Confidence → Kekuatan implikasi aturan
  - Lift → Kekuatan asosiasi relatif terhadap kejadian acak
  - Conviction → Tingkat kepercayaan aturan tidak dilanggar

**📌 f. Skenario Parameter Eksperimen**
- Dilakukan dua skenario untuk melihat pengaruh threshold:
- 🔹 Skenario 1 (Longgar)
  - min_support = 0.01
  - min_confidence = 0.2
  - Menghasilkan lebih banyak aturan, termasuk kombinasi kompleks (3-itemset)

- 🔹 Skenario 2 (Ketat)
  - min_support = 0.03
  - min_confidence = 0.4
  - Menghasilkan aturan lebih sedikit namun lebih kuat


**📊 Hasil Penelitian & Analisis**


**🔷 1. Gambaran Umum Pola Pembelian**
- Produk paling dominan pada 2016 dan 2017 adalah Coffee, diikuti oleh Bread dan Tea.
- Terjadi peningkatan frekuensi pembelian Coffee dari 2016 ke 2017.
- Pola pembelian menunjukkan kecenderungan kombinasi minuman + makanan ringan.
- Beberapa produk memiliki frekuensi sangat rendah (<10 kali), menunjukkan long-tail behavior.


**🔷 2. Hasil Skenario 1 (min_support = 0.01, min_confidence = 0.2)**

**📌 Karakteristik**
- Parameter longgar → menghasilkan lebih banyak aturan asosiasi.
- Berhasil menemukan 3-itemsets.
- Cocok untuk eksplorasi pola kompleks.

**📈 Tahun 2016**
- Itemset dengan support tertinggi:
  - (Coffee) → 47%
  - (Bread) → 32%
  - (Tea) → 14%
    
- Kombinasi populer:
  - (Coffee, Bread)
  - (Coffee, Pastry)
  - (Coffee, Tea)

- Kombinasi 3-itemset berhasil terbentuk pada skenario ini.

**📈 Tahun 2017**
- Coffee semakin dominan dibanding 2016.
- Kombinasi kuat:
  - (Coffee, Bread)
  - (Coffee, Pastry)
  - (Coffee, Tea)
- Jumlah aturan meningkat dibanding 2016 karena jumlah transaksi lebih banyak.

**🔎 Insight**
- Coffee menjadi pusat asosiasi (core product).
- Kombinasi snack + minuman konsisten muncul di dua tahun.
- Parameter rendah membuka peluang menemukan pola yang lebih kompleks.


**🔷 3. Hasil Skenario 2 (min_support = 0.03, min_confidence = 0.4)**

**📌 Karakteristik**
- Parameter lebih ketat → aturan lebih selektif.
- Tidak menghasilkan 3-itemset.
- Fokus pada aturan dengan kekuatan asosiasi tinggi

**📈 Tahun 2016 & 2017**
- Aturan yang muncul lebih sedikit namun lebih kuat.
- Kombinasi dengan confidence tinggi:
  - Jika membeli Pastry → kemungkinan membeli Coffee meningkat.
  - Jika membeli Cake → sering dikombinasikan dengan Coffee.
- Nilai lift > 1 menunjukkan asosiasi positif antar produk.

**🔎 Insight**
- Parameter ketat menyaring pola lemah.
- Cocok untuk strategi rekomendasi produk yang lebih akurat.
- Mengurangi noise dalam aturan asosiasi.


**🔷 4. Perbandingan 2016 vs 2017**
- Jumlah transaksi meningkat pada 2017 (5.478 vs 3.987).
- Pola pembelian relatif konsisten.
- Coffee tetap menjadi anchor product di kedua tahun.
- Terjadi peningkatan intensitas kombinasi Coffee dengan produk bakery.


**🔷 5. Temuan Strategis**
- Coffee dapat dijadikan produk utama dalam strategi bundling.
- Kombinasi Coffee + Pastry/Cake efektif untuk promosi.
- Parameter min_support dan min_confidence sangat memengaruhi jumlah dan kualitas aturan.
- Skenario 1 cocok untuk eksplorasi pola
- Skenario 2 cocok untuk implementasi strategi bisnis.

## 🏆 Kesimpulan Utama
- Algoritma Apriori berhasil mengidentifikasi pola pembelian konsumen secara konsisten pada dua periode waktu.
- Perubahan parameter threshold berdampak signifikan terhadap kompleksitas dan kekuatan aturan asosiasi.
- Market Basket Analysis efektif digunakan sebagai dasar strategi promosi, bundling, dan manajemen stok.
