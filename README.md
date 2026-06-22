# MLtool — A Machine Learning Software Tool for Multiclass Classification

[![Software Impacts](https://img.shields.io/badge/Software%20Impacts-10.1016%2Fj.simpa.2022.100383-blue)](https://doi.org/10.1016/j.simpa.2022.100383)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

This repository contains the software accompanying the paper:

> S. Wang, H. Lu, A. Khan, F. Hajati, M. Khushi, S. Uddin.
> **"A machine learning software tool for multiclass classification."**
> *Software Impacts*, Volume 13, 2022, 100383.
> https://doi.org/10.1016/j.simpa.2022.100383

The tool provides an end-to-end, reproducible pipeline that trains and compares
seven machine learning models for **multiclass classification**. It is
demonstrated on a healthcare problem: predicting chronic-disease **comorbidity
and multimorbidity** — that is, whether a patient has **no**, **one**, or
**two-or-more** concerned chronic diseases (a 3-class target) — using a
combination of patient features and network-analytics features derived from a
patient–disease network.

## Key idea

For each patient the tool predicts one of three classes:

| Class | Label    | Meaning                          |
|-------|----------|----------------------------------|
| 0     | `No CD`  | No concerned chronic disease     |
| 1     | `1 CD`   | One concerned chronic disease    |
| 2     | `>=2 CDs`| Two or more (multimorbidity)     |

It benchmarks seven classifiers with hyperparameter tuning and reports accuracy
and standard evaluation metrics, feature importance, and feature distributions.

## Models

- Logistic Regression (LR)
- K-Nearest Neighbours (KNN)
- Naive Bayes (NB)
- Random Forest (RF)
- XGBoost
- Multilayer Perceptron (MLP)
- Convolutional Neural Network (CNN)

XGBoost and Random Forest were the top performers in the paper (XGBoost reaching
~95% test accuracy). The analysis also shows that combining **network features**
with **patient features** substantially improves prediction over either set
alone.

## Repository structure

```
.
├── code_ocean/              # Reproducible capsule (the canonical artifact)
│   ├── code/
│   │   └── main.ipynb       # Full, runnable analysis that reproduces the paper
│   ├── data/
│   │   └── patient.csv      # Input dataset used by the notebook
│   └── results/             # Generated figures (Figure2–7) and tables (Table2–6)
├── data/                    # Additional dataset variants
│   ├── patient_chronic_dataset_no_dummy.csv
│   └── patient_chronic_data_with_network_nodisease.csv
├── scripts/                 # Original development scripts (see scripts/README.md)
│   ├── 110_CD_Prediction_Models.py
│   ├── 111_CD_Prediction_Models_winning_model.py
│   └── model_utilities.py
├── requirements.txt
├── CITATION.cff
├── LICENSE
└── README.md
```

> **Where to start:** The recommended entry point is
> [`code_ocean/code/main.ipynb`](code_ocean/code/main.ipynb). It is the cleaned,
> end-to-end version that loads the data, trains all seven models, and
> regenerates every figure and table in the paper. The files under `scripts/`
> are the earlier development versions kept for reference.

## Data

The dataset (`code_ocean/data/patient.csv`, ~29k patients) contains, per patient:

- **Patient features** — demographics (gender, age), service history, episode
  counts, ICD-code counts, comorbidity indicators (Elixhauser and other chronic
  conditions), smoking and alcohol flags.
- **Network features** — graph metrics computed from a patient network:
  degree, eigenvector centrality, triangle count, transitivity, several
  PageRank variants, neighbour count, and closeness.
- **Target** — `concerned_chronic_num` (0, 1, or ≥2).

## Installation

Requires Python 3.8+.

```bash
git clone https://github.com/haohuilu/MLtool.git
cd MLtool
python -m venv venv
source venv/bin/activate      # on Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## Usage

Launch Jupyter and run the notebook top to bottom:

```bash
jupyter notebook code_ocean/code/main.ipynb
```

Running all cells reproduces the model comparison, feature-importance analysis,
and the figures/tables found in `code_ocean/results/`.

## Citation

If you use this software, please cite the paper (see [`CITATION.cff`](CITATION.cff)):

```bibtex
@article{wang2022mltool,
  title   = {A machine learning software tool for multiclass classification},
  author  = {Wang, Shangzhou and Lu, Haohui and Khan, Arif and Hajati, Farshid and Khushi, Matloob and Uddin, Shahadat},
  journal = {Software Impacts},
  volume  = {13},
  pages   = {100383},
  year    = {2022},
  doi     = {10.1016/j.simpa.2022.100383}
}
```

## Authors

Shangzhou Wang, Haohui Lu, Arif Khan, Farshid Hajati, Matloob Khushi, and
Shahadat Uddin — School of Project Management, Faculty of Engineering,
The University of Sydney, Australia.

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file.
