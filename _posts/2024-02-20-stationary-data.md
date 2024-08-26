---
navigation: true
cover: assets/images/AutoCorr/stationary.png
title: What is Stationary Data & Unit Root Tests
date: 2024-02-20
class: post-template
tags: arima
layout: post
current: post
subclass: 'post'
---

To prepare for the next lesson, I wanted to provide a quick lesson explaining what stationary data is.

## What is Stationarity

By textbook definition, a stationary time series (a dataset which is a function of time) is one that contains properties which are **not** dependent on when the dataset is observed. In other words,  a stationary time series is a dataset that only contains periodic, or repeating, (cyclic) properties that won't affect the value at t. For example, time series which contain trends or have 'seasons' are not stationary because these properties will be affected depending on when you observe the graph. Contrary, a time series which is stationary would be white noise because it should look about the same, independent of when you observe the graph. To summarize, stationary time series will have no predictable patterns over time and it should have constant variance. 

### Differencing

One quick and easy way to convert a stationary time series to a non stationary one is by taking the difference between consecutive values; this is known as **differencing**.

To give an example, here is the data I will be using:
```python
  #installations
!pip install skforecast

# Data manipulation
# ==============================================================================
import numpy as np
import pandas as pd

from skforecast.datasets import fetch_dataset

# Plots
# ==============================================================================
import matplotlib.pyplot as plt
plt.style.use('fivethirtyeight')
plt.rcParams['lines.linewidth'] = 1.5
plt.rcParams['font.size'] = 10

# Data download
# ==============================================================================
data = fetch_dataset(name='h2o_exog', raw=True) #this dataset is on australian health system, from 1991 to 2008. This is from Hyndman (2023) fpp3
#Monthly expenditure ($AUD) on corticosteroid drugs that the Australian health system had between 1991 and 2008. Two additional variables (exog_1, exog_2) are simulated.

# Data preparation
# ==============================================================================
data = data.rename(columns={'fecha': 'date'})
data['date'] = pd.to_datetime(data['date'], format='%Y-%m-%d')
data = data.set_index('date')
data = data.asfreq('MS')
data = data.sort_index()
#data.head()

data = data.y

data.head()

```

This is a function that returns the differenced data, and as you can see, the new dataset will have a length of n-1 (as you can't difference the first element in the dataset). 
```python
def difference_data(data):
  new_data = data.copy()
  for i in range(1, len(data)):
    new_data.iloc[i] = data.iloc[i]-data.iloc[i-1]
  return new_data
```
This is called differencing with an order of 1, because we take the difference between t and t-1.

#### Seasonal Differencing
But you can also difference data which contains seasons, by differencing with order greater than 1:
```python
def seasonal_difference(data, seasons):
  new_data = data.copy()
  for i in range(len(data)):
    if (i >= seasons):
      new_data.iloc[i] = data.iloc[i] - data.iloc[i-seasons]
  return new_data

seasonal_dif_data = seasonal_difference(data, 12)
seasonal_dif_data.plot()
```
Here the differencing happens between observations across seasons. So for example, if we had a montly dataset, you would difference observations across all Januaries, across all Marches, etc. 
$$
  y_t` = y_t - y_{t-m}
$$
where m is the number of seasons (for the montly example above, m = 12). This is called lag-m differencing. 

If you run the above code, you should get something like this:
![img](assets/images/AutoCorr/stationary.png)


#### Second-order differencing
This is usefull when the data still seems stationary after first-order differencing. 
$$
  y_t`` = y_t` - y_t`
  y_t`` = (y_t - y_{t-1}) - (y_{t-1} - y_{t-2})
        = y_t - 2*y_{t-1} + y_{t-2}
$$
In this case, the output dataset will have a length of t-2, as you cannot take the difference of the first 2 values. 


#### Transformations

As you probably got introduced to in the prior lessons, you can also apply transformations. For example, transforming the dataset with logorithms can help stabailize the variance. 

```python
def bickel_doksum_transform(data, lam):
  new_data = data.copy()
  if (lam == 0):
    for i in range(len(data)):
      new_data.iloc[i] = np.log(data.iloc[i])
  else:
    for i in range(len(data)):
      new_data.iloc[i] = (get_sign(data.iloc[i])*(pow(abs(data.iloc[i]), lam)-1))/lam
  return new_data
  ```
  But for more information on this, please refer to the previous lessons. 



To summarize:
  - Stationary data is when the time series contains properties which are **not** dependent on when the dataset is observed.
  - You can make your own non-stationary by differencing
  - You can fix the variance via transformations
