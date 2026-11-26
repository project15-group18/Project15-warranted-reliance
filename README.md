# Warranted Reliance and Uncertainty in AI

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24093961.svg)](https://doi.org/10.5281/zenodo.24093961)
[![Kaggle](https://img.shields.io/badge/Kaggle-executed%20notebook-20BEFF?logo=kaggle&logoColor=white)](https://www.kaggle.com/code/nannudatascience/warranted-reliance-and-uncertainty)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
![Python](https://img.shields.io/badge/Python-3.13-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.6-F7931E?logo=scikitlearn&logoColor=white)
![Release](https://img.shields.io/badge/release-v1.1.2-blue)

**Project 15 · Group 18 "Mission Possible"**
Harshal Tittamelanahalli Venkatesh and Sagar Vig

A reproducible computational study of how predictive evidence, decision costs, distribution shift and limited human review affect when reliance on an AI recommendation is warranted.

| | |
|---|---|
| **Current version** | v1.1.2: analysis v1.1.0 (revised after technical assessment of v1.0.0), executed notebook and committed-run archive |
| **Kaggle notebook (executed, committed)** | https://www.kaggle.com/code/nannudatascience/warranted-reliance-and-uncertainty |
| **Zenodo archive (all versions, resolves to latest)** | https://doi.org/10.5281/zenodo.24093961 |
| **Zenodo versions** | v1.0.0: https://doi.org/10.5281/zenodo.24093962 · v1.1.0: https://doi.org/10.5281/zenodo.24545162 |
| **Target journal** | *Minds and Machines* (Springer Nature) |
| **Anchor paper** | Ferrario, A. (2026). Being pragmatic about reliance and trust in artificial intelligence. *Minds and Machines*, 36, 5. https://doi.org/10.1007/s11023-025-09754-9 |

## Research questions (revised)

1. **R1 — Decision context.** Under what combinations of error and deferral costs do confidence-based and cost-aware policies prescribe different actions for identical predictions, and how does this affect decision loss and automated coverage?
2. **R2 — Uncertainty in evidence.** How does finite-sample uncertainty in estimated predictive reliability affect the stability of reliance decisions, and when does incorporating it improve decisions compared with point estimates?
3. **R3 — Distribution shift.** Under what changes in population composition does a validated reliance policy become unreliable, and how far can recalibration restore it without retraining?
4. **R4 — Subgroup burdens and limited review.** When does abstention reduce automated error while increasing subgroup disparities in deferral burden, and how do review capacity and imperfect fallback decisions affect this trade-off?

## Repository contents

| File | Description |
|---|---|
| `Project15_warranted_reliance_v1.1.0.ipynb` | Executed notebook with all cell outputs: 31 code cells, 27 primary results (13 figures, 14 tables) |
| `Project15_Revised_Results.zip` | Results archive from the committed Kaggle run, 138 files: figures (PDF + 300 dpi PNG), tables (CSV + PDF), plotted data, predictions, splits, captions, configuration, provenance, SHA-256 manifest |
| `REPRODUCIBILITY.md` | Agreement between the three Kaggle runs (archives and notebook outputs) |
| `CITATION.cff` | Citation metadata (GitHub "Cite this repository" button) |
| `.zenodo.json` | Zenodo archive metadata (title, authors, license, keywords) |
| `LICENSE` | MIT License for the code |

Result files are prefixed by revised research question (`R1_`–`R4_`, including `R2_UQ_*` and `R4_GB_*`); supporting audits use `S0x_`. `metadata/rq_mapping.csv` links every file to its legacy pilot identifier.

## Data

Datasets are analysed separately and never merged.

- **UCI Default of Credit Card Clients**: all 30,000 records. Yeh (2009), https://doi.org/10.24432/C55S3H, CC BY 4.0.
- **ACSIncome** (Folktables task definition, nominal USD 50,000 target): Delaware 2018 (source, 4,713 eligible records), Maryland 2018 (12,000 sampled), Delaware 2019 (4,755 eligible). U.S. Census Bureau PUMS. Unweighted benchmark evaluation, not survey-representative estimates. Sex, race and relationship fields are excluded from the predictors.

## Reproducing the results

1. Open the Kaggle notebook above, then **Copy & Edit**. The input dataset is attached.
2. Use CPU (no accelerator) and **Run All**. A full run takes roughly 15–25 minutes.
3. The final cell must print `Validated: 27 primary results; archived files: 138`.

Splits, models and bootstrap draws use fixed seeds. Independent Kaggle runs of v1.1.0 reproduce all 14 primary tables byte-for-byte; other differences are at floating-point precision (≤ 2.2e-16). See `REPRODUCIBILITY.md`.

## Changes in v1.1.0

Made in response to a technical assessment of v1.0.0:

- **Always-defer baseline and all scenarios** (`R2_UQ_F3`, `R2_UQ_T1`). All nine prespecified (false-negative cost, deferral cost) scenarios are reported against an explicit always-defer baseline. In the primary setting both policies defer every case, so that setting alone is uninformative.
- **Validated uncertainty bounds** (`R2_UQ_T3`). The estimand and assumptions (A1–A5) of the cluster-weighted Hoeffding bin bounds are documented. A Monte Carlo study of the implemented function gives simultaneous coverage of 0.996–1.000 against nominal 0.95, in both singleton and correlated-household regimes constructed to satisfy the assumptions. Coverage on the benchmark data remains conditional on those assumptions, including that, given the within-bin cluster counts, cluster contributions are independent with conditional weighted mean equal to the bin rate.
- **Separated uncertainty sources** (`R2_UQ_T4`). Variability from refitting the model, calibrator and reliability evidence (50 whole-cluster bootstrap refits) is reported separately from conditional test-bootstrap intervals.
- **Alignment.** Files are renamed to the revised RQs with a legacy mapping, revised-RQ analyses are labelled exploratory, and costs, fallback error and capacity are described as assumed scenario values throughout.

## Key findings (R2)

- The interval policy is **never** significantly better than the point-estimate policy across the 18 dataset × scenario settings. It is significantly worse in 6, and both policies defer every case in 10.
- The bounds are valid but conservative: about 0.36 wide with ACS's 477 evidence records and about 0.12–0.15 at 3,000. That explains why worst-case reasoning mostly converts reliance into deferral.
- Refitting variability is often comparable to or larger than conditional test-bootstrap intervals, which therefore understate total uncertainty.

## Scope and limitations

- This is an **exploratory** revision after a pilot, not a preregistered confirmatory study.
- Error costs, deferral costs, reviewer (fallback) error and review capacity are **assumed scenario values**, not measurements of real costs or human behaviour.
- No human-trust study or real-world deployment evaluation is claimed. Unequal subgroup rates do not by themselves establish discrimination.
- Null and unfavourable results are retained.
- The philosophical argument and manuscript are developed separately in the write-up phase.

## License

- **Code** (notebook): [MIT License](LICENSE).
- **Results archive** (figures, tables, derived data): CC BY 4.0. Please cite the Zenodo DOI.
- **Source data** are not redistributed beyond derived outputs: UCI Default of Credit Card Clients (CC BY 4.0, https://doi.org/10.24432/C55S3H) and U.S. Census Bureau ACS PUMS (public domain), retrieved via the documented release files.

## Citation

Use the **"Cite this repository"** button on the right of this page, or:

Tittamelanahalli Venkatesh, H., & Vig, S. (2026). *Warranted Reliance and Uncertainty in AI: reproducible experiments (Project 15)* (Version 1.1.2) [Software and data]. Zenodo. https://doi.org/10.5281/zenodo.24093961
