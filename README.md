# Pemodelan Klasifikasi Tutupan Lahan Tahun 2020 dan 2023 & Prediksi Tutupan Lahan Tahun 2026

1. `Script_Klasifikasi_Tutupan_Lahan_2020_dan_2023.ipynb` — Klasifikasi citra 2020 & 2023 menggunakan Support Vector Machine (SVM)
2. `Script_Prediksi_Tutupan_Lahan_2026.ipynb` — Prediksi tutupan lahan tahun 2026 dengan metode CA-Markov

## Struktur Direktori

    BAHAN TES/
    ├── Training_Sample_Separate.shp     # field: Classname
    ├── aoi.shp
    ├── BAHAN/
    │   ├── Citra/                       # *2020*.tif, *2023*.tif
    │   ├── Faktor Pendorong/            # .shp / .tif (MCE)
    │   ├── Faktor Pembatas/             # .shp / .tif
    │   └── output/                      # dibuat otomatis (Script_Klasifikasi_Tutupan_Lahan_2020_dan_2023.ipynb)
    └── Output Prediksi Tutupan Lahan 2026/  # dibuat otomatis (Script_Prediksi_Tutupan_Lahan_2026.ipynb)
Sesuaikan pada sel KONFIGURASI jika struktur folder berbeda.

---

## Variabel

**1. Tutupan Lahan 2020 & 2023**
- Citra satelit 2020 & 2023
- Training sampel

**2. Prediksi Tutupan Lahan 2026**
- Peta pemodelan tutupan lahan 2020 & 2023
- Faktor pendorong: jaringan jalan dan kemiringan lereng
- Faktor pembatas: kawasan lindung

---

## Output

**1. Script Klasifikasi (Folder: Output_Klasifikasi_Tutupan_Lahan_2020_dan_2023**
| File | Isi |
|---|---|
| `Tutupan_Lahan_2020.tif` | Peta tutupan lahan 2020 |
| `Tutupan_Lahan_2023.tif` | Peta tutupan lahan 2023 |
| `Legenda_Kelas.csv` | Kode & nama kelas |
| `Hasil Validasi ... 2020/2023.xlsx` | OA, Kappa, PA/UA, confusion matrix |

**2. Script Prediksi (Folder: Output_Prediksi_Tutupan_Lahan_Tahun_2026)**
| File | Isi |
|---|---|
| `Matriks_Transisi_Markov.xlsx` | Probabilitas transisi antar kelas |
| `Confusion_Matrix_Validasi.xlsx` | Validasi CA-Markov (OA, Kappa, PA, UA) |
| `Tutupan_Lahan_Prediksi_2026.tif` | Peta prediksi 2026 (RAT) |
| `Statistik_Luas_Ha.xlsx` | Luas per kelas 2020/2023/2026 |
| `Grafik_Perubahan_Luas.png` | Visualisasi perubahan luas |

---

## Ulasan Hasil

**A. Pemodelan Tutupan Lahan 2020 dan 2023**

Pemodelan data tutupan lahan tahun 2020 dan 2023 menunjukkan akurasi klasifikasi yang sangat baik, dengan Overall Accuracy (OA) di atas 95% dan Cohen's Kappa di atas 0,93 pada kedua tahun, yang menandakan tingkat validitas model hampir sempurna (almost perfect agreement). Namun terdapat penurunan akurasi dari 2020 ke 2023, baik pada OA dari 96,28% menjadi 95,13% maupun Kappa dari 0,9522 menjadi 0,9374, di mana Kappa tahun 2020 tergolong almost perfect agreement yang solid, sedangkan Kappa tahun 2023 meskipun masih dalam kategori almost perfect, nilainya sudah mendekati batas bawah kategori tersebut sehingga perlu adanya evaluasi utamanya pada segi data training yang digunakan.

**B. Peta Prediksi Tutupan Lahan 2026**

**Prediksi 2026 vs tren 2020–2023:**

| Kelas | 2020–2023 | Prediksi 2026 |
|---|---|---|
| Permukiman | ↑ 26.387 → 28.367 ha | ↑ → 30.216 ha (+1.849) |
| Sawah | ↑ 50.766 → 61.337 ha | ↓ → 58.839 ha (−2.498) |
| Vegetasi Tegakan | ↑ 66.297 → 79.757 ha | ↑ → 80.348 ha (+591) |
| Tanah Terbuka | ↑ 1.955 → 2.436 ha | ↑ → 2.638 ha (+202) |
| Badan Air | ↓ 28.425 → 1.932 ha | ↓ → 1.788 ha (−144) |

Berdasarkan analisis prediksi tutupan lahan tahun 2026, data menunjukkan bahwa hanya Permukiman, Vegetasi Tegakan, dan Tanah Terbuka yang mengalami penambahan luas, sedangkan Sawah dan Badan Air mengalami penyusutan. Secara rinci, Permukiman diprediksi bertambah menjadi 30.215,53 ha (+1.848,69 ha), Vegetasi Tegakan menjadi 80.348,09 ha (+591,26 ha), dan Tanah Terbuka menjadi 2.638,24 ha (+202,04 ha). Sebaliknya, Sawah diprediksi menyusut menjadi 58.839,40 ha (−2.497,99 ha) dan Badan Air menjadi 1.788,24 ha (−144 ha). Pola ini berbeda dengan periode 2020–2023, di mana Permukiman (26.387,47 ha → 28.366,84 ha), Sawah (50.765,70 ha → 61.337,39 ha), Vegetasi Tegakan (66.296,64 ha → 79.756,83 ha), dan Tanah Terbuka (1.954,92 ha → 2.436,20 ha) semuanya bertambah, sementara hanya Badan Air yang menyusut dari 28.424,77 ha menjadi 1.932,25 ha. Dengan demikian, pada proyeksi 2026 terjadi pergeseran pola: Sawah yang sebelumnya meluas justru diprediksi menyusut, sementara Permukiman terus menunjukkan tren penambahan yang konsisten sejak 2020. Sebagai tambahan, faktor pendorong dan faktor pembatas kedepannya dapat dikaji ulang sesuai dengan kebutuhan yang akan dicapai.

