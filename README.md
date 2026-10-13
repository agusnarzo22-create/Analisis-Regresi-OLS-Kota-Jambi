# Analisis Regresi OLS: Belanja Modal Pendidikan & Kesehatan terhadap IPM
## Studi Kasus Kota Jambi (2014–2024)

Analisis **regresi linier berganda (Ordinary Least Squares)** untuk menguji pengaruh
**Belanja Modal Pendidikan** ($X_1$) dan **Belanja Modal Kesehatan** ($X_2$) terhadap
**Indeks Pembangunan Manusia / IPM** ($Y$) di **Kota Jambi** selama sebelas tahun.

---

## Mengapa Kota Jambi?

Dari 97 kota pada dataset, Kota Jambi dipilih karena **model regresinya paling kuat**:
kedua variabel bebasnya sama-sama signifikan pada alpha 5% dan modelnya signifikan
secara simultan. Ini menjadikannya studi kasus paling representatif untuk menunjukkan
bagaimana regresi berganda bekerja.

## Model Penelitian

$$\text{IPM} = \beta_0 + \beta_1 \cdot \text{bm\_pendidikan} + \beta_2 \cdot \text{bm\_kesehatan} + \varepsilon$$

| Simbol | Variabel | Keterangan |
|---|---|---|
| $Y$ | `IPM` | Indeks Pembangunan Manusia |
| $X_1$ | `bm_pendidikan` | Belanja modal fungsi pendidikan |
| $X_2$ | `bm_kesehatan` | Belanja modal fungsi kesehatan |

## Hasil Utama

Persamaan regresi terestimasi (Kota Jambi, n = 11):

$$\widehat{\text{IPM}} = 73{,}2717 + 0{,}0521 \cdot X_1 - 0{,}0660 \cdot X_2$$

| Variabel | Koefisien | Std. Error | t | p-value | Keputusan |
|---|---|---|---|---|---|
| Konstanta | 73,2717 | 4,2112 | 17,399 | < 0,001 | Signifikan |
| `bm_pendidikan` | +0,0521 | 0,0208 | 2,510 | 0,0364 | **Signifikan (positif)** |
| `bm_kesehatan` | −0,0660 | 0,0215 | −3,072 | 0,0153 | **Signifikan (negatif)** |

- **R² = 0,583** · **Adj. R² = 0,479** · **F = 5,602 (p = 0,0301)**
- Jauh di atas model gabungan 97 kota (R² = 0,006).

**Kesimpulan:**

1. **H1 didukung** — belanja modal pendidikan berpengaruh **positif signifikan** terhadap IPM
   Kota Jambi (+0,0521 poin per satuan indeks).
2. **H2 tidak didukung** — belanja modal kesehatan berpengaruh **negatif signifikan**
   (−0,0660 poin). Bukan berarti belanja kesehatan merugikan IPM, melainkan dapat mencerminkan
   pola *alokasi berbasis kebutuhan* dan efek jangka panjang belanja modal.
3. Secara simultan kedua variabel berpengaruh signifikan terhadap IPM.

## Struktur Repositori

```
.
├── Analisis_Regresi_OLS_Belanja_Dasar_vs_IPM.ipynb   # Notebook utama (sudah dieksekusi)
├── data/
│   └── dataset_fiskal_97_hipoFull.csv                 # Dataset panel 97 kota
├── docs/
│   └── index.html                                     # Webapp dashboard (GitHub Pages ready)
├── requirements.txt
├── LICENSE
└── README.md
```

## Alur Analisis

1. **Import library** — NumPy, Pandas, Statsmodels, Plotly.
2. **Memuat data** — dataset panel 97 kota, disaring untuk Kota Jambi (2014–2024).
3. **Statistik deskriptif & korelasi**.
4. **Estimasi regresi OLS** — output `summary()` dan tabel koefisien.
5. **Visualisasi** — 2 scatter + garis regresi, diagram batang koefisien, dan **bidang regresi 3D**.
6. **Kesimpulan & interpretasi**.

Untuk menganalisis kota lain, cukup ubah satu baris di sel pemuatan data:

```python
KOTA_FOKUS = "Kota Jambi"   # ganti dengan nama kota lain
```

## Tampilan Visualisasi

Grafik pada notebook sudah dikonfigurasi agar **terlihat di mana saja**:

| Lingkungan | Yang tampil |
|---|---|
| **GitHub** | Gambar statis (PNG) — karena output notebook disimpan sebagai gambar |
| **Jupyter / JupyterLab** | Gambar statis (PNG), bila `kaleido` terpasang |
| **Google Colab** | Grafik **interaktif**, karena `kaleido` tidak tersedia di Colab |

Cara kerjanya: notebook memakai `kaleido` bila tersedia untuk menghasilkan PNG, dan otomatis
beralih ke renderer interaktif (`colab` / `notebook_connected`) bila tidak tersedia.
Instal `kaleido` secara lokal dengan `pip install kaleido` bila ingin output PNG.

## Versi Webapp

Folder `docs/` berisi **dashboard statis** hasil analisis (satu berkas `index.html`, 16 KB,
tanpa server maupun build step). Isinya:

- Kartu ringkasan: jumlah observasi, R², Adj. R², F-statistik, jumlah variabel signifikan
- Persamaan regresi dan tabel koefisien lengkap
- **5 grafik interaktif**: 2 scatter + garis regresi, diagram batang koefisien,
  perkembangan IPM Kota Jambi, dan **bidang regresi 3D** (dapat diputar/di-zoom)

**Melihat secara lokal:** buka `docs/index.html` di browser (klik dua kali).

**Hosting gratis via GitHub Pages:**

1. Push repositori ini ke GitHub.
2. Buka **Settings → Pages**.
3. Pada *Source*, pilih **Deploy from a branch** → branch `main` → folder **`/docs`** → **Save**.
4. Tunggu 1–2 menit, webapp tersedia di `https://<username>.github.io/<nama-repo>/`.

## Cara Menjalankan Notebook

```bash
git clone <url-repo-anda>
cd OLS_Belanja_Dasar_vs_IPM
pip install -r requirements.txt
jupyter notebook Analisis_Regresi_OLS_Belanja_Dasar_vs_IPM.ipynb
```

Notebook juga dapat dijalankan langsung di **Google Colab** tanpa konfigurasi tambahan.

## Sumber Data

`https://raw.githubusercontent.com/Alam-A99/DATAAKSI/main/dataset_fiskal_97_hipoFull.csv`

## Push ke GitHub

Repositori lokal sudah di-*commit* dan siap di-*push*:

```bash
git remote add origin https://github.com/<username>/<nama-repo>.git
git branch -M main
git push -u origin main
```

---

## Lisensi

MIT License — bebas digunakan untuk keperluan akademik dan penelitian.
