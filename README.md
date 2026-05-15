# UTS Pengolahan Citra Digital 2025/2026

Repositori ini berisi implementasi program Python untuk memenuhi tugas **Ujian Tengah Semester (UTS)** mata kuliah Pengolahan Citra Digital.  
Proyek membahas penerapan dasar pengolahan citra digital menggunakan Python, mulai dari **deteksi warna, thresholding, segmentasi citra**, hingga **peningkatan kualitas gambar (image enhancement)** pada kondisi backlight.

---

# 👨‍💻 Informasi Mahasiswa

| Data | Keterangan |
|---|---|
| Nama | Muhammad Hafizh Wijdan |
| NIM | 202431005 |
| Kelas | A |
| Program Studi | Teknik Informatika |
| Institut | Institut Teknologi PLN |

---

# 📂 Struktur Repository

```bash
├── SOAL 1 - OPERASI WARNA/
├── SOAL 2 - OPERASI PIXEL/
├── UTS_PCD_202431005_MUHAMMAD_HAFIZH_WIJDAN_A.docx
├── .gitattributes
└── README.md
```

---

# 🚀 SOAL 1 — Operasi Warna

Bagian ini membahas implementasi pengolahan warna dan segmentasi citra digital menggunakan metode thresholding dan clipping.

## ✨ Implementasi

- Ekstraksi channel RGB
- Analisa histogram warna
- Threshold manual
- Threshold Otsu
- Clipping warna
- Operasi bitwise
- Inverse threshold
- Segmentasi warna

---

# 🚀 SOAL 2 — Operasi Pixel

Bagian ini membahas peningkatan kualitas citra digital terutama pada kondisi backlight menggunakan operasi piksel.

## ✨ Implementasi

- Konversi grayscale
- Brightness enhancement
- Contrast stretching
- Piecewise linear transformation
- Pencegahan overflow dengan `np.clip()`

---

# 🛠️ Teknologi dan Library

Library yang digunakan dalam proyek:

| Library | Fungsi |
|---|---|
| OpenCV (`cv2`) | Pengolahan dan manipulasi citra |
| NumPy (`np`) | Operasi matriks dan array |
| Matplotlib (`plt`) | Visualisasi histogram dan gambar |

---

# ⚙️ Cara Menjalankan Program

## 1. Install Dependency

```bash
pip install opencv-python numpy matplotlib
```

---

## 2. Jalankan Program

Buka file `.ipynb` atau `.py` menggunakan:

- Jupyter Notebook
- VSCode
- PyCharm
- Google Colab

Kemudian jalankan program secara berurutan.

---

# 📊 Hasil Implementasi

## SOAL 1
Berhasil melakukan:

- ekstraksi warna,
- thresholding,
- clipping,
- segmentasi warna,
- manipulasi bitwise.

## SOAL 2
Berhasil melakukan:

- peningkatan brightness,
- peningkatan contrast,
- perbaikan citra backlight,
- pengendalian color burn,
- peningkatan detail objek gelap.

---

# 📝 Kesimpulan

Pengolahan citra digital memungkinkan manipulasi visual dilakukan secara matematis menggunakan operasi piksel dan analisa histogram.

Dengan metode seperti thresholding, clipping, brightness adjustment, contrast stretching, dan piecewise transformation, kualitas citra dapat diperbaiki secara signifikan terutama pada kondisi pencahayaan yang tidak ideal seperti backlight.

---

# 📚 Referensi

1. Aulia, R., dkk. (2026). *Peningkatan Kualitas Citra Fotografi menggunakan Histogram Equalization*.
2. Azizah, A. Z. S., dkk. (2024). *Pengolahan Citra Digital Dengan Teknik Ambang Batas*.
3. Heryanto, I. W. A., dkk. (2020). *Segmentasi Warna Dengan Metode Thresholding*.
4. Prayogi, D., dkk. (2025). *Optimalisasi Segmentasi Citra Digital*.
5. Purwanto, D., & Agustiyar. (2024). *Global Thresholding Implementation*.

---

# 📌 Catatan

Proyek ini dibuat untuk keperluan akademik pada mata kuliah **Pengolahan Citra Digital** Tahun Akademik **2025/2026**.
