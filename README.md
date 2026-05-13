# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 02/05/2026

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load dataset
data = pd.read_excel('/content/Hyderabad-AirQ.xlsx')

# Convert Date column
data['Date'] = pd.to_datetime(data['Date'])

# Set Date as index
data.set_index('Date', inplace=True)

# Select PM2.5 column
data.rename(columns={'PM2.5': 'Air_Quality'}, inplace=True)

# 1. Original Data
plt.figure(figsize=(12,6))
plt.plot(data['Air_Quality'])
plt.title('Original Time Series')
plt.xlabel('Date')
plt.ylabel('PM2.5')
plt.grid(True)
plt.show()

# 2. Log Transformation
data['Air_Quality_Log'] = np.log(data['Air_Quality'])

plt.figure(figsize=(12,6))
plt.plot(data['Air_Quality_Log'])
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log(PM2.5)')
plt.grid(True)
plt.show()

# 3. Regular Differencing
data['Air_Quality_Diff'] = data['Air_Quality'].diff(1)

plt.figure(figsize=(12,6))
plt.plot(data['Air_Quality_Diff'])
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Difference')
plt.grid(True)
plt.show()

# 4. Seasonal Adjustments
data['Air_Quality_Seasonal_Diff'] = data['Air_Quality'].diff(7)

plt.figure(figsize=(12,6))
plt.plot(data['Air_Quality_Seasonal_Diff'])
plt.title('Seasonal Adjustments')
plt.xlabel('Date')
plt.ylabel('Seasonal Difference')
plt.grid(True)
plt.show()

# 5. Combined Transformations
data['Air_Quality_Log_Diff_Seasonal'] = (
    data['Air_Quality_Log'].diff(1).diff(7)
)

plt.figure(figsize=(12,6))
plt.plot(data['Air_Quality_Log_Diff_Seasonal'])
plt.title('LOG, REGULAR, AND SEASONAL DIFFERENCING')
plt.xlabel('Date')
plt.ylabel('Transformed Values')
plt.grid(True)
plt.show()

# Seasonal Decomposition
if len(data['Air_Quality'].dropna()) >= 14:

    decomposition = seasonal_decompose(
        data['Air_Quality'],
        model='additive',
        period=7
    )

    decomposition.plot()

    plt.suptitle('Seasonal Decomposition', y=1.02)

    plt.tight_layout()

    plt.show()

else:
    print("Not enough data for seasonal decomposition")
```

### OUTPUT:
<img width="1001" height="547" alt="image" src="https://github.com/user-attachments/assets/05e7c02e-8011-4579-bb9c-e71a8c6b996c" />

<img width="1005" height="547" alt="image" src="https://github.com/user-attachments/assets/80f45994-4925-4134-a981-8091bab920b1" />

REGULAR DIFFERENCING:
<img width="1008" height="547" alt="image" src="https://github.com/user-attachments/assets/45356738-e3c9-4569-b622-dce9f8183c83" />


SEASONAL ADJUSTMENT:
<img width="1017" height="547" alt="image" src="https://github.com/user-attachments/assets/f0415ff1-4e5d-41c3-9e90-8e03c6885924" />


LOG TRANSFORMATION:
<img width="1021" height="547" alt="image" src="https://github.com/user-attachments/assets/7ebe9a3a-efad-4c7a-8ce9-05ffb96eb080" />
<img width="629" height="494" alt="image" src="https://github.com/user-attachments/assets/635c612d-9c9e-4b09-91bb-f30b68df351a" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
