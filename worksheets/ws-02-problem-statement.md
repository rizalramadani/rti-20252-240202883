# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Machine Learning / Text Classification
  Konteks  : Deteksi spam email pada sistem email digital

System Context
  Input       : Email teks (subject + body)
  Process     : Preprocessing teks + ekstraksi fitur + klasifikasi
  Output      : Label email (spam / not spam)
  Outcome     : Sistem dapat memfilter email spam secara otomatis
  Constraints : Dataset terbatas, bahasa dominan Inggris, data tidak selalu seimbang
  Stakeholders: Pengguna email, perusahaan email provider, peneliti ML

Fenomena → Problem
  Fenomena yang diamati             : Banyak email spam masuk ke inbox pengguna
  Gejala (symptom) yang terukur     : Tingginya jumlah email tidak relevan yang tidak terfilter
  Masalah yang didiagnosis          : Sistem filtering email belum optimal dalam klasifikasi spam
  Masalah riset (researchable)      : Belum ada evaluasi komparatif yang konsisten antara Naive Bayes dan KNN pada dataset spam email modern
  Variabel yang terukur             : Akurasi, precision, recall, F1-score dari Naive Bayes dan KNN

Problem Quality Check
  [✓] Clarity — jelas membandingkan dua algoritma
  [✓] Measurability — ada metrik (accuracy, precision, recall)
  [✓] Relevance — penting untuk email security
  [✓] Testability — bisa diuji dan bisa gagal
  [✓] Impact — hasil dapat meningkatkan sistem filtering email

Problem Statement (1 paragraf):
  Penelitian ini membahas perbandingan kinerja algoritma Naive Bayes dan K-Nearest Neighbor dalam klasifikasi email spam menggunakan dataset teks email. Masalah yang diangkat adalah masih belum adanya evaluasi yang konsisten dan komprehensif terhadap kedua algoritma pada dataset email modern, sehingga diperlukan analisis untuk mengetahui metode yang lebih efektif berdasarkan metrik akurasi, precision, recall, dan F1-score.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Perbandingan Naive Bayes vs KNN untuk Klasifikasi Spam Email

| Tahap | Hasil |
|-------|-------|
| Tingkat spam yang tidak terfilter masih tinggi pada beberapa layanan email |
| Observed Issue (Symptom) | Tingkat spam yang tidak terfilter masih tinggi pada beberapa layanan email
 |
| Diagnosed Problem (Root Cause) |Algoritma filtering email belum optimal atau tidak konsisten dalam menangani berbagai pola spam baru |
| Researchable Problem |Belum ada analisis komparatif yang jelas antara Naive Bayes dan KNN dalam klasifikasi spam email pada dataset yang sama dengan evaluasi metrik lengkap |
| Measurable Variable |Akurasi, precision, recall, dan F1-score dari kedua algoritma |

**Apakah terjebak solution-first thinking?** [ ] Ya / [✓ ] Tidak
> Jika ya, kembali ke tahap mana? ________________________

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Dataset email (teks spam dan non-spam) |
| Process |Text preprocessing → feature extraction (TF-IDF) → training model Naive Bayes & KNN → evaluasi |
| Output |Prediksi spam / non-spam |
| Outcome |Sistem klasifikasi email yang lebih akurat dan efisien |
| Constraints |Dataset terbatas, imbalance data, variasi bahasa spam terus berubah |
| Stakeholders |Pengguna email, perusahaan email (Gmail/Yahoo/Outlook), peneliti |

**Komponen mana yang paling relevan dengan masalah riset?** Process (karena perbedaan algoritma dan preprocessing mempengaruhi hasil klasifikasi)

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | Sudah jelas membandingkan dua algoritma untuk spam detection |4 |
| Measurability |Menggunakan metrik kuantitatif: accuracy, precision, recall, F1-score |5 |
| Relevance |Spam detection sangat relevan dalam keamanan email |5 |
| Testability |Hipotesis dapat diuji dan bisa menghasilkan hasil berbeda |5 |
| Impact |Berguna untuk meningkatkan sistem filtering email, meskipun sudah banyak penelitian sebelumnya |4 |

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> Penelitian ini membahas perbandingan kinerja algoritma Naive Bayes dan K-Nearest Neighbor dalam klasifikasi email spam menggunakan dataset teks email. Fokus penelitian ini adalah mengevaluasi efektivitas kedua algoritma berdasarkan metrik evaluasi seperti akurasi, precision, recall, dan F1-score. Hasil penelitian diharapkan dapat memberikan gambaran metode yang paling optimal untuk sistem deteksi spam email.
> ___________________________________________________

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah coding (bug, error) bersifat teknis dan langsung memiliki solusi yang jelas, sedangkan masalah riset berfokus pada gap pengetahuan yang harus dibuktikan melalui eksperimen. Dalam riset, masalah harus diformulasikan secara terukur, memiliki variabel jelas, dan dapat diuji secara empiris, bukan sekadar diperbaiki seperti bug dalam sistem.
> 
