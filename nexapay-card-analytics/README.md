# 💳 NexaPay Card Analytics
### Card Analytics Project — Nexantara Financial (NexaPay)

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat&logo=pandas&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=flat&logo=googlecolab&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat&logo=plotly&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 📌 Project Overview

This project analyzes **6 months of credit-card transaction activity** at **NexaPay**, a digital credit-card issuer operating under Nexantara Financial and serving retail cardholders across Indonesia through fully-digital onboarding.

The portfolio spans **5,528 active cards** and **1,938 cardholders** across four card brands (Mastercard, Visa, American Express, JCB). Despite a healthy fraud rate of just **0.22%**, fraudulent transactions still erode **~14–15% of card profit**, and RFM segmentation reveals **457 cardholders (23.6%)** who are warm but under-transacting.

This analysis quantifies the fraud-vs-profit trade-off, segments cardholders by behaviour, and delivers actionable recommendations aimed at a **15–25% transaction-frequency uplift** among priority segments — achieved more efficiently than costly new-customer acquisition.

---

## ❓ Problem Statement

NexaPay lacks visibility into where profit leaks to fraud and which cardholders are under-transacting, making it impossible to prioritize growth campaigns or fraud controls. Without structured segmentation, warm-but-low-frequency cardholders quietly slip toward dormancy while card brands and credit segments are treated uniformly, with no data-driven targeting.

---

## 🎯 SMART Objective

To quantify NexaPay's fraud impact on profit, segment **1,938 cardholders** by RFM behaviour, and deliver data-driven recommendations targeting a **15–25% transaction-frequency uplift** among priority segments within the next 6 months.

---

## 🔍 Key Findings

| # | Finding | Impact |
|---|---------|--------|
| 1 | **Fraud rate is low (0.22%)** — better than the 0.5–1.2% fintech average — yet still erodes **~14–15% of card profit** | Margin protection, not crisis: real-time monitoring is the lever |
| 2 | **457 cardholders (23.6%) are under-transacting** — 289 Potential Loyalists + 168 Customers Needing Attention | Direct target for a 15–25% frequency uplift |
| 3 | **Card brands behave differently** — Mastercard leads volume, Amex leads value, JCB lags on both | Enables brand-specific promotion and fraud monitoring |
| 4 | **Growth pockets are low-risk** — age 30–45 and the healthy-DTI "Good" credit segment are under-utilised | Highest, lowest-risk uplift potential |

---

## 💡 Recommendations

**1. Card Usage Incentives — target the 457 priority cardholders**
- Tiered milestone incentives (cashback / fee waivers) tied to the 3rd, 5th and 8th transaction — light on margin
- Personalised nudges via in-app, WhatsApp and email based on past spend categories (dining, travel, top-ups)

**2. Loyalty / Membership Program — protect the top segments**
- Points or tiered membership rewarding repeat card usage, unlocking benefits at usage tiers
- Retention guardrails: alert when a Loyal/Champion cardholder's recency slips, then trigger re-engagement

**3. Real-Time Fraud Management — protect the ~14–15% profit erosion**
- Score transactions live; flag high-risk channel / merchant / method patterns
- Apply step-up OTP **only** to high-risk transactions — cut losses without adding friction for everyone

---

## 💰 Business Impact

| Metric | Value |
|--------|-------|
| Active Cards (cleaned) | 5,528 |
| Cardholders analyzed | 1,938 |
| Fraud rate (L6M) | 0.22% |
| Card profit eroded by fraud | ~14–15% |
| Priority cardholders (under-transacting) | 457 (23.6%) |
| **Targeted transaction-frequency uplift** | **15–25%** among priority segments |

> Profit is modelled from an MDR fee of **1.5%** on non-fraud transaction value, less total fraud value. Absolute rupiah figures are intentionally omitted because the dataset is synthetic; impact is expressed as the targeted frequency uplift.

---

## 🛠 Tools & Methodology

| Stage | Tool | Activity |
|-------|------|----------|
| Environment | Google Colab | Cloud notebook execution |
| Data Loading | Python (gdown) | Import `card.csv` + `user.csv` from source |
| Data Cleaning | Python (pandas, numpy) | Type casting, `clean_currency` parsing, missing-value treatment, de-duplication |
| Feature Engineering | pandas | Derive Age, Retired flag, DTI; merge card × user |
| EDA | pandas + Matplotlib/Seaborn | Profit & fraud, card-brand behaviour, DTI, age vs credit limit |
| RFM Segmentation | pandas | `qcut` quintile scoring, segment mapping, priority quantification |
| Communication | PowerPoint | Answer-first insight deck with recommendations |

---

## 📊 Analysis Deep Dive

### Layer 1 — Profit & Fraud Performance

| Metric | Value |
|--------|-------|
| Fraud rate (L6M) | 0.22% |
| Profit eroded by fraud | ~14–15% |
| Profit model | MDR fee 1.5% × non-fraud value − fraud value |
| Benchmark — conventional banks | 0.1–0.2% |
| Benchmark — digital banks / fintech | 0.5–1.2% |

**Critical Insight:** NexaPay already beats the fintech average and approaches conventional-bank standards. The win is protecting the profit that fraud still quietly removes — via real-time monitoring and targeted step-up authentication, not blanket friction.

![Fraud Rate](05_communication/charts/02_fraud_rate.png)
![Fraud Benchmark](05_communication/charts/03_fraud_benchmark.png)

---

### Layer 2 — Financial Health & Growth Pockets

The credit-score-to-DTI relationship is **inverse** — higher credit scores carry lower Debt-to-Income ratios. Average credit limit rises steadily with age, peaking at 65+, while the 18–24 segment holds the lowest limits.

**Critical Insight:** The **30–45 age group** pairs financial stability with moderate limits, and the **"Good" credit segment** shows healthy DTI (~0.23) yet lower transaction counts than riskier tiers — both are low-risk pockets where awareness and targeted offers can safely lift card usage.

![DTI by Credit Score](05_communication/charts/04_dti_by_credit_score.png)

---

### Layer 3 — Cardholder RFM Segmentation

RFM applied at cardholder level on non-fraud L6M activity, each dimension scored 1–5 via quintile:

- **Recency** — days since last non-fraud transaction
- **Frequency** — count of non-fraud transactions (L6M)
- **Monetary** — total non-fraud transaction value (L6M)

| Segment | Cardholders | % Base |
|---------|-------------|--------|
| Hibernating | 772 | 39.8% |
| Champions | 398 | 20.5% |
| Potential Loyalist | 289 | 14.9% |
| Loyal Customers | 287 | 14.8% |
| Customers Needing Attention | 168 | 8.7% |
| At Risk | 16 | 0.8% |
| Recent | 5 | 0.3% |
| Promising | 3 | 0.2% |

**Critical Insight:** **Potential Loyalist (289) + Customers Needing Attention (168) = 457 cardholders** are warm but under-transacting — recent, healthy-risk, and cheaper to reactivate than acquiring new customers. This is the direct target for the 15–25% frequency uplift.

![RFM Segments](05_communication/charts/01_rfm_segments.png)

---

## 📁 Data Model

**Two source tables, merged on `client_id`**

```
card.csv  ──┐
            ├──  df_merged  (card × user, inner join on client_id ↔ id)
user.csv  ──┘
```

| Table | Rows (raw → clean) | Description |
|-------|--------------------|-------------|
| card.csv | 5,559 → 5,528 | Card-level: brand, credit limit, expiry, L6M non-fraud & fraud count/value |
| user.csv | 1,938 | Cardholder master: birthdate, income, debt — enriched with Age, Retired flag, DTI |

**Data Window:** Last 6 Months (L6M) of non-fraud transaction activity
**Dataset:** Synthetic, structured to reflect realistic Indonesian digital credit-card patterns

---

## 🔑 Python / pandas Techniques Used

| Technique | Applied In |
|-----------|-----------|
| `pd.qcut(..., q=5)` | RFM quintile scoring (R, F, M) |
| `groupby().agg()` | RFM aggregation per cardholder |
| `clean_currency()` | Parsing `Rp` / thousands separators to float |
| IQR method | Income & debt outlier removal |
| Derived columns | Age, Retired flag (≥60), DTI = total_debt ÷ yearly_income |
| `pd.to_datetime` / `astype` | Type casting to match data dictionary |
| `merge(how='inner')` | Joining card × user on `client_id` |

---

## 📁 Project Structure

```
nexapay-card-analytics/
├── 01_define/
│   └── business_brief.md
├── 02_data_discovery/
│   └── data_dictionary.md
├── 03_data_preparation/
│   └── cleaning_notes.md
├── 04_analysis/
│   └── notebook/
│       └── nexapay_card_analytics.ipynb
├── 05_communication/
│   ├── deck/
│   │   └── NexaPay_Card_Analytics_Deck.pptx
│   └── charts/
│       ├── 01_rfm_segments.png
│       ├── 02_fraud_rate.png
│       ├── 03_fraud_benchmark.png
│       └── 04_dti_by_credit_score.png
├── 06_action/
│   └── recommendations.md
├── data/
│   └── raw/            # place card.csv & user.csv here (not tracked)
└── README.md
```

---

## 🎯 6-Month Implementation Roadmap

**Phase 1: Implement (Month 1–2)**
- Launch tiered usage incentives (3rd/5th/8th transaction)
- Stand up real-time fraud monitoring + step-up OTP rules
- Enrol priority segments into a loyalty pilot

**Phase 2: Monitor (Month 3–4)**
- Track frequency uplift by segment & card brand
- Refresh RFM monthly — catch new at-risk cardholders
- Watch the fraud-loss ratio vs baseline

**Phase 3: Evaluate (Month 5–6)**
- Measure uplift vs the 15–25% target
- Tune incentive tiers and fraud guardrails
- Report ROI to the business

---

## 🔗 Connect

**Deleonard Simanjorang**
Data Analyst | Card Analytics & People Analytics
📧 deleonard20@gmail.com
💼 [LinkedIn](https://www.linkedin.com/in/deleonard-simanjorang)
📱 WhatsApp: +62 812 4154 4992
🐙 [GitHub](https://github.com/deleonard20)

---

**⭐ If you found this analysis helpful, please consider starring this repository!**

> *Note: NexaPay / Nexantara Financial is a fictional company; the dataset is synthetic and used for portfolio demonstration.*
