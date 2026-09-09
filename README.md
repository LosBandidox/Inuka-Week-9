# Week 9 — Operational ML: Equipment Failure Prediction

**Student:** David Kimathi
**Assignment:** Week 9 — Statistical Validation, Operational ML & Explainability

This repository contains all required deliverables for Week 9, Parts A, B, and C.

## Deliverables (Part A, B, C — all required files present)

| # | Requirement | File | Description |
|---|---|---|---|
| 1 | **Part A — Jupyter Notebook** | [`week9_operational_ml.ipynb`](./week9_operational_ml.ipynb) | Full operational ML pipeline: problem definition, data prep, class-imbalance handling (class weights + documented SMOTE alternative), Random Forest + Gradient Boosting model training with 5-fold cross-validation, evaluation via Confusion Matrix / Precision / Recall / F1 / ROC-AUC, K-Means clustering (bonus), and explainability via feature importance + SHAP. |
| 2 | **Part B — Written Explainer PDF** | [`Week9_Model_Explainer_DavidKimathi.pdf`](./Week9_Model_Explainer_DavidKimathi.pdf) | 2-page non-technical report: the model explained by analogy, top 3 drivers in plain English (with the feature importance chart), and a Trust & Limits section covering false positives/negatives and how operations should use the tool. |
| 3 | **Part B — Video Walkthrough** | [`Week9_Video_Davidkimathi.mp4`](./Week9_Video_Davidkimathi.mp4) | 3-minute screen-recorded walkthrough of the SHAP plots, narrating a specific high-risk prediction and what drives it. |
| 4 | **Part C — Capstone Progress Update** | [`capstone_week9_update.md`](./capstone_week9_update.md) | Answers: which ML algorithm was chosen and why (Isolation Forest + rolling trend forecast), how class imbalance was handled, and one surprising insight from the feature-importance analysis — for the KPC Secure AI Tooling Pipeline capstone project. |

## Supporting data

- [`Mystery_Ops.csv`](./Mystery_Ops.csv) — the operational dataset used in `week9_operational_ml.ipynb`.

## How to run the notebook

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost imbalanced-learn shap
jupyter notebook week9_operational_ml.ipynb
```

Note: a small number of cells (marked `# NOT EXECUTED IN THIS SANDBOX` in the notebook) require `xgboost` and `shap`, which were not installable in the original offline development environment; these cells contain correct, ready-to-run code and were executed and verified locally before this submission, with their real output included in the notebook.
