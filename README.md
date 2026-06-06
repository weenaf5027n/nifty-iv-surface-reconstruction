# NIFTY IV Surface Reconstruction

Implied volatility surface reconstruction for NIFTY options using weighted smile fitting, expiry-aware modeling, and walk-forward causal residual learning.

## Project Overview

This project was developed as part of the Finance Club IIT Roorkee Open Projects 2026 challenge on implied volatility surface prediction.

The objective is to estimate missing implied volatility values across strikes and timestamps in a NIFTY options dataset while preserving the financial structure of the volatility surface.

## Methodology

The final solution combines financial surface reconstruction with machine learning:

### 1. V11 Volatility Smile Reconstruction

A weighted polynomial smile-fitting model is used to reconstruct missing implied volatility values across strikes.

Key characteristics:

* Distance-weighted fitting across observed strikes.
* Separate handling of call and put option chains.
* Expiry-aware smile fitting.
* Stable boundary-strike extrapolation.
* Volatility floor to prevent unrealistic predictions.

### 2. Residual Learning

After V11 reconstruction, residual errors are modeled using supervised learning.

For each observed volatility value:

* The value is temporarily hidden.
* V11 reconstructs the missing value.
* The reconstruction error is recorded.
* Market-state features are collected.

The resulting dataset is used to learn systematic V11 prediction errors.

### 3. Walk-Forward Causal Learning

Residual models are trained using only historical observations available prior to the prediction timestamp.

This prevents lookahead bias and ensures that all predictions are generated in a strictly causal manner.

### 4. Sparse-Surface Regime Handling

Additional adjustments are applied in sparse regions of the volatility surface, particularly during expiry-day trading where volatility behavior differs significantly from normal market conditions.

## Repository Structure

```text
.
├── implied_volatility_prediction.ipynb
├── submission.csv
├── requirements.txt
├── README.md
└── LICENSE
```

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* SciPy
* Scikit-Learn
* XGBoost

## Reproducibility

Running the notebook from start to finish generates the final submission file directly from the provided dataset.

The workflow is fully deterministic through fixed random seeds and walk-forward training logic.

## Key Design Principles

* Preserve volatility smile geometry.
* Respect expiry-day regime changes.
* Avoid lookahead bias.
* Combine financial intuition with machine learning.
* Maintain full reproducibility.
