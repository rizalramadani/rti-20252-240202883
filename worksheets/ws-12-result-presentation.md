# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : Apakah metode Naive Bayes menghasilkan performa klasifikasi email spam yang lebih baik dibandingkan K-Nearest Neighbor berdasarkan nilai Accuracy, Precision, Recall, dan F1-Score pada SpamAssassin Dataset?

Metrik Utama      : F1-Score

Tabel Hasil:

| Skenario | Accuracy (mean ± std) | F1-Score (mean ± std) | n |
|----------|----------------------|-----------------------|---|
| Naive Bayes | 96.4 ± 0.3% | 96.1 ± 0.4% | 5 |
| K-Nearest Neighbor | 94.9 ± 0.5% | 94.5 ± 0.6% | 5 |

Visualisasi yang Direncanakan:

| # | Jenis Grafik | Pesan Utama | Metrik |
|---|-------------|-------------|--------|
| 1 | Bar Chart + Error Bar | Membandingkan performa Naive Bayes dan KNN | Accuracy dan F1-Score |
| 2 | Box Plot | Menunjukkan distribusi hasil tiap algoritma | F1-Score |
| 3 | Scatter Plot | Membandingkan Accuracy dengan waktu komputasi | Accuracy dan Execution Time |

Bias Check:

[✓] Y-axis mulai dari 0
[✓] Error bar ditampilkan
[✓] Semua data disertakan (tidak cherry-picked)
[✓] Tidak menggunakan grafik 3D
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
| Naive Bayes | 96.4 ± 0.3% | 96.1 ± 0.4% | 5 |
|K-Nearest Neighbor|94.9 ± 0.5%|94.5 ± 0.6%|5|

**Checklist tabel:**
- [☑] Self-contained (judul jelas, satuan ada, N tercantum)
- [☑] Mean ± std (bukan single number)
- [☑] Diurutkan berdasarkan metrik utama
- [☑] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | Bar Chart + Error Ba | Membandingkan nilai Accuracy dan F1-Score antara Naive Bayes dan KNN | Mean Accuracy dan Mean F1-Score ± Standar Devias |
| 2 | Box Plot | Menampilkan distribusi F1-Score dari lima kali percobaan setiap algoritma | Seluruh nilai F1-Score dari setiap run |
| 3 | Scatter Plot | Menunjukkan hubungan antara Accuracy dan waktu komputasi masing-masing algoritma | Mean Accuracy dan Mean Execution Time |

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan? | Ya. Perbedaan 0,4% terlihat jauh lebih besar daripada kondisi sebenarnya karena sumbu Y tidak dimulai dari nol. |
| Apakah error bar ditampilkan? |Tidak. Grafik sebaiknya menampilkan error bar agar variasi hasil antar-run dapat diketahui.|
| Apakah semua kondisi ditampilkan? |Ya. Kedua metode ditampilkan sehingga tidak terjadi cherry-picking.|
| Apa solusinya? |Gunakan sumbu Y yang dimulai dari 0 atau berikan alasan jika menggunakan rentang tertentu, serta tambahkan error bar pada setiap batang grafik.|

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [☑] Semua bias check lulus
- [-] Ada yang perlu diperbaiki: ____

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Tabel dan grafik memiliki fungsi yang saling melengkapi dalam penyajian hasil penelitian. Tabel digunakan untuk menampilkan nilai secara rinci dan presisi sehingga pembaca dapat mengetahui hasil setiap metrik dengan tepat. Sebaliknya, grafik memudahkan pembaca melihat pola, tren, serta perbedaan antaralgoritma secara visual. Oleh karena itu, penggunaan keduanya akan membuat hasil penelitian lebih mudah dipahami dan dianalisis.
> Dalam penyusunan tugas sebelumnya, pernah dibuat grafik batang dengan rentang sumbu Y yang terlalu sempit sehingga selisih performa antaralgoritma terlihat lebih besar dari kondisi sebenarnya. Setelah memahami prinsip visualisasi ilmiah, grafik harus dibuat dengan skala yang tepat, menampilkan seluruh data, serta dilengkapi error bar agar penyajian hasil menjadi lebih objektif, jujur, dan tidak menyesatkan.
