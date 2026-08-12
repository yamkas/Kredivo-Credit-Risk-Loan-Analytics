## 1. Background & Business Problems

Perusahaan fintech lending seperti Kredivo menghadapi tantangan dalam menjaga keseimbangan antara **pertumbuhan penyaluran pinjaman dan kualitas portofolio kredit**. Peningkatan jumlah serta nilai pinjaman dapat meningkatkan potensi pendapatan perusahaan, tetapi pada saat yang sama juga meningkatkan exposure terhadap risiko gagal bayar.

Berdasarkan dataset sintesis yang dipakai, terdapat **50.000 data pinjaman** dengan informasi mengenai karakteristik peminjam, kondisi finansial, karakteristik pinjaman, serta status gagal bayar. Dari keseluruhan data tersebut, terdapat **9.863 pinjaman atau sekitar 19,73%** yang tercatat mengalami gagal bayar.

Kondisi tersebut menunjukkan adanya kebutuhan untuk memahami **karakteristik borrower dan karakteristik pinjaman yang berkaitan dengan risiko gagal bayar**, sehingga perusahaan dapat mengidentifikasi kelompok dengan tingkat risiko yang relatif lebih tinggi.

Untuk mendiagnosis akar masalah bisnis secara terstruktur, analisis akan menggunakan pendekatan **Framework 5 Whys**.

### 5 Whys — Root Cause Analysis

1. **Why 1: Mengapa perusahaan perlu memperhatikan risiko gagal bayar?**

   * *Jawaban:* Karena gagal bayar dapat meningkatkan risiko kerugian dan menurunkan kualitas portofolio pinjaman perusahaan.

2. **Why 2: Mengapa risiko gagal bayar dapat berbeda antar peminjam?**

   * *Jawaban:* Karena setiap peminjam memiliki karakteristik finansial dan profil kredit yang berbeda, seperti pendapatan, skor kredit, rasio DTI, serta kondisi pekerjaan.

3. **Why 3: Mengapa karakteristik finansial dan profil kredit perlu dianalisis?**

   * *Jawaban:* Karena perbedaan karakteristik tersebut dapat membentuk kelompok peminjam dengan tingkat risiko gagal bayar yang berbeda.

4. **Why 4: Mengapa perusahaan perlu mengidentifikasi kelompok peminjam berisiko tinggi?**

   * *Jawaban:* Karena informasi tersebut dapat membantu perusahaan menentukan prioritas evaluasi kredit dan strategi mitigasi risiko pada segmen yang memiliki tingkat risiko relatif lebih tinggi.

5. **Why 5 (Akar Masalah Utama):**

   * *Kesimpulan:* Perusahaan membutuhkan pemahaman yang lebih terstruktur mengenai **profil borrower dan karakteristik pinjaman yang berkaitan dengan gagal bayar**, agar pengelolaan risiko kredit dapat dilakukan berdasarkan karakteristik dan segmen risiko, bukan hanya berdasarkan jumlah pinjaman secara keseluruhan.

---

## 2. Business Questions

Berdasarkan masalah bisnis dan akar masalah di atas, analisis data ini akan difokuskan untuk menjawab **10 pertanyaan bisnis strategis** berikut:

1. **BQ 1 (Portfolio Risk):** Berapa tingkat gagal bayar (*default rate*) pada keseluruhan portofolio pinjaman?

   * *Metrik:* `Gagal_Bayar`, `ID_Pinjaman`

2. **BQ 2 (Credit Score):** Bagaimana tingkat gagal bayar berdasarkan kelompok skor kredit peminjam?

   * *Metrik:* `Skor_Kredit`, `Gagal_Bayar`

3. **BQ 3 (Debt Burden):** Bagaimana hubungan antara rasio DTI (*Debt-to-Income Ratio*) dengan tingkat gagal bayar?

   * *Metrik:* `Rasio_DTI`, `Gagal_Bayar`

4. **BQ 4 (Income & Risk):** Bagaimana tingkat gagal bayar berdasarkan kelompok pendapatan peminjam?

   * *Metrik:* `Pendapatan`, `Gagal_Bayar`

5. **BQ 5 (Loan Exposure):** Bagaimana tingkat gagal bayar berdasarkan besarnya jumlah pinjaman yang diberikan?

   * *Metrik:* `Jumlah_Pinjaman`, `Gagal_Bayar`

6. **BQ 6 (Interest Rate):** Apakah terdapat perbedaan tingkat gagal bayar pada kelompok suku bunga pinjaman yang berbeda?

   * *Metrik:* `Suku_Bunga`, `Gagal_Bayar`

7. **BQ 7 (Loan Term):** Bagaimana tingkat gagal bayar berdasarkan jangka waktu pinjaman?

   * *Metrik:* `Jangka_Waktu_Pinjaman`, `Gagal_Bayar`

8. **BQ 8 (Employment Profile):** Bagaimana tingkat gagal bayar berdasarkan jenis pekerjaan dan lama bekerja peminjam?

   * *Metrik:* `Jenis_Pekerjaan`, `Lama_Bekerja_Bulan`, `Gagal_Bayar`

9. **BQ 9 (Borrower Profile):** Bagaimana tingkat gagal bayar berdasarkan karakteristik demografis dan kondisi keluarga peminjam?

   * *Metrik:* `Usia`, `Pendidikan`, `Status_Pernikahan`, `Memiliki_Tanggungan`, `Gagal_Bayar`

10. **BQ 10 (Risk Segmentation):** Seperti apa karakteristik segmen peminjam yang memiliki tingkat gagal bayar paling tinggi?

    * *Metrik:* `Skor_Kredit`, `Rasio_DTI`, `Pendapatan`, `Jumlah_Pinjaman`, `Suku_Bunga`, `Jenis_Pekerjaan`, `Gagal_Bayar`

---

## 3. Stakeholder Identification

Hasil analisis data dan rancangan dashboard ditujukan kepada pihak-pihak internal berikut untuk mendukung pengambilan keputusan berbasis data (*data-driven decision making*):

* **Credit Risk Manager:** Menggunakan analisis risiko untuk mengidentifikasi karakteristik dan segmen borrower dengan tingkat gagal bayar relatif tinggi serta menentukan prioritas mitigasi risiko.

* **Credit / Loan Underwriting Team:** Menggunakan informasi mengenai credit score, DTI, pendapatan, dan karakteristik borrower sebagai bahan evaluasi dalam proses penilaian kredit.

* **Business / Product Manager:** Menggunakan analisis portofolio untuk memahami keseimbangan antara volume pinjaman, nilai exposure, dan tingkat risiko.

* **Head of Lending / Management:** Menggunakan KPI dan ringkasan performa risiko untuk mengevaluasi kualitas portofolio serta menentukan kebijakan strategis terkait pertumbuhan lending dan pengelolaan risiko.

### Primary Stakeholder

> **Credit Risk Manager**

Stakeholder utama dipilih karena fokus utama project adalah **mengidentifikasi pola dan segmen risiko gagal bayar** untuk mendukung pengelolaan kualitas portofolio kredit.

---

## 4. Scope of Work (SOW) & Data Selection

Untuk menjaga analisis tetap fokus, terukur, dan menghindari perluasan masalah (*scope creep*), project dibatasi pada analisis **deskriptif dan diagnostik terhadap risiko gagal bayar** berdasarkan data borrower dan karakteristik pinjaman.

Dataset terdiri dari **50.000 data pinjaman dan 18 kolom**. Seluruh variabel akan terlebih dahulu dievaluasi berdasarkan relevansi terhadap pertanyaan bisnis sebelum digunakan dalam analisis.

### 🟩 A. Scope of Variables Used

#### 1. Loan & Risk Variables

1. **`Gagal_Bayar`** *(Numerik/Biner)*: Target utama yang menunjukkan status gagal bayar peminjam. Digunakan sebagai indikator utama untuk mengukur risiko kredit.

2. **`Skor_Kredit`** *(Numerik)*: Indikator profil kredit peminjam yang digunakan untuk menganalisis perbedaan tingkat risiko berdasarkan kualitas kredit.

3. **`Rasio_DTI`** *(Numerik)*: Rasio beban utang terhadap pendapatan yang digunakan untuk mengevaluasi kemampuan finansial peminjam dalam menanggung kewajiban utang.

4. **`Jumlah_Pinjaman`** *(Numerik)*: Nilai nominal pinjaman yang digunakan untuk mengukur loan exposure dan menganalisis risiko berdasarkan besarnya pinjaman.

5. **`Suku_Bunga`** *(Numerik)*: Tingkat bunga pinjaman yang digunakan untuk menganalisis perbedaan risiko berdasarkan biaya pinjaman.

6. **`Jangka_Waktu_Pinjaman`** *(Numerik/Kategori)*: Durasi pinjaman dalam bulan yang digunakan untuk melihat hubungan antara tenor dan risiko gagal bayar.

#### 2. Financial & Employment Variables

7. **`Pendapatan`** *(Numerik)*: Pendapatan peminjam yang digunakan untuk menganalisis kapasitas finansial dan perbedaan tingkat risiko berdasarkan income segment.

8. **`Lama_Bekerja_Bulan`** *(Numerik)*: Lama masa kerja peminjam yang digunakan sebagai salah satu indikator stabilitas pekerjaan.

9. **`Jumlah_Garis_Kredit`** *(Numerik)*: Jumlah credit line yang dimiliki peminjam, digunakan sebagai informasi tambahan dalam memahami profil kredit.

10. **`Jenis_Pekerjaan`** *(Kategori)*: Jenis pekerjaan peminjam yang digunakan untuk membandingkan risiko berdasarkan employment profile.

#### 3. Demographic & Personal Variables

11. **`Usia`** *(Numerik)*: Usia peminjam yang digunakan untuk menganalisis perbedaan profil risiko berdasarkan kelompok usia.

12. **`Pendidikan`** *(Kategori)*: Tingkat pendidikan peminjam yang digunakan untuk melihat karakteristik risiko berdasarkan education profile.

13. **`Status_Pernikahan`** *(Kategori)*: Status pernikahan peminjam yang digunakan sebagai variabel demografis dalam analisis borrower profile.

14. **`Memiliki_Hipotek`** *(Kategori)*: Status kepemilikan hipotek yang digunakan untuk memahami kondisi finansial dan aset peminjam.

15. **`Memiliki_Tanggungan`** *(Kategori)*: Status kepemilikan tanggungan yang digunakan untuk menganalisis kondisi keluarga peminjam.

16. **`Memiliki_Penjamin`** *(Kategori)*: Status keberadaan penjamin yang digunakan sebagai karakteristik tambahan dalam analisis risiko.

17. **`Tujuan_Pinjaman`** *(Kategori)*: Tujuan penggunaan pinjaman yang digunakan untuk membandingkan tingkat risiko antar loan purpose.

18. **`ID_Pinjaman`** *(Identifier)*: ID unik pinjaman yang digunakan untuk identifikasi dan penghitungan jumlah observasi, bukan sebagai variabel analisis risiko.

### 🟥 B. Out of Scope

* **No Real-Time Credit Monitoring:** Analisis bersifat *static snapshot* berdasarkan dataset 50.000 pinjaman yang tersedia. Tidak mencakup monitoring perubahan status kredit secara real-time.

* **No Predictive Credit Scoring:** Project tidak membangun model Machine Learning untuk memprediksi apakah borrower akan gagal bayar. Fokus utama adalah **Descriptive & Diagnostic Analytics**.

* **No Fraud Detection:** Analisis tidak ditujukan untuk mendeteksi fraudulent applications atau aktivitas penipuan karena tidak terdapat indikator fraud yang menjadi fokus utama dataset.

* **No Profitability Analysis:** Project tidak menghitung profitabilitas perusahaan secara keseluruhan karena dataset tidak menyediakan komponen seperti COGS, operating cost, revenue recognition, atau net profit.

* **No Customer Lifetime Value Analysis:** Analisis tidak menghitung Customer Lifetime Value karena dataset berfokus pada data pinjaman dan status gagal bayar, bukan histori hubungan pelanggan secara longitudinal.

* **No Loan Approval Automation:** Hasil analisis tidak digunakan sebagai sistem otomatis untuk menyetujui atau menolak pengajuan pinjaman. Insight hanya digunakan sebagai dasar pendukung pengambilan keputusan.

---

## 5. KPI Utama Bisnis & Target Sukses

KPI berikut digunakan untuk mengukur kondisi portofolio dan mengevaluasi keberhasilan analisis risiko.

| Pertanyaan Bisnis (BQs)      | KPI Utama Bisnis                                                                               | Target / Success Criteria                                                                                                     |
| ---------------------------- | ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **BQ 1: Portfolio Risk**     | **Default Rate**<br>(Persentase pinjaman yang mengalami gagal bayar)                           | Menetapkan baseline *default rate* portofolio dan mengidentifikasi segmen yang memiliki tingkat gagal bayar di atas baseline. |
| **BQ 2: Credit Score**       | **Default Rate by Credit Score**<br>(Tingkat gagal bayar berdasarkan kelompok skor kredit)     | Mengidentifikasi kelompok skor kredit dengan risiko gagal bayar paling tinggi dan paling rendah.                              |
| **BQ 3: Debt Burden**        | **Default Rate by DTI**<br>(Tingkat gagal bayar berdasarkan rasio DTI)                         | Mengidentifikasi kelompok DTI yang memiliki tingkat gagal bayar relatif tinggi dibandingkan baseline portofolio.              |
| **BQ 4: Income & Risk**      | **Default Rate by Income Segment**<br>(Tingkat gagal bayar berdasarkan kelompok pendapatan)    | Mengidentifikasi kelompok pendapatan dengan risiko gagal bayar relatif tinggi.                                                |
| **BQ 5: Loan Exposure**      | **Default Exposure**<br>(Total nominal pinjaman dari pinjaman yang gagal bayar)                | Mengidentifikasi segmen yang memberikan kontribusi exposure gagal bayar terbesar.                                             |
| **BQ 6: Interest Rate**      | **Default Rate by Interest Rate**<br>(Tingkat gagal bayar berdasarkan kelompok suku bunga)     | Mengidentifikasi kelompok suku bunga dengan tingkat risiko relatif lebih tinggi.                                              |
| **BQ 7: Loan Term**          | **Default Rate by Loan Term**<br>(Tingkat gagal bayar berdasarkan tenor)                       | Mengidentifikasi tenor pinjaman yang memiliki tingkat gagal bayar relatif tinggi.                                             |
| **BQ 8: Employment Profile** | **Default Rate by Employment**<br>(Tingkat gagal bayar berdasarkan jenis dan masa kerja)       | Mengidentifikasi employment segment dengan tingkat risiko relatif tinggi.                                                     |
| **BQ 9: Borrower Profile**   | **Default Rate by Demographic Segment**<br>(Tingkat gagal bayar berdasarkan profil demografis) | Mengidentifikasi karakteristik borrower yang menunjukkan perbedaan risiko paling signifikan.                                  |
| **BQ 10: Risk Segmentation** | **High-Risk Segment Rate**<br>(Proporsi portfolio yang berada pada segmen risiko tinggi)       | Menghasilkan segmentasi borrower yang jelas berdasarkan kombinasi faktor risiko utama untuk men dukung strategi mitigasi.     |
> **Catatan:** Target numerik seperti "default rate harus turun 10%" sebaiknya **tidak kita tetapkan secara sembarangan**. Untuk project portfolio ini, kita terlebih dahulu menggunakan data sebagai *baseline*, kemudian target numerik dapat ditentukan setelah mengetahui kondisi aktual dan benchmark bisnis yang relevan.
