# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset           : SpamAssassin Public Corpus
Jumlah data awal  : 5.500 email

Cleaning:

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing | 0 | Tidak ada tindakan | Dataset tidak memiliki nilai kosong |
| Duplikat | 15 | Menghapus data duplikat | Menghindari data yang sama dihitung lebih dari satu kali |
| Error format | 8 | Standarisasi format teks (UTF-8) | Menyamakan format data agar dapat diproses dengan benar |

Transformation:

| Transformasi | Variabel | Detail | Alasan |
|-------------|----------|--------|--------|
| Case Folding | Text Email | Seluruh huruf menjadi huruf kecil | Menyeragamkan penulisan kata |
| Tokenization | Text Email | Memisahkan kalimat menjadi token | Mempermudah ekstraksi fitur |
| Stopword Removal | Text Email | Menghapus kata yang tidak memiliki makna penting | Mengurangi noise |
| TF-IDF Vectorization | Text Email | Mengubah teks menjadi bobot numerik | Sebagai fitur masukan algoritma klasifikasi |

Normalization:

Metode    : Tidak dilakukan
Alasan    : Data direpresentasikan menggunakan TF-IDF sehingga tidak memerlukan normalisasi tambahan.
Parameter : Tidak digunakan

Leakage Check:

[✓] Parameter preprocessing dilakukan setelah train-test split
[✓] Tidak ada informasi test set digunakan saat preprocessing
[✓] Cross-validation dilakukan setelah pembagian data

Jumlah data akhir : 5.485 email
Script tersedia   : [✓] Ya → path: preprocessing.py
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing value | 0 | Tidak ada | Dataset lengkap tanpa nilai kosong |
|Data duplikat|15|Menghapus data duplikat|Mencegah bias akibat data yang sama|
|Error format|8|Mengubah encoding menjadi UTF-8 dan membersihkan karakter khusus|Menyeragamkan format teks sebelum diproses|
|Karakter tidak diperlukan|35|Menghapus tanda baca dan simbol yang tidak relevan|Mengurangi noise pada proses klasifikasi|

**Jumlah data sebelum cleaning:** 5.500
**Jumlah data setelah cleaning:** 5.485
**Persentase data yang hilang/berubah:** 0,27%

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|-----------|-----------|----------|-------------------|--------|
| TF-IDF Feature | 0 – 1 | Sparse | Tidak | Tidak perlu | Nilai TF-IDF sudah berada pada rentang yang sesuai || Accuracy | 0 – 1 | Normal | Tidak | Tidak perlu | Digunakan sebagai metrik evaluasi, bukan fitur masukan ||F1-Score|0 – 1|Normal|Tidak|Tidak perlu|Sudah berada dalam rentang yang valid|

**Apakah normalisasi diperlukan?** [ ] Ya / [☑] Tidak
**Justifikasi:**
> Dataset menggunakan representasi fitur TF-IDF yang secara otomatis menghasilkan bobot pada rentang yang sesuai untuk proses klasifikasi. Selain itu, algoritma Naive Bayes dan K-Nearest Neighbor pada penelitian ini dapat memanfaatkan representasi TF-IDF tanpa memerlukan proses normalisasi tambahan. Oleh karena itu, normalisasi tidak dilakukan agar tidak mengubah distribusi data secara tidak perlu.
**Leakage check:**
- [☑] Parameter dihitung dari training set saja
- [☑] Normalisasi diterapkan setelah train-test split

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset:
   SpamAssassin Public Corpus

2. Data awal:
   5.500 records, 2 features (text, label)

3. Cleaning:
   - Missing values : 0 kasus, tidak ada penanganan
   - Duplikat       : 15 kasus, dihapus
   - Error format   : 8 kasus, dilakukan standarisasi encoding UTF-8

4. Transformation:
   - Case Folding
   - Tokenization
   - Stopword Removal
   - TF-IDF Vectorization

5. Normalisasi:
   Tidak dilakukan karena fitur TF-IDF sudah sesuai untuk proses klasifikasi.
   Parameter dihitung dari training set.

6. Data akhir:
   5.485 records, 2 features

7. Leakage Check:
   [✓] Lulus
```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

> Pada awal mempelajari machine learning, normalisasi sering dilakukan karena dianggap sebagai langkah standar tanpa mempertimbangkan karakteristik data maupun algoritma yang digunakan. Setelah memahami proses preprocessing, normalisasi sebaiknya hanya dilakukan apabila memang diperlukan oleh metode yang digunakan.
> Over-preprocessing dapat mengubah karakteristik asli data sehingga informasi penting menjadi hilang. Selain itu, preprocessing yang berlebihan dapat menyebabkan data menjadi kurang representatif terhadap kondisi sebenarnya dan berpotensi menghasilkan kesimpulan penelitian yang kurang akurat. Oleh karena itu, setiap langkah preprocessing harus memiliki alasan yang jelas, terdokumentasi, dan dapat direproduksi oleh peneliti lain.
