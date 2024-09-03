# Ex.No: 1B   CONVERSION OF NON STATIONARY TO STATIONARY DATA
### NAME :RAGUNATH R
### REGISTER NO:212222240081
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on electric production dataset.
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.

### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
%matplotlib inline

# Load the dataset
train = pd.read_csv("/content/daily-minimum-temperatures-in-me.csv")

# Convert the 'Date' column to datetime format
train['Date'] = pd.to_datetime(train['Date'], format='%m/%d/%Y')

# Set the 'Date' column as the index
train.set_index('Date', inplace=True)

# Convert the 'Daily minimum temperatures' column to numeric, forcing errors to NaN
train['Daily minimum temperatures'] = pd.to_numeric(train['Daily minimum temperatures'], errors='coerce')

# Drop any rows with NaN values that may have resulted from the conversion
train = train.dropna()

# Plot the time series data for 'Daily minimum temperatures'
train['Daily minimum temperatures'].plot(title='Daily Minimum Temperatures')

# Define the function to perform the Augmented Dickey-Fuller test
def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)

# Perform the ADF test on the 'Daily minimum temperatures' data
adf_test(train['Daily minimum temperatures'])

```

### Regular Differencing:
```
train['Temp_diff'] = train['Daily minimum temperatures'] - train['Daily minimum temperatures'].shift(1)
train['Temp_diff'].dropna().plot(title='Differenced Daily Minimum Temperatures')

```

### Seasonal adjustment:
```
n = 7 
train['Temp_seasonal_diff'] = train['Daily minimum temperatures'] - train['Daily minimum temperatures'].shift(n)
train['Temp_seasonal_diff'].dropna().plot(title='Seasonally Differenced Daily Minimum Temperatures')

```
### Log transformation
```
train['Temp_log'] = np.log(train['Daily minimum temperatures'])
train['Temp_log_diff'] = train['Temp_log'] - train['Temp_log'].shift(1)
train['Temp_log_diff'].dropna().plot(title='Log Differenced Daily Minimum Temperatures')

```


### OUTPUT:

![image](https://github.com/user-attachments/assets/dea717cd-5479-4ceb-96e6-bf550c1bc9fc)


REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/4e5d376d-3249-4844-b02a-3ee45c21e0f0)



SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/8e76aaac-1b82-45e3-ab77-23dc262b31e0)


LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/ce0de3b9-43a4-4491-ba35-04f0b76f5b31)



### RESULT:
Thus The python code has been created for the conversion of non stationary to stationary data on electric production dataset.


