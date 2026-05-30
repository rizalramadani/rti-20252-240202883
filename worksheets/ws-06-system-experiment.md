# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

  Contoh config YAML dengan feature toggles:
  ```yaml
  model:
    type: cnn          # IV: ganti "rf" untuk kondisi baseline
  features:
    use_temporal: true  # toggle komponen temporal
    use_normalization: true  # toggle preprocessing
  experiment:
    seed: 42
    runs: 5
  ```
  Dengan pendekatan ini, berbeda kondisi eksperimen = berbeda satu baris config, **tanpa mengubah kode**.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: Apakah metode Naive Bayes menghasilkan performa klasifikasi email spam yang lebih baik dibandingkan K-Nearest Neighbor berdasarkan nilai Accuracy, Precision, Recall, dan F1-Score pada SpamAssassin Dataset?

Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
|Jenis Algoritma (Naive Bayes, KNN)| IV   |Modul Classifier|Mengubah parameter model_type menjadi Naive Bayes atau KNN|
|Performa Klasifikasi| DV   |Modul Evaluasi (Metrics Collector)|Menghitung Accuracy, Precision, Recall, dan F1-Score|
|Text Preprocessing| CV   |Preprocessing Module|Tokenization, stopword removal, dan TF-IDF diterapkan sama untuk semua metode|

4 Prinsip Desain:
  [✓] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [✓] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [✓] Measurement Integration — Pengukuran DV built-in
  [✓] Reproducibility — Setup bisa direkonstruksi

Experimental Setup:
  Input data     : SpamAssassin Public Corpus
  Parameter      : dataset:
  name: SpamAssassin

preprocessing:
  tfidf: true
  stopword_removal: true

experiment:
  train_test_split: 0.8
  random_seed: 42

model:
  type: naive_bayes
  Output format  : | Algoritma   | Accuracy | Precision | Recall | F1-Score |
| ----------- | -------- | --------- | ------ | -------- |
| Naive Bayes | xx.xx%   | xx.xx%    | xx.xx% | xx.xx%   |
| KNN         | xx.xx%   | xx.xx%    | xx.xx% | xx.xx%   |

```

---

## Latihan 1 — Variable-to-Component Mapping

Apakah metode Naive Bayes menghasilkan F1-Score lebih tinggi dibandingkan K-Nearest Neighbor pada klasifikasi email spam menggunakan SpamAssassin Dataset?

**RQ:** __________________________________________________

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
| Jenis algoritma | IV | Modul classifier | Mengubah parameter model_type = NB / KNN pada config |
|Performa klasifikasi | DV |Modul evaluasi dan metrics collector |Menghitung Accuracy, Precision, Recall, dan F1-Score |
|Dataset email | CV |Modul dataset loader |Dataset dikunci menggunakan SpamAssassin Dataset |

**Apakah semua variabel bisa di-map?** [✓ ] Ya / [ ] Tidak
> Jika tidak,

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability |✅ |Setiap komponen sistem terkait langsung dengan variabel penelitian |
| Modularity |✅ |Modul classifier dapat diganti antara NB dan KNN tanpa mengubah modul lain |
| Controllability |✅ |Dataset dan parameter eksperimen disimpan pada config file |
| Measurability |✅ |Sistem otomatis menghasilkan confusion matrix dan metrik evaluasi |

**Prinsip mana yang paling sulit dipenuhi?** Modularity
**Strategi untuk mengatasinya:**
> Menggunakan arsitektur berbasis module/class sehingga algoritma classifier dapat di-swap hanya dengan mengubah konfigurasi tanpa mengubah kode utama sistem.

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

> **Panduan jumlah kondisi:** Untuk 3 komponen (A, B, C), kondisi minimal yang direkomendasikan:
> Full + (-A) + (-B) + (-C) = **4 kondisi dasar**. Jika waktu memungkinkan, tambahkan kombinasi ganda: (-A,-B), (-A,-C), (-B,-C) = **7 kondisi**. Sesuaikan dengan *computational cost* dan tenggat waktu penelitian.

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|-----------|-----------|-----------|----------------------|
| Full | *Contoh: ✅ CNN* | *Contoh: ✅ Temporal features* | *Contoh: ✅ Z-score norm* | Performa optimal sistem |
| – A | ❌ (ganti RF) | ✅ | ✅ |Mengetahui pengaruh algoritma terhadap performa |
| – B | ✅ | ❌ (tanpa temporal) | ✅ |Mengukur kontribusi TF-IDF terhadap akurasi |
| – C | ✅ | ✅ | ❌ (tanpa normalisasi) |Mengukur pengaruh preprocessing terhadap hasil klasifikasi |

**Komponen mana yang diprediksi paling berkontribusi?** Komponen B — TF-IDF Feature Extraction
**Mengapa?**
> TF-IDF membantu merepresentasikan kata-kata penting pada email spam sehingga model lebih mudah membedakan email spam dan non-spam. Tanpa feature extraction yang baik, performa klasifikasi diperkirakan turun signifikan.

---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Jika sistem dibangun seperti produk monolitik dengan banyak fitur tambahan, maka eksperimen menjadi sulit dikontrol karena perubahan satu komponen dapat memengaruhi komponen lain. Hal ini membuat hubungan sebab-akibat antar variabel menjadi tidak jelas.
> Arsitektur modular penting dalam riset karena memungkinkan isolasi variabel, pengujian yang reproducible, serta mempermudah eksperimen seperti perbandingan metode dan ablation study tanpa harus mengubah keseluruhan sistem
