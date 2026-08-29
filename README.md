# Electricity Consumption Forecasting — MSI608
 
Daily electricity consumption forecasting using Naive, SARIMA, and MLP models, developed for the **MSI608 — Special Topics in Data Science** course, Master's in Computer Engineering (Magíster en Ingeniería Informática), Universidad Andrés Bello (UNAB).
 
This repository accompanies the IEEE Access-format paper *"[Título del paper — completar]"*, which compares three forecasting approaches of increasing complexity over a four-year daily electricity demand series, and evaluates their performance at multiple aggregation horizons (daily, weekly, monthly, annual).
 
---
 
## Overview
 
| | |
|---|---|
| **Dataset** | Daily aggregated electricity consumption, 2018-01-01 to 2021-12-31 (1,461 observations) |
| **Task** | Univariate time-series forecasting |
| **Models compared** | Seasonal Naive (baseline), SARIMA(2,1,2)(1,0,1,7), MLP (autoregressive window, keras-tuner) |
| **Best model** | SARIMA — MAPE 6.72%, R² 0.852 (daily test set, 2021) |
| **Extended forecast** | 2022 (day / week / month / year), SARIMAX with annual Fourier terms vs. recursive MLP |
 
## Results Summary
 
**Daily test set (2021, n=365):**
 
| Model | MSE | RMSE | MAE | MAPE | R² |
|---|---|---|---|---|---|
| Naive (seasonal) | 439.60 | 20.97 | 16.40 | 11.09% | 0.613 |
| **SARIMA(2,1,2)(1,0,1,7)** | **168.37** | **12.98** | **9.75** | **6.72%** | **0.852** |
| MLP (keras-tuner) | 194.66 | 13.95 | 10.43 | 7.20% | 0.828 |
 
Full results, including weekly/monthly/annual aggregated metrics, are reported in the paper (Section IV) and reproducible from the notebook.
 
## Repository Structure
 
```
.
├── notebook/
│   └── analisis_consumo_autonomo.ipynb   # Full pipeline: EDA, modeling, evaluation, forecasting
├── dataset/
│   └── data_ys.csv                        # Daily aggregated consumption (year, month, day, consumption)
├── paper/
│   └── MSI608_Proyecto_1_final.docx       # IEEE Access paper (6 pages, double column)
├── figures/
│   ├── Figura1_Arquitectura_Pipeline.drawio   # Pipeline architecture diagram (editable, draw.io)
│   └── ...                                # Exported figures used in the paper (ACF/PACF, loss curve, predictions, etc.)
└── README.md
```
 
>  Adjust this structure to match your actual folder layout before pushing — this is a suggested organization based on the project's deliverables.
 
##  Methodology (brief)
 
1. **EDA & Preprocessing** — completeness, correctness, and IQR-based outlier checks; ADF stationarity test (d=1 confirmed); weekly seasonality (m=7) confirmed via ACF/PACF and seasonal decomposition.
2. **Chronological split** — training on 2018–2020 (1,096 obs.), testing on 2021 (365 obs.), no random shuffling to avoid data leakage.
3. **Modeling** — a seasonal naive baseline, a SARIMA model selected from ACF/PACF/ADF evidence, and an MLP trained on a 14-day autoregressive window with hyperparameters tuned via `keras-tuner` (Random Search).
4. **Evaluation** — MAE, RMSE, MAPE, and R², computed at daily, weekly, monthly, and annual aggregation levels.
5. **Future forecasting** — 2022 projection using SARIMAX with annual Fourier exogenous terms (to avoid the flattening pattern observed beyond a 7-day horizon) and a recursive MLP.
## ⚙️ Requirements
 
```bash
pip install pandas numpy matplotlib statsmodels tensorflow keras-tuner scikit-learn --break-system-packages
```
 
## How to Run
 
```bash
jupyter notebook notebook/analisis_consumo_autonomo.ipynb
```
 
The notebook is self-contained (dataset embedded); running all cells reproduces the full EDA, model comparison, and forecasting results reported in the paper.
 
## 👥 Team
 
- Eric Silva
- Brian Guzman
- Miguel González
- Edson Quevedo
- Jaime Rivera
  
**Course:** MSI608 — Special Topics in Data Science, Master's in Computer Engineering, Universidad Andrés Bello (UNAB)
**Delivery date:** August 29, 2026
 
## 📄 License
 
Academic project for course purposes — MSI608, UNAB. *[Adjust or remove if the course requires a specific license]*
