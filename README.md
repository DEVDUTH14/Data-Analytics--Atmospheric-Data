# Data-Analytics-Atmospheric-Data

**Goal:** Predict key cloud microphysical parameters — **Liquid Water Path (LWP)** and **Ice Water Path (IWP)** — from satellite-based **CERES** observations over South India, and compare **single-task vs multi-task** learning using **ANN** and **GRU**.

## 🚀 Impact

- **Enhanced climate-relevant predictions** for LWP and IWP, improving representation of cloud–radiation interactions in climate and weather models.
- **Multi-task GRU model** achieved **near-perfect accuracy (R² ≈ 0.999)** for both LWP and IWP, significantly outperforming single-task baselines.
- Demonstrated that **jointly learning correlated atmospheric variables** leads to better generalization and robustness, even under heavy outliers and missing data.

## 🧪 Methodology

- **Data:** NASA **CERES** satellite dataset (South India, monsoon months, 2018–2023).
- **Targets:**  
  - LWP (Liquid Water Path)  
  - IWP (Ice Water Path)
- **Features:** Radiative fluxes (SW, LW), surface/land surface temperature, surface pressure, wind speed, cloud-top/base temperature, cloud-top height, cloud optical depth, cloud particle radius, etc.
- **Preprocessing:**
  - Covariance-based **feature selection** to remove highly redundant features.
  - **Outlier detection** via box plots; addressed with **robust scaling (IQR-based)**.
  - **Missing values** handled using **KNN imputation** after comparing mean and linear-regression imputation.
  - Time-aware split: **2018–2022 train**, **2022–2023 test**.
- **Models:**
  - **ANN** (feed-forward baseline).
  - **GRU** (sequence model for meteorological time series).
- **Learning setups:**
  - **Single-task:** separate models for LWP and IWP.
  - **Multi-task:** shared model jointly predicting [LWP, IWP] to exploit their strong correlation (~0.84).
- **Optimization:** Hyperparameters tuned with **Optuna** (search over depth, hidden units, learning rate, regularization, etc.).

## 📊 Key Results

- **LWP – ANN:** R² improved from **0.77 → 0.83** when moving from single-task to multi-task.
- **LWP – GRU:** Multi-task GRU reached **R² ≈ 0.999**, with much lower MAE/RMSE than all other models.
- **IWP – ANN:** R² improved from **0.71 → 0.85** with multi-task learning.
- **IWP – GRU:** Multi-task GRU again achieved **R² ≈ 0.999**, proving highly robust even with many outliers.

> **TL;DR:** Multi-task GRU, combined with robust preprocessing and Optuna-based tuning, delivers near–state-of-the-art accuracy for satellite-based prediction of cloud microphysical properties.
