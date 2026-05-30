# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Perbandingan Naive Bayes dan K-Nearest Neighbor untuk Klasifikasi Email Spam
Database   : Google Scholar, IEEE Xplore, ResearchGate
Query      : ("email spam classification" OR "spam detection")
AND ("Naive Bayes" OR "K-Nearest Neighbor" OR "KNN")
AND ("machine learning")
Tahun      : 2020–2024
Hasil awal : 35 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|Sharma et al.|2021|Naive Bayes vs KNN|Enron Email Dataset|NB 94%, KNN 91%|Hanya email bahasa Inggris|
|Singh & Kumar|2022|SVM, NB, KNN|SpamAssassin|SVM 96%, NB 93%|Tidak diuji real-time|
|Lee et al.|2023|Random Forest, KNN|Ling-Spam Dataset|RF lebih baik dari KNN|Dataset relatif kecil|
|Ahmed et al.|2024|CNN, LSTM|Multi-language Email Dataset|Accuracy 98%|Komputasi tinggi|
|Zhang et al|2020|NB, DT, KNN|UCI Spam Base|NB paling cepat|Kurang efektif pada data tidak seimbang|

Pola yang ditemukan:
  Metode dominan     : Naive Bayes, KNN, SVM, Random Forest, dan Deep Learning (CNN/LSTM).
  Dataset umum       : SpamAssassin, Enron Email Dataset, Ling-Spam Dataset, UCI Spam Base.
  Limitasi berulang  : Dataset mayoritas berbahasa Inggris.
Belum banyak evaluasi multi-bahasa.
KNN memiliki waktu komputasi lebih tinggi.
Sebagian penelitian hanya fokus pada akurasi.

GAP IDENTIFICATION

Gap 1: [Jenis: Data]
  Deskripsi    : Sebagian besar penelitian menggunakan dataset email berbahasa Inggris sehingga belum mewakili kondisi email global atau lokal Indonesia.
  Bukti        : 4 dari 5 paper menggunakan Enron, SpamAssassin, atau UCI Spam Base yang seluruhnya berbahasa Inggris.
  Signifikansi : Model yang dilatih pada satu bahasa belum tentu memiliki performa yang sama pada bahasa lain.

Gap 2: [Jenis: Method Gap]
  Deskripsi    : Penelitian terbaru banyak membandingkan metode klasik dengan deep learning, tetapi perbandingan khusus antara Naive Bayes dan KNN pada dataset modern masih terbatas.
  Bukti        : Sebagian besar studi tahun 2023–2024 berfokus pada CNN, LSTM, atau Random Forest.
  Signifikansi : Perlu diketahui apakah metode sederhana seperti Naive Bayes masih kompetitif dibanding metode lain dengan biaya komputasi lebih rendah.

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
|Naive Bayes|Digunakan langsung untuk klasifikasi spam email|Salah satu algoritma paling umum dalam text classification|Sharma et al. (2021)|
|K-Nearest Neighbor|Digunakan untuk task yang sama|Sering digunakan sebagai metode pembanding|Sharma et al. (2021)|
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Perbandingan Naive Bayes vs KNN untuk Klasifikasi Spam Email
**Query pencarian:** ("spam email detection" AND "Naive Bayes" AND "KNN") OR ("email classification" machine learning)
**Database:** Google Scholar, IEEE Xplore, MDPI

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Email Spam Detection using ML Techniques (IEEE) | 2021 | Naive Bayes, KNN, SVM | SpamAssassin | NB lebih stabil | Dataset kecil & lama |
| 2 |Comparative Study of ML for Spam Email Detection |2020 |NB vs KNN vs DT |Enron Email Dataset |NB > KNN akuras |Bahasa Inggris saja |
| 3 |Spam Detection using TF-IDF + ML |2022 |NB, KNN, Logistic Regression |Public email dataset |KNN lebih lambat |Feature sederhana |
| 4 |Machine Learning for Spam Filtering (Review) |2023 |Review paper |Multi dataset |NB paling umum dipakai |Tidak eksperimen baru |
| 5 |Email Classification using Supervised Learning |2021 |NB, KNN |Spam dataset Kaggle |NB unggul di precision |Tidak real-time test |

**Pola yang terlihat — Metode dominan:** Naive Bayes (paling sering dan stabil), KNN (sering sebagai pembanding)
**Limitasi yang berulang:** dataset kecil, bahasa Inggris dominan, tidak real-time, fitur sederhana (TF-IDF)

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [✓ ] Ya / [ ] Tidak | Akurasi algoritma klasik menurun pada dataset email modern dengan pola spam yang kompleks |
| Method Gap | [✓ ] Ya / [ ] Tidak |Belum banyak penelitian yang mengombinasikan Naive Bayes dan KNN dengan teknik feature extraction modern |
| Data Gap | [✓ ] Ya / [ ] Tidak |Banyak penelitian masih memakai dataset lama seperti Enron dan Spam Base |
| Context Gap | [✓ ] Ya / [ ] Tidak |Belum banyak pengujian pada email berbahasa non-Inggris atau multi-domain |

**Gap utama yang dipilih:** Data Gap + Context Gap
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Karena sistem spam email di dunia nyata tidak hanya bergantung pada akurasi dataset lama, tetapi harus mampu menangani spam modern yang terus berubah dan bersifat real-time. Oleh karena itu, hasil penelitian sebelumnya belum sepenuhnya representatif untuk kondisi nyata.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | Naive Bayes + TF-IDF | Standar klasik spam detection | Paling sering dipakai di 4/5 paper | Naive Bayes dan KNN dipilih sebagai baseline klasik yang umum digunakan dalam penelitian spam email classification, bukan sebagai state-of-the-art method | IEEE 2021 |
| 2 |K-Nearest Neighbor (KNN) |Algoritma pembanding utama |Banyak dipakai untuk comparison study |Naive Bayes dan KNN dipilih sebagai baseline klasik yang umum digunakan dalam penelitian spam email classification, bukan sebagai state-of-the-art method |MDPI 2022 |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [ ✓] Tidak
> Justifikasi: Kedua baseline (Naive Bayes dan KNN) merupakan algoritma standar yang memang umum digunakan dalam penelitian spam email classification, sehingga perbandingan bersifat fair dan tidak bias.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Perbedaan "belum ada yang meneliti ini" dengan research gap yang valid adalah bahwa research gap harus dibuktikan melalui literatur yang sudah ada, bukan asumsi. Gap yang valid muncul dari pola berulang di beberapa paper, seperti keterbatasan dataset, metode yang dominan, atau konteks yang belum diuji. Cara membuktikannya adalah dengan systematic literature review menggunakan database akademik dan mencatat konsistensi limitasi pada beberapa penelitian.
> 
