# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (DSR). Penting untuk membedakan keduanya:

| Paradigma | Cara Kerja | Contoh di TI |
|-----------|-----------|---------------|
| **Positivis** | Uji hipotesis dengan eksperimen terkontrol | Apakah CNN lebih akurat dari RF pada dataset X? |
| **Design Science Research** | Bangun artefak (sistem/model/framework) untuk menguji proposisi | Dapatkah arsitektur hybrid CNN+LSTM membuktikan peningkatan recall ≥5%? |
| **Interpretivis** | Pahami makna melalui konteks & kualitatif | Bagaimana peneliti manafsirkan anomali data sensor IoT? |

Dalam DSR, artefak **bukan tujuan akhir** — ia adalah instrumen untuk menghasilkan pengetahuan. Pertanyaan riset tetap harus difalsifikasi.

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Rizal Ramadani
Tanggal          : 16 Mei 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya:
     Apakah dataset dan metode pengujiannya adil serta valid?

   - Data yang dibutuhkan untuk verifikasi:
     Dataset penelitian, jumlah data, metode evaluasi, confusion matrix,
     precision, recall, dan perbandingan baseline.

2. Posisi paradigma:
   - Pendekatan: [✓] Positivis  [ ] Interpretivis  [ ] Design Science  [ ] Mixed

   - Alasan:
     Penelitian menggunakan eksperimen terkontrol dan data numerik
     untuk membandingkan performa algoritma Naive Bayes dan KNN.

3. Identifikasi distorsi:
   - Asumsi tersembunyi:
     Dataset email dianggap mewakili seluruh jenis spam email.

   - Sumber bias potensial:
     Dataset mungkin hanya berisi email bahasa Inggris dan data lama.

   - Langkah mitigasi:
     Menggunakan dataset yang lebih beragam dan melakukan cross-validation.

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi:
     Hasil akurasi, precision, recall, dan data eksperimen.

   - Batasan yang diakui sejak awal:
     Hasil penelitian mungkin tidak berlaku untuk seluruh jenis spam modern.
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

> **Panduan pencarian paper:** Gunakan [IEEE Xplore](https://ieeexplore.ieee.org), [ACM Digital Library](https://dl.acm.org), atau Google Scholar. Pilih paper **tahun 2020 ke atas**, di topik yang Anda minati: deteksi anomali, klasifikasi citra, NLP, keamanan siber, IoT, dsb.
>
> **Contoh domain TI:** "Deteksi anomali lalu-lintas jaringan menggunakan CNN — akurasi meningkat 94% vs baseline SVM 87%." Distorsi potensial: apakah dataset normal/anomali seimbang? Apakah hanya diuji pada satu vendor traffic?

**Paper yang dipilih:**
> Judul: Comparison of Naive Bayes and K-Nearest Neighbor for Email Spam Classification
> Penulis (Tahun): Sharma et al. (2021)
> Sumber/Link DOI: IEEE Xplore / Google Scholar

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Mengumpulkan dataset email spam dan non-spam | Dataset hanya berasal dari email bahasa Inggris |
| Data → Processing |Membersihkan teks, menghapus simbol dan stopword |Penghapusan kata dapat menghilangkan makna penting |
| Processing → Analysis |Melatih model Naive Bayes dan KNN |Parameter KNN mungkin tidak dioptimalkan secara adil |
| Analysis → Inference |Membandingkan akurasi kedua algoritma |Akurasi tinggi belum tentu menunjukkan performa nyata |
| Inference → Knowledge |Menyimpulkan Naive Bayes lebih baik untuk spam detection |Klaim terlalu umum untuk semua jenis emai |

**Distorsi paling besar di tahap:** Processing → Analysis

**Dua distorsi spesifik yang teridentifikasi:**
1. Dataset tidak mewakili seluruh variasi spam email modern
2. Parameter KNN dan Naive Bayes mungkin tidak dibandingkan secara seimbang

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Peneliti harus melaporkan hasil dengan dan tanpa outlier |
| Transparansi |Alasan penghapusan outlier harus dijelaskan secara jelas |
| Peer review |Reviewer kemungkinan meminta bukti bahwa outlier memang data abnormal dan bukan manipulasi hasil |

**Keputusan akhir dan justifikasi:**
> Peneliti sebaiknya melaporkan kedua hasil eksperimen. Jika outlier dihapus, harus ada alasan metodologis yang valid seperti kesalahan input data atau kerusakan sensor, bukan untuk membuat hasil menjadi signifikan.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Perbandingan Naive Bayes dan KNN untuk Klasifikasi Spam Email

> **Skala 1–5:** 1 = tidak sesuai sama sekali dengan topik ini, 5 = sangat sesuai dan dominan digunakan pada riset bertopik serupa.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | menggunakan eksperimen kuantitatif dan pengukuran akurasi | tidak fokus pada makna sosial atau pengalaman pengguna | membangun model klasifikasi sederhana |
| Jenis data yang dikumpulkan | Dataset email, akurasi, precision, recall | Wawancara atau observasi pengguna email | Hasil performa model klasifikasi |
| Limitasi paradigma |Sulit memahami perilaku manusia di balik spam |Sulit menghasilkan pengukuran objektif |Fokus artefak bisa mengurangi analisis teoritis |

**Paradigma yang dipilih:** Positivis
**Alasan:** Penelitian berfokus pada pengujian hipotesis menggunakan data numerik dan eksperimen terkontrol untuk membandingkan performa dua algoritma klasifikasi.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum membaca materi ini, saya cenderung langsung percaya pada klaim akurasi tinggi tanpa mempertanyakan proses penelitian di baliknya. Setelah memahami rantai distorsi, saya mulai mempertanyakan sumber dataset, fairness eksperimen, validitas metrik, dan apakah hasil penelitian benar-benar dapat digeneralisasi ke kondisi nyata.
> 
