# Pemetaan Aksesibilitas dan Kondisi Infrastruktur Pedestrian Kota Bandung Berbasis GIS dan Pengolahan Citra Digital

## 1. Overview

Proyek ini bertujuan melakukan pemetaan kondisi dan aksesibilitas infrastruktur pedestrian di Kota Bandung dengan mengintegrasikan data geospasial, data fasilitas perkotaan, data demografi, serta analisis citra digital dari Mapillary.

Penelitian ini mengadaptasi kerangka metodologi dari tesis Institut Teknologi Bandung (ITB):

**Pemetaan Kota Ramah Penyandang Disabilitas Fisik: Pengukuran Indeks Aksesibilitas Spasial Berbasis Transportasi Inklusif di Kota Bandung.**

Bagian yang menjadi acuan utama adalah Bab III Metodologi Penelitian, khususnya:
- Variabel penelitian.
- Teknik pengumpulan data.
- Kebutuhan data.
- Unit analisis.
- Tahapan analisis GIS.
- Pengukuran indeks aksesibilitas.
- Pemetaan accessibility gap.

Selain mempertahankan seluruh kebutuhan data dari penelitian ITB, proyek ini menambahkan citra Mapillary sebagai sumber informasi kondisi visual infrastruktur pedestrian.

Citra tersebut dianalisis menggunakan semantic segmentation dan Pengolahan Citra Digital (PCD) untuk mengidentifikasi area trotoar dan mengekstraksi indikator visual kondisi permukaannya.

Hasil analisis selanjutnya diintegrasikan dengan data aksesibilitas dan demand disabilitas fisik untuk mendukung pemetaan serta identifikasi wilayah yang memerlukan perhatian atau intervensi.

### Tujuan proyek

1. Mengumpulkan dan mengintegrasikan data jaringan jalan, jaringan pedestrian, fasilitas, topografi, dan demografi Kota Bandung.
2. Mengukur aksesibilitas infrastruktur pedestrian berdasarkan Walking Distance (WD), Sidewalk Width (SW), dan Slope (SL).
3. Menghitung kebutuhan mobilitas berdasarkan persebaran penyandang disabilitas fisik.
4. Mengidentifikasi kondisi visual permukaan trotoar melalui citra Mapillary.
5. Mengintegrasikan seluruh variabel ke dalam GIS.
6. Menghasilkan peta aksesibilitas, kondisi visual pedestrian, serta wilayah prioritas pemeriksaan atau perbaikan.

---

## 2. Landasan Penelitian

### 2.1 Referensi utama

Penelitian ini mengacu pada tesis:

*Pemetaan Kota Ramah Penyandang Disabilitas Fisik: Pengukuran Indeks Aksesibilitas Spasial Berbasis Transportasi Inklusif di Kota Bandung.*

Digilib Institut Teknologi Bandung:

https://digilib.itb.ac.id/gdl/view_data/pemetaan-kota-ramah-penyandang-disabilitas-fisik-pengukuran-indeks-aksesibilitas-spasial-berbasis-transportasi-inklusif-di-kota-bandung-24224001

Dokumen acuan yang digunakan adalah Bab III Metodologi Penelitian.

### 2.2 Pendekatan penelitian

Penelitian ITB menggunakan pendekatan mixed method yang mengintegrasikan:

1. **Analisis kuantitatif-spasial**, untuk mengukur kondisi infrastruktur pedestrian (supply) dan persebaran kebutuhan mobilitas penyandang disabilitas fisik (demand).
2. **Observasi kualitatif**, untuk memverifikasi kondisi infrastruktur dan hambatan aktual di lapangan.

Penelitian tersebut menggunakan analisis berbasis jaringan pejalan kaki (*network-based analysis*) dan mengintegrasikan parameter jarak fasilitas, lebar pedestrian, serta kemiringan jalur.

Pendekatan tersebut menjadi dasar pengembangan proyek ini. Perbedaannya, proyek ini menambahkan analisis citra Mapillary untuk memperoleh informasi kondisi visual pedestrian yang lebih detail.

### 2.3 Komponen utama

Kerangka penelitian dibagi menjadi tiga komponen:

| Komponen | Variabel | Fungsi |
|---|---|---|
| Supply | Walking Distance, Sidewalk Width, Slope | Mengukur kondisi dan aksesibilitas infrastruktur pedestrian |
| Demand | Persebaran penyandang disabilitas fisik | Mengukur kebutuhan mobilitas secara spasial |
| Kondisi visual | Indikator permukaan dari Mapillary | Menambahkan informasi kondisi fisik pedestrian berdasarkan citra |

Data sosiodemografi digunakan sebagai variabel pendukung untuk memperkaya interpretasi hasil dan rekomendasi.

---

## 3. Variabel dan Parameter Penelitian

### 3.1 Variabel supply

Penelitian ITB membentuk tiga parameter utama untuk mengukur kondisi penyediaan infrastruktur pedestrian.

#### A. Walking Distance (WD)

WD mengukur jarak tempuh jaringan pejalan kaki menuju fasilitas esensial yang dibutuhkan penyandang disabilitas fisik.

Delapan kategori fasilitas dasar yang digunakan:

1. Kesehatan.
2. Pendidikan.
3. Perbelanjaan.
4. Rekreasi dan olahraga.
5. Institusi pemerintahan.
6. Yayasan disabilitas.
7. Peribadatan.
8. Simpul transportasi.

Parameter acuan dari Bab III:
- Rentang jangkauan berjalan sekitar 400 meter hingga maksimal 1.200 meter.
- Ambang service area maksimal 1.200 meter.
- Kecepatan berjalan yang digunakan dalam analisis adalah 1,5 m/s.
- Perhitungan dilakukan berdasarkan jaringan jalan.
- Nilai jarak dinormalisasi dan diagregasikan ke grid analisis 250 × 250 meter.

WD yang lebih rendah menunjukkan fasilitas lebih mudah dijangkau melalui jaringan berjalan kaki.

#### B. Sidewalk Width (SW)

SW mengukur lebar efektif jalur pedestrian yang tersedia untuk pergerakan pejalan kaki.

Penelitian ITB mengacu pada lebar minimum sekitar 1,5–1,8 meter berdasarkan standar yang dijelaskan dalam Bab III.

Karena keterbatasan atribut lebar pedestrian, penelitian tersebut melakukan generalisasi berdasarkan hierarki jalan.

Estimasi lebar pedestrian:

| Hierarki jalan | Estimasi lebar |
|---|---:|
| Arteri | 1,7 m |
| Kolektor | 1,4 m |
| Lokal | 1,2 m |
| Lingkungan | 1,0 m |

Klasifikasi skor lebar dalam analisis:

| Lebar pedestrian | Skor |
|---|---:|
| Tidak tersedia jalur pedestrian | 0 |
| Kurang dari 0,8 m | 1 |
| 0,8–1,2 m | 2 |
| Lebih dari 1,2 m | 3 |

SW yang lebih besar menunjukkan ketersediaan ruang gerak yang lebih baik.

Perlu dibedakan antara standar minimum 1,5–1,8 meter yang menjadi acuan kelayakan dan nilai estimasi lebar per hierarki jalan yang digunakan akibat keterbatasan data.

#### C. Slope (SL)

SL mengukur kemiringan memanjang jalur pedestrian menggunakan Digital Elevation Model (DEM).

Data topografi digunakan untuk mendapatkan nilai persentase kemiringan.

Klasifikasi slope berdasarkan Bab III:

| Kemiringan | Interpretasi |
|---|---|
| 0–5% | Sangat aksesibel |
| 5–8% | Masih dapat diterima |
| 8–15% | Mulai menghambat |
| 15–45% | Sangat menghambat |

Kemiringan yang lebih besar menunjukkan hambatan yang lebih tinggi bagi pergerakan pengguna kursi roda.

### 3.2 Variabel demand

Demand merepresentasikan kebutuhan mobilitas penyandang disabilitas fisik.

Variabel yang digunakan:

| Variabel | Isi | Sumber |
|---|---|---|
| Disability Count | Jumlah penyandang disabilitas fisik per RT | Laci RW 2026 |


### 3.3 Data sosiodemografi pendukung

Data sosiodemografi digunakan sebagai informasi kontekstual dalam interpretasi hasil.

| Variabel | Keterangan | Sumber |
|---|---|---|
| Karakteristik sosial | Informasi sosial penyandang disabilitas fisik | Dinas Sosial Kota Bandung 2025 |
| Karakteristik kependudukan | Informasi kependudukan penyandang disabilitas fisik | Dinas Sosial Kota Bandung 2025 |

Data ini digunakan untuk mendukung interpretasi spasial dan penyusunan rekomendasi kebijakan, bukan sebagai pengganti variabel demand.

### 3.4 Variabel kondisi visual Mapillary

Proyek menambahkan informasi kondisi visual infrastruktur pedestrian dari citra Mapillary.

Variabel tambahan:

| Variabel | Keterangan |
|---|---|
| Image ID | Identitas unik citra |
| Latitude | Koordinat lintang |
| Longitude | Koordinat bujur |
| Captured At | Waktu pengambilan citra |
| Sequence ID | Identitas rangkaian citra |
| Compass Angle | Arah kamera |
| Sidewalk Mask | Hasil segmentasi area trotoar |
| Sidewalk Ratio | Proporsi area trotoar pada citra |
| ROI | Area permukaan trotoar yang dianalisis |
| Edge Density | Kepadatan tepi pada ROI |
| Candidate Damage Pixels | Jumlah piksel kandidat kerusakan |
| Candidate Damage Ratio | Rasio kandidat kerusakan terhadap luas ROI |
| Candidate Region Count | Jumlah area kandidat kerusakan |
| Visual Review Status | Status pemeriksaan visual |

Variabel Mapillary merupakan tambahan proyek dan tidak berasal dari variabel kuantitatif tesis ITB.

Hasilnya digunakan sebagai layer kondisi visual yang melengkapi analisis aksesibilitas.

---

## 4. Kebutuhan dan Sumber Data

Seluruh kelompok data yang tercantum pada Tabel III.3 Bab III dipertahankan dalam proyek ini.

### 4.1 Tabel kebutuhan data utama

| Jenis data | Isi | Sumber yang disebut dalam Bab III | Kegunaan |
|---|---|---|---|
| Jaringan jalan | Hierarki arteri, kolektor, lokal, lingkungan | OpenStreetMap (OSM) dan RDTR Kota Bandung 2024 | Jaringan analisis dan dasar generalisasi lebar |
| Jaringan pedestrian | Jaringan jalur pedestrian | OSM dan DPU Kota Bandung 2024 | Basis analisis jaringan pedestrian |
| Lebar pedestrian | Sampel lebar per kelas jalan melalui audit virtual | Google Street View; dokumen audit jalan PUPR 2022; RDTR Kota Bandung 2024 | Estimasi lebar jalur pedestrian |
| Topografi | DEM wilayah Kota Bandung | DEMNAS | Analisis slope |
| Fasilitas dasar | Kesehatan, pendidikan, pemerintahan, perbelanjaan, peribadatan, olahraga/rekreasi, yayasan disabilitas | OSM | Titik tujuan untuk service area |
| Fasilitas transportasi | Halte bus | OSM | Titik tujuan perjalanan dan analisis akses halte |
| Demand disabilitas | Jumlah penyandang disabilitas fisik per RT, diagregasi ke grid | Laci RW 2026 | Variabel demand |
| Sosiodemografi pendukung | Karakteristik sosial dan kependudukan penyandang disabilitas fisik | Dinas Sosial Kota Bandung 2025 | Konteks interpretasi dan rekomendasi |
| Citra dan metadata visual | Citra street-level, koordinat, waktu, sequence, arah kamera | Mapillary API | Pengamatan kondisi visual pedestrian |
| Hasil segmentasi dan PCD | Sidewalk mask, ROI, dan indikator visual permukaan | Hasil pemrosesan proyek | Layer tambahan kondisi visual pedestrian |

### 4.2 Keterangan sumber data

**OpenStreetMap (OSM)**

Digunakan untuk memperoleh:
- Jaringan jalan.
- Jaringan pedestrian.
- Titik fasilitas dasar.
- Titik halte bus.

**RDTR Kota Bandung 2024**

Digunakan sebagai sumber data pendukung hierarki jalan dan informasi spasial tata ruang sesuai kebutuhan analisis.

**DPU Kota Bandung 2024**

Digunakan sebagai sumber jaringan jalur pedestrian.

**Google Street View**

Digunakan untuk audit virtual pengambilan sampel lebar pedestrian sebagaimana disebutkan dalam Bab III. Penggunaan citra harus mengikuti ketentuan layanan yang berlaku; citra tidak otomatis menjadi dataset bebas unduh untuk eksperimen PCD.

**Dokumen audit jalan PUPR 2022**

Digunakan sebagai referensi pendukung informasi jalan dan pengukuran lebar pedestrian.

**DEMNAS**

Digunakan untuk memperoleh data elevasi sebagai dasar analisis slope.

**Laci RW 2026**

Digunakan untuk memperoleh jumlah penyandang disabilitas fisik per RT.

**Dinas Sosial Kota Bandung 2025**

Digunakan sebagai sumber informasi karakteristik sosial dan kependudukan penyandang disabilitas fisik.

**Mapillary**

Digunakan untuk mengambil citra street-level beserta metadata geografis dan waktu pengambilan gambar.

---

## 5. Unit Analisis dan Sistem Grid

Penelitian ITB menggunakan unit grid 250 × 250 meter untuk proses pengolahan variabel spasial.

Grid tersebut digunakan untuk:
- Agregasi Walking Distance.
- Pengolahan Sidewalk Width.
- Pengolahan Slope.
- Agregasi demand penyandang disabilitas fisik.
- Penghitungan indeks aksesibilitas.
- Pemetaan accessibility gap.

Penelitian ITB menghasilkan sekitar 2.900 grid dan selanjutnya mengagregasikan hasil indeks ke tingkat kelurahan.

### 5.1 Grid dalam proyek

Proyek ini memiliki dua grid dengan fungsi berbeda:

| Grid | Ukuran | Kegunaan |
|---|---:|---|
| Search Grid | 1 × 1 km | Pembagian wilayah pengumpulan citra Mapillary |
| Analysis Grid | 250 × 250 m | Unit pengolahan variabel aksesibilitas, demand, dan integrasi hasil Mapillary |

Search grid 1 km tetap dipertahankan untuk pengumpulan citra yang sudah berjalan.

Analysis grid 250 m dibuat sebagai layer baru untuk mengikuti unit analisis penelitian ITB.

Kedua grid tidak boleh dianggap sebagai layer yang sama.

### 5.2 CRS

Sistem koordinat:

- WGS84 untuk koordinat geografis sumber.
- EPSG:32748 - WGS84 / UTM Zone 48S untuk pemrosesan spasial Kota Bandung.

CRS proyeksi digunakan agar pengukuran jarak dan luas dilakukan dalam satuan meter.

---

## 6. Pengumpulan Data Mapillary

### 6.1 Pengumpulan metadata

Citra dikumpulkan menggunakan Mapillary Graph API.

Field yang dikumpulkan:

- `image_id`
- `computed_geometry`
- `captured_at`
- `sequence`
- `compass_angle`
- `thumb_1024_url`

Metadata tambahan seperti creator, tipe kamera, resolusi, dan lisensi diambil apabila tersedia melalui API.

### 6.2 Spatial sampling

Pengumpulan awal menghasilkan:

- 3.482 image ID unik.
- 1.674 kandidat setelah spatial sampling.
- 477 sequence.
- Jarak minimum 10 meter dalam sequence yang sama.

Spatial sampling bertujuan mengurangi kepadatan foto berdekatan.

Sampling tersebut tidak menjamin bebas duplikasi lintas sequence, sehingga pasangan citra yang berdekatan tetap dapat memerlukan pemeriksaan manual.

### 6.3 Distribusi kandidat awal

Dari 1.674 kandidat:

| Kecamatan | Jumlah |
|---|---:|
| Astana Anyar | 449 |
| Sumur Bandung | 377 |
| Cicendo | 363 |
| Regol | 345 |
| Andir | 116 |
| Lengkong | 23 |
| Bandung Wetan | 1 |
| **Total** | **1.674** |

Dataset pilot ini baru berasal dari 5 dari 212 search grid Kota Bandung. Oleh karena itu, cakupan tersebut belum dapat dianggap mewakili seluruh wilayah.

### 6.4 Resolusi citra

Dua resolusi digunakan:

- Thumbnail 1024 px untuk screening dan pemeriksaan awal.
- Resolusi 2048 px atau resolusi lebih tinggi jika tersedia untuk citra yang dipilih dalam analisis PCD.

Citra yang tidak lolos screening tetap disimpan sebagai bagian dari arsip dataset.

---

## 7. Screening Citra

Screening bertujuan mengidentifikasi citra yang layak untuk analisis trotoar.

Tahap screening menggunakan prediksi semantic segmentation dan pemeriksaan visual.

Variabel screening:

| Variabel | Keterangan |
|---|---|
| sidewalk_ratio | Proporsi piksel yang diprediksi sebagai sidewalk |
| road_ratio | Proporsi piksel road |
| vehicle_ratio | Proporsi piksel kendaraan |
| person_ratio | Proporsi piksel orang |
| blur_score | Skor ketajaman berdasarkan varians Laplacian |
| image_width | Lebar gambar |
| image_height | Tinggi gambar |
| auto_suggestion | Kategori saran screening |

### 7.1 Aturan screening awal

| Kondisi | Kategori |
|---|---|
| Sisi terkecil gambar <320 px atau blur score <25 | LOW_QUALITY_CANDIDATE |
| sidewalk_ratio ≥0,02 | SIDEWALK_CANDIDATE |
| sidewalk_ratio ≤0,005 dan road_ratio ≥0,10 | NO_CLEAR_SIDEWALK |
| Selain kondisi di atas | MANUAL_REVIEW |

Threshold tersebut merupakan heuristik screening awal, bukan keputusan ground truth atau threshold kerusakan.

### 7.2 Hasil screening awal

Dari 1.674 kandidat:

| Kategori | Jumlah | Persentase |
|---|---:|---:|
| SIDEWALK_CANDIDATE | 933 | 55,7% |
| MANUAL_REVIEW | 539 | 32,2% |
| NO_CLEAR_SIDEWALK | 202 | 12,1% |
| LOW_QUALITY_CANDIDATE | 0 | 0% |
| **Total** | **1.674** | **100%** |

Hasil ini merupakan screening awal berbasis SegFormer-B0 dan belum dianggap sebagai label final untuk dataset keseluruhan.

Setelah model utama ditetapkan, screening perlu diselaraskan dan divalidasi kembali menggunakan model terpilih.

---

## 8. Model Comparison dan Pemilihan Model Segmentasi

Sebelum analisis kondisi permukaan, proyek melakukan perbandingan tiga model pretrained semantic segmentation.

Seluruh model digunakan untuk inference tanpa training atau fine-tuning.

### 8.1 Model yang diuji

| Model | Repository | Karakteristik |
|---|---|---|
| SegFormer-B0 Cityscapes | `nvidia/segformer-b0-finetuned-cityscapes-1024-1024` | Model ringan untuk semantic segmentation lingkungan jalan perkotaan |
| Mask2Former Mapillary Vistas | `facebook/mask2former-swin-large-mapillary-vistas-semantic` | Mask2Former dengan backbone Swin-Large dan domain training Mapillary Vistas |
| SegFormer-B4 Sidewalk Semantic | `nickmuchi/segformer-b4-finetuned-segments-sidewalk` | Model yang memiliki kelas sidewalk secara eksplisit |

### 8.2 Alasan perbandingan

Ketiga model memiliki latar belakang training yang berbeda:

- SegFormer-B0 digunakan sebagai baseline.
- Mask2Former memiliki kedekatan domain dengan citra street-level Mapillary yang digunakan proyek.
- SegFormer-B4 digunakan sebagai pembanding yang secara spesifik memiliki kelas sidewalk.

Ketiga model dijalankan pada 40 citra yang sama.

### 8.3 Parameter kontrol

| Parameter | Nilai |
|---|---|
| Jumlah sampel benchmark | 40 gambar |
| Maximum image side | 768 px |
| Aspect ratio | Dipertahankan |
| Padding | Kelipatan 32 |
| Mode | Inference |
| Training | Tidak dilakukan |
| Checkpoint | Per model |
| Model loading | Bergantian |

Sampel benchmark diambil berdasarkan urutan file setelah sorting, sehingga belum termasuk random stratified sample seluruh Bandung.

### 8.4 Pairwise mask IoU

Pairwise IoU digunakan untuk mengukur kesepakatan antar-mask prediksi.

| Model A | Model B | Mean IoU |
|---|---|---:|
| Mask2Former | SegFormer-B4 | 0,2795 |
| SegFormer-B0 | Mask2Former | 0,2935 |
| SegFormer-B0 | SegFormer-B4 | 0,2340 |

Nilai tersebut menggambarkan kesamaan prediksi antar-model, bukan akurasi terhadap ground truth.

### 8.5 Ground truth validation

Anotasi manual dilakukan pada gambar benchmark menggunakan polygon.

Status anotasi:

| Status | Keterangan |
|---|---|
| ANNOTATED | Gambar memiliki area trotoar yang dapat dianotasi |
| NO_SIDEWALK | Tidak ada area trotoar yang dapat diidentifikasi |
| UNCERTAIN | Gambar tidak cukup jelas untuk menentukan area trotoar |

Dari 40 sampel benchmark, terdapat 31 gambar yang dapat dievaluasi:
- 25 gambar memiliki ground-truth trotoar.
- 6 gambar tidak memiliki ground-truth trotoar.

Metrik evaluasi:

- IoU.
- Precision.
- Recall.
- F1-score.
- Empty-image correct rate.
- Mean false-positive ratio pada gambar ground truth kosong.

### 8.6 Hasil validasi model

| Metrik | Mask2Former | SegFormer-B0 | SegFormer-B4 |
|---|---:|---:|---:|
| Jumlah gambar dievaluasi | 31 | 31 | 31 |
| GT trotoar | 25 | 25 | 25 |
| GT tanpa trotoar | 6 | 6 | 6 |
| Mean IoU | **0,4672** | 0,3191 | 0,3304 |
| Median IoU | **0,5291** | 0,2343 | 0,3153 |
| Precision | **0,6954** | 0,5731 | 0,4819 |
| Recall | **0,5816** | 0,4746 | 0,5375 |
| F1-score | **0,6024** | 0,4542 | 0,4754 |
| Empty-image correct rate | **16,67%** | 0% | 0% |
| Mean false-positive ratio GT kosong | **0,92%** | 1,25% | 9,51% |

Metrik positif dihitung sebagai macro-average per gambar pada 25 gambar yang memiliki ground-truth trotoar. Metrik gambar kosong dihitung secara terpisah.

### 8.7 Keputusan model

**Model utama yang dipilih: Mask2Former Swin-Large Mapillary Vistas.**

Pertimbangan:

1. Kedekatan domain training dengan citra Mapillary.
2. Mean IoU tertinggi.
3. Median IoU tertinggi.
4. Precision dan recall tertinggi.
5. F1-score tertinggi.
6. Mean false-positive ratio terendah pada gambar tanpa trotoar.

Mask2Former menjadi kandidat utama untuk segmentasi trotoar.

SegFormer-B0 tetap digunakan sebagai baseline dan SegFormer-B4 sebagai model pembanding.

Keputusan masih bersifat provisional sampai validasi diperluas dengan citra dari grid dan kondisi lingkungan yang lebih bervariasi.

### 8.8 Batasan model segmentasi

Model bertugas mengidentifikasi area sidewalk, bukan mendeteksi kerusakan.

Taksonomi kelas Mapillary Vistas juga membedakan `Sidewalk`, `Pedestrian Area`, `Curb`, dan `Road`.

Definisi operasional trotoar harus konsisten pada saat membentuk mask dan ground truth. Area pedestrian tidak otomatis dimasukkan sebagai sidewalk.

---

## 9. Analisis Kondisi Visual dengan PCD

Setelah area trotoar diidentifikasi menggunakan Mask2Former, tahap berikutnya adalah analisis kondisi permukaan.

Landasan konseptualnya adalah indikator kualitas permukaan pedestrian pada penelitian ITB, yaitu permukaan yang stabil, kokoh, rata, tidak licin, dan tidak berlubang.

PCD digunakan untuk mengidentifikasi indikasi visual seperti:
- Retakan permukaan.
- Lubang.
- Paving rusak atau hilang.
- Ketidakrataan permukaan.
- Perubahan pola tekstur yang mengindikasikan kerusakan.

### 9.1 Pipeline PCD

```text
Mapillary Original Image
          |
          v
      Mask2Former
          |
          v
   Sidewalk Segmentation
          |
          v
    Sidewalk Region/ROI
          |
          v
    Grayscale Conversion
          |
          v
 Histogram Analysis / CLAHE
          |
          v
    Image Filtering
          |
          v
     Edge Detection
          |
          v
       Thresholding
          |
          v
 Morphological Operations
          |
          v
  Candidate Damage Regions
          |
          v
   Visual Review / Validation
          |
          v
      PCD Metrics
```

### 9.2 Metode PCD

| Tahap | Metode | Kegunaan |
|---|---|---|
| Grayscale | RGB to Grayscale | Menyederhanakan informasi intensitas |
| Contrast enhancement | CLAHE | Meningkatkan kontras lokal |
| Filtering | Gaussian / Median | Mengurangi noise |
| Edge detection | Sobel | Menghitung gradien intensitas |
| Edge detection | Prewitt | Mendeteksi perubahan intensitas |
| Edge detection | Canny | Mengekstraksi tepi |
| Thresholding | Binary threshold | Memisahkan area berdasarkan intensitas |
| Morphology | Erosion, Dilation, Opening, Closing | Mengolah bentuk mask dan kandidat area |

Metode-metode tersebut merupakan rancangan eksperimen PCD proyek, bukan parameter yang secara langsung diadopsi dari tesis ITB.

### 9.3 Parameter eksperimen PCD

| Kelompok | Parameter | Kegunaan |
|---|---|---|
| CLAHE | clipLimit | Batas peningkatan kontras |
| CLAHE | tileGridSize | Ukuran grid lokal |
| Gaussian | kernel size | Ukuran kernel filtering |
| Median | kernel size | Ukuran kernel median |
| Sobel | kernel size | Ukuran operator gradien |
| Canny | low threshold | Ambang bawah |
| Canny | high threshold | Ambang atas |
| Thresholding | threshold value | Ambang intensitas |
| Morphology | kernel size | Ukuran structuring element |
| Morphology | iterations | Jumlah iterasi |

Nilai final parameter harus ditentukan melalui eksperimen dan validasi visual pada citra trotoar.

### 9.4 Variabel output PCD

| Variabel | Definisi |
|---|---|
| edge_density | Proporsi piksel tepi dalam ROI |
| candidate_damage_pixels | Jumlah piksel kandidat kerusakan |
| candidate_damage_ratio | Rasio kandidat kerusakan terhadap luas ROI |
| candidate_region_count | Jumlah area kandidat kerusakan |
| candidate_region_area | Luas kandidat kerusakan |
| visual_review_status | Status validasi hasil |

Salah satu indikator yang digunakan:

```text
Candidate Damage Ratio =
Candidate Damage Pixels / Sidewalk ROI Pixels
```

Indikator ini menggambarkan proporsi kandidat kerusakan pada area trotoar yang dianalisis.

Nilai tersebut bukan ukuran langsung kekuatan atau kerusakan struktural.

Sambungan paving, bayangan, pola tekstur, dan noise dapat menghasilkan false positive. Karena itu, kandidat kerusakan perlu diverifikasi.

---

## 10. Observasi Kualitatif Infrastruktur Pedestrian

Selain variabel kuantitatif-spasial, Bab III ITB juga menggunakan 13 indikator observasi infrastruktur.

Indikator ini dipertahankan sebagai dasar audit dan validasi kondisi pedestrian.

### 10.1 Geometri dan jalur (Physical Supply)

| No. | Indikator | Keterangan |
|---|---|---|
| 1 | Lebar bersih jalur | Jalur bebas hambatan, acuan ≥1,5 m |
| 2 | Kualitas permukaan jalur | Stabil, kokoh, rata, tidak licin, tidak berlubang |
| 3 | Kemiringan memanjang | Acuan aksesibilitas ≤8% |
| 4 | Transisi level / curb ramp | Perbedaan tinggi permukaan dan ketersediaan ramp |

### 10.2 Fasilitas halte dan konektivitas

| No. | Indikator | Keterangan |
|---|---|---|
| 5 | Aksesibilitas masuk halte | Step-free dan terhubung ke trotoar |
| 6 | Informasi transit | Nomor rute, peta jaringan, tanda halte |
| 7 | Fasilitas menyeberang | Zebra cross/pelican crossing dan curb ramp |
| 8 | Atap halte | Perlindungan hujan dan panas |
| 9 | Tempat duduk | Ketersediaan tempat duduk yang aksesibel |

### 10.3 Hambatan dan keamanan

| No. | Indikator | Keterangan |
|---|---|---|
| 10 | Penerangan | Kecukupan penerangan jalur pedestrian |
| 11 | Okupasi jalur | PKL dan parkir liar yang menghalangi jalur |
| 12 | Intrusi kendaraan | Motor/mobil yang memasuki trotoar atau area halte |
| 13 | Fasilitas istirahat | Ketersediaan bangku di koridor menuju halte |

### 10.4 Skala penilaian

Skala observasi mengacu pada Bab III:

| Skor | Kriteria |
|---|---|
| 1 | Buruk: tidak ada fasilitas atau hambatan sangat berat |
| 2 | Cukup baik: fasilitas tersedia tetapi rusak, sempit, atau terhambat |
| 3 | Baik: memenuhi standar teknis minimum |

Indikator yang dapat diamati melalui Mapillary bergantung pada sudut kamera dan kualitas citra. Indikator lain tetap memerlukan data pendukung atau observasi lapangan.

Kualitas permukaan menjadi fokus utama PCD, sedangkan okupasi jalur, intrusi kendaraan, dan fasilitas lainnya disimpan sebagai indikator observasi terpisah.

---

## 11. Analisis GIS dan Perhitungan Indeks Aksesibilitas

Seluruh data dari penelitian ITB dan tambahan Mapillary diintegrasikan dalam QGIS.

### 11.1 Analisis Walking Distance

Walking Distance dihitung menggunakan jaringan pejalan kaki menuju titik fasilitas.

Tahapan:
1. Menyiapkan jaringan jalan dan pedestrian.
2. Menyiapkan titik fasilitas dasar dan halte.
3. Menggunakan QNEAT3 untuk analisis jaringan.
4. Menghitung jarak jaringan menuju fasilitas.
5. Menggunakan ambang maksimal 1.200 meter.
6. Mengagregasikan hasil ke grid 250 × 250 meter.

Kecepatan berjalan yang digunakan dalam acuan Bab III adalah 1,5 m/s.

Hasil yang disimpan pada setiap grid meliputi jarak menuju masing-masing kategori fasilitas.

### 11.2 Analisis Slope

Tahapan:
1. Memuat DEMNAS.
2. Memproses data elevasi.
3. Menghasilkan raster slope.
4. Mengklasifikasikan persentase slope.
5. Mengagregasikan nilai ke grid 250 × 250 meter.

Klasifikasi:
- 0–5%.
- 5–8%.
- 8–15%.
- 15–45%.

### 11.3 Analisis Sidewalk Width

Tahapan:
1. Menyiapkan hierarki jalan.
2. Mengumpulkan sampel lebar pedestrian melalui audit virtual.
3. Menggunakan nilai estimasi berdasarkan kelas jalan bila pengukuran presisi tidak tersedia.
4. Menghubungkan nilai lebar ke jaringan pedestrian atau grid.
5. Memberikan skor berdasarkan interval lebar.

Sumber pengukuran harus disimpan sebagai atribut agar nilai hasil pengukuran tidak tercampur dengan estimasi generalisasi.

Contoh atribut:

- `width_m`
- `width_source`
- `width_method`
- `road_class`
- `width_score`

### 11.4 Normalisasi variabel

Penelitian ITB menggunakan Min-Max Scaling untuk menstandarkan nilai variabel pada interval 0–1.

Normalisasi SW:

```text
N(SW) = (SWg - SWmin) / (SWmax - SWmin)
```

Lebar pedestrian yang semakin besar menghasilkan nilai aksesibilitas semakin tinggi.

Normalisasi WD:

```text
N(WD) = (WDmax - WDg) / (WDmax - WDmin)
```

Jarak fasilitas yang semakin dekat menghasilkan nilai aksesibilitas semakin tinggi.

Normalisasi SL:

```text
N(SL) = (SLmax - SLg) / (SLmax - SLmin)
```

Slope yang semakin curam menghasilkan nilai aksesibilitas semakin rendah.

### 11.5 Indeks komposit aksesibilitas (Composite Index)

Penelitian ITB menggabungkan tiga variabel supply menggunakan GIS-based Multi-Criteria Decision Analysis (MCDA).

Bobot dalam persamaan Bab III:

| Variabel | Bobot |
|---|---:|
| Walking Distance (WD) | 0,595 |
| Sidewalk Width (SW) | 0,382 |
| Slope (SL) | 0,023 |

Persamaan:

```text
CIg =
(0.382 × N(SWg)) +
(0.595 × N(WDg)) +
(0.023 × N(SLg))
```

CI menggambarkan indeks aksesibilitas supply pada setiap grid.

**Catatan verifikasi sumber:** uraian Bab III menyebut bobot SL sebesar 0,021, sedangkan tabel dan persamaan menggunakan 0,023. Nilai ini perlu dikonfirmasi terhadap dokumen asli sebelum perhitungan final. README menggunakan persamaan sebagaimana tercantum pada Bab III, tanpa menganggap perbedaannya sudah terselesaikan.

### 11.6 Demand disabilitas

Jumlah penyandang disabilitas fisik per RT diagregasikan ke grid 250 × 250 meter.

Hasilnya menjadi layer demand yang dapat dibandingkan dengan indeks supply.

Contoh atribut:
- `grid_id`
- `disability_count`
- `demand_density`
- `demand_class`

### 11.7 Bivariate Choropleth

Indeks aksesibilitas supply diintegrasikan dengan persebaran demand disabilitas untuk menghasilkan pemetaan accessibility gap.

Analisis ini bertujuan mengidentifikasi wilayah yang memiliki kebutuhan mobilitas tinggi tetapi kondisi supply aksesibilitas rendah.

Hasil klasifikasi dapat digunakan untuk mengenali tipologi seperti:
- High Demand – Low Supply.
- High Demand – High Supply.
- Low Demand – Low Supply.
- Low Demand – High Supply.

Pengelompokan akhir mengikuti klasifikasi yang ditetapkan pada analisis bivariate.

### 11.8 Uji sensitivitas dan robustness

Penelitian ITB melakukan variasi bobot:
- ±10% dari bobot dasar.
- ±20% dari bobot dasar.
- Skenario equal weight.

Stabilitas peringkat antar-grid diukur menggunakan korelasi rank Spearman.

Ambang korelasi yang disebut dalam Bab III adalah di atas 0,90.

Uji ini dapat digunakan untuk menilai apakah hasil indeks sensitif terhadap perubahan bobot.

---

## 12. Integrasi Hasil Mapillary ke GIS

Hasil Mapillary tidak menggantikan variabel WD, SW, SL, maupun demand.

Mapillary menjadi lapisan tambahan yang menyediakan informasi visual kondisi pedestrian.

### 12.1 Layer Mapillary

Layer yang disiapkan:

| Layer | Geometri | Isi |
|---|---|---|
| Mapillary Images | Point | Lokasi pengambilan gambar |
| Sidewalk Segmentation | Data raster/mask | Area trotoar hasil segmentasi |
| Sidewalk ROI | Raster/mask | Area permukaan yang dianalisis |
| PCD Results | Point/atribut | Indikator visual kerusakan |
| Visual Review | Point/atribut | Status validasi visual |

Mask dan ROI dapat disimpan sebagai file gambar, sedangkan metrik dan metadata dihubungkan ke layer titik Mapillary melalui `image_id`.

### 12.2 Pengaitan citra ke jaringan pedestrian

Koordinat Mapillary merepresentasikan lokasi kamera, bukan otomatis lokasi permukaan trotoar.

Karena itu, pengaitan citra ke segmen pedestrian perlu mempertimbangkan:
- Koordinat kamera.
- Compass angle.
- Jarak terhadap segmen pedestrian.
- Arah pandang kamera.
- Sisi jalan yang terlihat.
- Kejelasan permukaan trotoar.
- Pemeriksaan visual.

Contoh atribut hasil pencocokan:

| Atribut | Keterangan |
|---|---|
| image_id | ID gambar |
| pedestrian_id | ID segmen pedestrian yang terkait |
| distance_to_segment | Jarak kamera ke segmen |
| compass_angle | Arah kamera |
| match_method | Metode pencocokan |
| match_confidence | Tingkat keyakinan pencocokan |
| visual_status | Status keterlihatan trotoar |

Jika segmen pedestrian belum dapat diidentifikasi dengan yakin, gambar tetap disimpan pada layer titik tanpa dipaksakan menjadi bagian dari segmen tertentu.

### 12.3 Agregasi hasil Mapillary ke grid

Indikator PCD pada tingkat gambar dapat diagregasikan ke grid 250 × 250 meter.

Contoh atribut agregasi:

| Variabel | Keterangan |
|---|---|
| image_count | Jumlah citra yang tersedia |
| valid_image_count | Jumlah citra yang layak dianalisis |
| mean_candidate_damage_ratio | Rata-rata rasio kandidat kerusakan |
| max_candidate_damage_ratio | Rasio tertinggi |
| candidate_damage_count | Jumlah citra dengan kandidat kerusakan |
| visual_review_count | Jumlah citra yang telah diperiksa |
| coverage_status | Status kecukupan pengamatan |

Agregasi harus mempertimbangkan sequence dan kedekatan citra agar satu lokasi tidak mendapatkan bobot berlebihan hanya karena memiliki banyak foto.

Informasi tanggal pengambilan citra juga harus dipertahankan agar hasil tidak mencampurkan kondisi dari periode yang berbeda tanpa penjelasan.

---

## 13. Integrasi Supply, Demand, dan Kondisi Visual

Ketiga komponen penelitian digabungkan dalam GIS.

### 13.1 Konsep integrasi

```text
                    SUPPLY
                      |
         +------------+------------+
         |            |            |
         WD           SW           SL
         |            |            |
         +------------+------------+
                      |
                      v
             INDEKS AKSESIBILITAS
                      |
                      |
DEMAND                |           KONDISI VISUAL
   |                  |                 |
Jumlah disabilitas    |             Mapillary
   |                  |                 |
Agregasi grid         |             Mask2Former
   |                  |                 |
   |                  |              Sidewalk ROI
   |                  |                 |
   |                  |                PCD
   |                  |                 |
   |                  |          Candidate Damage
   |                  |              Indicators
   |                  |                 |
   +------------------+-----------------+
                      |
                      v
                INTEGRASI GIS
                      |
                      v
             PEMETAAN DAN ANALISIS
             PRIORITAS WILAYAH
```

### 13.2 Interpretasi hasil integrasi

Pemetaan dapat digunakan untuk melihat hubungan antara:

1. Kebutuhan aksesibilitas penyandang disabilitas.
2. Kondisi penyediaan infrastruktur pedestrian.
3. Indikasi visual kualitas permukaan trotoar.

Contoh interpretasi:

| Kondisi | Makna |
|---|---|
| Demand tinggi, supply rendah | Wilayah dengan kesenjangan aksesibilitas yang perlu diperhatikan |
| Demand tinggi, indikasi kerusakan tinggi | Wilayah yang berpotensi membutuhkan pemeriksaan dan intervensi lebih dahulu |
| Supply tinggi, indikasi kerusakan tinggi | Jalur yang secara spasial mudah dijangkau, tetapi kondisi permukaannya perlu diperiksa |
| Demand rendah, supply rendah | Wilayah dengan aksesibilitas rendah yang tetap memerlukan perhatian |
| Demand tinggi, supply tinggi, indikasi kerusakan rendah | Wilayah dengan kondisi relatif lebih baik berdasarkan indikator yang tersedia |

**Indeks aksesibilitas ITB dan candidate damage ratio Mapillary tidak langsung dijumlahkan.** Keduanya memiliki makna, skala, dan sumber ketidakpastian berbeda.

Tahap awal adalah melakukan overlay dan analisis bersama. Jika akan dibuat indeks prioritas gabungan, pembobotan dan klasifikasinya harus disusun serta divalidasi secara terpisah.

---

## 14. Struktur Layer QGIS

Berikut rancangan layer yang akan dibangun dalam proyek.

### 14.1 Administrasi dan grid

| Layer | Geometri | Fungsi |
|---|---|---|
| batas_kota_bandung | Polygon | Batas Kota Bandung |
| batas_kecamatan | Polygon | Batas kecamatan |
| batas_kelurahan | Polygon | Batas kelurahan |
| search_grid_1km | Polygon | Unit pencarian Mapillary |
| analysis_grid_250m | Polygon | Unit analisis utama |

### 14.2 Infrastruktur

| Layer | Geometri | Fungsi |
|---|---|---|
| road_network | Line | Jaringan jalan |
| pedestrian_network | Line | Jaringan pedestrian |
| sidewalk_width | Line/atribut | Informasi lebar pedestrian |
| sidewalk_slope | Raster/atribut | Informasi slope |
| demnas | Raster | Data elevasi |
| slope_raster | Raster | Hasil analisis slope |

### 14.3 Fasilitas

| Layer | Geometri | Fungsi |
|---|---|---|
| health_facilities | Point | Fasilitas kesehatan |
| education_facilities | Point | Fasilitas pendidikan |
| government_facilities | Point | Fasilitas pemerintahan |
| shopping_facilities | Point | Fasilitas perbelanjaan |
| worship_facilities | Point | Fasilitas peribadatan |
| recreation_facilities | Point | Fasilitas rekreasi dan olahraga |
| disability_foundations | Point | Yayasan disabilitas |
| bus_stops | Point | Halte bus |

### 14.4 Aksesibilitas dan demand

| Layer | Geometri | Fungsi |
|---|---|---|
| wd_service_area | Raster/Polygon | Hasil analisis jarak fasilitas |
| wd_grid | Polygon | Nilai WD per grid |
| sw_grid | Polygon | Nilai SW per grid |
| slope_grid | Polygon | Nilai slope per grid |
| accessibility_index | Polygon | Indeks supply |
| disability_demand_rt | Polygon/atribut | Demand per RT |
| disability_demand_grid | Polygon | Demand per grid |
| sociodemographic | Polygon/atribut | Informasi sosial dan kependudukan |
| accessibility_bivariate | Polygon | Peta accessibility gap |

### 14.5 Mapillary dan PCD

| Layer | Geometri | Fungsi |
|---|---|---|
| mapillary_image_points | Point | Lokasi kamera |
| mapillary_screening | Point/atribut | Hasil screening |
| sidewalk_roi_results | Point/atribut | Hasil analisis ROI |
| pcd_visual_indicators | Point/atribut | Indikator visual kerusakan |
| sidewalk_condition_grid | Polygon | Agregasi kondisi visual |
| sidewalk_visual_review | Point/atribut | Hasil verifikasi |

Nama layer merupakan rancangan organisasi data dan dapat disesuaikan dengan struktur file aktual.

---

## 15. Struktur Folder Proyek

```text
GIS-Trotoar-Bandung/
│
├── 01_RAW_DATA/
│   ├── ADMIN/
│   ├── OSM/
│   ├── RDTR/
│   ├── DPU/
│   ├── PUPR/
│   ├── DEMNAS/
│   ├── FACILITIES/
│   ├── DISABILITY_DEMAND/
│   ├── SOCIODEMOGRAPHIC/
│   └── MAPILLARY/
│       ├── METADATA/
│       └── IMAGES/
│           ├── THUMBNAILS_1024/
│           └── SELECTED_2048/
│
├── 02_INTERMEDIATE_DATA/
│   ├── NETWORK/
│   ├── FACILITIES/
│   ├── DEM/
│   ├── GRID/
│   └── MAPILLARY/
│
├── 03_GIS/
│   ├── raw/
│   ├── processed/
│   ├── analysis/
│   └── qgis_project/
│
├── 04_MODEL/
│   ├── MODEL_COMPARISON/
│   └── GROUND_TRUTH/
│
├── 05_ANALYSIS/
│   ├── PCD/
│   │   ├── CONTACT_SHEETS/
│   │   ├── ROI/
│   │   ├── RESULTS/
│   │   ├── MODEL_COMPARISON_40/
│   │   └── GROUND_TRUTH_40/
│   │
│   ├── ACCESSIBILITY/
│   ├── DEMAND/
│   ├── MCDA/
│   └── INTEGRATION/
│
├── 06_OUTPUT/
│   ├── MAPS/
│   ├── TABLES/
│   ├── REPORTS/
│   └── FIGURES/
│
└── README.md
```

Struktur ini merupakan rancangan organisasi akhir. Folder yang belum digunakan dapat dibuat ketika tahap pengolahan terkait dimulai.

---

## 16. Notebook dan Teknologi

### 16.1 Notebook

| Notebook | Fungsi |
|---|---|
| Notebook 02 - Mapillary Collector | Mengumpulkan metadata dan melakukan spatial sampling citra |
| Notebook 03 - Mapillary Screening & PCD | Download gambar, screening, dan analisis citra awal |
| Notebook 04 - Model Comparison | Membandingkan model segmentasi |
| Notebook 05 - Ground Truth Validation | Anotasi manual dan evaluasi model |
| Notebook berikutnya - PCD Analysis | Analisis indikator kondisi permukaan |
| Notebook berikutnya - GIS Integration | Integrasi hasil citra dan data aksesibilitas |

### 16.2 Teknologi

| Teknologi | Kegunaan |
|---|---|
| Python | Pemrosesan dan analisis data |
| Google Colab | Eksperimen PCD dan model |
| OpenCV | Pengolahan citra digital |
| PyTorch | Inference model segmentation |
| Hugging Face Transformers | Memuat model pretrained |
| Pandas | Pengolahan tabel dan metadata |
| GeoPandas | Pemrosesan data geospasial |
| QGIS | Analisis, integrasi, dan visualisasi GIS |
| QuickOSM | Pengambilan data OSM |
| QNEAT3 | Network analysis dan service area |
| GeoPackage | Penyimpanan layer spasial |

---

## 17. Batasan dan Catatan Metodologis

### 17.1 Cakupan data Mapillary

Dataset Mapillary saat ini baru mencakup 5 dari 212 search grid. Hasilnya belum mewakili seluruh Kota Bandung.

Pengumpulan data perlu diperluas secara bertahap.

### 17.2 Perbedaan unit grid

Search grid 1 km digunakan untuk mengelola pencarian citra.

Analysis grid 250 m digunakan untuk pengolahan variabel spasial dan demand.

Kedua unit tidak boleh dicampur.

### 17.3 Kualitas dan keterbatasan citra

Citra Mapillary mempunyai variasi resolusi, arah kamera, sudut pengambilan gambar, pencahayaan, dan occlusion.

Karena itu, tidak semua citra dapat digunakan untuk analisis permukaan.

### 17.4 Koordinat citra

Koordinat Mapillary merupakan lokasi kamera/gambar, bukan otomatis lokasi persis jalur pedestrian.

Pengaitan ke segmen harus mempertimbangkan arah kamera, jarak, dan konteks visual.

### 17.5 Batasan segmentasi

Mask2Former hanya mengidentifikasi area trotoar berdasarkan kelas semantik.

Model tidak mendeteksi kerusakan struktural.

Definisi `Sidewalk`, `Pedestrian Area`, `Curb`, dan `Road` harus konsisten dengan definisi operasional penelitian.

### 17.6 Batasan PCD

Edge detection dan thresholding dapat menghasilkan false positive dari sambungan paving, tekstur, bayangan, atau noise.

Candidate damage ratio merupakan indikator visual, bukan pengukuran kerusakan struktural.

### 17.7 Batasan pengukuran lebar

Lebar yang digeneralisasi berdasarkan hierarki jalan harus dibedakan dari lebar hasil pengukuran langsung.

Setiap nilai lebar perlu menyimpan sumber dan metode pengukurannya.

### 17.8 Batasan integrasi indeks

Indeks aksesibilitas dan indikator kerusakan visual tidak boleh langsung digabungkan tanpa normalisasi, justifikasi pembobotan, dan validasi.

Tahap awal dilakukan melalui overlay dan interpretasi bersama.

### 17.9 Batasan data demand dan sosiodemografi

Data demand dan sosiodemografi harus mengikuti unit wilayah, periode, definisi, dan keterbatasan sumber aslinya.

Agregasi spasial tidak boleh menimbulkan interpretasi seolah-olah data per grid tersedia langsung dari sumber.

---

## 18. Rencana Pekerjaan

Tahapan pengembangan proyek:

### Tahap 1 - Data Preparation

- Mengumpulkan jaringan jalan.
- Mengumpulkan jaringan pedestrian.
- Mengumpulkan data RDTR.
- Mengumpulkan data DPU.
- Mengumpulkan data DEMNAS.
- Mengumpulkan fasilitas dasar dan halte.
- Mengumpulkan data demand disabilitas.
- Mengumpulkan data sosiodemografi.
- Melanjutkan pengumpulan citra Mapillary.

### Tahap 2 - Spatial Processing

- Menyamakan CRS.
- Memeriksa geometri dan atribut.
- Menyiapkan batas wilayah.
- Mempertahankan search grid 1 km.
- Membuat analysis grid 250 m.
- Menyiapkan jaringan jalan dan pedestrian.
- Menyiapkan titik fasilitas.

### Tahap 3 - Accessibility Analysis

- Menghitung WD.
- Mengolah SW.
- Mengolah slope.
- Melakukan normalisasi.
- Menghitung Composite Index.
- Melakukan uji sensitivitas.
- Mengagregasikan demand.
- Membuat Bivariate Choropleth.

### Tahap 4 - Mapillary Analysis

- Memperluas pengumpulan citra.
- Menyelesaikan visual screening.
- Menambah ground truth.
- Memvalidasi Mask2Former.
- Menghasilkan sidewalk mask.
- Menentukan ROI.
- Melakukan PCD.
- Mengekstraksi indikator visual.
- Melakukan validasi visual.

### Tahap 5 - GIS Integration

- Memuat seluruh layer ke QGIS.
- Menghubungkan citra dengan segmen pedestrian atau grid.
- Mengagregasikan hasil PCD.
- Menggabungkan supply, demand, dan kondisi visual.
- Membuat peta tematik dan analisis prioritas.

### Tahap 6 - Validation and Reporting

- Memeriksa kualitas data.
- Memvalidasi hasil analisis spasial.
- Memeriksa hasil PCD.
- Melakukan observasi lapangan pada sampel lokasi bila memungkinkan.
- Menyusun peta, tabel, dan laporan.

---

## 19. Referensi

### Referensi utama

*Pemetaan Kota Ramah Penyandang Disabilitas Fisik: Pengukuran Indeks Aksesibilitas Spasial Berbasis Transportasi Inklusif di Kota Bandung.*

Digilib Institut Teknologi Bandung:

https://digilib.itb.ac.id/gdl/view_data/pemetaan-kota-ramah-penyandang-disabilitas-fisik-pengukuran-indeks-aksesibilitas-spasial-berbasis-transportasi-inklusif-di-kota-bandung-24224001

Bagian acuan:
- Bab III - Metodologi Penelitian.
- III.1 Pendekatan dan Metode Penelitian.
- III.2 Variabel Penelitian.
- III.3 Teknik Pengumpulan Data.
- III.4 Analisis Data.
- Tabel III.1 Operasionalisasi Variabel Penelitian.
- Tabel III.2 Variabel Observasi.
- Tabel III.3 Kebutuhan Data.

### Model semantic segmentation

1. SegFormer-B0 Cityscapes  
   https://huggingface.co/nvidia/segformer-b0-finetuned-cityscapes-1024-1024

2. Mask2Former Swin-Large Mapillary Vistas  
   https://huggingface.co/facebook/mask2former-swin-large-mapillary-vistas-semantic

3. SegFormer-B4 Sidewalk Semantic  
   https://huggingface.co/nickmuchi/segformer-b4-finetuned-segments-sidewalk

### Sumber data dan teknologi

- OpenStreetMap: https://www.openstreetmap.org/
- Mapillary: https://www.mapillary.com/developer
- QGIS: https://qgis.org/
- GeoPandas: https://geopandas.org/
- OpenCV: https://opencv.org/
- DEMNAS: https://tanahair.indonesia.go.id/demnas/

---

## 20. Kesimpulan

Proyek ini mengembangkan sistem pemetaan aksesibilitas dan kondisi infrastruktur pedestrian Kota Bandung dengan mengintegrasikan seluruh kebutuhan data dan variabel dari penelitian ITB serta menambahkan analisis citra Mapillary.

Variabel supply berupa Walking Distance, Sidewalk Width, dan Slope digunakan untuk membentuk indeks aksesibilitas. Variabel demand merepresentasikan persebaran kebutuhan mobilitas penyandang disabilitas fisik. Data sosiodemografi digunakan sebagai konteks interpretasi.

Sementara itu, citra Mapillary diproses menggunakan Mask2Former untuk mengidentifikasi area trotoar, kemudian dianalisis menggunakan PCD untuk memperoleh indikator visual kondisi permukaan.

Seluruh hasil diintegrasikan dalam QGIS dengan unit grid analisis 250 × 250 meter dan jaringan pedestrian sebagai dasar pengaitan data.

Hasil akhir yang diharapkan adalah peta yang tidak hanya memperlihatkan tingkat aksesibilitas pedestrian, tetapi juga memberikan informasi tambahan mengenai kondisi visual permukaan dan wilayah yang perlu diprioritaskan untuk pemeriksaan atau perbaikan.

**Prinsip utama proyek: seluruh variabel aksesibilitas dari penelitian ITB dipertahankan, sementara Mapillary menjadi lapisan informasi tambahan untuk memperkaya analisis kondisi fisik pedestrian.**
