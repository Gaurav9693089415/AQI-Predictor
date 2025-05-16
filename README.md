Air Quality Index (AQI) Forecasting System
Python
Pandas
Statsmodels
Matplotlib

A comprehensive air quality analysis and forecasting system that processes pollutant data, performs time series decomposition, and generates AQI forecasts using SARIMAX models.

Table of Contents
Features

Installation

Usage

Methodology

Data Requirements

Examples

License

Features
Core Functionality
AQI Categorization: Classifies air quality into standard EPA categories (Good to Hazardous)

Date-Specific Forecasts: Retrieves and displays AQI forecasts for user-specified dates

Dominant Pollutant Identification: Determines which pollutant drives the AQI for a given day

Advanced Analytics
Data Preprocessing:

Automatic handling of missing values (forward fill)

Datetime index conversion and frequency standardization

Spline interpolation for missing pollutant values

Time Series Decomposition:

STL (Seasonal-Trend decomposition using LOESS) analysis

Visualization of trend, seasonal, and residual components

Forecasting Models:

SARIMAX (Seasonal AutoRegressive Integrated Moving Average with eXogenous factors) implementation

Automatic parameter grid search for optimal model selection

Multi-pollutant forecasting with cross-pollutant dependencies

Evaluation & Visualization
Model performance metrics (MAE, RMSE, R²)

Comparative plots of actual vs predicted values

Forecast visualization for all pollutants

Installation
Prerequisites:

Python 3.7+

Required packages: pandas, numpy, statsmodels, scipy, matplotlib, scikit-learn

Install dependencies:

bash
pip install pandas numpy statsmodels scipy matplotlib scikit-learn
Usage
1. Data Preparation
Prepare your input data as a pandas DataFrame with:

A datetime index (daily frequency)

Columns for each pollutant: PM2.5, PM10, NO, NO2, Nox, NH3, SO2, CO, Ozone

2. Running the Analysis
python
from aqi_forecaster import run_analysis

# Load your data
df = pd.read_csv('your_data.csv', parse_dates=['Timestamp'], index_col='Timestamp')

# Run complete analysis pipeline
forecasts = run_analysis(df)

# Get AQI for specific date
get_aqi_for_date(forecasts)
3. Command Line Interaction
When prompted, enter a date in YYYY-MM-DD format to get:

Individual pollutant forecasts

Dominant pollutant identification

AQI category classification

Example output:

Enter a forecast date (YYYY-MM-DD): 2023-06-15

AQI Forecast for 2023-06-15:

PM2.5: 45.30
PM10: 62.10
Ozone: 58.75
NO2: 34.20

Dominant Pollutant: PM10 (62.10)
AQI Category: Moderate
Methodology
1. Data Preprocessing
Missing Value Handling: Forward fill followed by spline interpolation

Frequency Standardization: Ensures consistent daily timesteps

Multi-pollutant Coordination: Maintains temporal alignment across all pollutants

2. Time Series Decomposition
STL decomposition with 365-day seasonality period

Visual inspection of:

Long-term trends

Seasonal patterns

Residual noise

3. Forecasting Model
SARIMAX Implementation:

Automatic parameter selection via grid search (AIC minimization)

Incorporates cross-pollutant effects as exogenous variables

Handles both seasonal and non-seasonal patterns

Model Evaluation:

30-day holdout validation period

Comprehensive metrics (MAE, RMSE, R²)

Data Requirements
Input Format
CSV file with at minimum:

Timestamp column (convertible to pandas datetime)

Columns for each pollutant (µg/m³ for particulates, ppm for gases)

Expected Columns
Timestamp,PM2.5,PM10,NO,NO2,Nox,NH3,SO2,CO,Ozone
2020-01-01,32.1,45.6,0.12,0.23,0.35,0.02,0.11,0.56,0.043
...
Examples
STL Decomposition Visualization
STL Decomposition Example

Forecast vs Actual Comparison
Forecast Example

AQI Category Breakdown
AQI Range	Category	Health Implications
0-50	Good	Minimal impact
51-100	Moderate	Sensitive groups may be affected
101-150	Unhealthy for Sensitive Groups	Increased respiratory effects
151-200	Unhealthy	General public health affected
201-300	Very Unhealthy	Serious health effects
300+	Hazardous	Emergency conditions


AQI Forecast Web Application
Streamlit
Python
Pandas

A Streamlit web application for predicting and visualizing Air Quality Index (AQI) forecasts by date, with pollutant-specific breakdowns and health impact categorization.

Table of Contents
Application Overview

Key Features

Installation & Setup

Usage Instructions

Technical Implementation

Model Integration

Error Handling

License

Application Overview
This interactive web application provides:

Date-specific AQI forecasts

Multi-pollutant breakdown (PM2.5, PM10, NO2, SO2, CO, O3)

EPA-standard AQI categorization

Dominant pollutant identification

Health impact assessment

Key Features
User Interface
Date Picker: Calendar interface for selecting forecast dates

Interactive Display: Real-time forecast results

Visual Categorization: Color-coded AQI health impact levels

Core Functionality
Model Integration: Loads and executes SARIMAX forecasting model

Multi-Pollutant Analysis: Individual and comparative pollutant levels

Error Resilience: Graceful fallback to random values if model fails

Output Presentation
Numerical pollutant concentrations

Dominant pollutant identification

AQI category with health implications

Clean, responsive layout

Installation & Setup
Prerequisites
Python 3.7+

Streamlit

Pandas

Joblib

Statsmodels (for SARIMAX model)

Installation
Clone the repository:

bash
git clone https://github.com/your-repo/aqi-forecast-app.git
cd aqi-forecast-app
Install dependencies:

bash
pip install streamlit pandas joblib statsmodels
Place your trained model file (aqi_forecast_model.pkl) in the project root

Usage Instructions
Running the Application
bash
streamlit run aqi_app.py
Using the Application
Select a date using the calendar picker (future dates only)

Click "Get AQI Forecast" button

View results:

Individual pollutant concentrations

Dominant pollutant

AQI category with health implications

Example Output
AQI Forecast for 2023-06-15

PM2.5: 45.30
PM10: 62.10
NO2: 34.20
SO2: 28.50
CO: 1.20
O3: 58.75

Dominant Pollutant: PM10 (62.10)
AQI Category: Moderate (May cause breathing discomfort for sensitive groups)
Technical Implementation
Model Integration
python
# Load the trained SARIMAX model
forecast_model = joblib.load('aqi_forecast_model.pkl')

# Generate forecast
forecast = forecast_model.get_forecast(steps=1)
predicted_value = forecast.predicted_mean.iloc[0]
Core Functions
AQI Categorization:

python
def categorize_aqi(aqi_value):
    if aqi_value <= 50: return "Good"
    elif aqi_value <= 100: return "Moderate"
    ...
Forecast Generation:

python
def get_aqi_forecast(model, input_date):
    try:
        # Model prediction logic
    except:
        # Fallback to random value
UI Components
Date picker with minimum date validation

Responsive result cards

Color-coded health impact indicators

Model Integration
Requirements
Serialized SARIMAX model (.pkl file)

Compatible Python environment

Matching feature set (pollutant types)

Fallback Mechanism
If model prediction fails:

Logs detailed error

Generates plausible random value

Continues application operation

Error Handling
Robustness Features
Invalid date handling

Model loading failures

Prediction exceptions

Missing data scenarios

Error Recovery
Graceful degradation to random values

Detailed console logging

User-friendly error messages
