# AQI Forecasting System

A Python-based system for air quality forecasting using SARIMAX models. It processes pollutant data, performs seasonal decomposition (STL), and generates date-specific AQI predictions.

## Features

* **Forecasts AQI by date**
* **Identifies dominant pollutants**
* **Classifies AQI using EPA categories**
* **Handles missing values (forward fill + spline interpolation)**
* **Uses STL decomposition and SARIMAX modeling**
* **Visualizes forecasts and model performance (MAE, RMSE, R²)**

## Installation

```bash
pip install pandas numpy statsmodels scipy matplotlib scikit-learn streamlit joblib
```

## Usage

### Python Module

```python
from aqi_forecaster import run_analysis

# Load data
df = pd.read_csv('your_data.csv', parse_dates=['Timestamp'], index_col='Timestamp')
forecasts = run_analysis(df)
get_aqi_for_date(forecasts)
```

### Streamlit App

```bash
streamlit run aqi_app.py
```

## Input Format

CSV with columns: `Timestamp, PM2.5, PM10, NO, NO2, Nox, NH3, SO2, CO, Ozone`

## AQI Categories

| AQI     | Category                       |
| ------- | ------------------------------ |
| 0-50    | Good                           |
| 51-100  | Moderate                       |
| 101-150 | Unhealthy for Sensitive Groups |
| 151-200 | Unhealthy                      |
| 201-300 | Very Unhealthy                 |
| 300+    | Hazardous                      |

## Streamlit Features

* **Calendar picker for date selection**
* **Forecast display with pollutant breakdown**
* **Color-coded AQI impact levels**
* **Fallback handling on prediction failure**


