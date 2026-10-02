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
