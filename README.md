
````markdown
# Signature Presence Detection

Mini Project Pengolahan Citra Digital untuk mendeteksi keberadaan tanda tangan Dekan pada citra ijazah.

## Deskripsi

Program ini digunakan untuk mendeteksi apakah suatu area tanda tangan pada citra ijazah memiliki tanda tangan atau tidak.

Tahapan utama yang digunakan dalam program adalah:

1. Crop area tanda tangan Dekan
2. Konversi citra RGB menjadi grayscale
3. Global Thresholding
4. Otsu Thresholding
5. Morphological Opening
6. Morphological Closing
7. Perhitungan jumlah foreground pixel
8. Penentuan kondisi tanda tangan
9. Pengujian citra dengan tanda tangan dan tanpa tanda tangan

Karena seluruh citra ijazah asli yang digunakan memiliki tanda tangan, citra tanpa tanda tangan dibuat sebagai data simulasi dengan menghilangkan area tanda tangan menggunakan teknik inpainting.

---

## Teknologi yang Digunakan

- Python
- OpenCV
- NumPy
- Pandas

---

## Struktur Folder

```text
signature-detection/
│
├── main.py
├── README.md
├── requirements.txt
│
├── citra/
│   ├── 01_HighQuality_Enhanced.jpg
│   ├── 02_LowContrast.jpg
│   ├── 03_Blurred.jpg
│   ├── 04_HighNoise.jpg
│   ├── 05_LowResolution_Upsampled.jpg
│   ├── 06_Faded_Underexposed.jpg
│   ├── 07_ColorShift_WarmTint.jpg
│   ├── 08_JPEGCompression_Artifacts.jpg
│   └── 09_CombinedDegradation.jpg
│
└── hasil/
    ├── ada_ttd/
    ├── tanpa_ttd/
    ├── perbandingan/
    ├── hasil_threshold.csv
    └── hasil_pengujian.csv
````

---

# How to Run

## 1. Clone Repository

Clone repository dari GitHub menggunakan:

```bash
git clone https://github.com/Anisa-whystrn/TUGAS6_PCD_F1G124024.git
```

Masuk ke folder project:

```bash
cd signature-detection
```

---

## 2. Install Library

Install library yang diperlukan:



```bash
pip install opencv-python numpy pandas
```

---

## 3. Pastikan Dataset Berada di Folder `citra`

Masukkan citra ijazah ke dalam folder:

```text
citra/
```

Contoh:

```text
citra/
├── 01_HighQuality_Enhanced.jpg
├── 02_LowContrast.jpg
├── 03_Blurred.jpg
├── 04_HighNoise.jpg
├── 05_LowResolution_Upsampled.jpg
├── 06_Faded_Underexposed.jpg
├── 07_ColorShift_WarmTint.jpg
├── 08_JPEGCompression_Artifacts.jpg
└── 09_CombinedDegradation.jpg
```

---

## 4. Jalankan Program

Jalankan file utama:

```bash
python main.py
```

Program akan membaca seluruh citra yang terdapat pada folder `citra`.

---

## 5. Hasil Program

Setelah program selesai dijalankan, hasil akan disimpan pada folder:

```text
hasil/
```

Hasil terdiri dari:

### `ada_ttd/`

Berisi hasil pengolahan citra asli yang memiliki tanda tangan.

Output yang dihasilkan meliputi:

* Crop area tanda tangan
* Grayscale
* Global Threshold
* Otsu Threshold

### `tanpa_ttd/`

Berisi citra simulasi yang tidak memiliki tanda tangan.

Citra dibuat dengan menghilangkan area tanda tangan menggunakan teknik inpainting.

### `perbandingan/`

Berisi gambar perbandingan:

* Grayscale
* Global Threshold
* Otsu Threshold

Hasil ini digunakan untuk membandingkan kedua metode thresholding.

### `hasil_threshold.csv`

Berisi hasil perhitungan:

* Nama citra
* Kondisi citra
* Metode threshold
* Nilai threshold
* Jumlah foreground pixel
* Persentase foreground pixel

### `hasil_pengujian.csv`

Berisi hasil klasifikasi sistem:

* Kondisi sebenarnya
* Foreground ratio
* Prediksi sistem
* Status benar atau salah

---

# Metode

## 1. Crop

Area yang digunakan adalah area tanda tangan Dekan pada ijazah.

## 2. Grayscale

Citra RGB dikonversi menjadi grayscale untuk menyederhanakan citra menjadi intensitas keabuan.

## 3. Global Threshold

Global threshold menggunakan satu nilai threshold yang telah ditentukan untuk memisahkan foreground dan background.

## 4. Otsu Threshold

Otsu digunakan untuk menentukan nilai threshold secara otomatis berdasarkan histogram citra.

## 5. Morphological Opening

Opening digunakan untuk mengurangi noise atau objek kecil yang tidak diperlukan.

## 6. Morphological Closing

Closing digunakan untuk mengisi celah kecil pada objek hasil thresholding.

## 7. Foreground Pixel

Jumlah pixel foreground dihitung untuk mengetahui karakteristik area hasil segmentasi.

## 8. Klasifikasi

Sistem menggunakan nilai foreground ratio sebagai dasar keputusan:

```text
Foreground >= threshold keputusan
→ SIGNATURE PRESENT

Foreground < threshold keputusan
→ SIGNATURE ABSENT
```

---

# Pengujian

Pengujian dilakukan menggunakan:

* Citra asli yang memiliki tanda tangan
* Citra simulasi yang tidak memiliki tanda tangan

Karena seluruh citra ijazah asli memiliki tanda tangan, data tanpa tanda tangan dibuat dengan menghilangkan area tanda tangan dari citra asli menggunakan teknik inpainting.

---

# Output

Program menghasilkan:

```text
SIGNATURE PRESENT
```

jika sistem mendeteksi keberadaan tanda tangan.

Program menghasilkan:

```text
SIGNATURE ABSENT
```

jika sistem tidak mendeteksi tanda tangan.

Akurasi sistem juga dihitung berdasarkan hasil prediksi terhadap kondisi sebenarnya.

