# Stade de France — FNB Overstaffing Analysis

**What drives lateness and absenteeism among event staff, and how can we fix it?**

This project analyses two years of operational staffing data from CRIT Événementiel (Stade de France), covering 55+ events including the Rugby World Cup 2023 and Paris 2024 Olympics. The goal was to identify the root causes of no-shows and lateness in large-scale event staffing and propose data-backed recommendations to reduce operational waste.

**Data used with permission from CRIT Événementiel. All personal identifiers have been removed in compliance with GDPR.**
---

## Pipeline Architecture

```
55+ Raw Excel Files
        ↓
  Station A: Consolidation
  (EVENT_PIPE, HIRE_PIPE, RGDP_PIPE notebooks)
        ↓
  Station B: Transition
  (dataset.csv — uncleaned, consolidated)
        ↓
  Station C: Transformation
  (data_processing.ipynb)
        ↓
  clean_dataset.csv (27,648 rows — golden dataset)
        ↓
  Station D: Analytics
  (clean_stadefrance.ipynb)
        ↓
  Looker Studio Dashboard
```

---

## Dataset

| Property | Value |
|---|---|
| Source | CRIT Événementiel (private, used with formal agreement) |
| Coverage | 2023–2025, 55+ events |
| Final rows | 27,648 shifts |
| Columns | 27 |
| GDPR | All personal identifiers removed locally before cloud upload |

Raw source data is not included in this repository as it contains personal information. The clean, anonymized dataset is available in `/data/clean_dataset.csv`.

---

## 5 Key Insights

### 1. Gender — No impact found
No-show rate: Female 20.8% vs Male 21.5%. Late rate: Female 11.2% vs Male 14.9%.
Difference is not operationally significant.

### 2. Geography — Distance is not the problem
No-show rates vary by less than 4 percentage points across all Paris departments. Workers from further away compensate by arriving earlier, not later.

### 3. Age & Role — Role predicts reliability more than age
Manager: 15.6% no-show, 7.9% late — best performing role.
Runner: 18.9% no-show, 23.0% late — highest lateness rate.
Oldest workers (51+) are the most punctual age group.

### 4. Internal Process — The real bottleneck
82.7% of workers arrive at the stadium before their planned time (median 23.6 min early).
Yet 77.1% of on-time arrivals still start their shift late.
Average internal process time (check-in + accreditation + locker room): **53 minutes**.

> The problem is NOT recruitment — it is OPERATIONAL.

Reducing process time by 15 minutes across all affected shifts would recover **4,000+ working hours per year**.

### 5. Retention — Experience improves reliability
| Experience | No-show rate |
|---|---|
| 1–2 missions | 34.8% |
| 3–5 missions | 28.7% |
| 6–10 missions | 26.3% |
| 11–20 missions | 18.5% |
| 21+ missions | 11.0% |

Hypothesis rejected: experience does NOT reduce punctuality — it improves it significantly.

---

## Recommendations

**1. Gender doesn't matter**
Gender should not be used as a factor in recruitment or scheduling decisions.

**2. Distance is not the problem**
Investing in transport support based on geography would not meaningfully reduce operational risk.

**3. Hire by role, not demographics**
Focus on manager profiles for high-risk shifts. Role history is a stronger predictor of reliability than age or gender.

**4. Fix the internal flow**
Workers arrive early but the internal process — check-in, accreditation, locker room — takes 53 minutes on average. Reducing that by just 15 minutes across all affected shifts recovers over 4,000 working hours per year.

**5. Build a loyalty program**
Reward high-attendance workers. Link mission count to scheduling priority and incentives. Retaining experienced workers is the lowest-cost lever for reducing no-shows.

---

## Tools

| Tool | Purpose |
|---|---|
| Python (pandas, seaborn, matplotlib) | Data processing and visualization |
| Google Colab | Collaborative notebook environment |
| Google Drive | Shared storage and versioning |
| Looker Studio | Interactive dashboard |

---

## Repository Structure

```
stadefrance-fnb-overstaffing/
├── notebooks/
│   ├── data_processing.ipynb      # Station C: cleaning, translation, feature engineering
│   └── clean_stadefrance.ipynb    # Station D: analysis, 5 insights, charts
├── data/
│   └── clean_dataset.csv          # Golden dataset: 27,648 rows, anonymized
├── dashboard/
│   └── dashboard_screenshot.png   # Looker Studio dashboard preview
├── report/
│   └── STADEFRANCE_FNB_REPORT.docx
└── assets/
    └── pipeline_schema.png
```

---

## Contact

**Anil Eser** — Data Analyst
Career transition from copywriting and marketing to data analytics.

[LinkedIn](https://www.linkedin.com/in/anil-eser-anil)
