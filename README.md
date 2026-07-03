# 🛒 DQFresh Mart — Retail Crisis & Recovery Visualization Challenge

Solution to DQLab's `HACK-2026-PYTHON-01` hackathon: find *Rising Star* products
(consistent growth hidden by traditional top-10 dashboards) and frequent
product-pair bundles, using pandas and the Apriori algorithm.

## Problem

DQFresh Mart's dashboards only ever surface the same top-10 bestsellers by
total sales. That hides products with a strong, sustained upward trend —
the "rising stars" — and gives no signal on which products get bought
together. The task (full brief in [`SOAL-HACKATHON.pdf`](SOAL-HACKATHON-2026-PYTHON-01/SOAL-HACKATHON.pdf)):

1. **Rising Star Analysis** — for each product, compute a 3-day moving
   average of daily sales, find the longest run of consecutive up-days
   (the "rising trend session"), keep products with a session ≥ 12 days,
   and rank by growth % (session end vs. session start).
2. **Potential Packaging** — mine frequent product pairs bought in the
   same transaction with Apriori (via `mlxtend`).
3. Export both results to Excel and chart the rising stars.

## Data

[`data_penjualan.xlsx`](SOAL-HACKATHON-2026-PYTHON-01/data_penjualan.xlsx) — 42,446 transaction line items:

| column | meaning |
|---|---|
| `nomor_struk` | receipt/transaction number |
| `tgl_transaksi` | transaction date |
| `kode_produk` / `nama_produk` | product code / name |
| `jumlah_terjual` | quantity sold |
| `harga` | unit price |
| `total_nilai` | line total |

## Solution

[`solusi_retail.ipynb`](solusi_retail.ipynb) — run top to bottom:

1. Environment setup (`pandas`, `matplotlib`, `mlxtend`, `openpyxl`)
2. Load & inspect the dataset
3. Rising Star analysis (moving average → trend session → growth %)
4. Potential Packaging via Apriori
5. Export to `retail_insight.xlsx`
6. Visualizations → `rising_star_index.png`, `rising_star_actual.png`

## Setup

```bash
pip install pandas==2.3.1 matplotlib==3.10.7 mlxtend==0.23.4 openpyxl==3.1.5
jupyter notebook solusi_retail.ipynb
```

## Output

- `retail_insight.xlsx` — *Rising Star* and *Potential Packaging* sheets
- `rising_star_index.png` — indexed (relative, base 100) growth chart
- `rising_star_actual.png` — actual moving-average sales value chart

Reference outputs are in
[`SOAL-HACKATHON-2026-PYTHON-01/`](SOAL-HACKATHON-2026-PYTHON-01) as
`retail_insight_example.xlsx` and the `*_incomplete.png` charts (the
starter charts to be completed as part of the challenge).
