# **Project Overview: ARMA Model for Time Series Forecasting**

In this project, I explored the use of AutoRegressive Moving Average (ARMA) models to analyze and forecast time series data. My goal was to build a statistical model that captures the temporal dependencies in a dataset without requiring the differencing steps seen in ARIMA.

## **What is an ARMA Model?**

I chose the ARMA model because it combines two fundamental components of time series analysis:

1. **AutoRegressive (AR)**: This part implies that the current value is correlated with its own previous values. It assumes that what happened yesterday impacts what happens today.
2. **Moving Average (MA)**: This part models the error of the observation as a linear combination of error terms occurring contemporaneously and at various times in the past. It accounts for "shocks" in the system.

Mathematically, I define the ARMA($p, q$) model as:

**$$X_t = c + \epsilon_t + \sum_{i=1}^p \phi_i X_{t-i} + \sum_{j=1}^q \theta_j \epsilon_{t-j}$$**

**Where:**
- $X_t$ is the time series value at time $t$.
- $\phi_i$ are the AR coefficients (lag $p$).
- $\theta_j$ are the MA coefficients (lag $q$).
- $\epsilon_t$ is the white noise (error term).

## **How My Code Works**

1. **Data Generation**: Since I wanted to test the model in a controlled environment, I first wrote a script to generate synthetic data. I manually constructed a time series with known parameters ($\phi$ and $\theta$) so I could later verify if the model estimated them correctly.
2. **Model Fitting**: I utilized the statsmodels library. specifically the ARIMA class. Although statsmodels has deprecated the standalone ARMA class, I achieved the same result by setting the integration/differencing order ($d$) to 0.
3. **Forecasting**: I projected the model 20 steps into the future. I included confidence intervals in my visualization because it is crucial to communicate the uncertainty inherent in statistical predictions.
4. **Diagnostics**: I plotted the ACF (AutoCorrelation Function) and PACF (Partial AutoCorrelation Function) of the residuals. In my final check, I looked for residuals that resembled white noise—indicating that my model had successfully captured the signal in the data.

