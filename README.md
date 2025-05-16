# Air Quality Index (AQI) Forecasting System

A Python-based system for analyzing and forecasting air quality using time series decomposition and SARIMAX modeling. It includes both command-line and web-based (Streamlit) interfaces to generate date-specific forecasts, identify dominant pollutants, and classify AQI based on EPA standards.

---

## Features

### Core Functionality
- AQI forecasting using historical pollutant data  
- AQI categorization using EPA standards (Good to Hazardous)  
- Identification of dominant pollutants  
- Date-specific forecasts via CLI and Web UI  

### Advanced Analytics
- Automatic handling of missing values (forward fill and spline interpolation)  
- STL decomposition (Seasonal-Trend using LOESS)  
- SARIMAX modeling with exogenous inputs and automated parameter tuning  
- Forecast evaluation using MAE, RMSE, and R² metrics  
- Visualization of trends, seasonality, and forecast results  

---

## Installation

### Requirements
- Python 3.7 or above  
- Required Libraries:  
  `pandas`, `numpy`, `statsmodels`, `scipy`, `matplotlib`, `scikit-learn`, `streamlit`, `joblib`

### Install Dependencies
```bash
pip install pandas numpy statsmodels scipy matplotlib scikit-learn streamlit joblib
Usage
1. Prepare the Dataset
Prepare a CSV file with:

A Timestamp column (daily frequency, convertible to datetime)

Pollutant columns: PM2.5, PM10, NO, NO2, Nox, NH3, SO2, CO, Ozone

Example CSV Format:

csv
Copy
Edit
Timestamp,PM2.5,PM10,NO,NO2,Nox,NH3,SO2,CO,Ozone
2020-01-01,32.1,45.6,0.12,0.23,0.35,0.02,0.11,0.56,0.043
2. Forecasting Pipeline (Python)
python
Copy
Edit
from aqi_forecaster import run_analysis

df = pd.read_csv('your_data.csv', parse_dates=['Timestamp'], index_col='Timestamp')
forecasts = run_analysis(df)

get_aqi_for_date(forecasts)
3. Command-Line Interaction
When executed, the system will prompt for a forecast date:

css
Copy
Edit
Enter a forecast date (YYYY-MM-DD): 2023-06-15
Example Output:

yaml
Copy
Edit
AQI Forecast for 2023-06-15:
PM2.5: 45.30
PM10: 62.10
NO2: 34.20
Ozone: 58.75

Dominant Pollutant: PM10
AQI Category: Moderate
Streamlit Web Application
Setup
Clone the repository:

bash
Copy
Edit
git clone https://github.com/your-repo/aqi-forecast-app.git
cd aqi-forecast-app
Install required packages:

bash
Copy
Edit
pip install streamlit pandas joblib statsmodels
Place your trained model file (aqi_forecast_model.pkl) in the project root directory.

Run the Application
bash
Copy
Edit
streamlit run aqi_app.py
Web App Features
Calendar-based date selector

Real-time AQI forecasts with pollutant-level breakdown

Color-coded AQI category display

Health impact assessment

Graceful fallback if model prediction fails

Sample Output:

yaml
Copy
Edit
AQI Forecast for 2023-06-15:
PM2.5: 45.30
PM10: 62.10
NO2: 34.20
SO2: 28.50
CO: 1.20
O3: 58.75

Dominant Pollutant: PM10
AQI Category: Moderate
Methodology
STL decomposition using a 365-day seasonal cycle

SARIMAX time series forecasting

Parameter tuning via AIC-based grid search

Exogenous inputs from cross-pollutants

Model evaluation using MAE, RMSE, and R² on a 30-day holdout set

