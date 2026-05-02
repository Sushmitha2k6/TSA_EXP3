# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 02-05-2026

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



import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load CSV
df = pd.read_csv('/content/amazon_sales_dataset.csv')

# Clean column names
df.columns = df.columns.str.strip().str.lower()

# Convert date
df['order_date'] = pd.to_datetime(df['order_date'])

# 🔥 Combine same dates (very important)
df = df.groupby('order_date')['total_revenue'].sum().to_frame()

# Sort by date
df = df.sort_index()

# Use revenue column
data = df['total_revenue'].values

# Number of lags (adjust if needed)
lags = range(30)

autocorr_values = []

# Mean and variance
mean_data = np.mean(data)
variance_data = np.var(data)
N = len(data)

# Calculate autocorrelation
for lag in lags:
    
    if lag == 0:
        autocorr_values.append(1)
        
    else:
        auto_cov = np.sum(
            (data[:-lag] - mean_data) *
            (data[lag:] - mean_data)
        ) / N
        
        autocorr = auto_cov / variance_data
        
        autocorr_values.append(autocorr)

# Plot
plt.figure(figsize=(10,6))
plt.stem(lags, autocorr_values)

plt.axhline(y=0, linestyle='--')

plt.title('Autocorrelation of Amazon Sales')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')

plt.grid(True)
plt.show()
```
### OUTPUT:
<img width="899" height="577" alt="image" src="https://github.com/user-attachments/assets/e300bf11-cd71-44e5-ba61-6aedc6047556" />

### RESULT:
        Thus we have successfully implemented the auto correlation function in python.
