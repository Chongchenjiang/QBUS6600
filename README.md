# QBUS6600 Assignment 2 Workspace

This folder is the organised A2 workspace for the Next Gen membership-churn project. The data-processing and feature-engineering workflow has one canonical entry point so that every team member uses the same feature definitions, time boundary and validation folds.

## Start here

1. Read [`A2_data_processing_and_feature_engineering.md`](A2_data_processing_and_feature_engineering.md) for the processing specification and rationale.
2. Open [`notebooks/final/A2_data_processing_feature_engineering.ipynb`](notebooks/final/A2_data_processing_feature_engineering.ipynb).
3. Run the notebook from top to bottom. It locates the `a2` project folder automatically and never overwrites raw data.
4. Give the generated member table, feature dictionary and fixed fold assignments to Simin Zeng and Sam Zhu.
5. Use [`notebooks/reference`](notebooks/reference) and [`scripts/reference`](scripts/reference) only for provenance. They are not active A2 processing code.

## Canonical outputs

| Output | Purpose |
|---|---|
| `data/processed/member_table_A2.csv` | One row per member, with identical predictors for labelled and unlabelled members |
| `outputs/qa/feature_dictionary_A2.csv` | Definition, source, treatment and time window for every delivered column |
| `outputs/qa/fold_assignments_A2.csv` | Fixed five-fold household-aware validation assignment for labelled members |
| `outputs/qa/fold_summary_A2.csv` | Fold sizes, churn counts, churn rates and household-overlap checks |
| `outputs/qa/member_table_A2_qa.json` | Machine-readable processing and leakage checks |
| `outputs/qa/member_table_A2_missingness.csv` | Missingness profile for the final table |

## Folder structure

```text
a2/
|-- README.md
|-- A2_data_processing_and_feature_engineering.md
|-- data/
|   |-- raw/                 # Read-only source CSVs
|   `-- processed/           # Reproducible member-level output
|-- docs/
|   |-- requirements/        # Official brief and data definitions
|   |-- reference/           # A1 cleaning notes
|   `-- decisions/           # Provenance and internal rationale
|-- notebooks/
|   |-- reference/           # A1 notebooks retained for traceability
|   `-- final/               # Canonical A2 processing notebook
|-- scripts/
|   `-- reference/           # Archived legacy code as non-executable text
`-- outputs/
    |-- qa/                  # Generated validation and audit outputs
    `-- figures/             # Report or presentation figures
```

## Reproducibility rules

- Treat `data/raw` as read-only.
- Use `T0 = 2024-07-19 00:00:00` and an exclusive upper time boundary.
- Reuse the supplied fold assignments for every candidate model.
- Fit imputation, encoding, scaling, resampling, feature selection and threshold tuning inside each training fold only.
- Use `RANDOM_STATE = 42` for every shuffled or stochastic step that supports a seed.
- Do not use the 1,350 unlabelled members during model fitting, validation or threshold selection.
- When a feature definition changes, rerun the notebook and regenerate every output rather than editing a CSV manually.

ljy
