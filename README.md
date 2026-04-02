# Marketing-Performance-Dashboard
This Power BI dashboard provides a comprehensive view of Company A's digital marketing performance.


# 📊 Marketing Performance Dashboard
### Company A — Power BI Interactive Dashboard

---

## 🗂 Project Overview

This Power BI dashboard provides a comprehensive view of Company A's digital marketing performance across **4 channels** (Email, SMS, Social Media, Paid Search) over **104 weeks (Jan 2023 – Dec 2024)**.

The dashboard translates complex Marketing Mix Model (MMM) outputs and incrementality test results into clear, actionable insights for leadership and marketing teams.

> **Note:** Company A is an anonymized client. All data is simulated to reflect realistic marketing dynamics.

---

## 📋 Dashboard Pages

### Page 1 — Executive KPI Overview
 <img width="1300" height="733" alt="image" src="https://github.com/user-attachments/assets/a469eed5-2664-4c43-a122-e77455673bd7" />


High-level marketing performance summary including:
- Total Revenue, Total Spend, Conversions, Avg ROAS
- Weekly Revenue vs Spend trend
- Monthly Revenue vs Spend comparison
- Year and Quarter filters

**Key Insight:** Company A generated **$11.53M in revenue** from **$4.07M in media spend** — delivering an overall ROAS of 2.83x over 104 weeks.

---

### Page 2 — Channel Performance & ROAS
 <img width="1296" height="733" alt="image" src="https://github.com/user-attachments/assets/d8cef511-db34-4f6a-b338-6005edf0606b" />


Deep dive into channel-level performance including:
- Average ROAS by channel
- Total Spend vs Revenue Contribution
- Weekly Spend trends by channel
- Adstock decay and carryover profile table

**Key Insight:** SMS delivers the highest ROAS (1.12) despite the lowest spend — an underleveraged channel. Social Media shows signs of oversaturation with the lowest ROAS (0.92).

---

### Page 3 — Budget Optimization
<img width="1302" height="735" alt="image" src="https://github.com/user-attachments/assets/223c9786-5db4-41a4-962e-a4b22a9b972f" />


MMM-based budget reallocation recommendations including:
- Current vs Optimized weekly spend by channel
- Budget reallocation % waterfall chart
- ROAS improvement comparison
- Full optimization summary table

**Key Recommendation:** Reallocate **$2,450/week from Social Media (-20%)** to Email (+16%) and SMS (+10%). Total budget remains unchanged at $39,168/week.

| Channel | Current | Optimized | Change |
|---|---|---|---|
| Email | $7,807 | $9,050 | +16% ↑ |
| SMS | $4,054 | $4,471 | +10% ↑ |
| Paid Search | $15,146 | $15,936 | +5% ↑ |
| Social Media | $12,161 | $9,711 | -20% ↓ |

---

### Page 4 — Incrementality Test Results
<img width="1300" height="732" alt="image" src="https://github.com/user-attachments/assets/308402d5-2a85-4228-9231-cd74c19d3e86" />

Geo-lift test results measuring causal impact of email campaigns:
- Test vs Control region revenue comparison
- Weekly incremental lift over time
- Average lift by period (Pre-Treatment vs Treatment)
- Statistical significance confirmation

**Key Finding:** Email campaigns generated **~$2,954/week in incremental revenue** during the treatment period — a **12.4% causal lift** above baseline (p < 0.05).

---

## 📦 Data Sources

| File | Description | Rows |
|---|---|---|
| `01_weekly_performance.csv` | Weekly revenue, spend, conversions | 104 |
| `02_channel_attribution.csv` | Channel-level spend, revenue, ROAS | 416 |
| `03_budget_optimization.csv` | Current vs optimized budget per channel | 4 |
| `04_geo_lift.csv` | Test vs control geo-lift data | 104 |
| `05_kpi_summary.csv` | High-level KPI summary | 10 |

---

## 🔗 Data Model Relationships

```
01_weekly_performance[date] → 02_channel_attribution[date]
01_weekly_performance[date] → 04_geo_lift[date]
```

---

## 🛠 DAX Measures Used

```dax
-- Overall ROAS
Avg ROAS = 
DIVIDE(
    SUM('01_weekly_performance'[revenue]),
    SUM('01_weekly_performance'[total_spend]),
    0
)

-- Incremental Lift (Treatment Period)
Avg Treatment Lift = 
CALCULATE(
    AVERAGE('04_geo_lift'[incremental_lift]),
    '04_geo_lift'[is_treatment] = "Treatment"
)

-- Budget Reallocation Amount
Reallocation Amount = 
SUMX(
    FILTER('03_budget_optimization', 
    '03_budget_optimization'[change_pct] > 0),
    '03_budget_optimization'[optimized_spend] - 
    '03_budget_optimization'[current_spend]
)
```

---

## 🚀 How to Use

1. Clone or download this repository
2. Open Power BI Desktop
3. Click **Get Data → Text/CSV**
4. Load all 5 CSV files from the `data/` folder
5. Set relationships:
   - `01_weekly_performance[date]` → `02_channel_attribution[date]`
   - `01_weekly_performance[date]` → `04_geo_lift[date]`
6. Build visuals following the screenshots

---
🔗 Related Project
This dashboard is the visualization layer for the full MMM analysis: [Company A — MMM & Incrementality Testing](https://github.com/azar2020/marketing-mix-modeling-Robyn)
 (Data simulated based on MMM model outputs from the R/Robyn project.)
 
## 🛠 Tech Stack

| Tool | Purpose |
|---|---|
| Power BI Desktop | Dashboard development |
| DAX | Custom measures and calculations |
| Python | Data simulation |
| R + Robyn | Underlying MMM model |

---

## 👤 Author

**Azar Taheri**
[LinkedIn](https://linkedin.com/in/azar-taheri)  
