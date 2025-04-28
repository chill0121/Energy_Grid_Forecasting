# Energy Grid Forecasting

> Time series forecasting of energy load using statistical, machine learning, and deep learning models across short, medium, and long-term forecast horizons.

**For full technical details**, see:
- [`/Reports/Final/Project_Final_Report.pdf`](./Reports/Final/Project_Final_Report.pdf) – Technical write-up, results, methods
- [`/Energy_Forecasting.ipynb`](./Energy_Forecasting.ipynb) – Code, visualizations, and explanation and reasoning

---

## Overview

This project investigates the accuracy and efficiency of various forecasting models when applied to electrical energy demand data from the PJM grid. The aim is to determine how model selection should be tailored to different forecast horizon intervals—from 6 hours to 2 years—while considering compute limitations, seasonality, and real-world deployment constraints.

---

## Repository Structure

```bash
Energy-Grid-Forecasting/
├── Data/                    # Raw input data (energy, weather)
├── Models/                  # Saved models, predictions, checkpoints
├── Reports/                 # Proposals, final report, presentation slides
├── Images/                  # Visualizations used in analysis & reports
├── Energy_Forecasting.ipynb # Jupyter notebook | main project code
├── README.md                # This file
└── TODO_Tasks.md            # Project to-do list and future ideas
```

---

## Datasets Used

| Source            | Data                       | Period       | Format     |
|------------------|----------------------------|--------------|------------|
| PJM ISO          | Hourly load (by zone)      | 1993–2024    | CSV (gzip) |
| NOAA RCC ACIS    | Daily weather summaries    | 1993–2024    | CSV (gzip) |

Zones: AE, CE, DOM, JC, PEP – selected for geographic diversity and time series quality.

---

## Pipeline & Methodology

### Forecast Horizons

| Interval         | Definition                |
|------------------|---------------------------|
| Very Short-Term  | < 1 Hour                  |
| Short-Term       | 1 Hour to < 1 Week        |
| Medium-Term      | 1 Week to ≤ 1 Year        |
| Long-Term        | > 1 Year                  |

### Preprocessing
- Missing timestamps filled via interpolation
- Outlier removal via rolling window median replacement
- Merged hourly load + daily weather data by region

### Feature Engineering
- Temporal encodings (hour, day, week, month, year)
- Lag features at 6H, 1D, 1W, 1M
- Fourier transform features
- First & second-order derivatives
- Rolling means (30 days)

### Models Compared

| Type              | Models                                  |
|-------------------|------------------------------------------|
| Baseline          | Seasonal Naive, Mean                    |
| Statistical       | Holt-Winters, MSTL                      |
| Machine Learning  | SVR (RBF Kernel), XGBoost               |
| Deep Learning     | N-HiTS (Neural Hierarchical Interp.)    |

> SARIMA and TFT were removed due to hardware constraints.

---

## Evaluation

### Metrics
- **sMAPE**
- **RMSE**, **NRMSE** for scale-sensitive and zone comparison evaluation

### Time-Based Split
- **Train**: 1993–2018
- **Validation**: 2019–2021
- **Test**: 2022–2024

---

## Results Summary

### Best Models by Horizon

| Horizon    | Best Model       | Notes                                                  |
|------------|------------------|--------------------------------------------------------|
| 6 Hours    | MSTL / N-HiTS    | Statistical & DL models performed well                |
| 3 Days     | XGBoost / SVR    | ML models outperform others in 4/5 zones              |
| 1 Week     | XGBoost          | Outperformed both statistical and deep learning       |
| 1 Month    | XGBoost          | Retained edge over others                              |
| 6 Months   | XGBoost          | Some statistical models fell below baseline           |
| 2 Years    | XGBoost          | ML models generalize best to long-term forecasts      |

### Compute Efficiency (M1 MacBook, 16GB RAM)

| Model         | Train+Predict Time   |
|---------------|----------------------|
| Seasonal Naive| Instant              |
| Mean          | Instant              |
| Holt-Winters  | ~9 minutes           |
| MSTL          | ~95 minutes          |
| SVR           | ~59 minutes          |
| XGBoost       | ~2 minutes           |
| N-HiTS        | 9 → ~570 minutes*    |

\* Extrapolated estimate for full training set

---

## Key Insights

- **XGBoost** offered the best trade-off of accuracy and efficiency, though requires extensive feature engineering and retraining.
- **Statistical models** still shine in short-horizon settings with clear seasonality.
- **Deep learning models**, while powerful, demand substantial compute for modest performance gains.
- Hardware constraints significantly impact feasible modeling strategies, especially with large datasets.

---

## Future Work

- Test SARIMA & TFT models on more powerful hardware
- Automate model tuning with Optuna/Ray Tune
- Develop zone-specific ensemble models
- Build an interactive dashboard for operators and forecasters
- Reintroduce anomaly detection module in post-processing
