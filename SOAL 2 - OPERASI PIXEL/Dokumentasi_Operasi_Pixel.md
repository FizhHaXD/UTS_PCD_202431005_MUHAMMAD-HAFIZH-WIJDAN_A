# Dokumentasi Pengolahan Citra: Operasi Kecerahan dan Kontras

### 1. Import Library
**Tujuan:** Memuat pustaka (library) Python yang dibutuhkan untuk pengolahan citra.
*   `cv2` (OpenCV): Digunakan untuk membaca matriks gambar dari direktori komputer.
*   `numpy` (sebagai `np`): Digunakan untuk manipulasi array dan matriks secara efisien, serta mengatur tipe data matematis pada piksel gambar.
*   `matplotlib.pyplot` (sebagai `plt`): Digunakan untuk melakukan *plotting*, menampilkan gambar, dan membuat grafik histogram.

### 2. Membaca Data & Menampilkan Gambar 1 (Asli)
**Penjelasan Logika:**
Pada tahapan ini, citra foto dengan efek *backlight* (latar belakang sangat terang, profil gelap) dibaca ke dalam memori menggunakan `cv2.imread()`. Secara *default*, OpenCV membaca gambar dalam format warna **BGR** (Blue-Green-Red). Agar gambar tidak terlihat kebiruan ketika ditampilkan dengan Matplotlib, dilakukan konversi ruang warna dari BGR ke **RGB** menggunakan perintah `cv2.cvtColor()`.
Selanjutnya, dimensi gambar (jumlah baris dan kolom piksel) disimpan untuk kebutuhan proses *looping* di tahap berikutnya. Citra asli ditampilkan berdampingan dengan histogramnya untuk menganalisis distribusi intensitas cahaya sebelum diproses.

### 3. Gambar 2: Konversi ke Grayscale (Keabuan)
**Penjelasan Logika:**
Gambar berwarna (RGB) yang memiliki 3 *channel* dikonversi menjadi gambar *grayscale* (1 *channel*) secara manual melalui proses perulangan bersarang (*nested loop*). 
Rumus yang digunakan adalah pendekatan standar luminansi televisi (NTSC):
`f(x,y) = 0.299 * R + 0.587 * G + 0.114 * B`

Nilai desimal (R, G, B) yang memiliki bobot berbeda tersebut ditambahkan dan diubah menjadi *integer* untuk merepresentasikan tingkat keabuan mata manusia. Hasil dari langkah ini menjadi citra dasar `f(x,y)` untuk diproses pada tahap kecerahan dan kontras.

### 4. Gambar 3: Operasi Kecerahan (Penambahan Nilai Beta)
**Penjelasan Logika:**
Operasi kecerahan bertujuan untuk mengangkat intensitas cahaya, terutama pada area profil wajah/tubuh yang gelap akibat *backlight*. Hal ini dilakukan dengan menambahkan nilai skalar **Beta** (β = 60) ke setiap piksel. 
Rumus yang digunakan: `g(x,y) = f(x,y) + β`

**Mekanisme Pencegahan Color Burn:**
Pada saat penambahan, tipe data `uint8` (bernilai 0-255) memiliki kelemahan *integer overflow*. Apabila piksel langit (misal: 200) ditambah 60, hasilnya adalah 260. Karena kapasitas `uint8` hanya sampai 255, komputer akan meresetnya menjadi angka 4 (menjadi hitam/abu-abu gelap). Fenomena *error* matematis inilah penyebab utama *color burn* parah pada gambar. 
Oleh karena itu, kode melakukan *casting* (mengubah sementara tipe data piksel ke `float` sebelum operasi matematika), lalu memotong paksa nilainya di batas maksimum 255 menggunakan perintah `np.clip()`.

### 5. Gambar 4: Operasi Kontras (Perkalian dengan Alpha)
**Penjelasan Logika:**
Operasi kontras bertujuan untuk memperlebar jarak/rentang intensitas antar piksel sehingga perbedaan antara area gelap dan terang semakin tajam. Hal ini dilakukan dengan mengalikan setiap intensitas piksel dengan nilai skalar **Alpha** (α = 1.4). 
Rumus yang digunakan: `g(x,y) = f(x,y) * α`

Serupa dengan operasi kecerahan, setiap nilai piksel dikonversi ke `float` terlebih dahulu. Setelah dikalikan, nilai yang melebihi batas 255 akan dipangkas secara aman oleh fungsi `np.clip()` agar tidak terjadi *color burn* (terbakar warna yang mengakibatkan gambar rusak/pecah).

### 6. Gambar 5: Operasi Gabungan (Logika Piecewise Linear)
**Penjelasan Logika:**
Tahap ini adalah implementasi utama untuk menjawab studi kasus *"meningkatkan kontras di area gelap dan mengurangi kontras di area terang"*. Operasi gabungan linear biasa `(alpha * f(x,y) + beta)` tidak cukup karena akan membuat langit yang sudah terang dipaksa menjadi lebih putih solid, yang merusak detail langit (kualitas visual menurun).

Sebagai solusinya, diterapkan algoritma **Piecewise Linear Transformation** menggunakan kondisi *If-Else*:
1.  **Jika Intensitas Piksel < 128 (Area Gelap / Profil):**
    Di area wajah dan baju, diterapkan α > 1 (misal 1.5) untuk **meningkatkan kontras** sehingga tekstur profil terlihat jelas, dan ditambahkan nilai β yang besar (misal 40) untuk mencerahkan bayangan gelapnya.
2.  **Jika Intensitas Piksel ≥ 128 (Area Terang / Langit Latar Belakang):**
    Di area latar belakang, diterapkan α < 1 (misal 0.5) untuk **mengurangi kontras**. Pengurangan kontras di area ini berfungsi untuk menekan rentang piksel langit agar tidak menabrak batas 255 (mencegah *color burn*). Dengan penyesuaian nilai skalar ini, detail awan dan langit terang tetap terselamatkan secara wajar.

Hasil akhirnya disatukan dengan `np.clip()` untuk merender gambar yang harmonis: profil tubuh bagian depan terlihat jelas dan menonjol, sementara *background* matahari terbenam/langit tetap memiliki detail visual yang tidak terbakar.
