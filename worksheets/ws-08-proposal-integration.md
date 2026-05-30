# WS-08: Proposal Integration (UTS)

> **Bab 8 — Proposal & Checkpoint**
> **Nama:** Rizal Ramadani | **Tanggal:** 18 Mei 2026

---

## Ringkasan Materi

### Proposal = Satu Argumen Utuh

Proposal riset bukan kumpulan bab yang independen. Ia adalah **satu argumen** yang mengalir dari masalah ke rencana solusi. Jika satu koneksi putus, seluruh proposal kehilangan koherensi.

### Integration Map — 6 Koneksi Kritis

```
Problem (Bab 2) → Gap (Bab 3) → RQ & H (Bab 4) → Metrik (Bab 5) → Sistem (Bab 6) → Eksperimen (Bab 7)
```

| Koneksi | Pertanyaan Verifikasi |
|---------|----------------------|
| Problem → Gap | Apakah gap muncul dari analisis literatur terhadap masalah? |
| Gap → RQ | Apakah RQ langsung menjawab gap yang teridentifikasi? |
| RQ → Metrik | Apakah setiap variabel di RQ punya metrik terdefinisi? |
| Metrik → Sistem | Apakah setiap metrik bisa diukur oleh komponen sistem? |
| Sistem → Eksperimen | Apakah desain eksperimen menggunakan sistem sebagai instrumen? |

### Koherensi Vertikal + Horizontal

- **Vertikal** — Alur logis atas-ke-bawah (problem → experiment). Setiap section menjawab pertanyaan yang diangkat section sebelumnya dan memunculkan pertanyaan baru.
- **Horizontal** — Konsistensi terminologi (nama variabel di RQ = di hipotesis = di metrik = di desain)

**Operasionalisasi Red Thread:**

```
Bab 2 (Problem) → | memperkenalkan masalah X + evidensi |
                          ↓ menimbulkan pertanyaan: "apa akar gap-nya?"
Bab 3 (Gap)     → | menjawab pertanyaan tadi + membuka "lalu apa yang perlu diteliti?" |
                          ↓
Bab 4 (RQ/H)    → | menjawab gap dengan pertanyaan spesifik + prediksi terukur |
                          ↓
Bab 5-7 (Method)→ | menjawab RQ melalui desain eksperimen yang tepat |
```

Jika ada lompatan (section B tidak menjawab pertanyaan section A), red thread putus.

### Jebakan Kognitif

| Jebakan | Deskripsi |
|---------|-----------|
| "Selling" Introduction | Menulis promosi, bukan menyajikan data dan gap |
| Copy-paste Methodology | Menyalin deskripsi textbook tanpa menyesuaikan ke RQ |
| Optimistic Timeline | Meremehkan waktu implementasi; selalu tambah buffer 30-50% |
| No Possibility of Failure | Mengimplikasikan hasil pasti sukses — proposal jujur mengakui H₀ mungkin tidak ditolak |

### Struktur Proposal

1. **Pendahuluan** — Latar belakang + problem statement (Bab 1-2)
2. **Tinjauan Pustaka** — Literature review + gap + baseline (Bab 3)
3. **RQ / Kontribusi / Hipotesis** — (Bab 4)
4. **Metodologi** — Metrik + sistem + desain eksperimen (Bab 5-7)
5. **Timeline & Output**

### Istilah Penting

- **Integration Map** — Diagram 6 koneksi kritis antar komponen proposal
- **Vertical Coherence** — Alur logis atas-ke-bawah
- **Horizontal Coherence** — Konsistensi terminologi di semua bagian
- **Checkpoint** — Titik self-assessment sebelum transisi dari desain ke eksekusi

---

## Template A.8 — Integration Checklist

```
PROPOSAL INTEGRATION CHECKLIST

Koneksi Vertikal (Flow Atas-Bawah):
  [✓] Problem → Gap: masalah terdokumentasi di literatur
  [✓] Gap → RQ: pertanyaan menjawab gap spesifik
  [✓] RQ → Hypothesis: hipotesis memprediksi jawaban
  [✓] Hypothesis → Metric: metrik mengukur variabel dalam hipotesis
  [✓] Metric → System: komponen sistem menghasilkan/mengukur metrik
  [✓] System → Experiment: desain eksperimen menggunakan sistem

Koneksi Horizontal (Konsistensi):
  [✓] Istilah sama di semua bagian
  [✓] Variabel di RQ = variabel di hipotesis = metrik di desain
  [✓] Scope tidak berubah dari masalah ke eksperimen

Cognitive Trap Checklist:
  [✓] Tidak ada paragraf "promosi" di pendahuluan (hanya data & gap)
  [✓] Metodologi disesuaikan ke RQ, bukan copy-paste textbook
  [✓] Timeline sudah ditambah buffer 30-50% dari estimasi awal
  [✓] Proposal mengakui kemungkinan H₀ tidak ditolak (honest uncertainty)
  [✓] Tidak ada klaim "pasti berhasil" atau "meningkatkan signifikan"

Rubrik Self-Assessment:
| Kriteria    | 1 (Lemah)                                      | 2 (Cukup)                                     | 3 (Baik)                                         | Skor |
|-------------|------------------------------------------------|-----------------------------------------------|--------------------------------------------------|------|
| Koherensi   | >2 koneksi vertikal terputus                   | 1-2 koneksi lemah, argumen masih bisa diikuti | Semua 6 koneksi terhubung, red thread jelas      |  3   |
| Specificity | Variabel/metrik masih abstrak, tidak ada angka | Sebagian metrik terdefinisi numerik           | Semua metrik + threshold + unit pengukuran jelas |  3   |
| Feasibility | Timeline >6 bulan tanpa memperhitungkan sumber | Timeline 3-6 bulan dengan asumsi tertentu     | Timeline 1-3 bulan realistis dengan rencana detail |  2  |
| Rigor       | Baseline tidak jelas atau straw man            | 1-2 baseline dengan justifikasi partial       | 2+ baseline SOTA + justifikasi pemilihan lengkap |  2   |
```

---

## Latihan 1 — Kompilasi Proposal Mini

Kumpulkan hasil dari WS-02 sampai WS-07 menjadi satu ringkasan proposal.

| Komponen | Sumber | Isi (1-2 kalimat) |
|----------|--------|-------------------|
| Problem Statement | WS-02 | Sistem filtering spam email belum optimal karena belum ada evaluasi komparatif yang konsisten antara Naive Bayes dan KNN pada dataset email modern. Gap antara performa algoritma pada kondisi dataset lama dan pola spam modern yang terus berkembang belum diteliti secara komprehensif. |
| Gap | WS-03 | Mayoritas penelitian masih menggunakan dataset lama (Enron, SpamBase) yang tidak merepresentasikan pola spam modern, dan belum ada evaluasi komparatif dengan metrik lengkap antara Naive Bayes dan KNN pada dataset email terkini. |
| RQ | WS-04 | Apakah metode Naive Bayes menghasilkan F1-Score lebih tinggi dibandingkan K-Nearest Neighbor pada klasifikasi email spam menggunakan SpamAssassin Dataset? |
| Hipotesis | WS-04 | H₁: Naive Bayes menghasilkan F1-Score lebih tinggi dibandingkan KNN (α = 0.05). H₀: Tidak ada perbedaan signifikan F1-Score antara kedua metode pada SpamAssassin Dataset. |
| Variabel & Metrik | WS-05 | IV = jenis algoritma (Naive Bayes vs KNN, nominal); DV = Accuracy, Precision, Recall, F1-Score (ratio, %); CV = SpamAssassin Dataset (dikunci). |
| Sistem | WS-06 | Sistem modular: modul dataset loader (CV dikunci), modul preprocessing TF-IDF, modul classifier yang dapat di-swap via config (IV), dan modul evaluasi otomatis yang menghasilkan confusion matrix dan semua metrik (DV). |
| Desain Eksperimen | WS-07 | Comparison study dua kondisi: Control (KNN) vs Treatment (Naive Bayes). Dataset, preprocessing, split 80:20, seed 42, dan metrik evaluasi identik untuk kedua kondisi. |

---

## Latihan 2 — Integration Checklist

Verifikasi 6 koneksi kritis. Isi dengan merujuk tabel di Latihan 1.

| Koneksi | Status | Bukti |
|---------|--------|-------|
| Problem → Gap | ✅ | Gap (dataset lama dan kurangnya evaluasi komparatif) muncul langsung dari analisis 5 paper di WS-03 yang menunjukkan limitasi dataset dan metrik berulang pada penelitian sebelumnya. |
| Gap → RQ | ✅ | RQ langsung menanyakan perbandingan NB vs KNN dengan F1-Score pada SpamAssassin Dataset — menjawab gap kurangnya evaluasi komparatif dengan metrik lengkap pada dataset modern. |
| RQ → Hypothesis | ✅ | H₁ memprediksi Naive Bayes menghasilkan F1-Score lebih tinggi dari KNN dengan threshold α = 0.05 — prediksi terukur dan falsifiable dari RQ. |
| Hypothesis → Metric | ✅ | Metrik F1-Score (+ Accuracy, Precision, Recall) terdefinisi numerik di WS-05, berskala ratio, dihitung dari confusion matrix, dan langsung terhubung ke variabel dalam H₁. |
| Metric → System | ✅ | Modul evaluasi otomatis di WS-06 menghasilkan confusion matrix dan semua metrik; modul classifier di-swap via satu baris config untuk mengukur DV pada kedua kondisi. |
| System → Experiment | ✅ | Desain di WS-07 menggunakan sistem sebagai instrumen: kondisi Control (KNN) dan Treatment (Naive Bayes) dijalankan pada sistem yang sama, modul loader mengunci CV, modul evaluasi mencatat output. |

**Koneksi mana yang paling lemah?** Problem → Gap

**Bagaimana cara memperkuatnya?**
> Gap statement perlu diperkuat dengan angka konkret dari literatur — misalnya menyebutkan berapa persen paper yang menggunakan dataset Enron/SpamBase (4 dari 5 paper yang dianalisis di WS-03) dan rentang tahun dataset tersebut (2000-an). Ini membuat gap terasa lebih urgen dan bukan sekadar klaim kualitatif.

**Konsistensi horizontal — apakah istilah dan scope konsisten?** [✓] Ya
> Terminologi "Naive Bayes", "K-Nearest Neighbor", "F1-Score", "SpamAssassin Dataset", dan "klasifikasi email spam" konsisten digunakan dari WS-02 hingga WS-07 tanpa perubahan nama atau scope.

---

## Latihan 3 — Rubrik Self-Assessment

Evaluasi proposal mini menggunakan rubrik.

| Kriteria | Skor (1-3) | Justifikasi |
|----------|-----------|-------------|
| Koherensi | 3 | Semua 6 koneksi vertikal terhubung. Red thread jelas: masalah dataset lama → gap evaluasi komparatif → RQ perbandingan F1-Score → hipotesis NB lebih baik → metrik terdefinisi → sistem modular → eksperimen comparison study yang fair. |
| Specificity | 3 | Semua metrik (Accuracy, Precision, Recall, F1-Score dalam %) terdefinisi numerik dengan skala ratio. Dataset dikunci (SpamAssassin), threshold statistik ditetapkan (α = 0.05), split data (80:20), seed (42). |
| Feasibility | 2 | Eksperimen dapat diselesaikan dalam 1-2 bulan dengan Python/Scikit-learn. Namun belum ada rincian timeline per tahap dan buffer 30-50% dari estimasi awal. |
| Rigor | 2 | Dua baseline (NB dan KNN) dipilih dengan justifikasi dari literatur WS-03. Namun belum mencantumkan SOTA terbaru (misalnya transformer-based spam detection) untuk memperkuat positioning riset. |

**Skor total:** 10 / 12

**Apakah proposal siap untuk fase eksekusi?** [✓] Ya / [ ] Belum
> Proposal memenuhi syarat minimum untuk masuk fase eksekusi — semua 6 koneksi terhubung dan metrik terdefinisi numerik. Dua hal yang perlu diperkuat sebelum submit final: (1) tambahkan angka konkret pada gap statement, dan (2) lengkapi timeline dengan buffer 30-50% beserta milestone per tahap.

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-08, bagian mana yang paling mudah dan paling sulit? Mengapa? Apa yang akan dilakukan berbeda jika mengulang dari awal?

**Bagian termudah:** WS-05 (Variabel & Metrik)
> Topik perbandingan algoritma secara alami memiliki struktur IV-DV yang jelas: algoritma sebagai IV dan metrik klasifikasi sebagai DV. Metrik seperti F1-Score, Accuracy, Precision, dan Recall sudah familiar dari praktik machine learning sehingga tinggal mendokumentasikan dan menjustifikasi pilihan tersebut.

**Bagian tersulit:** WS-03 (Literature Mapping & Gap)
> Mengidentifikasi gap yang valid — bukan sekadar "belum ada yang meneliti" — membutuhkan pemahaman mendalam terhadap pola yang muncul dari beberapa paper sekaligus. Sulit menentukan apakah gap yang ditemukan cukup signifikan. Mencari paper relevan dengan query Boolean yang tepat juga memerlukan beberapa iterasi.

**Yang akan dilakukan berbeda:**
> Jika mengulang dari awal, saya akan memulai dengan literature review yang lebih sistematis sebelum menentukan topik final — bukan sebaliknya. Dengan memahami gap terlebih dahulu, formulasi RQ dan hipotesis akan lebih tajam dan tidak perlu direvisi berulang kali. Selain itu, setiap keputusan desain (pemilihan dataset, metrik, threshold) akan didokumentasikan sejak awal beserta justifikasinya agar integrasi proposal di WS-08 menjadi lebih mulus.
