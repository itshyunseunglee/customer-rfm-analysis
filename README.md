# Customer RFM Segmentation

Used a marketing dataset to segment customers based on RFM (Recency, Frequency, Monetary) scores and explored the behavioral and demographic differences between segments.

---

## Dataset

`data/customer_data.csv` — tab-separated, 2,240 rows × 23 columns.

Key columns:
- `signup_ym`, `birth_year`, `annual_income`, `marital_status`, `children`
- `recency` — days since last purchase
- `amount_alcohol`, `amount_fruit`, `amount_meat`, `amount_fish`, `amount_snack`, `amount_general`
- `num_purchase_web`, `num_purchase_store`, `num_purchase_discount`
- `promotion_1` through `promotion_6` — binary flags for each campaign

---

## What I did

**Preprocessing**
- Dropped 24 rows with missing `annual_income`
- Converted `birth_year` to `age` (2023 baseline)
- Removed 3 outliers with age ≥ 100 (likely data entry errors)
- Removed income outliers using IQR method
- Created `amount_total` (sum of all category amounts) and `num_purchase_total` (sum of all channel counts)
- Binned age into groups: under_20s, 30s, 40s, 50s, over_60

**RFM Scoring**
- Each of R, F, M was split into 3 quantile-based grades using `pd.qcut`
- Recency graded in reverse (lower recency = better)
- Final RFM score = R×0.2 + F×0.4 + M×0.4
- Mapped scores to 3 segments (1 = low, 3 = high value)

**Segment Profiling**
Broke down each segment by:
- Age group and marital status distribution
- Number of dependent children
- Spending share by product category (alcohol, meat, etc.)
- Average promotion acceptance rate per campaign

---

## Findings

- Alcohol and meat consistently make up the largest spending share across all segments
- High-value customers (segment 3) show noticeably higher promotion engagement, especially campaigns 1, 4, and 5
- Low-value customers (segment 1) barely interact with promotions except campaign 6
- Spending per segment differs significantly — segment 3 accounts for a disproportionate share of total revenue

---

## Stack

Python, pandas, matplotlib, seaborn

---

## Structure

```
Market_project/
├── data/
│   └── customer_data.csv
├── RFM_analysis.ipynb
└── README.md
```
