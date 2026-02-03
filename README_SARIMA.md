### **Understanding the SARIMA Model**

In my journey to master time series forecasting, I found that standard ARIMA models often fall short when dealing with data that has repeating cycles—like holiday sales spikes or temperature changes. That is why I implemented **SARIMA** (Seasonal AutoRegressive Integrated Moving Average).

Here is how I break down the acronym to understand the mechanics:



* **S (Seasonal):** This is the "secret sauce." It looks at the relationship between the current observation and observations from previous seasonal cycles (e.g., this January vs. last January).
* **AR (AutoRegressive):** The model uses the dependent relationship between an observation and some number of lagged observations.
* **I (Integrated):** To make the time series stationary (constant mean and variance), I use differencing (subtracting an observation from an observation at the previous time step).
* **MA (Moving Average):** This component focuses on the relationship between an observation and a residual error from a moving average model applied to lagged observations.


#### **The Hyperparameters**

In the code above, you will see two sets of parameters:



1. **Order $(p, d, q)$:** These handle the standard, non-seasonal trends.
2. **Seasonal Order $(P, D, Q, s)$:** These handle the cyclical patterns. Note the **$s$**, which I set to 12 because my data is monthly.


---


### **How My Code Works**

Here is a walkthrough of the logic I used in the script above:


#### **1. Data Preprocessing & Visualization**

Before feeding any data into a model, I always visualize it first.

I used seasonal_decompose to break my time series into three clear parts:



* **Trend:** Is the data generally going up or down?
* **Seasonality:** Is there a repeating pattern?
* **Residual:** What is left over (random noise)?


#### **2. Stationarity and Parameter Selection**

SARIMA requires the data to be stationary. I used differencing (the d parameter) to stabilize the trend. To select the p and q parameters, I inspected the **ACF (AutoCorrelation Function)** and **PACF (Partial AutoCorrelation Function)** plots.

<img width="3999" height="2999" alt="image" src="https://github.com/user-attachments/assets/a097e61f-e595-48ae-8f82-c0ab377d86e6" />

* **ACF:** Helps me estimate the Moving Average (MA) term ($q$).
* **PACF:** Helps me estimate the AutoRegressive (AR) term ($p$).


#### **3. Model Fitting**

I used the statsmodels library, which is the industry standard for statistical modeling in Python. I defined the model with order=(1,1,1) and seasonal_order=(1,1,1,12).



* *Note:* In a production environment, I would likely use a grid search or pmdarima to automatically find the optimal parameters that minimize the AIC (Akaike Information Criterion).


#### **4. Evaluation**

Finally, I visualized the forecast against the actual test data. The **RMSE (Root Mean Squared Error)** gives me a single number to judge how far off my predictions were on average. I also plotted the **confidence intervals** (the pink shaded area) to show the uncertainty range of my predictions—essentially saying, "I'm 95% sure the real value will fall within this pink 
