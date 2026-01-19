# PS1 / HST Faint Quasar Detectability  
## This is just for a practice!!!! I'm not that good at python and astronomy both
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
├── info_and_bg.py
├── injection_recovery.py
├── psf_utils.py
├── detection_utils.py
├── plotting_utils.py
├── figures/
├── notebooks/
└── README.md
```

---

## 1. info_and_bg.py

This script performs all preparatory and background-related analysis:

(1) Functions include
- FITS header inspection (BUNIT, gain, exposure time)
- pixel value diagnostics (min/max, histograms)
- NaN / inf / extreme-value masking
- source detection and masking using photutils
- sigma-clipped background statistics (mean / median / RMS)
- visualization (raw image, masked image, background histograms, sigma-clipping diagnostics)

(2) Purpose
- Understand image characteristics
- Validate background estimation robustness
- Produce figures for Method/Appendix sections

## 2. injection_recovery.py

This script quantifies the practical detection limit via simulations.

(1) Workflow
- PSF estimation or loading
- injection of artificial point sources at random positions
- magnitude grid sampling
- source recovery using the same detection pipeline as real data
- recovery fraction vs magnitude
- estimation of 50% completeness magnitude

(2) Outputs
- completeness curves
- PS1 vs HST sensitivity comparison
- limiting magnitude estimates based on recovery statistics
-> Primary metric for scientific interpretation

## 3. psf_utils.py

(1) Utility functions for:
- PSF FWHM estimation
- empirical PSF construction from bright stars
- Gaussian / Moffat PSF generation
- PSF normalization for flux-conserving injection

(2) Used by:
- injection_recovery.py
- analytical SNR calculations

## 4. detection_utils.py

(1) Shared functions implementing:
- detect_threshold
- detect_sources
- SegmentationImage.make_source_mask
- combined masking logic (sources + NaN + extreme pixels)

(2) Ensures identical detection logic across:
- background estimation
- injection–recovery simulations

## 5. plotting_utils.py

(1) Standardized plotting routines for:
- image display with consistent stretch
- background histograms
- sigma-clipping convergence
- completeness curves
Keeps figures consistent and publication-ready.

---

This research made use of Photutils, an Astropy package for detection and photometry of astronomical sources (Bradley et al. <2026>)
