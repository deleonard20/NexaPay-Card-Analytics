# 03 — Data Preparation & Cleaning Notes

All steps were performed in `pandas` (see `04_analysis/notebook/nexapay_card_analytics.ipynb`).

## Card Data (`card.csv`)

| Step | Action | Reasoning | Result |
|------|--------|-----------|--------|
| 1 | Cast data types to match the data dictionary (`id`/`client_id` → string, `expires`/`acct_open_date` → datetime, currency fields → float, count fields → int) | Correct types enable reliable processing | Types aligned |
| 2 | Parse currency with `clean_currency()` — strip `Rp` and thousands separators, cast to float | Currency stored as text cannot be aggregated | Numeric currency columns |
| 3 | Impute missing values with `0` | An empty `credit_limit` = no credit facility; empty transaction fields = no activity in the window | 0% missing |
| 4 | Fix `card_brand` typos (`Jcb` → `JCB`, trim whitespace) | Consistent categories for grouping | Clean brand values |
| 5 | Drop `card_number` and `cvv` | Sensitive PII, irrelevant to the analysis | Columns removed |
| 6 | Remove duplicate rows | Identical records recorded twice would bias counts | Duplicates dropped |
| 7 | Filter out expired cards (expiry ≤ 2025-05-31) and `credit_limit == 0` | Expired / never-used cards cannot transact | **5,559 → 5,528 rows** |

## User Data (`user.csv`)

| Step | Action | Reasoning | Result |
|------|--------|-----------|--------|
| 1 | Cast types (`id` → string, `birthdate` → datetime, income/debt → float) | Match the data dictionary | Types aligned |
| 2 | Add `age` = `(cutoff − birthdate).days // 365` (cutoff 2025-08-10) | Enables age-band and retirement analysis | New column |
| 3 | Add `retired_flag` = `1` if `age ≥ 60` | Retirees show lower, more stable activity | New column |
| 4 | Add `DTI` = `total_debt ÷ yearly_income` | Assesses financial health / default risk | New column |

## Merge & Outlier Handling

| Step | Action | Reasoning |
|------|--------|-----------|
| 1 | Merge `card × user` (inner join, `client_id` ↔ `id`) | Combine card behaviour with cardholder profile |
| 2 | Remove `yearly_income` & `total_debt` outliers via the **IQR method** | Extreme values distort averages and segmentation |

## Key Assumptions

- Missing `credit_limit` indicates **no credit facility** (set to 0, then filtered out).
- Missing transaction counts/values indicate **no activity** in the L6M window (set to 0).
- Expiry cutoff of **2025-05-31** defines a still-active card.
- Card profit is modelled from an **MDR fee of 1.5%** on non-fraud transaction value.

---

*Dataset is synthetic and used for portfolio demonstration.*
