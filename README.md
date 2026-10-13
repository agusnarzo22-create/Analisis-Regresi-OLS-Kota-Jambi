# Analisis Regresi OLS: Belanja Modal Pendidikan & Kesehatan terhadap IPM

Analisis **regresi linier berganda (Ordinary Least Squares)** untuk menguji pengaruh
**Belanja Modal Pendidikan** ($X_1$) dan **Belanja Modal Kesehatan** ($X_2$) terhadap
**Indeks Pembangunan Manusia / IPM** ($Y$) pada **97 kota di Indonesia (2014–2024)**.

---

## Model Penelitian

$$\text{IPM} = \beta_0 + \beta_1 \cdot \text{bm\_pendidikan} + \beta_2 \cdot \text{bm\_kesehatan} + \varepsilon$$

| Simbol | Variabel | Keterangan |
|---|---|---|
| $Y$ | `IPM` | Indeks Pembangunan Manusia |
| $X_1$ | `bm_pendidikan` | Belanja modal fungsi pendidikan |
| $X_2$ | `bm_kesehatan` | Belanja modal fungsi kesehatan |

## Hasil Utama

Persamaan regresi terestimasi (N = 1.067 observasi):

$$\widehat{\text{IPM}} = 73{,}2347 + 0{,}002592 \cdot X_1 - 0{,}007432 \cdot X_2$$

| Variabel | Koefisien | Std. Error | t | p-value | Keputusan |
|---|---|---|---|---|---|
| Konstanta | 73,2347 | 0,7678 | 95,382 | < 0,001 | Signifikan |
| `bm_pendidikan` | +0,002592 | 0,003006 | 0,863 | 0,3886 | Tidak signifikan |
| `bm_kesehatan` | −0,007432 | 0,003027 | −2,455 | 0,0142 | Signifikan (negatif) |

- **R² = 0,0062** · **Adj. R² = 0,0044** · **F = 3,331 (p = 0,0361)**

**Kesimpulan:** belanja modal pendidikan tidak berpengaruh signifikan terhadap IPM, sedangkan
belanja modal kesehatan signifikan dengan arah negatif. Daya penjelas model rendah (0,62%),
menandakan IPM lebih ditentukan faktor lain di luar belanja modal layanan dasar.

> Grafik Plotly bersifat interaktif dan paling baik dilihat di **Jupyter / JupyterLab / Google Colab**.

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

## Versi Webapp

Folder `docs/` berisi **dashboard statis** hasil analisis (satu berkas `index.html`, tanpa
server maupun build step).

**Fitur:**

- **Pemilih kota interaktif** — centang kota yang ingin dianalisis (dilengkapi pencarian,
  *Pilih Semua*, *Kosongkan*, dan *Balik Pilihan*). Seluruh angka, tabel, dan grafik
  dihitung ulang **real-time di browser**.
- Kartu ringkasan: jumlah observasi, R², Adj. R², F-statistik, jumlah variabel signifikan.
- Persamaan regresi dan tabel koefisien (koefisien, std. error, t-stat, p-value, keputusan).
- **5 grafik interaktif**: scatter pendidikan vs IPM, scatter kesehatan vs IPM, diagram batang
  koefisien, tren rata-rata IPM tahunan, dan **grafik 3D bidang regresi** (*scatter3d* + *surface*).
- Kesimpulan yang ikut diperbarui mengikuti hasil perhitungan.

> Regresi di browser dihitung dengan *normal equations* dan telah diverifikasi identik
> dengan output `statsmodels` (baik untuk seluruh 97 kota maupun subset kota).

**Melihat secara lokal:** cukup buka `docs/index.html` di browser (klik dua kali).

**Hosting gratis via GitHub Pages:**

1. Push repositori ini ke GitHub.
2. Buka **Settings → Pages**.
3. Pada *Source*, pilih **Deploy from a branch** → branch `main` → folder **`/docs`** → **Save**.
4. Tunggu 1–2 menit, webapp akan tersedia di:
   `https://<username>.github.io/<nama-repo>/`

## Alur Analisis

1. **Import library** — NumPy, Pandas, Statsmodels, Plotly.
2. **Memuat data** — dataset panel 97 kota × 11 tahun.
3. **Filter kota (opsional)** — isi variabel `KOTA_DIPILIH` untuk membatasi analisis pada
   kota tertentu; kosongkan untuk memakai seluruh kota.
4. **Statistik deskriptif & korelasi**.
5. **Estimasi regresi OLS** — output `summary()` dan tabel koefisien.
6. **Visualisasi** — scatter + garis regresi, diagram batang koefisien, dan **bidang regresi 3D**.
7. **Kesimpulan & interpretasi**.

## Cara Menjalankan

```bash
# 1. Clone repositori
git clone <url-repo-anda>
cd OLS_Belanja_Dasar_vs_IPM

# 2. (Opsional) buat virtual environment
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

# 3. Pasang dependensi
pip install -r requirements.txt

# 4. Jalankan notebook
jupyter notebook Analisis_Regresi_OLS_Belanja_Dasar_vs_IPM.ipynb
```

Notebook juga dapat dijalankan langsung di **Google Colab** tanpa konfigurasi tambahan.

## Sumber Data

`https://raw.githubusercontent.com/Alam-A99/DATAAKSI/main/dataset_fiskal_97_hipoFull.csv`

## Push ke GitHub

Repositori lokal sudah di-*commit* dan siap di-*push*. Jalankan:

```bash
# 1. Buat repositori kosong di GitHub (tanpa README), lalu:
git remote add origin https://github.com/<username>/<nama-repo>.git
git branch -M main
git push -u origin main
```

---

## Lisensi

MIT License — bebas digunakan untuk keperluan akademik dan penelitian.
