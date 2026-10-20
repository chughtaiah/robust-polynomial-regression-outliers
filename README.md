# Robust Curve Regression with Outliers

Reproducible experiments for robust **polynomial and B-spline regression** under multiple outlier mechanisms.

This repository accompanies the Towards Data Science article:

**[Don’t Let Messy Data Bend Your Curves](https://towardsdatascience.com/dont-let-messy-data-bend-your-curves/)**

It extends the first article in the series:

- [How to Make Linear Regression Survive Outliers](https://towardsdatascience.com/how-to-make-linear-regression-survive-outliers/)
- [robust-linear-regression-outliers](https://github.com/chughtaiah/robust-linear-regression-outliers)

## What is compared?

The notebook uses the same six estimators as the linear-regression study:

- Ordinary least squares (OLS)
- Huber regression
- RANSAC
- GNC-GM
- GNC-TLS
- ASOR

and applies them to three curve representations:

- quadratic polynomial;
- cubic polynomial;
- quadratic B-spline.

The central idea is simple:

> **Change the basis; keep the robust-estimation machinery.**

## Experiments

The notebook includes:

- zero-mean Gaussian replacement outliers;
- biased Gaussian replacement outliers;
- biased uniform replacement outliers;
- a coherent competing curve;
- contamination ratios from 0% to 90%;
- sample-size scaling;
- nominal-noise scaling;
- RANSAC minimal-sample analysis;
- a common-ground-truth model-richness experiment;
- an illustrative local-support experiment;
- wind-turbine power-curve and GNSS Doppler case studies.

Each exact condition in the full benchmark is repeated over **30 Monte Carlo realizations**.

## Repository structure

```text
robust-curve-regression-outliers/
├── figures/
├── License
├── README.md
├── requirements.txt
└── robust_curve_regression_outliers.ipynb
```

The `figures/` folder contains the main visual assets used in the article, including the polynomial-basis and B-spline animations and the wind-turbine and GNSS illustrations.

## Installation

Clone the repository and install the dependencies:

```bash
git clone https://github.com/chughtaiah/robust-curve-regression-outliers.git
cd robust-curve-regression-outliers
pip install -r requirements.txt
```

Then open the notebook:

```bash
jupyter notebook robust_curve_regression_outliers.ipynb
```

## Quick and full runs

The notebook defaults to:

```python
RUN_PROFILE = "quick"
```

for a fast check of the complete pipeline.

To reproduce the full article benchmark, change it to:

```python
RUN_PROFILE = "full"
```

The full profile runs 30 Monte Carlo realizations for each exact condition and generates the detailed numerical results and figures.

## Main benchmark settings

- Baseline sample size: `N = 100`
- Predictor range: `[-100, 100]`
- Baseline nominal variance: `σ_in² = 1000`
- Contamination ratios: `0%, 10%, 30%, 50%, 70%, 90%`
- Sample-size sweep: `N = 50, 100, 200, 500, 1000, 2000, 5000`
- Noise-variance sweep: `10, 100, 1000, 10000`

For the controlled model-richness experiment, the **same quadratic ground truth and the same contaminated observations** are fitted using quadratic, cubic, and B-spline bases. This isolates the effect of changing the representation while keeping the data fixed.

## Reproducibility notes

- Every estimator sees the same dataset within a Monte Carlo realization.
- Random seeds are fixed and documented in the notebook.
- The robust-estimator implementations retain the settings used in the previous linear-regression study.
- Only model-specific changes, such as the design matrix and RANSAC minimal sample size, are introduced where necessary.
- Reported empirical conclusions are limited to the benchmark conditions tested here.

## Disclosure

Aamir Hussain Chughtai was the primary designer of ASOR in the cited work. All estimators are evaluated on the same Monte Carlo realizations using fixed and documented settings.

## License

This repository is released under the MIT License. See `License`.
