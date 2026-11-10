<div align="center">

# Dataset Putusan Narkotika
### Direktori Putusan Mahkamah Agung RI · Pidana Khusus · Narkotika dan Psikotropika

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![Colab](https://img.shields.io/badge/Google%20Colab-Notebook-F9AB00?logo=googlecolab&logoColor=white)
![Format](https://img.shields.io/badge/Dataset-PDF%20%2B%20XLSX-2E7D32)
![Putusan](https://img.shields.io/badge/Jumlah%20Putusan-5-blue)
![Bahasa](https://img.shields.io/badge/Bahasa-Indonesia-red)
![Mata Kuliah](https://img.shields.io/badge/Mata%20Kuliah-Temu%20Kembali%20Informasi-6A1B9A)

*Kumpulan putusan pengadilan perkara narkotika beserta ringkasan terstruktur hasil ekstraksi otomatis, disiapkan sebagai dataset untuk penelitian dan praktikum Temu Kembali Informasi (TKI).*

</div>

---

## Daftar Isi

- [Tentang Dataset](#-tentang-dataset)
- [Ringkasan Cepat](#-ringkasan-cepat)
- [Struktur Repositori](#-struktur-repositori)
- [Sumber dan Kriteria Pengumpulan Data](#-sumber-dan-kriteria-pengumpulan-data)
- [Isi Dataset](#-isi-dataset)
- [Kamus Data (Overview.xlsx)](#-kamus-data-overviewxlsx)
- [Contoh Data](#-contoh-data)
- [Bagaimana Dataset Ini Dibuat](#-bagaimana-dataset-ini-dibuat)
- [Aturan Ekstraksi](#-aturan-ekstraksi)
- [Kontrol Kualitas](#-kontrol-kualitas)
- [Cara Menggunakan](#-cara-menggunakan)
- [Potensi Pemanfaatan](#-potensi-pemanfaatan)
- [Keterbatasan](#-keterbatasan)
- [Etika dan Lisensi](#-etika-dan-lisensi)
- [Tim Penyusun](#-tim-penyusun)
- [Sitasi](#-sitasi)

---

## Tentang Dataset

Putusan pengadilan merupakan dokumen publik yang kaya akan informasi hukum: identitas perkara, fakta persidangan, dakwaan, tuntutan, pertimbangan hakim, hingga amar putusan. Karena bersifat terbuka, dokumen ini sangat cocok dijadikan sumber pengetahuan sekaligus **dataset untuk domain Temu Kembali Informasi (TKI)**, misalnya untuk membangun mesin pencari dokumen hukum.

Repositori ini memuat:

1. **Dokumen putusan asli** berformat PDF yang diunduh secara manual dari Direktori Putusan Mahkamah Agung RI.
2. **Ringkasan terstruktur (`Overview.xlsx`)** yang berisi nomor putusan, lembaga peradilan, barang bukti, dan amar putusan dari setiap dokumen.
3. **Dokumentasi** (README ini) yang menjelaskan sumber, struktur, dan proses pembuatan dataset.

Dataset ini disusun untuk memenuhi **Soal Tugas 2 (SubCPMK-2)** pada Ujian Tengah Semester mata kuliah **Temu Kembali Informasi**, Fakultas Teknik, Universitas Muhammadiyah Malang, Semester Ganjil 2026/2027.

## Ringkasan Cepat

| Atribut | Keterangan |
|---|---|
| Domain | Hukum pidana khusus |
| Klasifikasi perkara | Narkotika dan Psikotropika |
| Sumber | [Direktori Putusan Mahkamah Agung RI](https://putusan3.mahkamahagung.go.id/direktori.html) |
| Pengadilan | PN Bojonegoro |
| Tahun putusan | 2023-2025 |
| Jumlah dokumen | 50 putusan (PDF) |
| Jumlah baris ringkasan | 50 |
| Kolom ringkasan | `No`, `No Putusan`, `Lembaga Peradilan`, `Barang Bukti`, `Amar Putusan` |
| Status putusan | Belum berkekuatan hukum tetap |
| Bahasa | Indonesia (ragam bahasa hukum) |
| Metode ekstraksi | Rule-based (regular expression) dengan Python |
| Tanggal pengambilan data | 29 Oktober 2026 |

## Struktur Repositori

```
Dataset-Narkotika_460_464/
├── Dataset/
│   └── Narkotika.zip          # Berisi 5 dokumen putusan (*.pdf)
├── Overview/
│   └── Overview.xlsx          # Ringkasan terstruktur 5 putusan
├── extract_putusan.ipynb      # Notebook Colab untuk ekstraksi
└── README.md                  # Dokumentasi ini
```

## Sumber dan Kriteria Pengumpulan Data

Seluruh putusan diunduh **secara manual** dari Direktori Putusan Mahkamah Agung RI dengan ketentuan berikut:

| Ketentuan | Penerapan pada dataset ini |
|---|---|
| Kategori direktori | Pidana Khusus |
| Klasifikasi | Narkotika dan Psikotropika |
| Pengadilan | Satu Pengadilan Negeri, tidak sama dengan kelompok lain |
| Tahun | Direkomendasikan 2023 – 2025 |
| Status putusan | Bukan putusan berkekuatan hukum tetap |
| Format berkas | PDF |
| Hak kekayaan intelektual | Dokumen putusan bersifat terbuka dan tidak terikat HaKI |

## Isi Dataset

### `Dataset/Narkotika.zip`
Arsip ZIP berisi dokumen putusan asli dalam format `*.pdf`. Setiap berkas merupakan satu putusan lengkap dari Direktori Putusan Mahkamah Agung RI, termasuk halaman identitas, dakwaan, tuntutan, pertimbangan hakim, dan amar putusan. Berkas inilah yang menjadi sumber untuk ekstraksi, pengindeksan, dan pencarian pada tahap TKI berikutnya.

### `Overview/Overview.xlsx`
Ringkasan terstruktur yang dihasilkan dari dokumen pada `Narkotika.zip`. Satu baris mewakili satu putusan, dengan urutan sesuai nama berkas.

## Kamus Data (Overview.xlsx)

| Kolom | Tipe | Deskripsi | Contoh format |
|---|---|---|---|
| `No` | Integer | Nomor urut baris, dimulai dari 1 | `1` |
| `No Putusan` | String | Nomor perkara pidana khusus, berpola `nomor/Pid.Sus/tahun/PN nama` | `408/Pid.Sus/2021/PN Gpr` |
| `Lembaga Peradilan` | String | Pengadilan Negeri yang mengadili perkara | `PN Kab Kediri` |
| `Barang Bukti` | String | Daftar barang bukti dalam amar putusan, dipisahkan tanda `;` | `Narkotika jenis sabu-sabu ...; 1 (satu) buah timbangan digital; ...` |
| `Amar Putusan` | String | Teks diktum putusan setelah kata *MENGADILI*, diratakan menjadi satu sel | `Menyatakan Terdakwa ... terbukti secara sah dan meyakinkan bersalah ...` |

**Catatan penting:**
- `Barang Bukti` hanya memuat nama dan jumlah barang. Kalimat status barang bukti (misalnya "dirampas untuk dimusnahkan") dan "Terdakwa tetap ditahan" tidak dimasukkan, tetapi tetap ada pada `Amar Putusan`.
- `Amar Putusan` memuat butir-butir diktum: pernyataan terbukti, pidana penjara, pidana denda, pengurangan masa tahanan, status penahanan, barang bukti, dan biaya perkara.

## Contoh Data

Contoh format satu baris (ilustrasi, dipersingkat):

| No | No Putusan | Lembaga Peradilan | Barang Bukti | Amar Putusan |
|---|---|---|---|---|
| 1 | 408/Pid.Sus/2021/PN Gpr | PN Kab Kediri | Narkotika jenis sabu-sabu dalam 4 (empat) plastik klip ...; 1 (satu) buah timbangan digital; 1 (satu) buah HP Merk VIVO warna hitam; | Menyatakan Terdakwa ... telah terbukti secara sah dan meyakinkan bersalah ...; Menjatuhkan pidana kepada Terdakwa ... pidana penjara selama 7 (tujuh) tahun; ... |

Membaca dengan Python:

```python
import pandas as pd

df = pd.read_excel("Overview/Overview.xlsx")
print(df.shape)          # (5, 5)
print(df.columns.tolist())
df.head()
```

## Bagaimana Dataset Ini Dibuat

```
┌──────────────┐   ┌──────────────┐   ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
│ 1. Unduh PDF │ → │ 2. Baca teks │ → │ 3. Bersihkan │ → │ 4. Ekstraksi │ → │ 5. Validasi  │
│  (manual dari│   │  (PyMuPDF)   │   │  boilerplate │   │  field regex │   │  & ekspor    │
│  direktori)  │   │              │   │  situs MA    │   │              │   │ Overview.xlsx│
└──────────────┘   └──────────────┘   └──────────────┘   └──────────────┘   └──────────────┘
```

1. **Unduh**: putusan diunduh manual dari Direktori Putusan Mahkamah Agung RI, lalu dikumpulkan dalam `Narkotika.zip`.
2. **Baca teks**: PDF dibaca dengan PyMuPDF (`get_text("text", sort=True)`) agar urutan teks mengikuti urutan baca visual.
3. **Bersihkan**: tanda air, *disclaimer* Kepaniteraan, header/footer, dan nomor halaman yang dicetak situs pada setiap halaman dihapus. Spasi dan baris kosong dinormalisasi.
4. **Ekstraksi**: setiap kolom diambil dengan pola kalimat khas putusan perkara narkotika (lihat bagian berikut).
5. **Validasi dan ekspor**: setiap berkas diperiksa dan dicatat pada log peringatan, lalu hasilnya diekspor ke `Overview.xlsx`.

Seluruh proses terdapat pada [`extract_putusan.ipynb`](extract_putusan.ipynb) dan dapat dijalankan di Google Colab.

## Aturan Ekstraksi

| Kolom | Kata kunci / pola kalimat | Aturan |
|---|---|---|
| `No Putusan` | `Nomor <angka>/Pid.<jenis>/<tahun>/PN <nama>` | Spasi di sekitar garis miring dinormalisasi |
| `Lembaga Peradilan` | `Pengadilan Negeri ... yang mengadili` | Diberi awalan `PN`, huruf kapital di awal kata |
| `Amar Putusan` | Teks setelah `MENGADILI` hingga sebelum `Demikianlah diputuskan` | Diratakan menjadi satu baris |
| `Barang Bukti` | `Menetapkan barang bukti berupa ...` | Mengambil kemunculan **terakhir**, dipotong sebelum `Membebankan` / `Menetapkan agar` / `Demikianlah`, status barang bukti dan penahanan dibuang |

**Kasus khusus yang ditangani:**

- **Butir amar berpindah posisi.** Pada sebagian PDF, hasil baca membuat butir "Menjatuhkan pidana kepada Terdakwa ..." muncul sebelum kata *MENGADILI*. Kalimat tersebut dicari lalu disisipkan kembali sebagai butir ke-2 amar.
- **Barang bukti tidak ada di amar.** Jika tidak ditemukan, daftar barang bukti diambil dari bagian *Menimbang* ("telah diajukan barang bukti berupa ...").
- **Pengadilan pada header dan penutup berbeda.** Ditandai sebagai peringatan untuk dicek manual.

Notebook juga dapat mengekstrak kolom tambahan (`Terdakwa` dan `Tuntutan`) ke berkas `extended.csv` sebagai pengayaan opsional.

## Kontrol Kualitas

Setiap berkas menghasilkan catatan pada `extraction_log.csv`. Baris dengan status selain `ok` diperiksa dan diperbaiki secara manual terhadap dokumen PDF aslinya.

| Kode peringatan | Arti |
|---|---|
| `ok` | Seluruh kolom terisi dan lolos pemeriksaan |
| `no_putusan_missing` | Nomor putusan tidak ditemukan |
| `not_Pid.Sus (...)` | Nomor putusan bukan jenis Pid.Sus |
| `lembaga_missing` | Nama pengadilan tidak ditemukan |
| `closing_court_mismatch (...)` | Pengadilan pada header dan penutup berbeda |
| `amar_missing` | Bagian *MENGADILI* tidak ditemukan |
| `amar_has_no_sentence` | Amar tidak memuat frasa *Menjatuhkan pidana* |
| `amar_item2_repositioned` | Butir 2 amar disisipkan kembali |
| `barang_bukti_missing` | Barang bukti tidak ditemukan |
| `barang_bukti_from_menimbang_fallback` | Barang bukti diambil dari bagian *Menimbang* |
| `error: ...` | Berkas gagal diproses |

Hasil akhir pada `Overview.xlsx` telah diperiksa secara manual terhadap dokumen sumber.

## Cara Menggunakan

### Opsi 1: Langsung memakai dataset
1. Unduh `Dataset/Narkotika.zip` untuk dokumen putusan PDF.
2. Buka `Overview/Overview.xlsx` untuk ringkasan terstruktur.

### Opsi 2: Mereproduksi ekstraksi di Google Colab
1. Buka `extract_putusan.ipynb` di [Google Colab](https://colab.research.google.com/).
2. Jalankan sel instalasi:
   ```python
   !pip -q install pymupdf pandas openpyxl
   ```
3. Unggah `Narkotika.zip` (atau *mount* Google Drive dan atur variabel `FOLDER`).
4. Jalankan seluruh sel hingga `run(FOLDER, OUT_DIR)` selesai.
5. Unduh `output/Overview.xlsx`.

**Dependensi:** Python 3, `pymupdf`, `pandas`, `openpyxl`.

## Potensi Pemanfaatan

- **Mesin pencari dokumen hukum**: praproses, pengindeksan, dan pencarian pada teks putusan (TF-IDF, BM25, dan sebagainya).
- **Praproses teks hukum bahasa Indonesia**: tokenisasi, penghapusan *stopword*, dan *stemming*.
- **Ekstraksi informasi**: pengenalan entitas seperti terdakwa, barang bukti, dan jenis pidana.
- **Analisis deskriptif putusan**: pola pidana penjara dan denda pada perkara narkotika.
- **Penalaran berbasis kasus**: pencarian putusan serupa.

## Keterbatasan

- Ekstraksi bersifat *rule-based*, sehingga format putusan yang menyimpang dari pola dapat menghasilkan kolom kosong atau terpotong.
- PDF hasil pindai tanpa lapisan teks tidak dapat dibaca tanpa OCR.
- Pola nomor putusan dirancang untuk perkara `Pid.Sus` tingkat pertama.
- Jumlah dokumen masih terbatas (5 putusan) sehingga belum mewakili seluruh variasi putusan narkotika.
- Barang bukti dan amar berupa teks bebas, belum dipecah menjadi atribut terstruktur (jenis, jumlah, satuan, lama pidana).

## Etika dan Lisensi

- Putusan bersumber dari publikasi resmi Mahkamah Agung RI dan bersifat terbuka untuk publik.
- Dokumen dapat memuat data pribadi pihak berperkara. Gunakan dataset ini secara bertanggung jawab dan hanya untuk keperluan akademik dan penelitian.
- Dataset ini **bukan** dokumen hukum resmi dan tidak boleh dijadikan rujukan hukum tanpa memverifikasi ke putusan asli.
- Hak atas isi putusan tetap berada pada pihak yang berwenang.

## Tim Penyusun

| Anggota | GitHub |
|---|---|
| Jelita Aufashshifaari Zahda Putri Prayitno | [@jelitaaufa](https://github.com/jelitaaufa) |
| Tia Dwi Febrianti]* | *[@username]* |

**Mata kuliah:** Temu Kembali Informasi · **Dosen pengampu:** Galih W. W
**Program Studi:** Informatika, Fakultas Teknik, Universitas Muhammadiyah Malang

## Sitasi

```
[Nama Penyusun]. (2026). Dataset Putusan Narkotika Direktori Putusan Mahkamah Agung RI
[Dataset]. Universitas Muhammadiyah Malang. Sumber asli: Direktori Putusan Mahkamah Agung
Republik Indonesia (https://putusan3.mahkamahagung.go.id/).
```

---

<div align="center">

Dibuat untuk UTS Temu Kembali Informasi · Semester Ganjil 2026/2027

</div>
