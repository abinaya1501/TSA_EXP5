# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date:10.05.26 


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```

import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
import warnings

warnings.filterwarnings("ignore")

# Load dataset
data = pd.read_csv('Video_Games_Sales.csv')

# Clean column names
data.columns = data.columns.str.strip()

# Convert year column
data['Year_of_Release'] = pd.to_datetime(
    data['Year_of_Release'],
    format='%Y',
    errors='coerce'
)

# Remove missing values
data = data.dropna(subset=['Year_of_Release', 'Global_Sales'])

# Set index
data.set_index('Year_of_Release', inplace=True)

# Aggregate yearly sales
data = data.groupby(data.index)['Global_Sales'].sum()

# Convert into dataframe
data = pd.DataFrame(data)

# Remove missing values
data = data.dropna()

# Seasonal decomposition
decomposition = seasonal_decompose(
    data['Global_Sales'],
    model='additive',
    period=2
)

# Plot graphs
plt.figure(figsize=(10, 12))

# Original
plt.subplot(411)
plt.plot(data['Global_Sales'], label='Global Sales')
plt.legend(loc='upper left')
plt.title('Global Video Game Sales')

# Trend
plt.subplot(412)
plt.plot(decomposition.trend, label='Trend', color='orange')
plt.legend(loc='upper left')
plt.title('Trend Plot')

# Seasonal
plt.subplot(413)
plt.plot(decomposition.seasonal, label='Seasonal', color='green')
plt.legend(loc='upper left')
plt.title('Seasonality Plot')

# Residual
plt.subplot(414)
plt.plot(decomposition.resid, label='Residual', color='red')
plt.legend(loc='upper left')
plt.title('Residual Plot')

plt.tight_layout()
plt.show()

```
### OUTPUT:

<img width="868" height="1019" alt="image" src="https://github.com/user-attachments/assets/6ec1c09a-e329-4374-9169-f17afe46f717" />

### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
