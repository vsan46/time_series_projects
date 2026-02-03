# Time Series Projects: A Statistical Modeling Portfolio

Welcome to my repository dedicated to Time Series Analysis. This collection represents my comprehensive journey into understanding how sequential data behaves over time. My objective here is to move beyond simple data visualization and dive deep into statistical forecasting. I have built this compendium to document my implementation of various modeling techniques, ranging from fundamental univariate methods to complex, seasonally adjusted algorithms that account for external variables.

In this project, I utilize Python and Jupyter Notebooks to break down the logic behind each model. Rather than just applying libraries blindly, I focus on the "why" and "how" of model selection—examining how past values, past errors, and seasonal cycles interact to predict future outcomes.

## Project Breakdown & Methodology

My work is organized by specific model architectures. In each directory, I explore the unique strengths and specific use cases for the following techniques:

### 1. The Foundations: AR, MA, and ARMA
I began this analysis by deconstructing time series into its most basic components.

* **[AR_Model](./AR_Model):** In these notebooks, I explore the idea that "history repeats itself." I analyze how a current observation is linearly dependent on its own previous values. This section focuses on identifying significant lags and understanding memory in data.
* **[MA_Model](./MA_Model):** Here, I shift focus from past values to past *errors*. I demonstrate how to model a system that is impacted by random shocks or unexpected events, smoothing out noise to find the signal.
* **[ARMA_Model](./ARMA_Model):** By combining the two approaches above, I create models that account for both momentum (AR) and shock impacts (MA), providing a more robust framework for stationary data.

### 2. Handling Non-Stationarity: ARIMA
Real-world data is rarely stable; it trends upwards or fluctuates wildly.

* **[ARIMA](./ARIMA_Model):** This section documents my work on making data "stationary." I walk through the process of differencing data—removing trends to stabilize the mean and variance—before applying AR and MA components. This is crucial for forecasting metrics like stock prices or economic indicators.

### 3. Complexity and Cycles: SARIMA & SARIMAX
The most advanced part of this repository deals with data that has repeating patterns (seasonality) and external influences.

* **[SARIMA_Model](./SARIMA_Model):** Many datasets, such as retail sales or weather data, have predictable cycles. I implement SARIMA to capture these seasonal repetitions, ensuring that my forecasts respect yearly, quarterly, or weekly patterns.
* **[SARIMAX_model](./SARIMAX_model):** Finally, I expand the forecasting horizon by introducing "exogenous" variables. This model allows me to predict a target variable not just based on its own history, but also based on external factors (for example, predicting electricity demand based on past demand *plus* the current temperature).

## Tools and Technologies

* **Language:** Python
* **Environment:** Jupyter Notebooks
* **Core Libraries:** Pandas for data manipulation, Statsmodels for statistical testing and model generation, and Matplotlib/Seaborn for visualizing residuals and forecasts.

Through these projects, I aim to demonstrate a solid grasp of the statistical underpinnings required for accurate forecasting and data-driven decision-making.
