# People Analytics: Technical Hiring Analysis

## Summary

This project analyzes a synthetic technical hiring problem in a manufacturing company. It investigates time-to-fill growth, early attrition, source quality, manager-level patterns, and recruiting bottlenecks using Python-generated synthetic data.

The goal is to translate recruiting and employee data into practical recommendations, such as reducing interview delays, improving offer acceptance, strengthening referral and university sourcing, and lowering early attrition through onboarding and training improvements.

---

## Problem

A manufacturing company is experiencing hiring difficulties in technical roles such as Technician, Planner, Quality Inspector, and Maintenance.

Key signals:

- **Time-to-fill:** increased from 39 days to 71 days (+82%)
- **Early attrition:** 26.3% within the first 6 months
- **Offer acceptance:** only 5.3% for agency-sourced candidates

This project identifies where the problem occurs, why it may be happening, and which operational actions could improve the hiring process.

---

## Approach

Since real company data was not available, the project uses synthetic data generated with Python. The synthetic scenario simulates:

- Increasing delays between recruitment stages in the last 6 months
- Higher offer decline and early attrition for agency-sourced candidates
- Manager/team patterns where overtime and attrition rise together
- Higher early attrition among employees who did not complete training

---

## Dataset

| File | Description | Rows |
|------|-------------|-----:|
| `data/recruitment.csv` | Candidate-level recruitment process data | 900 |
| `data/employee.csv` | Employee-level performance and attrition data | 350 |

**Note:** The dataset is fully synthetic. Names, dates, and metrics were generated with Python and do not represent a real company.

---

## Analyses

### 1. Recruitment Funnel
Out of 900 applications, 234 candidates were hired (26%). The largest drop occurs in the final stage: only 46% of candidates who received an offer actually started.

### 2. Time-to-Fill Decomposition

| Stage | Previous 12 Months | Last 6 Months | Increase |
|-------|-------------------:|--------------:|---------:|
| Applied→Screen | 7 days | 11 days | +4 days |
| Screen→Interview | 14 days | 21.5 days | +7.5 days |
| Interview→Offer | 6 days | 12 days | +6 days |
| Offer→Start | 15 days | 26 days | +11 days |

Most critical delays: **Offer→Start (+11 days)** and **Screen→Interview (+7.5 days)**.

### 3. Early Attrition Analysis

- Attrition without training: **46.5%**
- Attrition with training: **19.7%**
- Some manager groups show attrition around **40–50%** together with high overtime.

### 4. Source Analysis

| Source | Hire Rate | Offer Decline |
|--------|----------:|--------------:|
| Referral | 33% | 6% |
| LinkedIn | 33% | 8% |
| Agency | 3% | 27% |

---

## Recommendations

| Finding | Action | Expected Effect |
|---------|--------|-----------------|
| Screen→Interview delay | Set two fixed interview days per week and analyze recruiter throughput | Time-to-fill ~-20% |
| Offer→Start delay | Improve digital onboarding and review offer competitiveness | Time-to-fill ~-10% |
| High agency offer decline | Strengthen referral and university channels | Offer acceptance ~+15% |
| High attrition among untrained employees | Require training completion within the first 30 days | Early attrition ~-30% |
| Manager/team-level attrition pattern | Add manager coaching, team survey, and overtime balancing | Lower employee-risk concentration |

---

## Repository Structure

```text
├── data/
│   ├── recruitment.csv
│   ├── employee.csv
│   ├── funnel.png
│   ├── ttf_decomposition.png
│   └── attrition_analysis.png
├── notebooks/
│   ├── 01_generate_data.ipynb
│   └── 02_analysis.ipynb
└── README.md
```

---

## Technologies

- Python 3.13
- pandas, numpy
- matplotlib, seaborn
- Faker for synthetic data generation

---

## Limitations and Assumptions

- The dataset is synthetic and may not fully reflect real company dynamics.
- Delay parameters were manually designed and would require calibration with real data.
- Manager-level observations are correlation-based and do not claim causality.
- Early attrition is defined with a 180-day threshold; industry standards may differ.
