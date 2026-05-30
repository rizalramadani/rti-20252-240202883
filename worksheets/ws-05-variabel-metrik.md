# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question: ____________________

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
|Jenis Algoritma (Naive Bayes, KNN)| IV   |Pendekatan klasifikasi email spam|Kategori algoritma yang digunakan|Nominal|-|Mengubah parameter model pada sistem eksperimen|Variabel utama yang dibandingkan dalam penelitian|
|Performa Klasifikasi| DV   |Kemampuan model mendeteksi email spam|Recall|Ratio|%|Recall = TP/(TP+FN)|Mengukur kemampuan menemukan seluruh spam|
|Dataset SpamAssassin| CV   |Sumber data eksperimen|Dataset tetap|Nominal|-|Menggunakan dataset yang sama pada seluruh eksperimen|Menjaga konsistensi pengujian|

Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [ ] Setiap langkah terdokumentasi
  [ ] Tidak ada "lompatan logis"
  [ ] Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Apakah metode Naive Bayes menghasilkan F1-Score lebih tinggi dibandingkan K-Nearest Neighbor pada klasifikasi email spam menggunakan SpamAssassin Dataset?

**RQ:** __________________________________________________

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
| Jenis Algoritma | IV | Pendekatan klasifikasi | Naive Bayes vs KNN | Nominal | — |
|Performa klasifikasi | DV |Kemampuan model mendeteksi spam |Accuracy, Precision, Recall, F1-Score |Ratio | %|
| Dataset email| CV |Sumber data eksperimen |SpamAssassin Dataset |Nominal |— |

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [✓ ] Tidak
> Jika ya, di mana? ____________________________________

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5 |F1-Score mewakili keseimbangan precision dan recall pada klasifikasi spam |
| Sensitive |4 |F1-Score cukup sensitif terhadap perubahan performa model terutama pada data tidak seimbang |
| Feasible |5 |Metrik dapat dihitung langsung menggunakan confusion matrix pada Python/Scikit-Lear |

**Apakah perlu secondary metric?** [✓ ] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? Secondary metric berupa execution time diperlukan untuk melihat efisiensi komputasi antara Naive Bayes dan KNN karena KNN biasanya lebih lambat pada dataset besar

**Contoh kasus ceiling effect untuk metrik ini:**
> Jika kedua model memperoleh accuracy di atas 99%, maka accuracy menjadi kurang sensitif untuk membedakan performa model sehingga diperlukan F1-Score atau recall sebagai metrik tambahan.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | Apakah semua data point terkumpul? |Kemungkinan ada email kosong atau corrupt |Membersihkan dataset dan menghapus data invalid |
| Consistency | Apakah ada kontradiksi internal? |Format email mungkin berbeda-beda |Standarisasi preprocessing teks |
| Validity | Apakah benar-benar mengukur yang dimaksud? |Dataset memang berisi label spam dan non-spam |Menggunakan dataset publik terpercaya |
| Representativeness | Apakah sampel mewakili populasi target? |Dataset dominan email bahasa Inggris |Menambahkan dataset multi-bahasa jika memungkinkan |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data dianggap p-hacking karena peneliti bisa memilih metrik yang paling menguntungkan hasil eksperimen sehingga kesimpulan menjadi bias dan tidak objektif. Hal ini dapat menyebabkan hasil penelitian terlihat signifikan padahal sebenarnya tidak konsisten.
> Berbeda dengan eksplorasi data yang sah, eksplorasi dilakukan untuk memahami karakteristik data dan biasanya dilaporkan sebagai exploratory analysis, bukan sebagai bukti utama untuk menerima atau menolak hipotesis.