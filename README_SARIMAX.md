### **What is SARIMAX?**

In this project, I utilized **SARIMAX**, which stands for **Seasonal AutoRegressive Integrated Moving Average with eXogenous regressors**. While standard ARIMA models are great for univariate time series, I needed a model that could handle both **seasonality** (repeating patterns over time) and **external factors** (exogenous variables).

Here is how I break down the acronym to understand the components I'm using:



* **AR (AutoRegressive):** I use past values of the series to predict the future. (e.g., If sales were high last month, they might be high this month).
* **I (Integrated):** I difference the data to make it stationary (removing trends so the statistical properties remain constant).
* **MA (Moving Average):** I use past forecast errors to correct current predictions.
* **S (Seasonal):** This is crucial for my dataset because it repeats a pattern every 12 steps (months). It applies the ARIMA concepts to the seasonal lag.
* **X (eXogenous):** This allows me to feed parallel data into the model. In my code, I generated an "exogenous" variable (like marketing spend or temperature) that influences the target variable. This makes the model more robust than just looking at history alone.


### **How My Code Works**



1. **Data Simulation:** Since I wanted to demonstrate the model's capabilities clearly, I generated a synthetic dataset. I created a sine wave to mimic seasonality and added a linear trend. Crucially, I added an exog variable and multiplied it into the final data, ensuring that the target variable is dependent on this external factor.
2. **Fitting the Model:** I used the statsmodels library. When defining SARIMAX, I specified two sets of orders:
    * order=(1, 1, 1): This handles the immediate trends (non-seasonal).
    * seasonal_order=(1, 1, 1, 12): This tells the model to look at the value from 12 steps ago (last year) to predict the current value.
3. **Diagnostics:** Before trusting the forecast, I ran model_fit.plot_diagnostics(). This generated four plots that helped me verify that my residuals (errors) were normally distributed and resembled white noise. If there were patterns in the errors, it would mean my model missed something.
4. **Forecasting with Exogenous Variables:** When forecasting the future (the test set), I had to provide the exog values for that future period. This is a key limitation/feature of SARIMAX: **to predict $Y$ in the future, you must know (or predict) the value of $X$ in the future.**
5. **Visualization:** Finally, I visualized the results using Matplotlib. I plotted the training data, the actual test data, and my red dashed forecast line. I also included a shaded confidence interval to show the range within which the true value is likely to fall.
