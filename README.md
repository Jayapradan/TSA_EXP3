# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# Load the Melbourne dataset
data = pd.read_csv("/kaggle/input/time-series-melbourn/daily-minimum-temperatures-in-me.csv", on_bad_lines='skip')
data.columns = ["Date", "Temp"]
data["Date"] = pd.to_datetime(data["Date"])
data["Temp"] = pd.to_numeric(data["Temp"], errors='coerce')
data = data.dropna()

# Use only temperature values
time_series_data = data["Temp"].values

# Length
N = len(time_series_data)

# Lags (0–34)
lags = range(min(35, N // 2))

# Empty list
autocorr_values = []

# Mean & Variance
mean_data = np.mean(time_series_data)
variance_data = np.var(time_series_data)

# Calculate ACF manually
for lag in lags:
    if lag == 0:
        autocorr_values.append(1)  # ACF at lag 0 is 1
    else:
        auto_cov = np.sum((time_series_data[:-lag] - mean_data) *
                          (time_series_data[lag:] - mean_data)) / N
        autocorr_values.append(auto_cov / variance_data)

# Plot ACF
plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)   # FIXED (removed use_line_collection)
plt.title('Autocorrelation Function (ACF) - Melbourne Temperature')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')
plt.grid(True)
plt.show()
```
### OUTPUT:
<img width="915" height="525" alt="image" src="https://github.com/user-attachments/assets/27c764a4-6896-4c19-932e-7eb856cf321a" />


### RESULT:
        Thus we have successfully implemented the auto correlation function in python.
