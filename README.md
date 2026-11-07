# DSC8307 Data Mining, Modeling and Analytics — Advent 2026 Assignment

This repository contains the two projects of the assignment. Each project has its own Jupyter notebook.

| Project | Notebook | Data |
|---|---|---|
| 1. Bank Marketing — predicting term-deposit subscription | `project1_bank_marketing.ipynb` | `data/bank-additional-full.csv` |
| 2. Concrete Compressive Strength — predicting strength from mix and age | `project2_concrete_strength.ipynb` | `data/Concrete_Data.csv` |

## Repository structure

```
.
├── README.md
├── requirements.txt                    # dependency file
├── project1_bank_marketing.ipynb
├── project2_concrete_strength.ipynb
└── data/
    ├── bank-additional-full.csv
    ├── bank-additional-full-README.txt
    ├── Concrete_Data.csv
    └── Concrete_Data_README.txt
```

## How to run

Requires **Python 3.11 or newer**.

```bash
git clone <this-repository-url>
cd <repository-folder>

python -m venv .venv
# Windows:   .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate

pip install -r requirements.txt
jupyter notebook
```

Open each notebook and choose **Kernel → Restart & Run All**. The notebooks read the data from the `data/` folder using relative paths, so start Jupyter from the repository root.

Approximate run time on a 2-core machine: Project 1 about 2.5 minutes, Project 2 about 2 minutes. All random processes use a fixed seed (`42`), so results are reproducible.

## Summary of results

**Project 1 — Bank Marketing**
- `duration` was removed because it is only known after the call (target leakage). The majority-class baseline is 88.7% accurate but finds no subscribers.
- Ranking: (1) random forest, (2) logistic regression, (3) gradient boosting. The ranking uses cross-validated and test PR-AUC plus robustness under a time-ordered validation.
- Recommended decision threshold: **0.15**. On the test set this means calling about 17% of customers and reaching about 63% of subscribers. The trade-off is analysed for different call-cost/subscription-value ratios.

**Project 2 — Concrete Strength**
- Validation is grouped by mixture, because the same mix is tested at several ages.
- Gradient boosting (test RMSE ≈ 5.7 MPa, R² ≈ 0.90) beats the best linear model (≈ 7.1 MPa) and the mean baseline (≈ 18 MPa).
- Predictions are weakest for high-strength concrete (above 60 MPa) and complex blended mixes.
- A predictive cement–strength association is **not** proof of a causal effect of changing the mix.

## Data sources

- Moro, S., Rita, P., & Cortez, P. (2014). Bank Marketing [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5K306
- Yeh, I.-C. (2007). Concrete Compressive Strength [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5PK67

Full literature references are listed at the end of each notebook.
