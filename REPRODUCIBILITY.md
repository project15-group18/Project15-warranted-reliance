# Reproducibility record

Analysis code: v1.1.0 (unchanged in v1.1.1 and v1.1.2). Three Kaggle CPU runs of the identical notebook were made:

| Run | Type | Date (CET) | Role in this repository |
|---|---|---|---|
| A | Interactive session | 25 Nov 2026, ~23:30 | Archive shipped in release v1.1.0 / v1.1.1 |
| B | Committed version (Save & Run All) | 25 Nov 2026, late evening | **`Project15_Revised_Results.zip` in this release** |
| C | Interactive session | 26 Nov 2026, ~01:00 | Source of the executed notebook (outputs) in this release |

Kaggle does not export a committed version together with its cell outputs, so the executed notebook comes from run C and the archive from run B.

## Run A vs run B (results archives, all CSV files)

- Files compared: 86 CSV files (manifest excluded). Both archives contain the same 138 paths; each archive's SHA-256 manifest verifies.
- Primary result tables: 14 of 14 are byte-for-byte identical.
- Files that differ: 9, predictions, figure data and model diagnostics; maximum absolute numeric difference 2.2e-16 (floating-point rounding or number representation; values with difference 0 differ only in how a float is written).

| File | Max abs. difference |
|---|---|
| `data/R1_F1_reliability_data.csv` | 0.0e+00 |
| `data/RQ1_same_case_reversals_UCI.csv` | 9.7e-17 |
| `data/predictions_UCI_42_test.csv` | 1.1e-16 |
| `data/predictions_UCI_42_val.csv` | 2.2e-16 |
| `data/predictions_UCI_43_test.csv` | 2.2e-16 |
| `data/predictions_UCI_43_val.csv` | 1.1e-16 |
| `data/predictions_UCI_44_test.csv` | 2.2e-16 |
| `data/predictions_UCI_44_val.csv` | 2.2e-16 |
| `tables/S04_model_diagnostics.csv` | 1.1e-16 |

PDF figures and tables differ in bytes only through embedded creation timestamps.

## Run C vs run B (notebook outputs vs archive)

Every numeric value displayed in the notebook's table outputs was matched against the run-B CSVs at displayed precision; no disagreement was found. Values not matched automatically are displayed in a different number format, not with a different value. Both runs print `Validated: 27 primary results; archived files: 138`.

## Software (from `metadata/software_versions.json`)

Python 3.13.18, NumPy 2.1.3, pandas 2.3.3, scikit-learn 1.6.1, Matplotlib 3.10.0 (Kaggle CPU image). Seeds are fixed in the configuration cell.
