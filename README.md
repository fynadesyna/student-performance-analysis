# Student Performance Factors Analysis

Data cleaning, descriptive statistics, and an interactive Power BI dashboard exploring what actually correlates with student exam performance across 6,600+ student records.

## Overview

A university dataset of student academic and lifestyle factors (study hours, attendance, tutoring, teacher quality, family income, and more) was cleaned from a messy 20-column raw export down to a focused 11-variable analysis set, then explored through descriptive statistics, correlation analysis, and an interactive dashboard aimed at academic administrators.

The guiding question: **which factors are actually worth acting on if a university wants to improve student outcomes?**

## Key Features

- Full data cleaning pipeline: column pruning (9 low-value/high-missingness columns dropped), interval-based outlier correction, missing-value imputation, duplicate removal
- Descriptive statistics (mean, median, mode, variance, skewness, IQR) across all six numerical variables
- Correlation analysis identifying Attendance (r ≈ 0.58) and Hours Studied (r ≈ 0.29) as the strongest — though still moderate — predictors of Exam Score
- Interactive Power BI dashboard built for a specific stakeholder (Dean of Academic Affairs) with 5 KPI cards and 4 comparison charts

## Key Findings

- **Attendance is the strongest single correlate of exam performance** (r ≈ 0.58) among the variables tested — stronger than study hours.
- **Students scored ~8 points lower on average** than their historical average (mean Score Improvement = −7.84), a signal worth investigating further.
- **Exam Score is right-skewed** (skewness ≈ 2.13) — most students cluster around a typical range, with a smaller group of high performers pulling the distribution.
- **Tutoring usage is low** — median of just 1 session — suggesting under-utilized academic support infrastructure.
- No meaningful gender difference in the attendance–performance relationship.

## Tech Stack

- **Python 3.12**, **pandas**, **NumPy**, **Matplotlib**, **SciPy** (for skewness)
- **Power BI** for the interactive dashboard

## Project Structure

```
student-performance-analysis/
├── notebooks/
│   └── data_cleaning_and_descriptive_stats.ipynb
├── dashboard/
│   └── student_performance_dashboard.pbix
├── docs/
│   ├── images/                 # Chart exports referenced in the README/notebook
│   └── report/                 # Written report (cleaning + stats + dashboard writeup)
├── data/
│   └── README.md               # Dataset source + how to obtain it
├── requirements.txt
└── README.md
```

## Getting Started

```bash
git clone <repo-url>
cd student-performance-analysis
pip install -r requirements.txt
```

Download `StudentPerformanceFactors.csv` from [Kaggle](https://www.kaggle.com/datasets/ayeshasiddiqa123/student-performance) into `data/`, then run:

```bash
jupyter notebook notebooks/data_cleaning_and_descriptive_stats.ipynb
```

To view the interactive dashboard, open `dashboard/student_performance_dashboard.pbix` in [Power BI Desktop](https://www.microsoft.com/en-us/power-platform/products/power-bi/desktop) . A static preview is in `docs/images/powerbi_dashboard.png`.

## Methodology

### Data Cleaning
1. **Column selection** — dropped 9 columns (e.g., `Parental_Involvement`, `Sleep_Hours`, `Motivation_Level`) that were either indirect/self-reported, highly imbalanced (>89% one value), or had substantial missingness with weak academic relevance. Full list and justification in the [report](docs/report/).
2. **Missing values** — after column selection, only `Teacher_Quality` had missing values (78 records, 1.18%), imputed with the mode.
3. **Invalid value correction** — interval validation caught 1,462 `Hours_Studied` values above the physically possible 24-hour daily maximum, and 1 `Exam_Score` above 100; both replaced with the column median.
4. **Duplicates** — 1 exact duplicate row identified and removed.
5. **Feature engineering** — added `Score_Improvement = Exam_Score − Previous_Scores` to capture whether a student improved or declined relative to prior performance.

### Descriptive Statistics & Visualization
Computed mean, median, mode, standard deviation, variance, skewness, and IQR for all six numerical variables, then visualized relationships via a correlation heatmap and two scatter plots (Hours Studied vs. Exam Score; Attendance vs. Exam Score by Gender).

### Dashboard
An interactive Power BI dashboard built for the Dean of Academic Affairs persona, with KPI cards (avg. exam score, score improvement, study hours, ECA participation, attendance rate) and four comparison charts (Study Hours vs. Performance, Attendance vs. Outcome, Teacher Quality vs. Score Benchmark, Resource Access vs. Performance Variance) plus demographic breakdowns. The dashboard's data source connects directly to the Python-cleaned dataset.

## My Contribution

This was a group project (team of 4) for a "Foundations in Business Analytics" course. My personal contribution was the **data cleaning pipeline (in Python) and the descriptive statistics analysis and writeup** — the material reproduced in `notebooks/data_cleaning_and_descriptive_stats.ipynb`. Dashboard design and the predictive-analysis framing section were collaborative team work.

## Limitations

- Descriptive/correlational only — no predictive model was actually trained; Section 4 of the notebook documents *candidate* modeling approaches (regression for score prediction, classification for risk status) identified during the project, not implemented results.
- The strong Previous Scores ↔ Score Improvement correlation (r ≈ −0.96) is largely a mathematical artifact of how `Score_Improvement` was defined, not an independent finding.
- Correlations found are weak-to-moderate at best (max r ≈ 0.58) — no single variable in this dataset is a strong standalone predictor of exam performance.

## Future Improvements

- [RECOMMENDED IMPROVEMENT] Train and validate the regression/classification models outlined in the predictive-analysis section.
- [RECOMMENDED IMPROVEMENT] Add cross-validation and feature importance ranking to move from correlation to a defensible predictive model.
- [RECOMMENDED IMPROVEMENT] Publish the dashboard to Power BI Service with a shareable read-only link instead of requiring Power BI Desktop.

## License

MIT — see [LICENSE](LICENSE). This covers the code, analysis, and written report in this repo; it does not extend to the third-party dataset (see `data/README.md` for its source and license).
