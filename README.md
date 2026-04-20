# gCI: Group-Level Fairness Assessment for Clinical Risk Prediction

This repository contains the analysis code and organized notebooks for the paper on **group-level discrimination metrics** for fairness assessment in predictive models. The paper proposes **gCI** and **gAUC**, which summarize subgroup-specific discrimination relative to the broader population, and contrasts them with traditional **within-group CI/AUC** and pairwise **xCI/xAUC** analyses.

## Repository purpose

This repo is designed to make the project easier to review, share, and maintain. It has three goals:

1. Keep the original analysis notebooks in a cleaner, GitHub-friendly structure.
2. Separate **data preparation**, **exploratory analysis**, and **fairness metric analysis**.
3. Provide a lightweight, reusable Python implementation of the core ranking metrics in `src/gci_metrics.py`.

## Paper summary

In many fairness analyses, subgroup performance is reported using within-group discrimination metrics such as the concordance index (CI) or the AUC. Those metrics only evaluate ranking **within** a subgroup. In practice, however, clinical decisions are often made across a shared population, so it is also important to understand how well people in a given group are ranked **relative to everyone else**.

This project introduces:

- **xCI / xAUC**: pairwise cross-group ranking metrics
- **gCI / gAUC**: group-level summary metrics that aggregate all relevant comparisons involving a subgroup

The motivating use case is the **PREVENT** equation for 10-year ASCVD risk prediction.

## Repository layout

```text
gci-paper-repo/
├── README.md
├── .gitignore
├── data/
│   └── README.md
├── docs/
│   ├── RELEASE_CHECKLIST.md
│   └── REPOSITORY_NOTES.md
├── figures/
│   └── README.md
├── notebooks/
│   ├── README.md
│   ├── 01_data_preparation/
│   │   ├── 01_data_preprocessing_riddhiman_R.ipynb
│   │   ├── 02_variable_curation_prevent_pce_R.ipynb
│   │   └── 03_prevent_pce_data_prep_R.ipynb
│   ├── 02_exploratory_analysis/
│   │   └── 01_prevent_eda.ipynb
│   └── 03_metric_analysis/
│       ├── 01_prevent_analysis.ipynb
│       ├── 02_xci_analysis.ipynb
│       └── 03_gci_analysis.ipynb
├── requirements/
│   ├── python-requirements.txt
│   └── r-packages.txt
└── src/
    └── gci_metrics.py
```

## Suggested workflow

### 1) Data preparation
Use the R notebooks in `notebooks/01_data_preparation/` to assemble the study cohort, curate variables, and generate analytic artifacts in the Truveta environment.

### 2) Exploratory analysis
Use `notebooks/02_exploratory_analysis/01_prevent_eda.ipynb` for exploratory checks, distributions, and intermediate validation.

### 3) Fairness metric analysis
Use the notebooks in `notebooks/03_metric_analysis/` to compute:

- within-group CI / AUC
- pairwise cross-group xCI / xAUC
- proposed group-level gCI / gAUC

## Reusable metric code

The file `src/gci_metrics.py` contains a clean NumPy-based reference implementation of:

- `xci`
- `gci`
- `xauc`
- `gauc`

This makes it easier to test the metric definitions outside the original notebooks.

## Data availability

The original study uses **Truveta EHR data** and Truveta-specific notebook tooling. For that reason:

- raw data are **not included** in this repository
- some notebooks require a Truveta-managed environment to run
- artifact paths and population IDs should be parameterized before a public release

A good public-facing statement is:

> Due to data use restrictions, source EHR data cannot be shared publicly. This repository contains code used for cohort construction, risk score computation, and fairness metric evaluation.

## Environment notes

This project currently mixes **R notebooks** and **Python notebooks**.

### Python packages
See `requirements/python-requirements.txt`.

### R packages
See `requirements/r-packages.txt`.

## Before making the repo public

Please review the following:

- Remove or parameterize any remaining environment-specific identifiers.
- Confirm that no protected data, tables, screenshots, or outputs remain in the notebooks.
- Add a formal citation once the manuscript is accepted or posted as a preprint.
- Add a license if you want others to reuse the code.

## Citation

If you make the repository public, replace this section with the final manuscript or preprint citation.

```bibtex
@misc{wang_gci_prevent,
  title  = {A simplified metric to streamline between-group fairness assessment for predictive models},
  author = {Wang, Haoyuan and Hong, Chuan and Pencina, Michael and Engelhard, Matthew},
  note   = {Manuscript in revision}
}
```

## Contact

For questions about the code or reproducibility details, please contact the repository maintainer.
