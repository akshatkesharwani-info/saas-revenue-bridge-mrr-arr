# SaaS Revenue Bridge (MRR / ARR) Analysis

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Cost](https://img.shields.io/badge/Cost-Free%20(Google%20Colab)-orange)
![Data](https://img.shields.io/badge/Data-Simulated-lightgrey)

A monthly MRR bridge (waterfall) that splits revenue change into New, Expansion, Contraction and Churn, with ARR, NRR, GRR and logo churn.

## Table of Contents
1. [Problem Statement](#problem-statement)
2. [STAR Summary](#star-summary)
3. [Dataset](#dataset)
4. [What the Notebook Does](#what-the-notebook-does)
5. [Key Results (from the executed run)](#key-results-from-the-executed-run)
6. [Sample Output](#sample-output)
7. [Checks and Fallbacks](#checks-and-fallbacks)
8. [Limitations](#limitations)
9. [Tech Stack](#tech-stack)
10. [How to Run](#how-to-run)
11. [Files](#files)
12. [About Me](#about-me)

## Problem Statement
A subscription software company wants to understand why its monthly recurring revenue (MRR) moved each month. Revenue changes because of new customers, upgrades, downgrades and cancellations, and each of these needs a different action.

## STAR Summary
- **Situation:** MRR was growing, but a single total hid how much came from new customers versus existing ones and how much was lost to churn.
- **Task:** Build an MRR bridge and the standard SaaS health metrics.
- **Action:** Built a customer x month MRR table for 900 customers over 18 months, classified every monthly change as New, Expansion, Contraction or Churn, reconciled the bridge to the closing MRR, and calculated ARR, ARPA, NRR, GRR, logo churn and a plan-wise view.
- **Result:** MRR grew from 15,604 to 59,523 (+281.5%) with ARR of 714,276 in December 2025. New customers drove 46,476 of the growth, while churn removed 11,457. Average monthly NRR was 99.6%, so growth depends on new customers.

## Dataset
- **Simulated data created inside the notebook** (fixed random seed), not real company data: 900 customers, 3 plans (Basic 29, Pro 79, Business 199 per month), 18 months from July 2024 to December 2025.
- About 30% of customers exist in the first month, the rest join later. Customers can upgrade, downgrade or cancel, with higher churn on cheaper plans built into the generator. The findings therefore show that the analysis recovers those patterns. They are not claims about a real SaaS company.

## What the Notebook Does
1. Creates the subscription data and a customer x month MRR table.
2. Calculates total MRR, ARR, active customers and ARPA per month.
3. Builds the MRR bridge: New (0 last month, pays now), Expansion (pays more), Contraction (pays less), Churn (paid last month, pays 0 now).
4. Reconciles the bridge: opening MRR + movements = closing MRR.
5. Draws the full-period waterfall and a monthly movements chart.
6. Calculates NRR, GRR, MRR growth % and logo churn per month.
7. Compares plans (customer share, MRR share, cancellations).
8. Prints insights and saves charts and CSV files.

## Key Results (from the executed run)
| Metric | Value |
|---|---|
| MRR, Jul 2024 to Dec 2025 | 15,604 to 59,523 (+281.5%) |
| ARR, Dec 2025 | 714,276 |
| Active customers / ARPA, Dec 2025 | 697 / 85.4 |
| New MRR / Expansion MRR | +46,476 / +13,800 |
| Contraction MRR / Churn MRR | -4,900 / -11,457 |
| Average monthly NRR / GRR | 99.6% / 97.32% |
| Average monthly logo churn | 2.61% |
| Approx annual NRR / GRR (monthly average compounded 12 times) | 95.3% / 72.2% |
| Best / weakest growth month | Oct 2024 (17.25%) / Nov 2025 (2.26%) |

| Plan (Dec 2025) | Customers | MRR | Customer share | MRR share | Cancelled |
|---|---|---|---|---|---|
| Basic | 302 | 8,758 | 43.3% | 14.7% | 30.1% |
| Pro | 232 | 18,328 | 33.3% | 30.8% | 19.7% |
| Business | 163 | 32,437 | 23.4% | 54.5% | 8.9% |

Business is 23.4% of customers but 54.5% of MRR, and Basic has the highest cancellation share.

## Sample Output
```
Bridge check (should be all 0): 0.0
Starting MRR: 15604 | Ending MRR: 59523
Check: 59523 should equal 59523

KEY INSIGHTS
--------------------------------------------------
1. MRR grew from 15604 to 59523 ( 281.5 % in 17 months )
2. Current ARR is 714276
3. New customers added 46476 MRR and expansion added 13800 MRR -> biggest growth driver is New
4. Churn removed 11457 MRR and contraction removed 4900 MRR -> biggest loss is Churn
5. Average monthly NRR is 99.6 % and GRR is 97.3 %
6. Average monthly logo churn is 2.61 %
7. Highest share of cancellations: Basic plan ( 30.1 % )
8. Best growth month: Oct 2024 | Weakest month: Nov 2025
```

## Checks and Fallbacks
- The bridge reconciles: opening + New + Expansion + Contraction + Churn minus closing MRR equals 0 in every month, and the full-period waterfall ties out (59,523 = 59,523).
- ARR is MRR x 12, and annual NRR/GRR are marked as approximations.
- Data is generated with a fixed seed, so the numbers above repeat on every run.
- No LLM or paid API is used, so there is no cost or latency to track.

## Limitations
- The data is simulated, so the plan-level churn pattern comes from the generator settings.
- The generator has no reactivations, so a customer who cancels never returns.
- Annual NRR/GRR are approximations from the monthly average. They are not cohort-based annual figures.

## Tech Stack
| Area | Tools |
|---|---|
| Language | Python |
| Data handling | pandas, numpy |
| Charts | matplotlib, seaborn |
| Environment | Google Colab |

## How to Run
1. Open `saas_revenue_bridge_mrr_arr.ipynb` in Google Colab.
2. Click Runtime > Run all.
3. No dataset download or API key is needed.
4. Charts and CSV files are saved in the Colab file panel.

## Files
- `saas_revenue_bridge_mrr_arr.ipynb` (executed notebook with outputs)
- `requirements.txt`
- Generated by the notebook: `mrr_trend.png`, `mrr_bridge_waterfall.png`, `monthly_mrr_movements.png`, `nrr_grr_trend.png`, `plan_mix.png`, `mrr_bridge_monthly.csv`, `mrr_arr_summary.csv`, `plan_summary.csv`

## About Me
**Akshat Kesharwani** | Data Analyst and Data Scientist (fresher) | Sagar, Madhya Pradesh
- Portfolio: https://akshatkesharwani-info.github.io/
- GitHub: https://github.com/akshatkesharwani-info
- Email: akshatkesharwani12345@gmail.com
