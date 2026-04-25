# Traffic-Forecasting
# Overview
This assignment analyzes daily traffic volume data from the Baregg Tunnel in Switzerland (November 2003 – November 2005) and compares two forecasting methods: a Naïve forecast and a Linear Regression (TSLM) model.

# Dataset
PropertyDetailsSourceBareggTunnel.csvMeasureDaily vehicle count through the Baregg TunnelPeriodNovember 1, 2003 – November 21, 2005FrequencyDailyTotal Records748 observations
Summary Statistics:
Min1st Qu.MedianMean3rd Qu.Max53,09898,794108,204106,568115,477139,840

# Key Observations from EDA

Trend: Traffic is relatively stable over the two-year period with no strong upward or downward trend.
Seasonality: A clear weekly pattern exists — weekdays have higher traffic, weekends have lower traffic.
Anomalies: Occasional dips likely correspond to public holidays, road closures, or extreme weather events.


# Methodology
Data Split
SetPeriodObservationsTrainingUp to June 30, 2005608ValidationJuly 1 – November 21, 2005139
# Model 1: Naïve Forecast

Uses the last observed value as the forecast for all future periods.
Serves as a baseline benchmark.

# Model 2: Linear Regression (TSLM)

Includes a trend component and day-of-week dummy variables to capture weekly seasonality.
Formula: Number.of.vehicles ~ trend() + season("week")


# Results
Accuracy Metrics (Validation Period)
ModelMERMSEMAEMAPEMASEACF1Naïve-12,733.5116,820.6213,605.5313.15%2.7850.376Linear Regression-1,603.495,869.163,899.743.70%0.7980.622
Manual MASE
ModelMASENaïve1.444Linear Regression0.414 ✅

A MASE < 1 means the model outperforms the Naïve benchmark.


# Diagnostic Analysis
DiagnosticNaïve ModelLinear RegressionResidual patternClear weekly cyclical patternMostly random, no clear trendHistogramRoughly centered at zeroRoughly centered at zeroACF of errorsSignificant spikes at lags 7, 14, 21Few significant spikes — near white noiseBias (ME)-12,733.51 (under-forecasting)-1,603.49 (near unbiased)

# Conclusion
Winner: Linear Regression Model 🏆
The Linear Regression model outperforms the Naïve forecast because it:

Achieves lower RMSE, MAE, and MAPE
Has a MASE of 0.414 (beats the Naïve benchmark)
Captures the weekly seasonal pattern via day-of-week variables
Produces more random residuals with less autocorrelation

# Limitations & Future Improvements

Holiday effects are not modeled — adding holiday indicators could improve accuracy
Annual seasonality may exist but requires more years of data to detect
Advanced models (ARIMA, exponential smoothing, ML) could reduce remaining error
External variables (weather, fuel prices, economic indicators) might explain residual variation


# Tools & Libraries

Language: R
Key Package: fpp3 (Forecasting: Principles and Practice)
Functions used: NAIVE(), TSLM(), accuracy(), gg_tsresiduals(), autoplot()


References

Hyndman, R.J. & Athanasopoulos, G. (2021). Forecasting: Principles and Practice, 3rd ed. https://otexts.com/fpp3/
