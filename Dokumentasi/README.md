## 🧩 **Metodologi Klasifikasi Email Spam Menggunakan Naive Bayes**

Metodologi ini terdiri dari beberapa tahapan utama:

1. pengumpulan data, 2) preprocessing, 3) ekstraksi fitur,
2. pelatihan model, 5) evaluasi, dan 6) implementasi/prediksi.

---

## **1. Pengumpulan & Pemahaman Dataset**

Dataset biasanya berupa email dengan label:

* **Spam**
* **Ham** (non-spam)

Format dataset bisa berupa:

* CSV (`text`, `label`)
* Raw email (*.eml)
* Public dataset seperti Enron, Ling-Spam, SpamAssassin

Pada tahap ini dilakukan:

* Analisis distribusi kelas (spam vs ham)
* Memeriksa kualitas teks (noise, HTML, simbol, karakter aneh)
* Memeriksa apakah dataset imbalance

Tujuan: mengetahui kondisi awal data untuk menentukan teknik preprocessing.

---

## **2. Text Preprocessing (Pembersihan Teks)**

Teks email mentah biasanya:

* Ada HTML
* URL panjang
* Email address
* Angka, tanda baca
* Case campuran (uppercase/lowercase)

Tahapan preprocessing umum:

### **a. Lowercasing**

Semua huruf jadi kecil → “FREE” = “free”.

### **b. Remove HTML tags**

Gunakan regex atau parser.

### **c. Hapus URL, email, angka, dan simbol tidak relevan**

Karena cenderung tidak informatif.

### **d. Tokenization**

Memecah teks menjadi kata-kata.

### **e. Stopword removal**

Menghapus kata-kata umum seperti “the”, “and”, “you”.

### **f. Stemming atau Lemmatization**

Mengubah kata ke bentuk dasarnya:
“running” → “run”, “better” → “good”

Tujuan preprocessing adalah membuat teks lebih bersih dan konsisten sehingga Naive Bayes dapat menangkap pola statistik dengan akurat.

---

## **3. Ekstraksi Fitur**

Teks perlu diubah menjadi angka. Dua metode paling populer:

### **A. Bag of Words (CountVectorizer)**

Menghitung frekuensi kata dalam email.

Contoh:
email = "free money click"
fitur = {free:1, money:1, click:1}

### **B. TF-IDF (Term Frequency - Inverse Document Frequency)**

Memberikan bobot lebih tinggi ke kata yang unik dan penting.

TF-IDF sangat umum dipakai untuk algoritma Naive Bayes karena:

* Mengurangi pengaruh kata yang terlalu umum
* Memperkuat kata-kata yang menjadi indikator spam (misal: "free", "winner")

### Bentuk Matriks:

Setiap email → vektor fitur
Model → bekerja pada statistik kemunculan kata

---

## **4. Pemilihan Algoritma Naive Bayes**

Untuk teks, jenis paling cocok adalah:

### **Multinomial Naive Bayes**

Kenapa?

* Dirancang untuk data frekuensi kata
* Sangat cepat
* Biasanya performa bagus untuk spam detection
* Tidak mudah overfitting

Model bekerja dengan:

* Menghitung probabilitas setiap kata muncul pada kelas spam dan ham
* Memakai Teorema Bayes untuk menghitung P(spam | email)

---

# **5. Training / Pelatihan Model**

Pada tahap ini:

* Dataset dibagi menjadi training dan testing (misal 80:20)
* Model mempelajari pola kata yang sering muncul di spam vs ham

Contoh pola yang biasanya dipelajari:

* Kata "free", "winner", "cash", "promo" → muncul sering di spam
* Kata "meeting", "project", "update" → banyak di non-spam

Model menghitung:

* Likelihood kata per kelas
* Prior probability kelas

Hasilnya adalah model Naive Bayes siap memprediksi.

---

# **6. Evaluasi Model**

Mengukur kemampuan model memprediksi email yang belum pernah dilihat.

Metrics umum:

### **Accuracy**

Persentase prediksi benar.

### **Precision (Spam)**

Seberapa sering prediksi spam benar
(penting agar email penting tidak masuk spam!)

### **Recall / Sensitivity**

Seberapa banyak spam yang berhasil terdeteksi.

### **F1-Score**

Rata-rata harmonik Precision & Recall.

### **Confusion Matrix**

Menunjukkan:

* Benar spam
* Benar ham
* Spam yang dianggap ham (false negative)
* Ham yang dianggap spam (false positive)

Dalam kasus email, **false positive** sangat penting untuk diminimalkan.

---

# **7. Implementasi / Prediksi**

Tahap ini biasanya dipakai untuk sistem nyata:

1. Input email baru
2. Jalankan preprocessing
3. Convert ke TF-IDF vector
4. Model Naive Bayes memprediksi:

   * `spam`
   * `ham`

Tambahan opsional:

* Confidence score
* Threshold tuning (menaikkan sensitivitas spam)

---

# **8. Deployment (opsional)**

Jika mau pakai di sistem nyata:

* Bungkus model ke API (Flask/FastAPI)
* Atur pipeline preprocessing otomatis
* Simpan model + vectorizer
* Terapkan ke sistem email server atau aplikasi

---

# 📌 **Ringkasan Sederhana Alur Naive Bayes Spam Filter**

1. **Dataset**
2. **Preprocessing**
3. **TF-IDF**
4. **Train Naive Bayes**
5. **Evaluate**
6. **Deploy / Predict**

---
