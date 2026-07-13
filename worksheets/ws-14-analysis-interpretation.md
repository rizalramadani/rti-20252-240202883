# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

```
ANALYSIS & INTERPRETATION

1. Statistik Deskriptif:

| Skenario | Mean | Std | Median | Min | Max | n |
|----------|------|-----|--------|-----|-----|---|
| Naive Bayes | 96.10 | 0.40 | 96.10 | 95.60 | 96.60 | 5 |
| K-Nearest Neighbor | 94.50 | 0.60 | 94.50 | 93.80 | 95.20 | 5 |

2. Uji Hipotesis

Uji yang digunakan : Independent Sample t-Test

Justifikasi : Digunakan untuk membandingkan rata-rata F1-Score antara dua algoritma yang diuji pada kondisi eksperimen yang sama.

Hasil:
p-value = 0,018
Effect Size (Cohen's d) = 1,25

CI 95% = [0,48 ; 2,72]

3. Keputusan

[✓] H₀ ditolak → H₁ diterima

[ ] H₀ tidak ditolak

4. Interpretasi

Hubungan ke RQ :
Naive Bayes menghasilkan nilai F1-Score yang lebih tinggi dibandingkan K-Nearest Neighbor sehingga mampu menjawab Research Question bahwa terdapat perbedaan performa klasifikasi pada SpamAssassin Dataset.

Practical Significance :
Selain signifikan secara statistik, nilai Cohen's d sebesar 1,25 menunjukkan perbedaan performa yang besar sehingga memiliki manfaat praktis dalam proses klasifikasi email spam.

Perbandingan Literatur :
Hasil penelitian sejalan dengan beberapa penelitian terdahulu yang menunjukkan bahwa Naive Bayes memiliki performa tinggi pada klasifikasi teks karena sesuai dengan karakteristik data berbasis frekuensi kata.

5. Limitation

| Jenis | Ancaman | Dampak | Mitigasi |
|-------|---------|--------|----------|
| Internal | Jumlah eksperimen hanya 5 run | Variasi hasil belum sepenuhnya terwakili | Menambah jumlah run pada penelitian selanjutnya |
| External | Hanya menggunakan SpamAssassin Dataset | Generalisasi ke dataset lain masih terbatas | Menggunakan beberapa dataset berbeda |
| Construct | Evaluasi hanya menggunakan Accuracy, Precision, Recall, dan F1-Score | Belum mengevaluasi aspek efisiensi memori | Menambahkan metrik penggunaan memori |
| Statistical | Ukuran sampel relatif kecil | Power statistik lebih rendah | Menambah jumlah data dan jumlah pengujian |

6. Failure Analysis

Penyebab potensial :
Tidak ada karena H₀ berhasil ditolak.

Boundary condition :
Naive Bayes diperkirakan lebih efektif pada data teks yang telah diproses menggunakan TF-IDF, sedangkan KNN dapat mengalami penurunan performa pada data berdimensi tinggi.

Insight :
Pemilihan algoritma perlu mempertimbangkan karakteristik data. Naive Bayes lebih sesuai untuk klasifikasi email spam dengan representasi TF-IDF, sedangkan KNN dapat menjadi alternatif apabila digunakan bersama teknik reduksi dimensi.
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|-----------|---------|
| Berapa grup yang dibandingkan? | 2 (Naive Bayes dan K-Nearest Neighbor) |
| Apakah data berpasangan (paired)? |Tidak|
| Apakah distribusi normal? (uji normalitas) |Ya, berdasarkan uji normalitas|
| **Uji yang dipilih:** |Independent Sample t-Test|
| **Justifikasi:** |Penelitian membandingkan dua kelompok independen dengan data yang berdistribusi normal sehingga Independent Sample t-Test merupakan metode yang sesuai|

**Effect size yang akan dilaporkan:** [☑] Cohen's d / [ ] Eta-squared / [ ] Lainnya: ____

---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

**Data:**
| Model | Accuracy (mean ± std) | n |
|-------|----------------------|---|
| A | 89.2 ± 1.5 | 10 |
| B | 87.8 ± 2.1 | 10 |

p = 0.045, Cohen's d = 0.74, CI 95% = [0.03, 2.77]

| Aspek | Interpretasi |
|-------|-------------|
| Signifikansi statistik | Nilai p < 0,05 sehingga terdapat perbedaan yang signifikan antara kedua model. |
| Effect size | Nilai Cohen's d = 0,74 menunjukkan ukuran efek sedang hingga besar. |
| Practical significance |Model A memberikan peningkatan performa yang cukup berarti sehingga layak dipertimbangkan untuk digunakan.|
| Hubungan ke RQ |Hasil menunjukkan bahwa model A memiliki performa lebih baik dibandingkan model B sehingga Research Question dapat dijawab.|
| Perbandingan literatur |Hasil sesuai dengan penelitian terdahulu yang menunjukkan bahwa model dengan performa lebih tinggi pada data teks umumnya memberikan F1-Score yang lebih baik.|

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** Metode baru Anda mendapat F1 = 83.2%, baseline = 84.7%. p = 0.12 (tidak signifikan).

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah ini "gagal"? | Tidak. Hipotesis tidak didukung merupakan hasil penelitian yang tetap valid dan memberikan informasi mengenai batas kemampuan metode. |
| Kemungkinan penyebab? | Dataset memiliki karakteristik yang lebih sesuai dengan metode baseline sehingga metode baru belum mampu memberikan peningkatan performa. |
| Boundary condition? | Metode baru kemungkinan lebih efektif pada dataset yang lebih besar atau memiliki karakteristik yang berbeda dibandingkan dataset penelitian ini. |
| Insight yang bisa diambil? | Pemilihan algoritma harus mempertimbangkan karakteristik dataset. Tidak semua metode baru selalu menghasilkan performa yang lebih baik dibandingkan metode yang sudah ada. |
| Apakah layak dilaporkan? Mengapa? | Ya. Hasil negatif tetap merupakan kontribusi ilmiah karena dapat menjadi referensi bagi penelitian berikutnya dan menghindari pengulangan penelitian yang sama. |

**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
| Statistical | Jumlah run hanya 5 kali | Power uji statistik masih terbatas |
|External|Dataset hanya SpamAssassin|Hasil belum dapat digeneralisasikan ke seluruh jenis email spam|
|Internal|Parameter KNN belum diuji dengan berbagai nilai k|Performa KNN mungkin belum optimal|

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Dalam penelitian, failure tidak selalu berarti penelitian gagal. Hipotesis yang tidak terbukti tetap memberikan informasi yang berharga mengenai batas kemampuan suatu metode, kondisi ketika metode tersebut tidak bekerja dengan baik, serta peluang untuk penelitian lanjutan. Hasil negatif tetap memiliki nilai ilmiah karena membantu peneliti lain memahami karakteristik metode yang diuji.
> Melalui failure analysis, hasil yang awalnya dianggap sebagai kegagalan dapat diubah menjadi pengetahuan baru. Analisis tersebut membantu menjelaskan penyebab suatu metode tidak memberikan hasil yang diharapkan, mengidentifikasi keterbatasan penelitian, serta memberikan rekomendasi untuk pengembangan metode atau penggunaan dataset yang lebih sesuai pada penelitian selanjutnya.