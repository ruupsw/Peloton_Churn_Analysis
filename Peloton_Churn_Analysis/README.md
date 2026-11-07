# Peloton Subscription Churn Analysis

An exploratory analysis of subscriber churn in a fitness app, developed as a portfolio data analytics project. The objective is to identify factors associated with cancellations and recommend practical, measurable retention initiatives.

## Business question

Which customer behaviors and subscription characteristics are associated with churn, and where should the membership team focus its retention efforts?

## Key findings

| Factor | Evidence | Interpretation |
| --- | --- | --- |
| Low early workout engagement | Subsequent 90-day churn: **30.91%** for zero workouts in signup month vs. **8.87%** for 6+ workouts | Strong inverse association with later cancellations, present within monthly and annual plans |
| Promotional acquisition | First 90-day churn: **28.36%** for Promo Offer vs. **10.02%** for Referral; among monthly plans **43.90% vs. 15.17%** | Promotion-acquired monthly members warrant focused retention tests |
| Annual subscription lifecycle | Preliminary 330–359-day cancellation proportion: **42.54%** annual vs. **4.31%** monthly | A high-risk period near the first anniversary; the underlying mechanism remains unverified |

The most common reported reason was **not using enough** (570 of 1,768 cancellations, **32.24%**). **21.61%** of canceled subscribers provided no reason.

These are **observational associations, not causal effects**. The 30-day tenure estimates are approximate and not fully corrected for partial follow-up.

## Dataset

- `data/subscriptions.csv` — 4,200 customers with signup date, plan attributes, acquisition channel, device, age group, churn outcome and reported cancellation reason.
- `data/usage.csv` — monthly workouts, activity minutes, class bookings and support tickets. After removing 160 exact duplicate rows: **30,525** customer-month records.
- Observation period: July 2024 – December 31, 2025.

The data are provided for this project case. They are **not official Peloton production records** and findings should not be generalized to Peloton's actual customer base.

## Methodology

1. Audit and clean duplicates, inconsistent tier labels, date fields and missing values. Preserve unknown cancellation reasons and missing activity minutes.
2. Define churn and observed tenure at the study end. Describe calendar-month cancellation trends and 30-day tenure intervals with censoring caveats.
3. Compare plan type, tier, acquisition channel, device and age cohorts. For early churn, require **90 days of potential follow-up since signup**.
4. Join monthly usage to subscription attributes, analyze signup-month workouts and compare **subsequent** 90-day churn using a non-overlapping follow-up window.
5. Compare self-reported cancellation reasons with customer activity and subscription characteristics.
6. Prioritize three factors and recommend measurable interventions.

The analysis uses **pandas**, **NumPy**, and **Matplotlib** for data preparation, cohort comparisons, and visualization.

## Repository structure

```text
Peloton_Churn_Analysis/
├── Churn_analysis.ipynb
├── README.md
├── requirements.txt
└── data/
    ├── subscriptions.csv
    └── usage.csv
```

## Reproduce the analysis

1. Download or clone the repository, keeping `data/` and the notebook in the same project folder.
2. From that folder, create and activate a Python environment if desired.
3. Install dependencies: `pip install -r requirements.txt`.
4. Start Jupyter Notebook or JupyterLab and open `Churn_analysis.ipynb`.
5. Run **Kernel → Restart & Run All** to regenerate tables and charts.

All file paths in the notebook are relative (`data/*.csv`). Executed figures and tables are also retained in the supplied notebook.

## Suggested experiments

- **Onboarding:** test personalized workout plans and first-week prompts for new low-engagement members. Monitor subsequent 90-day churn and workout adoption, with notification opt-outs as a guardrail.
- **Promo retention:** test transparent post-offer pricing and targeted onboarding for monthly Promo Offer subscribers. Monitor first-90-day churn and revenue per acquired subscriber.
- **Annual lifecycle:** investigate renewal touchpoints and cancellation feedback; test pre-anniversary value summaries. Measure age-matched annual cancellation rates and renewal outcomes when renewal data becomes available.

## Limitations

- This is observational analysis; measured associations cannot establish causality.
- Signup-month workouts do not represent the same number of available workout days for all members.
- Annual-tenure interval proportions are approximate and affected by within-interval censoring.
- Exact renewal events and detailed historical offer exposure are not present.
- 382 of 1,768 canceled users (**21.61%**) did not provide cancellation reasons.
- The monthly churn measure counts anyone with subscription overlap during a month, even if active for only part of that month.

## Deliverable

The notebook contains the methodology, validated calculations, six core visualizations, a three-factor summary, and a one-page leadership recommendation.
