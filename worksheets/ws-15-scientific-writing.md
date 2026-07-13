# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title :
Perbandingan Algoritma Naive Bayes dan K-Nearest Neighbor (KNN)
untuk Klasifikasi Email Spam Menggunakan SpamAssassin Dataset

Target :
[✓] Jurnal
[ ] Konferensi
[ ] Laporan

Section Check:

[✓] Abstract — masalah, metode, hasil utama, kontribusi
[✓] Introduction — konteks → gap → research question → kontribusi → struktur paper
[✓] Related Work — concept-centric dan gap penelitian
[✓] Method — desain penelitian, variabel, metrik, setup eksperimen, prosedur
[✓] Results — tabel, grafik, dan hasil eksperimen tanpa interpretasi
[✓] Discussion — interpretasi, perbandingan dengan penelitian sebelumnya, implikasi, limitation
[✓] Conclusion — jawaban research question, kontribusi, dan saran penelitian selanjutnya

Consistency Matrix:

[✓] Research Question pada Introduction sama dengan Method dan Conclusion
[✓] Variabel pada Method sama dengan Results
[✓] Klaim pada Discussion didukung oleh data Results
[✓] Limitasi pada Discussion dibahas kembali pada Future Work

Writing Quality:

[✓] Clarity
[✓] Precision
[✓] Conciseness
```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section | Konten Utama (2-3 kalimat) | Target Kata |
|---------|---------------------------|------------|
| Abstract | Penelitian ini membandingkan algoritma Naive Bayes dan K-Nearest Neighbor untuk klasifikasi email spam menggunakan SpamAssassin Dataset. Evaluasi dilakukan menggunakan Accuracy, Precision, Recall, dan F1-Score. Hasil menunjukkan bahwa Naive Bayes memiliki performa lebih baik dibandingkan KNN. | 200-250 |
| Introduction | Menjelaskan pentingnya deteksi email spam, perkembangan metode klasifikasi, kesenjangan penelitian, rumusan masalah, tujuan penelitian, dan kontribusi penelitian. | 500-700 |
| Related Work |Membahas penelitian terdahulu mengenai klasifikasi email spam menggunakan Naive Bayes, KNN, dan metode machine learning lainnya serta menunjukkan research gap yang menjadi dasar penelitian ini| 700-1000 |
| Method |Menjelaskan dataset SpamAssassin, preprocessing (case folding, tokenization, stopword removal, TF-IDF), implementasi Naive Bayes dan KNN, serta metode evaluasi menggunakan confusion matrix dan F1-Score.| 800-1200 |
| Results |Menyajikan tabel dan grafik hasil Accuracy, Precision, Recall, F1-Score, serta waktu komputasi dari kedua algoritma berdasarkan lima kali percobaan.| 500-800 |
| Discussion |Menginterpretasikan hasil eksperimen, membandingkan dengan penelitian sebelumnya, menjelaskan kelebihan Naive Bayes, keterbatasan penelitian, serta implikasi hasil penelitian.| 600-900 |
| Conclusion |Menyimpulkan bahwa Naive Bayes memberikan performa terbaik pada SpamAssassin Dataset serta memberikan saran penelitian selanjutnya menggunakan dataset yang lebih beragam dan algoritma tambahan.| 200-400 |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

|  | Intro | Method | Result | Discussion | Conclusion |
|--|-------|--------|--------|-----------|-----------|
| *Contoh: RQ1* | *✓* | *✓* | *✓* | *✓* | *✓* |
| *Contoh: Metrik-X* | *✗ ←* | *✗ ←* | *✓* | *✗ ←* | *✗ ←* |
| RQ1 |✓|✓|✓|✓|✓|
| RQ2 |✓|✓|✓|✓|✓|
| Metrik utama |✓|✓|✓|✓|✓|
| Variabel IV |✓|✓|✓|✓|✓|
| Variabel DV |✓|✓|✓|✓|✓||
| Klaim/kontribusi |✓|✓|✓|✓|✓|

**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan:**
> Tidak ditemukan inkonsistensi. Seluruh Research Question, variabel penelitian, metrik evaluasi, serta kontribusi penelitian telah dibahas secara konsisten pada setiap bagian paper.

**Tindakan perbaikan:**
> Tetap melakukan pengecekan ulang setiap revisi agar seluruh bagian paper tetap konsisten dan tidak terjadi perubahan istilah maupun variabel penelitian.
---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:**
> (Penelitian ini membandingkan algoritma Naive Bayes dan K-Nearest Neighbor untuk mengetahui algoritma yang mempunyai performa lebih baik dalam klasifikasi email spam. Hasil penelitian menunjukkan bahwa Naive Bayes mempunyai hasil yang lebih baik dibandingkan KNN sehingga dapat digunakan sebagai metode klasifikasi email spam.)

| Kriteria | Evaluasi | Perbaikan |
|----------|---------|-----------|
| Clarity | Kalimat cukup jelas tetapi belum menyebutkan metrik evaluasi yang digunakan. | Menambahkan informasi mengenai metrik Accuracy, Precision, Recall, dan F1-Score. |
| Precision |Istilah "hasil lebih baik" masih umum.|Diganti menjadi "memperoleh nilai F1-Score dan Accuracy lebih tinggi".|
| Conciseness |Terdapat pengulangan frasa "algoritma".|Menggabungkan beberapa kalimat agar lebih ringkas.|

**Paragraf setelah perbaikan:**
> (Penelitian ini membandingkan performa algoritma Naive Bayes dan K-Nearest Neighbor dalam klasifikasi email spam menggunakan SpamAssassin Dataset. Evaluasi dilakukan berdasarkan nilai Accuracy, Precision, Recall, dan F1-Score. Hasil eksperimen menunjukkan bahwa Naive Bayes memperoleh nilai Accuracy dan F1-Score yang lebih tinggi dibandingkan K-Nearest Neighbor sehingga lebih efektif digunakan untuk klasifikasi email spam pada dataset yang digunakan.)

---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> Menulis tentang riset hanya menjelaskan proses atau hasil penelitian secara deskriptif, sedangkan menulis sebagai argumen riset berarti menyusun seluruh isi penelitian secara logis untuk membuktikan bahwa metode yang digunakan mampu menjawab rumusan masalah dan memberikan kontribusi ilmiah. Setiap bagian dalam paper harus saling berkaitan mulai dari latar belakang, metode, hasil, hingga kesimpulan.
> Urutan penulisan Method → Results → Discussion → Introduction membantu menghasilkan tulisan yang lebih konsisten karena peneliti telah mengetahui proses dan hasil penelitian terlebih dahulu. Dengan demikian, pendahuluan dapat disusun sesuai dengan temuan yang diperoleh sehingga seluruh isi paper memiliki alur yang jelas, tidak bertentangan, dan lebih mudah dipahami oleh pembaca.
