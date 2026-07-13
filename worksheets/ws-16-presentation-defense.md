# WS-16: Presentation & Defense (UAS)

> **Bab 16 — Presentasi & Pertahanan Ilmiah**

---

## Ringkasan Materi

### Scientific Defense Model

```
Research Work → Presentation → Questioning → Defense → Evaluation → Acceptance
```

### Presentasi ≠ Ringkasan Paper

| Paper | Presentasi |
|-------|-----------|
| Dibaca (self-paced) | Didengar (presenter-paced) |
| Detail lengkap | Ide kunci + highlight |
| Tabel numerik detail | Grafik visual + angka kunci |
| Pembaca bisa re-read | Audiens dengar sekali |

**Prinsip:** Presentasi membutuhkan **reformulasi**, bukan kompresi. Medium berbeda = pendekatan berbeda.

### Claim-Evidence-Reasoning (CER)

Setiap jawaban defense harus memiliki:
1. **Claim** — Pernyataan yang dijawab
2. **Evidence** — Data/fakta pendukung
3. **Reasoning** — Logika yang menghubungkan evidence ke claim

**Contoh:**
| Pertanyaan | Bad Answer | Good Answer (CER) |
|-----------|-----------|-------------------|
| "Kenapa hanya 3 dataset?" | "Tiga sudah cukup" | "3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy [E]. Generalisasi perlu validasi lanjut — listed as limitation [R]" |
| "Hasil DS-3 menurun?" | "Itu outlier" | "Ya, karena distribusi heavy-tail melanggar asumsi Gaussian [E]. Ini menunjukkan boundary condition metode [R]" |
| "Effect size?" | "p=0.003, jadi signifikan" | "Cohen's d=1.2 (large effect) [E] — bukan hanya signifikan tapi substansial [R]" |

### Slide Design — One Slide, One Message

**Optimal 9-Slide Plan (15 menit):**

| # | Slide | Waktu | Pesan |
|---|-------|-------|-------|
| 1 | Title + context | 1 min | Apa ini tentang apa |
| 2 | Problem + motivation | 2 min | Mengapa penting |
| 3 | Gap + RQ | 1.5 min | Apa yang belum terjawab |
| 4 | Method overview | 2 min | Bagaimana dijawab (diagram) |
| 5 | Key result — tabel | 2 min | Temuan utama |
| 6 | Key result — grafik | 2 min | Pola visual |
| 7 | Interpretation + failure | 2 min | Apa artinya |
| 8 | Limitation + future | 1.5 min | Batasan & arah |
| 9 | Conclusion + contribution | 1 min | Closing message |

### Anticipatory Defense

Prediksi pertanyaan berdasarkan kategori:

| Kategori | Contoh Pertanyaan |
|---------|------------------|
| Problem | "Mengapa masalah ini penting?" |
| Gap | "Bagaimana dengan studi X yang sudah menjawab ini?" |
| Method | "Mengapa metode ini, bukan Y?" |
| Results | "Bagaimana menjelaskan anomali di DS-3?" |
| Generalization | "Apakah bisa diterapkan di domain lain?" |

### Tiga Prinsip Jawaban

1. **Direct** — Jawab dulu, elaborasi kemudian
2. **Data-based** — Tunjuk evidence spesifik
3. **Honest** — Akui limitasi jika memang ada

### Jebakan Kognitif

1. "Presentasi = semua yang ada di paper" → terlalu padat
2. "Slide cantik = presentasi bagus" → konten > estetika
3. "Tidak bisa jawab = gagal" → "I don't know, but..." menunjukkan kejujuran
4. "Tidak perlu latihan — saya paham riset saya" → latihan = menemukan celah

---

## Template A.16 — Defense Preparation Sheet

```
DEFENSE PREPARATION

Slide Deck Plan:

Total slides   : 11 (10 slide materi + 1 slide penutup)
Time per slide : ±1,5 menit
Total time     : 15 menit

Slide Outline:

| # | Pesan Utama | Visual | Waktu |
|---|-------------|--------|-------|
| 1 | Judul Penelitian | Cover | 1 menit |
| 2 | Latar Belakang | Diagram email spam | 2 menit |
| 3 | Research Gap & Research Question | Tabel gap penelitian | 1,5 menit |
| 4 | Metode Penelitian | Flowchart penelitian | 2 menit |
| 5 | Dataset & Preprocessing | Diagram preprocessing | 1,5 menit |
| 6 | Hasil Eksperimen | Tabel hasil | 2 menit |
| 7 | Visualisasi Hasil | Bar chart Accuracy & F1-Score | 2 menit |
| 8 | Analisis & Limitasi | Diagram kesimpulan | 1,5 menit |
| 9 | Kesimpulan | Ringkasan poin penting | 1 menit |
|10 | Kontribusi & Future Work | Diagram roadmap | 0,5 menit |
|11 | Terima Kasih & Tanya Jawab | Closing | 0,5 menit |

Anticipatory Defense Matrix:

| Kategori | Pertanyaan Potensial | Jawaban (CER) |
|----------|----------------------|---------------|
| Problem | Mengapa memilih klasifikasi email spam? | Email spam masih menjadi masalah keamanan digital. Penelitian menunjukkan jumlah spam terus meningkat sehingga diperlukan metode klasifikasi yang akurat. Oleh karena itu penelitian ini membandingkan dua algoritma yang umum digunakan. |
| Gap | Apa perbedaan penelitian Anda dengan penelitian sebelumnya? | Penelitian ini membandingkan Naive Bayes dan KNN menggunakan SpamAssassin Dataset dengan evaluasi Accuracy, Precision, Recall, dan F1-Score secara konsisten pada beberapa kali eksperimen. |
| Method | Mengapa memilih Naive Bayes dan KNN? | Kedua algoritma merupakan metode klasifikasi yang populer dan memiliki karakteristik berbeda sehingga menarik untuk dibandingkan pada data email spam. |
| Results | Mengapa Naive Bayes memiliki hasil lebih baik? | Naive Bayes bekerja efektif pada data teks hasil TF-IDF karena menghitung probabilitas kemunculan kata sehingga menghasilkan F1-Score lebih tinggi. |
| Generalization | Apakah hasil ini dapat diterapkan pada dataset lain? | Dapat dijadikan referensi, namun perlu validasi menggunakan dataset lain karena penelitian ini hanya menggunakan SpamAssassin Dataset. |

Latihan:

Latihan 1 : 18 Juni 2026 — Waktu presentasi masih 17 menit, perlu dipersingkat.

Latihan 2 : 20 Juni 2026 — Penyampaian lebih lancar, waktu menjadi 15 menit.

Latihan 3 : 22 Juni 2026 — Sudah sesuai target, siap untuk presentasi.
```

---

## Latihan 1 — Slide Outline

Rencanakan presentasi 15 menit untuk riset Anda.

| # | Pesan Utama | Visual yang Digunakan | Waktu |
|---|-------------|----------------------|-------|
| 1 | Judul penelitian dan identitas | Cover penelitian | 1 menit |
| 2 | Latar belakang pentingnya klasifikasi email spam | Ilustrasi email spam dan statistik spam | 2 menit |
| 3 | Research Gap dan Research Question | Tabel penelitian terdahulu | 1,5 menit |
| 4 |Metode penelitian|Flowchart penelitian|2 menit|
| 5 |Dataset dan preprocessing|Diagram preprocessing (Case Folding, Tokenization, Stopword Removal, TF-IDF)|1,5 menit|
| 6 |Hasil eksperimen|Tabel Accuracy, Precision, Recall, dan F1-Score|2 menit|
| 7 |Visualisasi hasil|Bar Chart dan Box Plot|2 menit|
| 8 |Analisis hasil, limitation, dan future work|Diagram analisis|1,5 menit|
| 9 |Kesimpulan dan kontribusi penelitian|Ringkasan poin utama|1,5 menit|

**Total waktu estimasi:** 15 menit menit

---

## Latihan 2 — Anticipatory Defense

Prediksi 5 pertanyaan yang mungkin diajukan penguji, lalu siapkan jawaban CER.

| # | Kategori | Pertanyaan | Claim | Evidence | Reasoning |
|---|----------|-----------|-------|----------|-----------|
| 1 | Problem | Mengapa memilih klasifikasi email spam? | Email spam masih menjadi masalah penting dalam keamanan informasi | Banyak email spam mengandung phishing dan malware. |Metode klasifikasi diperlukan agar email spam dapat dideteksi |
| 2 | Method | Mengapa menggunakan Naive Bayes dan KNN?| Kedua algoritma merupakan metode klasifikasi yang banyak digunakan. | Banyak penelitian terdahulu menggunakan kedua algoritma tersebut. | Perbandingan dilakukan untuk mengetahui algoritma yang lebih efektif pada SpamAssassin Dataset. |
| 3 |Results|Mengapa Naive Bayes memperoleh hasil lebih baik?|Naive Bayes lebih sesuai untuk data teks.|Nilai Accuracy dan F1-Score lebih tinggi dibandingkan KNN.|TF-IDF menghasilkan representasi fitur yang sesuai dengan asumsi probabilistik Naive Bayes.|
| 4 |Limitation|Mengapa hanya menggunakan satu dataset?|Penelitian difokuskan pada SpamAssassin Dataset.|Dataset memiliki jumlah data yang cukup dan banyak digunakan pada penelitian email spam.|Pengujian pada dataset lain direncanakan sebagai penelitian lanjutan.|
| 5 |Generalization|Apakah hasil dapat diterapkan pada dataset lain?|Belum tentu secara langsung.|Setiap dataset memiliki karakteristik yang berbeda.|Diperlukan validasi tambahan agar hasil dapat digeneralisasi.|

---

## Latihan 3 — Simulasi Q&A

Minta teman/kolega mengajukan 3 pertanyaan tentang riset Anda. Catat pertanyaan dan evaluasi jawaban Anda.

| # | Pertanyaan | Jawaban Saya | Evaluasi |
|---|-----------|-------------|---------|| 1 | Mengapa memilih SpamAssassin Dataset? | Karena merupakan dataset publik yang banyak digunakan pada penelitian klasifikasi email spam sehingga memudahkan perbandingan hasil penelitian | [✓] Direct [✓] Data-based [✓] Honest || 1 | | | [ ] Direct [ ] Data-based [ ] Honest |
| 2 |Mengapa tidak menggunakan algoritma Deep Learning?|Penelitian ini bertujuan membandingkan algoritma machine learning klasik yang lebih sederhana dan memiliki waktu komputasi lebih cepat. Penggunaan Deep Learning menjadi pengembangan penelitian selanjutnya.| [✓] Direct [✓] Data-based [✓] Honest |
| 3 |Apa kelemahan penelitian Anda?|Penelitian hanya menggunakan satu dataset dan lima kali eksperimen sehingga hasil belum dapat digeneralisasi secara luas.| [✓] Direct [✓] Data-based [✓] Honest |

**Pertanyaan yang paling sulit dijawab:**
> Bagaimana performa algoritma apabila diterapkan pada dataset email berbahasa Indonesia atau dataset yang memiliki karakteristik berbeda?
**Apa yang perlu disiapkan lebih baik:**
> Menyiapkan referensi penelitian yang menggunakan dataset lain serta memahami karakteristik berbagai algoritma klasifikasi sehingga dapat menjawab pertanyaan penguji dengan lebih mendalam.
---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-16 — dari paradigma riset hingga presentasi — bagian mana yang paling mengubah cara Anda berpikir tentang riset? Apa satu hal yang akan selalu Anda terapkan di riset berikutnya?

**Insight terbesar:**
> Bagian yang paling mengubah cara berpikir adalah proses analisis hasil penelitian dan penyusunan argumen ilmiah. Penelitian bukan hanya menghasilkan nilai Accuracy atau F1-Score yang tinggi, tetapi juga mampu menjelaskan mengapa hasil tersebut diperoleh, bagaimana keterbatasannya, serta apa kontribusinya terhadap penelitian sebelumnya. Selain itu, hasil yang tidak sesuai hipotesis tetap memiliki nilai ilmiah apabila dianalisis secara objektif.

**Yang akan selalu diterapkan:**
> Pada penelitian berikutnya, setiap tahap penelitian akan didokumentasikan secara lengkap, mulai dari perencanaan eksperimen, preprocessing, pengujian, analisis hasil, hingga penyusunan laporan. Dokumentasi yang baik membuat penelitian lebih mudah direproduksi, dipertanggungjawabkan secara ilmiah, dan memberikan kontribusi yang lebih bermanfaat bagi penelitian selanjutnya.
