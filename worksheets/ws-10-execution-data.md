# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1     |Naive Bayes - SpamAssassin| 42|TF-IDF, Split 80:20|Planned|±15 detik| nb_run01.csv|
| 2     |Naive Bayes - SpamAssassin|123|TF-IDF, Split 80:20|Planned|±15 detik|nb_run02.csv|
| 3     |Naive Bayes - SpamAssassin| 456|TF-IDF, Split 80:20|Planned|±15 detik|nb_run03.csv|
|6      |KNN - SpamAssassin|  42|TF-IDF, Split 80:20, k=5|Planned|±20 detik|knn_run01.csv|
| 7     | KNN - SpamAssassin | 123 | TF-IDF, Split 80:20, k=5 | Planned | ±20 detik | knn_run02.csv |
| 8     | KNN - SpamAssassin | 456 | TF-IDF, Split 80:20, k=5 | Planned | ±20 detik | knn_run03.csv |

Jumlah runs per skenario : 5
Total runs               : 8

DATA LOG (per run):
  Run ID    : run-001
  Timestamp : 2026-07-13 10:30:00
  Skenario  : Naive Bayes - SpamAssassin
  Input     : SpamAssassin Dataset
  Output    : Accuracy, Precision, Recall, F1-Score, Confusion Matrix
  Anomali   : Tidak ada
  Catatan   : Eksperimen berjalan sesuai konfigurasi
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| 1 | Naive Bayes – SpamAssassin | 42 | TF-IDF, Split 80:20 | Planned |
| 2 | Naive Bayes – SpamAssassin | 123 | TF-IDF, Split 80:20 | Planned |
| 3 |Naive Bayes – SpamAssassin|456|TF-IDF, Split 80:20|Planned|
| 4 |Naive Bayes – SpamAssassin|789|TF-IDF, Split 80:20|Planned|
| 5 |Naive Bayes – SpamAssassin|999|TF-IDF, Split 80:20|Planned|
| 6 |KNN – SpamAssassin|42|TF-IDF, Split 80:20, k=5|Planned|
| 7 |KNN – SpamAssassin|123|TF-IDF, Split 80:20|Planned|
| 8 |KNN – SpamAssassin|456|TF-IDF, Split 80:20|Planned|
| 9 |KNN – SpamAssassin|789|TF-IDF, Split 80:20|Planned|
| 10 |KNN – SpamAssassin|999|TF-IDF, Split 80:20, k=5|Planned|

**Total skenario:** 2
**Run per skenario:** 5
**Total run keseluruhan:** 10

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID | run-001 |
| Timestamp | 2026-07-13T10:30:00 |
|Skenario|Naive Bayes - SpamAssassin|
|Operator|Rizal Ramadani|

**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| Seed | 42 |
| Code version | commit abc1234 |
|Dataset|SpamAssassin Dataset|
|Train-test split|80:20|
|Algoritma|Naive Bayes|

**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
| Accuracy | Float | 0.0 – 1.0 |
|Precision|Float|0.0 – 1.0|
|Recall|Float|0.0 – 1.0|
|F1-Score|Float|0.0 – 1.0|
|Execution Time|Float|> 0 detik|

**Format output:** [☑] CSV / [☑] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) | Run gagal (crash) | Program berhenti saat proses training | Dokumentasikan penyebab, perbaiki kesalahan, kemudian lakukan run ulang dengan konfigurasi yang sama|
| Hasil ekstrem |Accuracy atau F1-Score jauh lebih rendah dibanding run lain|Periksa dataset, preprocessing, dan seed yang digunakan, lalu ulangi eksperimen jika diperlukan|
| Waktu eksekusi anomali |Waktu proses jauh lebih lama dari run lain|Periksa penggunaan CPU/RAM dan pastikan tidak ada proses lain yang mengganggu|
| Inkonsistensi dengan run lain |Nilai metrik berbeda jauh meskipun konfigurasi sama|Periksa random seed, versi library, dan konfigurasi eksperimen, kemudian lakukan verifikasi ulang|

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Pada beberapa tugas praktikum, hasil eksperimen hanya diperoleh dari satu kali proses eksekusi. Cara tersebut memang lebih cepat, tetapi hasilnya belum dapat menggambarkan performa algoritma secara konsisten karena masih dipengaruhi faktor acak, seperti pembagian data maupun konfigurasi sistem.
**Yang akan dilakukan berbeda:**
> Pada penelitian ini, setiap algoritma akan dijalankan sebanyak lima kali dengan random seed yang berbeda. Seluruh hasil akan dicatat dalam data log dan dihitung nilai rata-rata serta variasinya. Dengan demikian, hasil penelitian menjadi lebih konsisten, dapat diuji secara statistik, dan lebih mudah direproduksi oleh peneliti lain.
