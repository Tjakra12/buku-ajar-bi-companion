# Companion Materials — Buku Ajar Business Intelligence

**Dataset & material pendamping untuk Buku Ajar Business Intelligence: Dari Data Mentah ke Keputusan Cerdas**

Penulis: **Raden Johnny Hadi Raharjo, SE., MM.**  
Program Studi Manajemen — Universitas Pembangunan Nasional "Veteran" Jawa Timur  
Edisi Pertama, 2026

---

## Tentang Repository Ini

Repository ini berisi **dataset, panduan, dan starter code** yang menyertai buku ajar. Tujuannya: agar pembelajar mandiri di seluruh Indonesia dapat mempraktikkan setiap teknik BI yang dibahas di buku, tanpa perlu meminta dataset ke dosen atau institusi tertentu.

Buku dapat dibaca tanpa repository ini, tapi repository ini **tidak bisa berdiri sendiri** — referensi ke nomor bab dan studi kasus mengacu pada buku.

## Cara Pakai

### Untuk pembelajar yang baru mulai

1. **Download seluruh repository** dengan klik tombol hijau `<> Code` → `Download ZIP` di pojok kanan atas halaman utama repository ini.
2. **Ekstrak ZIP** di folder yang mudah diingat di laptop Anda (misal: `Documents/buku-ajar-bi/`).
3. **Buka buku** di Bab 1 dan ikuti alurnya. Setiap kali buku menyebutkan dataset, file-nya ada di folder yang sesuai di repository ini.

### Untuk pembelajar yang sudah pakai Python

Load dataset langsung dari URL tanpa download manual:

```python
import pandas as pd

BASE = 'https://raw.githubusercontent.com/Tjakra12/buku-ajar-bi-companion/main/dataset-master-roti-nusantara'

df_transaksi = pd.read_csv(f'{BASE}/transactions_clean.csv')
df_produk = pd.read_csv(f'{BASE}/products.csv')
df_toko = pd.read_csv(f'{BASE}/customers.csv')

print(df_transaksi.head())
print(f'Jumlah transaksi: {len(df_transaksi):,} baris')
```

## Struktur Repository

```
buku-ajar-bi-companion/
├── README.md                           ← file ini
├── LICENSE                             ← Creative Commons BY-NC 4.0
├── ERRATA.md                           ← daftar koreksi typo & klarifikasi
│
├── dataset-master-roti-nusantara/      ← dataset utama Bab 1–14
│   ├── transactions_clean.csv          ← transaksi bersih (39.453 baris)
│   ├── transactions_messy.csv          ← transaksi mentah (40.242 baris) — untuk ETL practice
│   ├── customers.csv                   ← master toko/pelanggan
│   ├── products.csv                    ← master produk
│   ├── customer_reviews.csv            ← review pelanggan
│   ├── finance_monthly.csv             ← finance bulanan 24 bulan
│   ├── finance_cashflow_monthly.csv    ← cashflow bulanan
│   ├── hr_employees.csv                ← data karyawan
│   ├── hr_engagement_survey.csv        ← survei engagement
│   ├── hr_engagement_survey_codebook.csv ← codebook survei
│   ├── marketing_campaigns.csv         ← kampanye marketing
│   └── operation_daily.csv             ← operasional harian 4 tahun
│
├── dataset-capstone-nsi/               ← dataset Capstone (Bab 15) PT Nusantara Segar
│   ├── 00_README.md
│   ├── 00_DATA_DICTIONARY.md
│   ├── 01_store_master.csv             (350 toko)
│   ├── 02_sku_master.csv               (2.000 SKU)
│   ├── 03_pos_transactions_q4_2025.csv (50.000 transaksi)
│   ├── 04_inventory_snapshot.csv       (16.648 snapshot)
│   ├── 05_hr_employees.csv             (5.066 karyawan)
│   ├── 06_customer_complaints.csv      (5.000 ticket)
│   ├── 07_marketing_campaigns.csv      (350 kampanye)
│   ├── 08_financial_gl_monthly.csv     (336 line items)
│   └── 09_nps_survey.csv               (12.000 response)
│
├── CONTOH_DATA_BAB9.xlsx               ← contoh khusus untuk forecasting Bab 9
│
└── notebooks/
    └── 00_starter_load_all_data.ipynb  ← Jupyter starter siap pakai
```

## Pemetaan Dataset ke Bab Buku

| Bab | Topik | Dataset yang dipakai |
|---|---|---|
| Bab 1 | Selamat Datang di BI | Konseptual (tidak ada dataset) |
| Bab 2 | Data Sebagai Bahan Bakar Keputusan | `dataset-master-roti-nusantara/transactions_messy.csv` |
| Bab 3 | Toolkit Wajib BI | `dataset-master-roti-nusantara/transactions_clean.csv` |
| Bab 4 | Konsep ETL | `dataset-master-roti-nusantara/transactions_messy.csv` |
| Bab 5 | ETL Power Query | `dataset-master-roti-nusantara/transactions_messy.csv` |
| Bab 6 | ETL Google Sheets | `dataset-master-roti-nusantara/transactions_messy.csv` |
| Bab 7 | Descriptive Analytics | `transactions_clean.csv` + `products.csv` + `customers.csv` |
| Bab 8 | Diagnostic Analytics | `transactions_clean.csv` |
| Bab 9 | Predictive Analytics | `finance_monthly.csv` + `CONTOH_DATA_BAB9.xlsx` |
| Bab 10 | Data Mining | `transactions_clean.csv` + `customers.csv` |
| Bab 11 | Prescriptive Analytics | `transactions_clean.csv` (RFM analysis) |
| Bab 12 | Merancang KPI | `finance_monthly.csv` + `operation_daily.csv` |
| Bab 13 | Dashboard Looker Studio | `transactions_clean.csv` + lainnya |
| Bab 14 | Data Storytelling | `transactions_clean.csv` |
| Bab 15 | Capstone 5-Track | **Seluruh** `dataset-capstone-nsi/` |
| Bab 16 | Karier BI | Refleksi (tidak ada dataset) |

## Lisensi

Repository ini dilisensikan di bawah **Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)**.

**Anda boleh:**
- Mengunduh, menggunakan, dan memodifikasi dataset untuk pembelajaran pribadi
- Membagikan ulang ke teman sekelas atau komunitas
- Memakainya untuk pengajaran di institusi pendidikan

**Anda tidak boleh:**
- Menjual dataset ini atau turunannya untuk keuntungan komersial
- Menggunakan dalam produk berbayar tanpa izin tertulis penulis

**Anda wajib:**
- Mencantumkan kredit ke penulis: *"Dataset bersumber dari Buku Ajar Business Intelligence oleh Raden Johnny Hadi Raharjo, UPN Veteran Jawa Timur, 2026."*

Detail lengkap lihat file `LICENSE`.

## Catatan Penting

1. **Dataset bersifat sintetis** — dibuat khusus untuk pembelajaran. Skala, distribusi, dan pola dirancang menyerupai data nyata FMCG di Jawa Timur, tetapi tidak merepresentasikan perusahaan riil mana pun.

2. **Format file** — semua dataset utama dalam `.csv` (Comma Separated Values), bisa dibuka di Excel, Google Sheets, pandas Python, R, atau SQL apa pun.

3. **Encoding** — semua file CSV menggunakan UTF-8.

4. **Update & koreksi** — silakan buka [Issue](../../issues) di repository ini.

## Kontak

**Penulis:** Raden Johnny Hadi Raharjo, SE., MM.  
**Institusi:** Program Studi Manajemen, UPN "Veteran" Jawa Timur

Untuk pertanyaan teknis tentang dataset, buka [Issues](../../issues).

---

*Buku ini didedikasikan untuk seluruh pembelajar manajemen yang ingin memahami data — bukan karena terpaksa, tapi karena ingin membuat keputusan yang lebih baik.*
