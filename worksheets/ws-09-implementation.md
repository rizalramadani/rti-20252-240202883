# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

> **Mengapa reproducibility penting?** Sains dibangun di atas prinsip verifikasi — temuan harus bisa dikonfirmasi oleh peneliti lain. _Replicability crisis_ yang terjadi di banyak paper riset ML/AI disebabkan oleh environment tidak terdokumentasi: orang lain tidak bisa reproduksi, hasil diragukan, kepercayaan terhadap temuan hilang. Prinsip: **dokumentasi environment = snapshot kredibilitas riset Anda.**

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
   - **Docker** = teknologi container yang "membungkus" aplikasi beserta seluruh dependency-nya dalam satu unit terisolasi. Hasilnya: kode berjalan identik di laptop, server, maupun reviewer lain. Intro singkat: `docker run -v $(pwd):/workspace environment-image python run_experiment.py`
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Dependency Locking

Mengandalkan "install library terbaru" berbahaya: versi berbeda = perilaku berbeda = hasil tidak reproducible. Praktik:
- **Python**: buat `requirements.txt` dengan versi eksplisit: `scikit-learn==1.3.2`, lalu kunci dengan `pip freeze > requirements.txt`
- **Conda**: gunakan `conda env export > environment.yml` untuk snapshot lengkap
- **Node.js/R/Julia**: gunakan `package-lock.json` / `renv.lock` / `Project.toml` — semua fungsi serupa: lock versi + hash

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : Intel Core i5-1135G7 (4 Core, 8 Thread)
  RAM     : 8 GB DDR4
  GPU     : Intel Iris Xe Graphics (CPU-only)
  Storage : SSD 512 GB

Software:
  OS        : Windows 11 Pro 64-bit
  Runtime   : Python 3.11
  Framework : Scikit-learn 1.3.2

Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|scikit-learn|1.3.2|PyPI|requirements.txt|
|pandas|2.2.2|PyPI|requirements.txt|
|numpy|1.26.4|PyPI|requirements.txt|

Konfigurasi:
  Config file     : config.json
  Random seed     : 42
  Hyperparameters : rain-test split = 80:20
TF-IDF Vectorizer
KNN (k = 5)
Naive Bayes (MultinomialNB)

Reproducibility Check:
  [☑] Dependency terdokumentasi (requirements.txt / lock file)
  [☑] Seed ditetapkan di semua level (Python, NumPy, framework)
  [☑] Config di version control
  [☑] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | Intel Core i5-1135G7 (4 Core, 8 Thread) |
| RAM | 8 GB DDR4 |
| GPU | Intel Iris Xe Graphics (CPU-only) |
| OS | Windows 11 Pro 64-bit |
| Runtime |Python 3.11|
| Framework |Scikit-learn 1.3.2|
| Random Seed |42|

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|scikit-learn|1.3.2|Implementasi algoritma Naive Bayes, KNN, serta evaluasi model|
| pandas | 2.2.2 | Membaca dan mengelola dataset SpamAssassin |
|numpy|1.26.4|Operasi numerik dan manipulasi array|
|matplotlib|3.9.0|Visualisasi hasil eksperimen|
|seaborn|0.13.2|Menampilkan confusion matrix dan grafik evaluasi|


---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | 42 | F1-Score = 97,1% | — |
| 2 |42|F1-Score = 97,1%| [☑] Ya / [ ] Tidak |
| 3 |42|F1-Score = 97,1%| [☑] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**

> Penyebab umum non-repeatability:
> - Random seed belum diterapkan pada seluruh library. — CPU/GPU overheating pada run berturut-turut → clock speed turun → waktu eksekusi berubah
> - Dataset berubah akibat preprocessing yang tidak konsisten. — antivirus scan, update OS, atau cloud sync aktif saat run berlangsung
> - Terdapat proses lain yang menggunakan resource komputer. — hasil tersimpan di memori/disk sehingga run berikutnya tidak menjalankan komputasi penuh
> - Cache hasil eksperimen belum dibersihkan. — Python seed di-set, tapi NumPy/PyTorch/TensorFlow punya seed independen

___________________________________________________

**Checklist kontrol yang sudah diterapkan:**
- [☑] Random seed di-set di semua level
- [☑] Tidak ada background process yang mengganggu
- [☑] Cache dibersihkan antar-run
- [☑] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Perbandingan Algoritma Naive Bayes dan K-Nearest Neighbor (KNN)
untuk Klasifikasi Spam Email Menggunakan SpamAssassin Dataset

## 1. Environment
> CPU          : Intel Core i5-1135G7
RAM          : 8 GB DDR4
GPU          : Intel Iris Xe Graphics
OS           : Windows 11 Pro
Python       : 3.11
Framework    : Scikit-learn 1.3.2
Random Seed  : 42

## 2. Installation
> pip install -r requirements.txt

## 3. Data
> Dataset menggunakan SpamAssassin Public Corpus dalam format CSV.
Seluruh data diproses menggunakan preprocessing yang sama berupa
tokenization, stopword removal, dan TF-IDF.

## 4. Execution
> python main.py

## 5. Configuration
> Config file : config.json

- random_seed = 42
- train_test_split = 0.8
- classifier = naive_bayes / knn
- k = 5

## 6. Expected Output
> Output yang dihasilkan berupa:
- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang? Ya. Eksperimen telah dilengkapi dengan spesifikasi hardware dan software, versi library, parameter eksperimen, random seed, serta langkah instalasi dan eksekusi. Dengan menggunakan dataset yang sama, konfigurasi yang identik, dan dependency yang telah dikunci melalui requirements.txt, peneliti lain dapat menjalankan eksperimen dan memperoleh hasil yang sama atau sangat mendekati.

**Level saat ini:** [☑] Repeatability / [☑] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Repository GitHub proyek.
>File requirements.txt dan config.json sebagai lampiran.
>Struktur folder proyek.
>Dokumentasi preprocessing secara lebih rinci.
>Dokumentasi hasil pengujian untuk setiap percobaan.