# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : ____________________
Hypothesis        : ____________________
Tipe Eksperimen   : [ ] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control |           |          |             |
| Treatment |         |          |             |

Fairness Checklist:
  [ ] Dataset identik untuk semua kondisi
  [ ] Preprocessing setara
  [ ] Tuning effort setara
  [ ] Environment identik
  [ ] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    |                 |          |
| External    |                 |          |
| Construct   |                 |          |
| Conclusion  |                 |          |

Statistical Plan:
  Uji statistik   : ____________________
  Justifikasi      : ____________________
  Alpha            : ____________________
  Effect size min  : ____________________
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Apakah metode Naive Bayes menghasilkan F1-Score lebih tinggi dibandingkan K-Nearest Neighbor pada klasifikasi email spam menggunakan SpamAssassin Dataset?
**Tipe eksperimen:** [ ] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Baseline metode klasifikasi menggunakan KNN | K-Nearest Neighbor | SpamAssassin Dataset, split 80:20, preprocessing sama, seed 42 |
| Treatment |Metode klasifikasi menggunakan Naive Bayes |Naive Bayes |SpamAssassin Dataset, split 80:20, preprocessing sama, seed 42 |

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | ✅ |Kedua metode menggunakan SpamAssassin Dataset yang sam |
| Preprocessing setara |✅ |Cleaning, tokenizing, stopword removal, dan TF-IDF sama |
| Tuning effort setara |✅ |Kedua model menggunakan parameter tuning sederhana dengan effort yang sebanding |
| Environment identik |✅ |Eksperimen dijalankan pada perangkat dan environment Python yang sama |
| Metrik evaluasi sama |✅ |Accuracy, Precision, Recall, dan F1-Score digunakan pada kedua metod |

**Ada yang tidak fair?** [ ] Ya / [✓ ] Tidak
> Jika ya, bagaimana cara memperbaikinya?Semua kondisi eksperimen telah dibuat identik sehingga perbandingan lebih valid dan objektif.

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Data leakage antara data training dan testing | Menggunakan stratified train-test split dan memastikan tidak ada overlap |
| External |Dataset hanya email bahasa Inggris |Menambahkan dataset multi-bahasa pada penelitian lanjuta |
| Construct |F1-Score belum sepenuhnya menggambarkan efisiensi sistem |Menambahkan execution time sebagai secondary metric |
| Conclusion |Jumlah sampel terbatas sehingga hasil kurang stabil |Menggunakan cross-validation dan beberapa pengulangan eksperimen |

**Ancaman mana yang paling sulit dimitigasi?** External Validity
**Mengapa?**
> Karena dataset yang tersedia mayoritas menggunakan email bahasa Inggris sehingga sulit memastikan hasil penelitian dapat digeneralisasi ke email multi-bahasa atau konteks lokal Indonesia tanpa pengumpulan data tambahan.

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah semua baseline dibandingkan menggunakan dataset, preprocessing, dan environment yang identik?
2. Apakah baseline yang dipilih merupakan metode relevan dan representatif dari literatur terbaru?
3. Apakah peningkatan performa yang dilaporkan signifikan secara statistik dan bukan hanya kebetulan eksperimen?
