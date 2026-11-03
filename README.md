# Analisis Tren dan Pola Musiman Penyewaan Sepeda

**Midterm Project — CAK4XBB3 Visualisasi Data · Kelompok 3 · Telkom University**

Analisis *time series* data penyewaan sepeda Capital Bikeshare (Washington D.C.) tahun 2011–2012 untuk melihat tren jangka panjang, pola musiman (bulanan dan mingguan), perbedaan perilaku penyewa *registered* dan *casual*, serta pengaruh kondisi hari dan cuaca terhadap jumlah penyewaan.

## Anggota Kelompok

| Nama | NIM |
|---|---|
| Alexandra Yohana Junita S | 103012430049 |
| Jeffry Kurniawan Visnu | 103012300186 |
| Fransisca Anggraeni Hartakaadi | 103012300366 |
| Naufal Raja Pradiptya Pribadi | 103012300235 |
| Godwin Halley Wattimena | 103012580020 |

## Dataset

- **Nama:** Bike Sharing Dataset — Fanaee-T & Gama (2013)
- **Sumber:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset)
- **File yang dipakai:** `day.csv` (data harian, 731 observasi, 1 Jan 2011 – 31 Des 2012)
- **Variabel utama:**
  - `cnt`: total penyewaan per hari (`casual` + `registered`)
  - `casual`: penyewa non-member
  - `registered`: penyewa member terdaftar
  - `temp`, `weathersit`, `season`, `workingday`, `holiday`: kondisi hari

Data sudah bersih: tidak ada *missing value*, tanggal duplikat, atau tanggal yang hilang.

## Pertanyaan Analisis

1. Bagaimana tren jangka panjang penyewaan sepeda selama dua tahun?
2. Apakah ada pola musiman, baik bulanan maupun mingguan?
3. Bagaimana perbedaan perilaku penyewa *registered* dan *casual*?
4. Bagaimana kondisi hari (hari kerja, libur, cuaca) memengaruhi jumlah penyewaan?

## Isi Notebook

| No | Bagian | Keterangan |
|---|---|---|
| 1 | Import library & pengaturan visual | pandas, numpy, matplotlib, seaborn |
| 2 | Load data | Membaca `day.csv`, atau mengunduhnya otomatis dari UCI jika belum ada |
| 3 | Cleaning & persiapan data | *Parse* tanggal, cek *missing*/duplikat, konversi suhu ke °C |
| 4 | Line plot | Penyewaan harian beserta titik tertinggi dan terendah |
| 5 | Area plot | Akumulasi mingguan *casual* vs *registered* |
| 6 | Multiple time series | *Registered* vs *casual* (rolling 7 hari) dengan *direct labeling* |
| 7 | Seasonal plot | Pola bulanan 2011 vs 2012, pola hari dalam seminggu, *calendar heatmap* |
| 8 | Analisis tren | *Moving average* 7 & 30 hari, *linear* & *polynomial fit* (`numpy.polyfit`) |
| 9 | Statistik pendukung | Pengaruh hari kerja, musim, dan cuaca |
| 10 | Komponen time series | Identifikasi *trend*, *seasonality*, *cyclic*, *noise* |
| 11–12 | Insight & kesimpulan | Ringkasan temuan dan keterbatasan |

## Insight Utama

1. **Pertumbuhan pesat.** Total penyewaan naik **64,9%**, dari 1,24 juta (2011) menjadi 2,05 juta (2012). Rata-rata harian naik dari 3.406 menjadi 5.600 sewa.
2. **Musim adalah penggerak terbesar.** Januari selalu menjadi bulan terendah. Rata-rata musim *Fall* (5.644/hari) lebih dari dua kali musim *Spring* (2.604/hari). Korelasi suhu dengan penyewaan **r = 0,63**.
3. **Dua tipe penyewa.** *Registered* (81,2% dari total) berpola komuter, tinggi di hari kerja. *Casual* berpola rekreasi: penyewaan hari Sabtu sekitar 2,7× hari Rabu.
4. **Cuaca buruk memicu anomali.** Hari terendah adalah 29 Okt 2012 dengan 22 sewa, bertepatan dengan Badai Sandy. Hari hujan/salju rata-rata 63% lebih rendah dari hari cerah.
5. **Pertumbuhan terbesar di bulan dingin.** Januari naik +153% dan Maret +157% (2012 vs 2011), sedangkan bulan puncak hanya naik 41–44%.
6. **Puncak musiman bergeser** dari Juni (2011) ke September (2012). Hari tersibuk adalah Sabtu, 15 Sep 2012 dengan 8.714 sewa.

**Kesimpulan:** data merupakan gabungan tren naik yang kuat, musiman tahunan yang jelas, dan pola mingguan yang membedakan penyewa komuter dan rekreasi. *Noise* terbesar berasal dari cuaca ekstrem.

## Struktur Repository

```
.
├── Kelompok_3_Midterm_Project_Bikesharing.ipynb   # notebook utama
├── day.csv                                        # data harian (dipakai di analisis)
├── hour.csv                                       # data per jam (belum dipakai)
├── Readme.txt                                     # deskripsi dataset asli dari UCI
└── README.md
```

## Cara Menjalankan

**Google Colab**

1. Buka notebook di [Google Colab](https://colab.research.google.com/).
2. Upload `day.csv` lewat panel file di sebelah kiri. Jika file tidak di-upload, notebook akan mencoba mengunduhnya langsung dari UCI.
3. Jalankan semua sel (*Runtime → Run all*).

**Lokal**

```bash
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook Kelompok_3_Midterm_Project_Bikesharing.ipynb
```

## Keterbatasan & Pengembangan

- Data hanya mencakup 2 tahun, sehingga komponen *cyclic* belum dapat diidentifikasi.
- Konteks Badai Sandy dan hari libur nasional AS berasal dari pengetahuan umum, bukan dari kolom dataset.
- Pengembangan berikutnya: memakai `hour.csv` untuk melihat pola jam sibuk.

## Deklarasi Penggunaan AI

Kelompok ini menggunakan alat AI generatif (Claude) untuk membantu memahami tugas, eksplorasi dataset, pembuatan visualisasi, dan penyusunan narasi interpretasi. Rincian lengkap dan *screenshot prompting* tersedia di bagian akhir notebook.

## Referensi

- Fanaee-T, H., & Gama, J. (2013). Event labeling combining ensemble detectors and background knowledge. *Progress in Artificial Intelligence*, 2(2–3), 113–127.
- UCI Machine Learning Repository — [Bike Sharing Dataset](https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset)
