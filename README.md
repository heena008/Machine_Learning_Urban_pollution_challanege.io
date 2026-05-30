# Urban Energy & Air Quality Project

A Python  machine learning models for urban PM2.5 air quality prediction based on Zindi Challenge.

---

## Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [PM2.5 Machine Learning Module](#pm25-machine-learning-module)
- [Installation](#installation)
- [Usage](#usage)
- [Model Performance](#model-performance)
- [References](#references)

---

## Overview
:

 **PM2.5 Prediction** — Machine learning models (Random Forest, XGBoost, Gradient Boosting) trained to forecast urban fine particulate matter (PM2.5) concentrations using meteorological and emissions data.

---

## Project Structure

```

├──Heena.ipynb                 
├──big_code.ipynb                
├── README.md
└── requirements.txt
```


## PM2.5 Machine Learning Module

### Problem

PM2.5 (fine particulate matter, diameter ≤ 2.5 µm) poses serious health risks. This module predicts urban PM2.5 concentrations from meteorological and emissions features.

### Physics-Inspired Model

The feature set is grounded in the following formulation:

```
PM2.5 = α₁E + α₂(SO₂ + NOₓ + VOCs) + α₃·RH + α₄·T − α₅·W + ε
```

Where **E** = primary emissions, **RH** = relative humidity, **T** = temperature, **W** = wind dispersion.

### Models Compared

| Model              | Approach                                      |
|--------------------|-----------------------------------------------|
| Rolling Mean (baseline) | 3-day lag average — no meteorological features |
| Linear Regression  | Physics-inspired feature set                  |
| Random Forest      | Ensemble of independent decision trees        |
| Gradient Boosting  | Sequential tree ensemble                      |
| **XGBoost**        | Optimized gradient boosting — **best performer** |

### Air Quality Categories

Predictions are mapped to standard AQI bands:

| Category                    | PM2.5 (µg/m³) |
|-----------------------------|---------------|
| Good                        | 0 – 12        |
| Moderate                    | 12 – 35       |
| Unhealthy for sensitive groups | 35 – 55    |
| Unhealthy                   | 55 – 150      |
| Very Unhealthy              | > 150         |

---

## Installation

```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo
pip install -r requirements.txt
```

**Key dependencies:**

- `scikit-learn`
- `xgboost`
- `pandas`
- `numpy`
- `matplotlib`

---

## Usage

```python


# PM2.5 prediction (example after training)
import xgboost as xgb
model = xgb.XGBRegressor()
model.load_model("models/xgboost_pm25.json")
prediction = model.predict(X_test)
```

---

## Model Performance

### PM2.5 Models (Training Metrics)

| Model             | RMSE  | MAE   | R²   |
|-------------------|-------|-------|------|
| Rolling Mean      | 28.04 | —     | —    |
| Linear Regression (extended baseline) | 25.18 | 15.77 | 0.71 |
| Random Forest     | 15.53 | 11.10 | 0.89 |
| Gradient Boosting | 29.70 | 21.39 | 0.60 |
| **XGBoost**       | **13.41** | **9.57** | **0.92** |

XGBoost achieved the best performance across all metrics, benefiting from its sequential boosting approach, nonlinearity handling, and robustness to rare pollution events.

---

## References

1. V. T. T. Minh et al., "PM2.5 Forecast System by Using Machine Learning and WRF Model," *Aerosol and Air Quality Research*, vol. 21, 2021.
2. A. Engels et al. (eds.), *Hamburg Climate Futures Outlook 2023*, Cluster of Excellence CLICCS, Hamburg, 2023.


## Set up your Environment

Please make sure you have forked the repo and set up a new virtual environment. For this purpose you can use the following commands:

The added [requirements file](requirements.txt) contains all libraries and dependencies we need to execute the hands-on ml notebooks.

*Note: If there are errors during environment setup, try removing the versions from the failing packages in the requirements file. M1 shizzle.*

### **`macOS`** type the following commands : 


- Install the virtual environment and the required packages by following commands:

    ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/bin/activate
    pip install --upgrade pip
    pip install -r requirements.txt
    ```
### **`WindowsOS`** type the following commands :

- Install the virtual environment and the required packages by following commands.

   For `PowerShell` CLI :

    ```PowerShell
    pyenv local 3.11.3
    python -m venv .venv
    .venv\Scripts\Activate.ps1
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```

    For `Git-bash` CLI :
  
    ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/Scripts/activate
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```
     **`Note:`**
    If you encounter an error when trying to run `pip install --upgrade pip`, try using the following command:

    ```Bash
    python.exe -m pip install --upgrade pip
    ```
    
The data used in this notebook is saved in a `.zip` file. To unzip it, copy the block below into your terminal:

```Bash
unzip data.zip
```

