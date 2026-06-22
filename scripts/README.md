# Development scripts

These are the **original development scripts** used while building the tool.
They are kept for reference and reproducibility of the research process. For a
clean, end-to-end, runnable version of the analysis, use
[`../code_ocean/code/main.ipynb`](../code_ocean/code/main.ipynb) instead.

| File | Purpose |
|------|---------|
| `110_CD_Prediction_Models.py` | Trains and grid-searches the candidate models (LR, KNN, NB, RF, XGBoost) and saves comparison metrics. |
| `111_CD_Prediction_Models_winning_model.py` | Fits the winning XGBoost model and produces feature-importance / clustering analysis. |
| `model_utilities.py` | Helper functions (label mapping, confusion-matrix plotting) imported by the scripts above. |

> **Note:** These scripts expect `model/`, `image/`, and `results/` output
> directories to exist relative to the working directory, read data from a
> `data/` folder, and were written against an older pandas API (they use the
> removed `DataFrame.append`). They are not maintained — the notebook is the
> supported entry point.
