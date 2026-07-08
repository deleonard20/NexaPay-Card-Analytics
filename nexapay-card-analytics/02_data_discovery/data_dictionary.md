# 02 — Data Dictionary

Two source tables are joined on the cardholder key (`card.client_id` ↔ `user.id`).

## `card.csv` — Card-level table

| Column | Type | Description |
|--------|------|-------------|
| `id` | string | Card ID (unique per card) |
| `client_id` | string | Cardholder ID — foreign key to `user.id` |
| `card_brand` | string | Card brand: Mastercard, Visa, American Express, JCB |
| `credit_limit` | float | Credit limit (Rp); `0` = no credit facility |
| `expires` | datetime | Card expiry date |
| `acct_open_date` | datetime | Account opening date |
| `year_pin_last_changed` | int | Year the PIN was last changed |
| `days_since_last_trx` | int | Days since the last transaction (→ RFM Recency) |
| `count_nonfraud_trx_L6M` | int | Count of non-fraud transactions, last 6 months (→ RFM Frequency) |
| `amt_nonfraud_trx_L6M` | float | Value of non-fraud transactions, last 6 months (→ RFM Monetary) |
| `count_fraud_trx_L6M` | int | Count of fraudulent transactions, last 6 months |
| `amt_fraud_trx_L6M` | float | Value of fraudulent transactions, last 6 months |
| `card_number` | string | **Dropped** — sensitive, irrelevant to analysis |
| `cvv` | string | **Dropped** — sensitive, irrelevant to analysis |

## `user.csv` — Cardholder-level table

| Column | Type | Description |
|--------|------|-------------|
| `id` | string | Cardholder ID — primary key |
| `birthdate` | datetime | Date of birth |
| `per_capita_income` | float | Per-capita income (Rp) |
| `yearly_income` | float | Annual income (Rp) |
| `total_debt` | float | Total outstanding debt (Rp) |
| `credit_score` | int | Credit score (300–850) |
| `retirement_age` | int | Expected retirement age |

## Derived fields (feature engineering)

| Column | Source | Definition |
|--------|--------|------------|
| `age` | `user.birthdate` | `(cutoff_date − birthdate).days // 365` (cutoff = 2025-08-10) |
| `retired_flag` | `age` | `1` if `age ≥ 60`, else `0` |
| `DTI` | `user.total_debt`, `user.yearly_income` | `total_debt ÷ yearly_income` (Debt-to-Income ratio) |

## Key reference values

| Item | Definition |
|------|------------|
| DTI risk bands | Low `< 0.30` · Medium `< 0.60` · High `≥ 0.60` |
| Credit-score bands | 300–579 Poor · 580–669 Fair · 670–739 Good · 740–799 Very Good · 800–850 Exceptional |
| Profit model | MDR fee `1.5%` × non-fraud value − fraud value |
| Fraud rate | total fraud value ÷ total transaction value |

---

*Dataset is synthetic and used for portfolio demonstration.*
