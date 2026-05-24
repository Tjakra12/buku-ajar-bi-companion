# Data Dictionary — Dataset NSI

## 01_store_master.csv (350 rows)
| Column | Type | Description |
|--------|------|-------------|
| store_id | string | Format NSI-XXXX |
| store_name | string | Nama toko |
| region | string | Jawa/Sumatera/Sulawesi/Kalimantan/Bali/NTB |
| city | string | Kota |
| store_size | string | small/medium/large |
| store_format | string | apotek / apotek+klinik / apotek+wellness / apotek+klinik+wellness |
| has_klinik | int | 0 atau 1 |
| has_wellness | int | 0 atau 1 |
| open_date | date | YYYY-MM-DD |
| monthly_revenue_baseline_jt | int | Rp juta per bulan (baseline pre-2025) |

## 02_sku_master.csv (2.000 rows)
| Column | Type | Description |
|--------|------|-------------|
| sku_id | string | Format SKU-XXXXX |
| sku_name | string | Nama produk |
| category | string | apotek_resep / apotek_otc / wellness_suplemen / wellness_kosmetik / wellness_alat / klinik_lab |
| unit_price_idr | int | Harga jual per unit (IDR) |
| margin_pct | float | Persentase margin |
| supplier | string | Nama supplier |
| is_active | int | 0 atau 1 |
| introduced_date | date | YYYY-MM-DD |

## 03_pos_transactions_q4_2025.csv (~50.000 rows)
| Column | Type | Description |
|--------|------|-------------|
| transaction_id | string | Format TXN-XXXXXXXX |
| transaction_date | date | YYYY-MM-DD |
| transaction_time | time | HH:MM:SS |
| store_id | FK | → store_master |
| sku_id | FK | → sku_master |
| qty | int | Quantity |
| unit_price_idr | int | Harga saat transaksi |
| total_idr | int | qty × unit_price |
| customer_id | string | CUST-XXXXXX (kosong jika walk-in) |
| payment_method | string | cash/debit/credit/qris/gopay/ovo/dana/bca_va |
| source | string | offline / apps |

## 04_inventory_snapshot.csv (~20.000 rows)
| Column | Type | Description |
|--------|------|-------------|
| snapshot_date | date | 2025-12-31 |
| store_id | FK | → store_master |
| sku_id | FK | → sku_master |
| qty_on_hand | int | Stok di toko |
| qty_in_transit | int | Sedang dalam pengiriman |
| last_purchase_date | date | Terakhir restock |
| last_sold_date | date | Terakhir terjual |
| expired_date | date | **CATATAN: banyak NULL** |
| days_since_sold | int | Hari sejak terakhir terjual (turunkan dari last_sold_date) |

## 05_hr_employees.csv (~4.700 rows)
| Column | Type | Description |
|--------|------|-------------|
| employee_id | string | Format EMP-XXXXX |
| name | string | Nama karyawan |
| department | string | **CATATAN: TIDAK KONSISTEN** ("Marketing", "Mktg", "MARKETING") |
| position | string | Jabatan |
| hire_date | date | YYYY-MM-DD |
| exit_date | date | Kosong jika masih aktif |
| is_active | int | 0 atau 1 |
| salary_band | string | Band-1 sampai Band-5 |
| region | string | Lokasi kerja |

## 06_customer_complaints.csv (5.000 rows)
| Column | Type | Description |
|--------|------|-------------|
| ticket_id | string | Format TKT-XXXXXX |
| created_at | datetime | YYYY-MM-DD HH:MM:SS |
| customer_id | string | CUST-XXXXXX |
| category | string | **CATATAN: TIDAK KONSISTEN** tagging |
| description | string | Deskripsi |
| priority | string | low/medium/high |
| status | string | open/pending/closed/escalated |
| agent_id | string | AGT-XXX |
| response_time_hours | int | Jam hingga respons pertama |
| resolved_at | datetime | Kosong jika belum resolved |
| source | string | apps/website/whatsapp/phone |

## 07_marketing_campaigns.csv (350 rows)
| Column | Type | Description |
|--------|------|-------------|
| campaign_id | string | Format CAMP-XXXX |
| campaign_name | string | Nama kampanye |
| start_date | date | Mulai |
| end_date | date | Selesai |
| channel | string | digital_ads/apps_push/sms_blast/in_store_promo/loyalty/kol |
| target_segment | string | mass/wellness_premium/senior/young_family/b2b |
| budget_idr | int | Anggaran |
| revenue_attributed_idr | int | Revenue dari kampanye |
| roi | float | revenue/budget |
| owner | string | Marketing-X |

## 08_financial_gl_monthly.csv (~336 rows)
| Column | Type | Description |
|--------|------|-------------|
| month | string | YYYY-MM |
| account_code | string | 4-XXXX (revenue) / 5-XXXX (cogs) / 6-XXXX (opex) |
| account_name | string | Nama akun |
| segment | string | apotek/klinik/wellness/b2b/marketing/digital/supply/all |
| debit_idr_jt | int | Debit dalam IDR juta |
| credit_idr_jt | int | Credit dalam IDR juta |
| cost_center | string | APOTEK/KLINIK/WELLNESS/B2B/CORPORATE/MARKETING/DIGITAL/SUPPLY |

## 09_nps_survey.csv (12.000 rows)
| Column | Type | Description |
|--------|------|-------------|
| response_id | string | Format NPS-XXXXXX |
| response_date | date | Tanggal respons |
| customer_id | string | CUST-XXXXXX |
| channel_source | string | apps/in_store/b2b |
| nps_score | int | 0-10 |
| category | string | Promoter (9-10) / Passive (7-8) / Detractor (0-6) |
| top_complaint | string | Keluhan utama (kategorikal) |
| would_recommend | string | yes/no/definitely_no |
| comment_id | string | ID komentar bebas (kosong jika tidak ada) |

---

## Cara Join Tabel (Star Schema)

```
                  pos_transactions (fact)
                    │ store_id, sku_id, customer_id, date
                    ▼
  store_master  ◄──┴──►  sku_master
                    │
                    │  customer_id
                    ▼
              nps_survey, customer_complaints

  inventory_snapshot ──► store_id, sku_id
  hr_employees ──► department, region
  marketing_campaigns ──► date, target_segment
  financial_gl_monthly ──► month, segment
```
