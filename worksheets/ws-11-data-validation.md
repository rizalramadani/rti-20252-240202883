# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [✓] Semua skenario tercakup
  [✓] Jumlah run sesuai rencana
  [✓] Tidak ada file output hilang
  Missing: 0 dari 10 data points

Format Consistency:
  [✓] Semua file format sama (CSV/JSON/...)
  [✓] Header konsisten
  [✓] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [✓] Nilai dalam range masuk akal
  [✓] Tidak ada waktu negatif
  [✓] Metrik 0–100%, tidak di luar range
  Anomali ditemukan: Tidak ada anomali yang memerlukan re-run

Cross-Validation:
  [✓] Run identik → hasil mendekati
  [✓] Trend konsisten dengan ekspektasi teori

Keputusan:
  [✓] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run (skenario: -)
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| Naive Bayes – SpamAssassin | 5 | 5 | 0 | - |
| K-Nearest Neighbor – SpamAssassin | 5 | 5 | 0 | - |

**Total expected:** 10 | **Total actual:** 10 | **Missing:**0

**Keputusan untuk data missing:**
> Seluruh data berhasil dikumpulkan sesuai execution plan pada WS-10 sehingga tidak diperlukan pengumpulan data tambahan maupun pengulangan eksperimen.

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (atau data Anda sendiri):**

| Run | Accuracy (%) |
|-----|-------------|
| 1 | 96.4 |
| 2 | 96.2 |
| 3 | 96.5 |
| 4 | 95.9 |
| 5 | 96.3 |

**Deteksi outlier:**
- Q1 = 96.2 | Q3 = 96.4 | IQR = 0.2
- Batas bawah (Q1 - 1.5×IQR) = 95.9
- Batas atas (Q3 + 1.5×IQR) = 96.7
- Outlier terdeteksi:Tidak ada

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| Tidak ada | —* | Seluruh nilai masih berada dalam batas IQR |Data dipertahankan dan digunakan untuk analisis |

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data terkumpul
**2. Format:** [☑] Konsisten / [ ] Ada inkonsistensi: 
**3. Range check (anomali):** Seluruh nilai Accuracy, Precision, Recall, dan F1-Score berada pada rentang 0–100% sehingga tidak ditemukan nilai yang berada di luar batas logis.
**4. Logic check:** [☑] Parameter sesuai plan / [ ] Ada ketidaksesuaian: ____

**Kesimpulan:** [☑] Data siap analisis / [ ] Perlu tindakan: ____

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> Data yang benar adalah data yang berhasil diperoleh dari proses eksperimen, sedangkan data yang dipercaya adalah data yang telah melalui proses validasi sehingga terbukti lengkap, konsisten, dan sesuai dengan desain penelitian. Data yang benar belum tentu dapat dipercaya apabila masih terdapat kesalahan pencatatan, data yang hilang, atau inkonsistensi format.
> Proses validasi formal tetap diperlukan meskipun data dikumpulkan secara otomatis karena sistem pencatatan juga dapat mengalami kesalahan, seperti bug pada logger, file yang tidak lengkap, atau konfigurasi eksperimen yang tidak sesuai. Dengan melakukan validasi terhadap kelengkapan data, format, rentang nilai, dan kesesuaian dengan desain eksperimen, hasil penelitian menjadi lebih andal, mudah direproduksi, dan dapat dipertanggungjawabkan secara ilmiah.
