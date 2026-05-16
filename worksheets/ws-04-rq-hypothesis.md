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

Gap Statement  : ____________________

Research Question:
  Tipe         : [ ] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : ____________________
  Variabel IV  : ____________________
  Variabel DV  : ____________________
  Metrik       : ____________________
  Dataset      : ____________________
  Baseline     : ____________________

Quality Check RQ:
  [ ] Variabel spesifik
  [ ] Metrik jelas
  [ ] Baseline ada
  [ ] Konteks disebutkan
  [ ] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : ____________________
  Jenis kontribusi        : [ ] Improvement  [ ] Comparison  [ ] Novel approach
  Gap yang diisi          : ____________________

Hypothesis Pair:
  H₀ : ____________________
  H₁ : ____________________
  Threshold              : ____________________
  Justifikasi threshold  : ____________________
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
