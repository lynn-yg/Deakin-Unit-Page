# SIT719 — Diabetes Classification on PIMA (Baselines + Novel Variant)

[![Open In Colab](https://colab.research.googleusercontent.com/assets/colab-badge.svg)](https://colab.research.google.com/github/<your-username>/<your-repo>/blob/main/notebooks/SIT719_PIMA_Baselines.ipynb)

A reproducible pipeline for the SIT719 9.2D task: reproduce **Decision Tree**, **SVM (RBF)**, and **Random Forest** baselines on the **PIMA Indians Diabetes** dataset, report **Accuracy, Precision, Recall, F1**, and compare against a simple **novel variant** (optional: **SMOTE+SVM**).

## Reproducibility at a glance

* Pinned dependencies; one‑click Colab; documented model selection.
* **CV‑driven selection**: BEST by **CV F1** (tie‑break: Recall, then Accuracy).
* Exports a detailed CV+test table and a compact **Table‑4‑like** CSV for the report.

## Project structure

```
.
├── notebooks/
│   └── SIT719_PIMA_Baselines.ipynb      # Colab‑ready notebook
├── src/
│   └── pima_pipeline.py                 # Script version (local run)
├── requirements.txt                     # Pinned versions
└── README.md
```

> Dataset is fetched directly from GitHub at run‑time (no manual upload needed).

## Quickstart (Colab — recommended)

1. Click the **Open in Colab** badge above.
2. **Runtime → Run all** (installs deps, downloads data, trains models, saves results).
3. Outputs in the working directory:

   * `pima_results_with_cv_and_test.csv`
   * `pima_results_table4_like.csv`

## Quickstart (Local)

```bash
# 1) Create a clean environment (macOS/Linux)
python -m venv .venv
source .venv/bin/activate

# 2) Install dependencies
pip install -r requirements.txt

# 3) Run
python src/pima_pipeline.py
# If the script expects a local CSV path, edit CSV_PATH inside the file.
```

## Method overview

* **Preprocess**: replace implausible zeros (Glucose, BloodPressure, SkinThickness, Insulin, BMI) → NaN; median impute; standardize features.
* **Models**: Decision Tree, SVM (RBF), Random Forest. Optional **SMOTE+SVM** (novel variant).
* **Split**: Stratified 80/20 train/test; Stratified 5‑fold CV for tuning.
* **Tuning**: GridSearchCV with multi‑metric scoring; `refit = 'f1'`.
* **Selection rule**: choose BEST by CV F1; tie‑breakers: CV Recall → CV Accuracy.

## Outputs

* `pima_results_with_cv_and_test.csv` — CV & Test metrics per model + best params.
* `pima_results_table4_like.csv` — compact 4‑metric table.
* Console/log: BEST model summary, confusion matrix, classification report.

## Notes on the novel variant

* Use **SMOTE** inside the CV pipeline for SVM (after scaling) to improve minority‑class **Recall**.
* Keep the same CV/selection logic for a fair baseline comparison.

## How to cite (IEEE examples)

> Replace placeholders with your final bibliography.

\[1] *A robust and generalized framework in diabetes classification across heterogeneous environments*, **Computers in Biology and Medicine**, 2025. (Add authors, volume, pages, DOI.)

\[2] PIMA Indians Diabetes Dataset, GitHub repository: `npradaschnor/Pima-Indians-Diabetes-Dataset` (accessed: Sep. 2025).

## License

MIT (or your institution’s required license).

## Maintainer

<Your Name> — [your.email@example.com](mailto:your.email@example.com)
