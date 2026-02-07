# Apple Stock Signals + Prophet Forecasting

## Overview
This project analyses Apple’s historical stock prices and combines two approaches:
1) Rule-based trading signals using moving averages.
2) Time-series forecasting using Prophet with custom seasonality.

The goal is to understand trend + momentum from past data and generate an interpretable 90-day forward-looking forecast with uncertainty ranges.

## Data
- Historical stock data downloaded using yfinance (2018-01-01 to 2023-01-01)
- Core variable used: Closing price
- Dates are converted and cleaned for modelling

## Tools & Libraries
- yfinance (data collection)
- pandas, numpy (processing)
- matplotlib (visualisation)
- prophet (forecasting)
- pyspark (Spark session created for scalable processing context + CSV export)
- joblib (model saving)

## Methodology

### 1) Moving Average Signals
- Short moving average: 5-day
- Long moving average: 20-day
- Momentum confirmation uses the previous day’s short MA

Signal rules:
- Buy (+1): short MA > long MA and short MA > previous short MA
- Sell (-1): short MA < long MA and short MA < previous short MA
- Hold (0): otherwise

### 2) Prophet Forecasting
- Reformatted data into Prophet structure: ds (date), y (close price)
- Time-ordered split: 80% train / 20% test
- Prophet configured with yearly + weekly seasonality, plus:
  - Monthly seasonality (period ~30.5)
  - Quarterly seasonality (period ~91.25)

Outputs include forecast plots with uncertainty bands and a 90-day daily forecast table (yhat, yhat_lower, yhat_upper).

## Outcome
A complete notebook demonstrating:
- Signal creation using moving averages + momentum logic
- Forecasting with Prophet and custom seasonal patterns
- A saved Prophet model for reuse and iterative forecasting
