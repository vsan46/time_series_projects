# **Time Series Forecasting with ARIMA**

In this project, I explored Time Series Analysis by building an **ARIMA (AutoRegressive Integrated Moving Average)** model in Python. The goal was to understand how to forecast future data points based on historical trends and to visualize the performance of the model against actual data.


## **What is an ARIMA Model?**


I chose ARIMA because it is one of the most standard and effective statistical models for linear time series forecasting. It combines three distinct components to model data:



1. **AR (AutoRegressive):** This part looks at the relationship between an observation and a number of lagged observations (previous time steps). It assumes that the past values influence the current value.
2. **I (Integrated):** This represents the differencing of raw observations (e.g., subtracting the current value from the previous value). I used this to make the time series **stationary**, which is a requirement for ARIMA.
3. **MA (Moving Average):** This component models the error of the observation as a combination of previous error terms.

Mathematically, the model predicts a value $Y_t$ based on past values and errors:

$$Y_t = c + \phi_1 Y_{t-1} + \dots + \phi_p Y_{t-p} + \theta_1 \epsilon_{t-1} + \dots + \theta_q \epsilon_{t-q} + \epsilon_t$$

Where:



* $p$ is the number of lag observations included in the model.
* $d$ is the number of times that the raw observations are differenced.
* $q$ is the size of the moving average window.


## **How My Code Works**

To implement this, I used the statsmodels library in Python. Here is the breakdown of my workflow:



* **Data Generation:** I created a synthetic dataset representing daily sales. I introduced a linear upward trend and random Gaussian noise to simulate real-world volatility.
* **Stationarity Check:** I utilized the **Augmented Dickey-Fuller (ADF)** test. Since ARIMA requires stationary data (where mean and variance are constant over time), checking the p-value helps determine if differencing ($d$) is required.
* **ACF & PACF Plots:** I plotted the **Autocorrelation Function** and **Partial Autocorrelation Function**. These visual tools helped me estimate the initial parameters for $p$ and $q$.
* **Modeling:** I fitted an ARIMA(1,1,1) model.
    * I set $d=1$ because the data had a clear upward trend (non-stationary).
    * I set $p=1$ and $q=1$ to account for immediate lag effects and moving average errors.
* **Visualizing Predictions:** I plotted the forecast against the actual test data. I also included a **Confidence Interval** (the shaded pink region in the plot) to show the range within which the true values are likely to fall.


## **Results**

The final visualization in the notebook demonstrates that the model successfully captured the upward trend of the data. While the random noise makes perfect prediction impossible, the forecast line tracks the central tendency of the actual test data accurately.


## **Improving Model Fit with Auto-ARIMA**

In the initial version of this project, I manually selected the ARIMA parameters. However, in this updated version, I implemented **Auto-ARIMA** using the pmdarima library to mathematically guarantee a better fit.


### **How I Optimized the Model**

Finding the right "order" $(p, d, q)$ for an ARIMA model is often difficult. If you pick parameters that are too simple, the model underfits (misses the trend). If you pick parameters that are too complex, it overfits (memorizes the noise).

To solve this, my code performs a **Stepwise Grid Search**:



1. **Iterative Search:** The algorithm tries different combinations of $p$ (lag), $d$ (differencing), and $q$ (moving average).
2. **Minimizing AIC:** For each combination, it calculates the **AIC (Akaike Information Criterion)**.
    * $$AIC = 2k - 2\ln(\hat{L})$$
    * The goal is to find the model with the **lowest** AIC. This metric rewards the model for fitting the data well but penalizes it for using too many variables (complexity).


### **Performance Metrics**

To prove the model fits better, I calculated standard error metrics on the test set:



* **RMSE (Root Mean Squared Error):** This tells me the standard deviation of the prediction errors. A lower number means the forecast points are closer to the real line.
* **MAE (Mean Absolute Error):** The average absolute difference between the forecast and the actual values.

By automating the parameter selection, I ensured the model captures the underlying signal of the time series as accurately as possible without human bias.
