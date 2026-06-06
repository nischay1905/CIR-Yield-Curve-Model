# Stochastic Interest Rate Modelling and Prediction using the CIR Model

## Finance Club IIT Roorkee – Open Projects 2026

### Project Overview

This project implements, calibrates, and extends the Cox–Ingersoll–Ross (CIR) interest rate model using historical yield curve data.

The objective is to reconstruct the yield curve using only the observed 3-Month yield and evaluate the model's out-of-sample predictive performance.

---

## Problem Statement

Interest rates evolve randomly over time and play a central role in bond pricing, derivative valuation, and risk management.

This project investigates whether a stochastic short-rate model can:

- Be calibrated using historical yield data
- Reconstruct an entire yield curve using only the 3M yield
- Achieve strong out-of-sample predictive performance
- Be improved using advanced model extensions

---

## Dataset

The dataset contains daily zero-coupon yields for the following maturities:

| Tenor | Maturity (Years) |
|---------|---------|
| 3M | 0.25 |
| 6M | 0.50 |
| 9M | 0.75 |
| 1Y | 1 |
| 2Y | 2 |
| 5Y | 5 |
| 10Y | 10 |
| 20Y | 20 |
| 30Y | 30 |

The data was cleaned using:

- Missing value treatment
- Forward filling and interpolation
- Outlier handling
- Date alignment across datasets

---

## CIR Model

The short-rate dynamics are modeled as:

$$
dr_t = a(b-r_t)dt + v\sqrt{r_t}dW_t
$$

where:

- **a** = mean reversion speed
- **b** = long-run equilibrium rate
- **v** = volatility parameter
- **Wₜ** = Brownian motion

The CIR model ensures positive interest rates and produces closed-form bond pricing formulas.

---

## Methodology

### 1. Data Preprocessing

- Cleaned historical yield data
- Removed inconsistencies
- Prepared training and testing datasets

### 2. Time-Series Calibration

Estimated CIR parameters using:

- Maximum Likelihood Estimation (MLE)
- Ordinary Least Squares (OLS)

### 3. Cross-Sectional Calibration

Optimized CIR parameters by fitting the entire yield curve:

$$
\sum (y_{model} - y_{actual})^2
$$

This calibration was used for prediction.

### 4. Yield Curve Reconstruction

For each test day:

- Only the 3M yield was used as input
- The remaining maturities were reconstructed using the calibrated CIR model

### 5. Model Extensions

Implemented and analyzed:

- CIR++
- Two-Factor CIR
- Jump Diffusion CIR

---

## Results

### Out-of-Sample Performance

| Model | Calibration | OOS R² |
|---------|---------|---------|
| Base CIR | Cross-Sectional CIR | 0.8934 |
| CIR++ | CIR + Deterministic Shift | 0.8777 |
| OLS Benchmark | Linear Regression on 3M | 0.7895 |

### Evaluation Requirement

Required:

$$
R^2 > 0.85
$$

Achieved:

$$
R^2 = 0.8934
$$

**Status: PASS **

---

## Key Findings

- The Base CIR model successfully exceeded the project requirement.
- Cross-sectional calibration performed significantly better than pure time-series calibration.
- CIR++ improved curve fitting but did not improve forecasting accuracy.
- Two-Factor CIR demonstrated the importance of slope dynamics.
- Jump-Diffusion models better captured stress-period behaviour.

---

## Repository Structure

```text
.
├── CIR_Project.ipynb
├── README.md
├── requirements.txt
```

---

## Technologies Used

- Python
- NumPy
- Pandas
- SciPy
- Matplotlib
- Scikit-Learn
- Jupyter / Google Colab

---

## Conclusion

The calibrated one-factor CIR model successfully reconstructed the yield curve using only the observed 3-Month yield as input.

The model achieved an out-of-sample R² of **0.8934**, exceeding the project requirement of **0.85**.

The results show that a single-factor affine term structure model captures a significant portion of yield curve dynamics, while extensions such as CIR++, Two-Factor CIR, and Jump Diffusion help explain limitations related to curve slope and stress-period behaviour.
