# Machine Learning Midterm Project

**Breast Cancer Wisconsin and Wine Classification**  
**Submission date:** 11 November 2026

This project compares supervised classification and unsupervised K-Means clustering on two datasets available in scikit-learn. It includes data-quality checks, exploratory analysis, stratified train/validation/test splits, standardization, repeated experiments, final test evaluation, and visualizations.

## Datasets

Both datasets are loaded directly from `sklearn.datasets`; no separate dataset download is required.

| Dataset | Loader | Samples | Features | Class labels |
|---|---|---:|---:|---|
| Breast Cancer Wisconsin (Diagnostic) | `load_breast_cancer()` | 569 | 30 | `0 = malignant`, `1 = benign` |
| Wine Classification | `load_wine()` | 178 | 13 | `0`, `1`, `2` |

## Experiment design

- One fixed 20% test split, with stratification and `random_state=42`.
- Approximately 70% training / 10% validation / 20% testing.
- Training/validation experiments repeated for seeds **42, 52, and 62**.
- Both original (`unscaled`) and `StandardScaler`-transformed (`scaled`) features evaluated.
- Classifiers: Decision Tree (depths `2`, `3`, `5`, `10`, `None`), KNN (neighbors `1`, `3`, `5`, `7`, `11`), and Gaussian Naive Bayes.
- K-Means: `n_clusters=2` for Breast Cancer and `n_clusters=3` for Wine, with `n_init=10`.
- Classifier selection was based on mean **validation macro-F1**; the fixed test set was reserved for final evaluation.

**Total recorded fits:** 132 classification + 12 K-Means = **144**.

## Final classifier results

| Dataset | Selected model | Test accuracy | Test macro-F1 | Test ROC-AUC |
|---|---|---:|---:|---:|
| Breast Cancer | Scaled KNN, `k=7` | 0.9737 | 0.9713 | 0.9888 |
| Wine | Scaled KNN, `k=11` | 1.0000 | 1.0000 | 1.0000 |

These are results from the particular fixed test sets, not guarantees of performance on new data.

## Files

```text
Machine_Learning_Project/
├── breast_cancer.ipynb           # Executed Breast Cancer notebook
├── wine.ipynb                    # Executed Wine notebook
├── report.docx                   # Written report
├── classifier_runs.csv           # 132 classifier runs
├── classifier_summary.csv        # 44 configuration summaries
├── classifier_test.csv           # 2 final classifier evaluations
├── kmeans_runs.csv               # 12 K-Means runs
├── kmeans_summary.csv            # 4 K-Means summaries
├── kmeans_test.csv               # 4 final K-Means evaluations
├── figures/                      # EDA, validation, test and clustering plots
├── requirements.txt              # Exact environment dependencies
├── README.md
└── AI_DISCLOSURE.md
```

> Before submitting, ensure the actual notebook filename is `breast_cancer.ipynb` (not a working copy name), all listed files are present, and generated CSVs/figures match the submitted notebooks.

## Installation and execution

**Python version:** `[INSERT OUTPUT OF: python --version]`  
**Package versions:** See `requirements.txt` in this repository. The environment primarily uses `numpy`, `pandas`, `scikit-learn`, `matplotlib`, and Jupyter/IPython; the exact installed versions should be recorded in `requirements.txt`.

In a terminal opened at the project root:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m notebook
```

Alternatively, open the two `.ipynb` files in **VS Code**, select the `.venv` Python kernel, and execute the cells in order.

1. Open and run `breast_cancer.ipynb` in order; inspect the data checks, classification, and clustering results.
2. Open and run `wine.ipynb` in order. Its final CSV export section combines the results for both datasets; keep the project CSV files in the working directory when running this section.
3. Confirm the six combined CSV row counts shown below, and inspect the `figures/` folder.
4. Use a **backup copy** of the project for a fresh-kernel/Run All reproducibility test before submission; avoid accidentally replacing final combined CSVs with dataset-only exports.

To create an exact package-version file from the environment used for the results, run:

```powershell
python -m pip freeze > requirements.txt
```

This step should be done **in the original working environment**, and the resulting `requirements.txt` should be included in the repository.

## Expected output inventory

| File | Rows |
|---|---:|
| `classifier_runs.csv` | 132 |
| `classifier_summary.csv` | 44 |
| `classifier_test.csv` | 2 |
| `kmeans_runs.csv` | 12 |
| `kmeans_summary.csv` | 4 |
| `kmeans_test.csv` | 4 |

The previous project check found **21 PNG figures**. Verify the count and contents against the final submitted version.

## Repository and walkthrough

- **GitHub repository: https://github.com/SouthSideDrip/Machine-Learning-Midterm** ``


The notebook outputs, report, and CSV files must reflect the same final project state. AI use is documented in [AI_DISCLOSURE.md](AI_DISCLOSURE.md).
