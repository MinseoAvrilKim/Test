# PS1 / HST Faint Quasar Detectability  
## Background Estimation & Completeness Analysis

This repository contains modular analysis code for estimating robust background/noise and detection limits
in PS1 (Pan-STARRS1) and HST WFC3/IR imaging data, with a focus on faint quasar detectability.

---

## Scientific Motivation

Detecting faint quasars in wide-field (PS1) and space-based (HST) imaging is limited by
non-Gaussian background structures:
scattered light and bright wings (PS1)
extended nebular emission (HST)
Naive percentile-based background estimation fails in such regimes.

This project implements source-masked, sigma-clipped background estimation and uses injection–recovery experiments to quantify realistic detection limits.

---

## Repository Structure

```text
.
├── info_and_bg.py
├── injection_recovery.py
├── psf_utils.py
├── detection_utils.py
├── plotting_utils.py
├── figures/
├── notebooks/
└── README.md

---

(1) info_and_bg.py

This script performs all preparatory and background-related analysis:
