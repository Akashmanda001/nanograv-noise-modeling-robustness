# nanograv-noise-modeling-robustness
Exploratory analysis of how pulsar selection and noise modeling affect pairwise correlations in the NANOGrav 15-year dataset.
# NANOGrav Noise Modeling Robustness

Exploratory analysis of how pulsar selection and noise modeling affect pairwise correlations in the NANOGrav 15-year dataset.

## Project Overview

This project investigates how pulsar-specific noise modeling and pulsar selection affect the apparent correlations between pulsar timing residuals.

The analysis uses the public NANOGrav 15-year dataset and focuses on:

- Pulsar positions
- Pairwise angular separations
- Residual RMS before and after whitening
- Pulsar-selection groups based on RMS reduction
- Pairwise Pearson correlations
- Comparison with the theoretical Hellings–Downs relationship

The goal is to perform a reproducible exploratory robustness analysis rather than reproduce the full NANOGrav pulsar-timing-array likelihood analysis.

## Dataset

The analysis uses the NANOGrav 15-year pulsar timing dataset.

Dataset:
https://nanograv.org/science/data

The dataset is not included in this repository.

## Methods

### 1. Pulsar Positions

The pulsar timing-model `.par` files are used to extract ecliptic longitude and latitude for the 68 pulsars.

### 2. Pairwise Angular Separation

The angular separation between each pair of pulsars is calculated using their sky positions.

For two pulsars:

\[
\cos\theta =
\sin\delta_1\sin\delta_2 +
\cos\delta_1\cos\delta_2
\cos(\alpha_1-\alpha_2)
\]

This produces 2,278 unique pulsar pairs.

### 3. Noise Whitening

The project compares the RMS of the original timing residuals with the RMS of the published whitened residual products.

The percentage RMS reduction is calculated as:

\[
\text{Reduction} =
100\left(1-\frac{\mathrm{RMS}_{white}}
{\mathrm{RMS}_{original}}\right)
\]

### 4. Pulsar Selection Groups

For exploratory analysis, pulsars are divided according to their RMS reduction:

- Strong: >50%
- Moderate: 10–50%
- Weak: <10%

These thresholds are analysis choices and are not intended to represent physically privileged categories.

### 5. Pairwise Correlations

Residuals from different pulsars are matched approximately by observing time.

Pearson correlation coefficients are then calculated for the matched residuals before and after whitening.

### 6. Hellings–Downs Comparison

The measured correlations are compared with the theoretical Hellings–Downs relationship expected for an isotropic stochastic gravitational-wave background.

The Hellings–Downs curve used is:

\[
\Gamma(\theta)
=
\frac{1}{2}
-\frac{x}{4}
+\frac{3x}{2}\ln x
\]

where

\[
x=\frac{1-\cos\theta}{2}.
\]

## Repository Structure

```text
nanograv-noise-modeling-robustness/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── src/
│   ├── config.py
│   ├── 01_extract_pulsar_positions.py
│   ├── 02_compute_pair_separations.py
│   ├── 03_rms_whitening_analysis.py
│   ├── 04_define_selection_groups.py
│   ├── 05_pairwise_correlations.py
│   ├── 06_make_figures.py
│   └── 07_summary_statistics.py
│
└── results/
