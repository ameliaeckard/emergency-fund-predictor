# Emergency Fund Predictor _(emergency-fund-predictor)_

Lab report: [Emergency Fund Predictor](https://lab.ameliaeckard.com/notes/2026-10-08-emergency-fund-predictor)

A machine-learning study of financial fragility using Federal Reserve SHED and regional economic data.

## Background

The project asks whether a respondent can cover a $400 emergency expense with cash or savings. It combines 12,295 SHED respondents with regional economic indicators and compares linear and tree-based classifiers.

## Install

```bash
git clone https://github.com/ameliaeckard/emergency-fund-predictor.git
cd emergency-fund-predictor
pip install -r requirements.txt
```

## Usage

Run the analysis notebooks under `notebooks/`. Data inputs live under `data/` and generated outputs under `results/`.

```bash
jupyter notebook
```

## Results

- Logistic regression: 58.0% accuracy, 0.512 F1, 0.639 ROC-AUC
- Random forest: 59.9% accuracy, 0.512 F1, 0.639 ROC-AUC
- Gradient boosting: 58.8% accuracy, 0.493 F1
- 43.7% of respondents could cover the expense with cash or savings

Tree models overfit while logistic regression generalized more consistently. The plateau suggests the current feature set is a stronger limitation than model complexity alone.

## Data

Primary sources are the Federal Reserve 2024 SHED, Bureau of Economic Analysis regional price data, and FRED-derived state indicators.

## Maintainer

[Amelia Eckard](https://github.com/ameliaeckard)

## Contributing

Issues are welcome for bugs or documentation problems. Please open an issue before a substantial pull request.
