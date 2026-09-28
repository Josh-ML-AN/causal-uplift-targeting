# Causal Uplift Targeting with the Criteo Experiment

This repository contains the notebook accompanying an article on using causal inference and uplift modeling to make targeting decisions under capacity constraints.

The core question is:

> The customer most likely to respond is not necessarily the customer whose behavior is most likely to change because of an intervention.

The analysis uses the public **Criteo Uplift Prediction Dataset (v2.1)** from a randomized advertising incrementality experiment and compares two targeting strategies:

- ranking users by predicted visit probability under treatment;
- ranking users by predicted treatment uplift.

The notebook then evaluates both strategies on a fresh **5 million-row held-out randomized population**, alongside a random-targeting benchmark.

## What the notebook covers

- treatment/control balance checks;
- average treatment effect (ATE);
- conditional average treatment effects (CATE);
- a T-learner using two LightGBM response models;
- response-model diagnostics including ROC-AUC, log loss, Brier score, and calibration checks;
- top-10% policy evaluation on the held-out population;
- bootstrap uncertainty for the difference between targeting policies;
- Qini / cumulative incremental gain analysis across different targeting capacities.

## Dataset

The dataset is **not included in this repository**.

Download the **Criteo Uplift Prediction Dataset v2.1** from Criteo's official dataset page:

https://ailab.criteo.com/criteo-uplift-prediction-dataset/

The notebook expects the file:

```text
criteo-research-uplift-v2.1.csv.gz
```

Only the following columns are used:

```text
f0 ... f11
treatment
visit
```

Dataset license: The Criteo Uplift Prediction Dataset is currently distributed under the CC BY-NC-SA 4.0 license. The dataset is not redistributed in this repository; users should obtain it directly from Criteo and comply with the applicable license terms.

## Running the notebook

1. Download `criteo-research-uplift-v2.1.csv.gz`.
2. Place it somewhere accessible to the notebook.
3. Update `DATA_PATH` near the top of the notebook to point to the downloaded file.
4. Install the dependencies in `requirements.txt`.
5. Restart the kernel and run the notebook from top to bottom.

Example:

```python
from pathlib import Path

DATA_PATH = Path("criteo-research-uplift-v2.1.csv.gz")
```

## Dependencies

Install the Python dependencies with:

```bash
pip install -r requirements.txt
```

The analysis uses:

- NumPy
- pandas
- Matplotlib
- SciPy
- scikit-learn
- LightGBM

## Reproducibility

The notebook uses fixed random seeds for the main data split, random targeting reference cohort, and bootstrap procedure.

The 5 million-row final evaluation population is held out from model fitting, calibration, and model diagnostics. Model development is performed on the remaining observations, with separate fit, early-stopping, calibration, and diagnostic subsets within the treatment and control arms.

Because the full dataset contains roughly 14 million rows, execution requires substantially more memory and compute than a small demonstration notebook.

## Notes

This project is an illustrative analysis using a public benchmark dataset. It does not claim production deployment or production uplift results.

The dataset itself is intentionally not redistributed in this repository.
