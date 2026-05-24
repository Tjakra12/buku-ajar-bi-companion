# Dataset Capstone — PT Nusantara Sehat Indonesia (NSI)

Paket data sintetis ini didesain untuk Studi Kasus Capstone Business Intelligence
mahasiswa Manajemen Semester 7. Data sintetis tapi pola-polanya **realistis dan
menyertakan delapan gejala** yang disebutkan di dokumen kasus.

## Cara Pakai

1. **Mulai dari `00_README.md` dan `00_DATA_DICTIONARY.md`** untuk memahami struktur.
2. **Fase 1 ETL:** Mahasiswa harus mengaudit isu kualitas di tiap file (sengaja
   dibuat tidak rapi — ada inconsistency, missing values, format mixed).
3. **Fase 2 Diagnostic:** Pola 8 gejala TERTANAM dalam data. Mahasiswa harus
   mengidentifikasi via drill-down + korelasi.
4. **Fase 3-4:** Gunakan data untuk forecast, predictive model, dan prescriptive.

## Sembilan File Dataset

| File | Rows | Periode | Catatan Kualitas |
|------|------|---------|------------------|
| 01_store_master.csv | 350 | Master | Bersih |
| 02_sku_master.csv | 2.000 | Master | Bersih |
| 03_pos_transactions_q4_2025.csv | ~50.000 | Q4 2025 | Sample untuk audit ETL |
| 04_inventory_snapshot.csv | ~20.000 | 31 Des 2025 | expired_date banyak NULL |
| 05_hr_employees.csv | ~4.700 | Snapshot | Department names INCONSISTENT |
| 06_customer_complaints.csv | 5.000 | 2025 | category INCONSISTENT tagging |
| 07_marketing_campaigns.csv | 350 | 2024-2025 | Bersih |
| 08_financial_gl_monthly.csv | ~336 | 24 bulan | Bersih |
| 09_nps_survey.csv | 12.000 | 2025 | Bersih |

## Hint Diagnostic (untuk dosen/penilai)

Berikut pola yang TERTANAM dalam data — mahasiswa BAIK akan menemukan ini, mahasiswa
KURANG akan menyimpulkan "semua merata":

- **G1 SSSG drop:** Konsentrasi di toko Jawa kategori medium (60% dari toko medium Jawa
  menunjukkan penurunan 25% transaksi).
- **G2 conversion apps drop:** Setelah Mei 2025 (asumsi platform migration).
- **G4 inventory turnover:** Slow-moving items 21% (vs ~12% baseline), konsentrasi
  di kategori Wellness (last_sold_date >90 hari).
- **G5 Marketing turnover 28%:** Konsentrasi Q2-Q3 2025. Korelasi dengan G6.
- **G6 customer complaints stok_tidak_akurat naik 45%** setelah Q3 2025. Korelasi
  dengan G5 (response time naik karena kurang agen Marketing).
- **G7 Wellness margin compression:** COGS Wellness naik mulai Apr 2025 (kompetitor
  private label di marketplace memaksa diskon).
- **G8 EBITDA decline:** Akumulasi dari semua di atas.

## Data Quality Issues (sengaja ditanam — bagian dari Tugas ETL)

Mahasiswa harus IDENTIFY dan PERBAIKI minimum 24 isu kualitas (dari 5 dimensi). Beberapa
yang sudah tertanam:

- **HR**: kolom `department` tidak konsisten ("Marketing", "Mktg", "MARKETING")
- **Complaints**: kolom `category` tidak konsisten ("stok_tidak_akurat_apps", "stock_issue", "STOCK_INACCURATE")
- **Inventory**: kolom `expired_date` banyak NULL (~15%)
- **Mahasiswa diharapkan menemukan lebih banyak via audit sistematis**.
