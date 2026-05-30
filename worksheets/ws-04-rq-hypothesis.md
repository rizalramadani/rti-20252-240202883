# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Apakah metode Naive Bayes menghasilkan performa klasifikasi email spam yang lebih baik dibandingkan K-Nearest Neighbor berdasarkan nilai Accuracy, Precision, Recall, dan F1-Score pada SpamAssassin Dataset?

Research Question:
  Tipe         : [✓] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : Apakah metode Naive Bayes menghasilkan performa klasifikasi email spam yang lebih baik dibandingkan K-Nearest Neighbor berdasarkan nilai Accuracy, Precision, Recall, dan F1-Score pada SpamAssassin Dataset?
  Variabel IV  : Jenis algoritma klasifikasi (Naive Bayes dan K-Nearest Neighbor)
  Variabel DV  : Performa klasifikasi email spam
  Metrik       : Accuracy, Precision, Recall, dan F1-Score
  Dataset      : SpamAssassin Public Corpus
  Baseline     : K-Nearest Neighbor (KNN)

Quality Check RQ:
  [✓] Variabel spesifik
  [✓] Metrik jelas
  [✓] Baseline ada
  [✓] Konteks disebutkan
  [✓] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : Memberikan bukti empiris mengenai perbandingan performa Naive Bayes dan K-Nearest Neighbor dalam klasifikasi email spam menggunakan dataset yang sama dan kondisi eksperimen yang identik.
  Jenis kontribusi        : [ ] Improvement  [✓] Comparison  [ ] Novel approach
  Gap yang diisi          : Method Gap dan Performance Gap

Hypothesis Pair:
  H₀ : Tidak terdapat perbedaan performa yang signifikan antara Naive Bayes dan K-Nearest Neighbor berdasarkan nilai F1-Score pada SpamAssassin Dataset
  H₁ : Terdapat perbedaan performa yang signifikan antara Naive Bayes dan K-Nearest Neighbor berdasarkan nilai F1-Score pada SpamAssassin Dataset.
  Threshold              : α = 0,05
  Justifikasi threshold  : Nilai signifikansi 0,05 merupakan standar yang umum digunakan dalam penelitian machine learning dan data mining untuk menentukan apakah perbedaan performa yang diperoleh signifikan secara statistik.
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:**Sebagian besar penelitian klasifikasi email spam masih menggunakan dataset email bahasa Inggris dan belum banyak membandingkan performa Naive Bayes dan K-Nearest Neighbor pada dataset email modern dengan pola spam yang terus berubah.

**RQ versi pertama (tulis bebas):**
> Bagaimana perbandingan performa Naive Bayes dan K-Nearest Neighbor dalam klasifikasi email spam?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | ya |Naive Bayes vs K-Nearest Neighbor |
| Metrik terukur |ya |Accuracy, Precision, Recall, F1-Score |
| Baseline | ya|KNN sebagai pembanding NB |
| Dataset/konteks |ya |Dataset email spam modern (SpamAssassin / Enron Dataset) |

**Tipe RQ:** [✓ ] Comparison / [ ] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Apakah metode Naive Bayes menghasilkan F1-Score lebih tinggi dibandingkan K-Nearest Neighbor pada klasifikasi email spam menggunakan SpamAssassin Dataset?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | Tidak ada perbedaan signifikan F1-Score antara Naive Bayes dan K-Nearest Neighbor pada klasifikasi email spam menggunakan SpamAssassin Dataset |
| H₁ |Naive Bayes menghasilkan F1-Score yang lebih tinggi dibandingkan K-Nearest Neighbor pada klasifikasi email spam menggunakan SpamAssassin Dataset |
| Metrik |Accuracy, Precision, Recall, F1-Score |
| Threshold |α = 0.05 |
| Justifikasi threshold |Nilai signifikansi 0.05 umum digunakan dalam penelitian machine learning untuk menentukan apakah perbedaan performa signifikan secara statistik |

**Apakah hipotesis ini falsifiable?** [✓ ] Ya / [ ] Tidak
>  Dengan melakukan eksperimen pada dataset SpamAssassin dan menghitung F1-Score kedua metode. Jika hasil uji statistik menunjukkan tidak ada perbedaan signifikan atau KNN memiliki performa lebih baik, maka H₁ ditolak dan H₀ diterima.

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | Apakah Naive Bayes menghasilkan F1-Score lebih tinggi dibandingkan KNN pada klasifikasi email spam menggunakan SpamAssassin Dataset? |
| Variable (IV) | Jenis algoritma klasifikasi (Naive Bayes vs KNN) |
| Variable (DV) |Performa klasifikasi email spam |
| Metric |Accuracy, Precision, Recall, F1-Score |
| Data source |SpamAssassin Dataset dan Enron Email Dataset |
| Analysis method |Perbandingan hasil confusion matrix dan uji statistik performa model |

**Apakah rantai lengkap?** [✓ ] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? ______________

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Comparison of Navie Bayes and K-Nearest Neighbor for Email Spam Classification
**RQ yang diekstrak:** Apakah Naive Bayes memiliki performa lebih baik dibandingkan K-Nearest Neighbor dalam klasifikasi email spam?
**Komponen yang hilang:** Dataset spesifik tidak disebutkan pada judul
Metrik evaluasi belum disebutkan secara eksplisit
Belum ada konteks mengenai jenis email atau ukuran dataset yang digunakan
