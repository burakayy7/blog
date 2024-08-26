---
navigation: true
cover: assets/images/AutoCorr/ACmain.png
title: Using Scikit & SKtime for Forecasting 
date: 2024-02-24
class: post-template
tags: arima
layout: post
current: post
subclass: 'post'
---

Before we take a deep dive into how ARIMA models work, I wanted to show you some alternatives, mainly using Python ML libraries to do the prediction/forecasting.

In this lesson, we will be using two main libraries: SKforecast (SciKit) and SKtime.

The first library is SciKit:
#### Using SciKit SKforecast library
SKforecast is an open-source Python Library that implements time series forecasting using ML models; it is compatible with many other ML/DP based techniques like Keras.

If you're running this in colab:
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

# Modeling and Forecasting
# ==============================================================================
from sklearn.linear_model import Ridge
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_squared_error
from sklearn.metrics import mean_absolute_error
from sklearn.preprocessing import StandardScaler

from skforecast.ForecasterAutoreg import ForecasterAutoreg
from skforecast.ForecasterAutoregCustom import ForecasterAutoregCustom
from skforecast.ForecasterAutoregDirect import ForecasterAutoregDirect
from skforecast.model_selection import grid_search_forecaster
from skforecast.model_selection import backtesting_forecaster
from skforecast.utils import save_forecaster
from skforecast.utils import load_forecaster

# Warnings configuration
# ==============================================================================
import warnings
warnings.filterwarnings('once')

# Data download
# ==============================================================================
data = fetch_dataset(name='h2o_exog', raw=True) #this dataset is on australian health system, from 1991 to 2008. This is from Hyndman (2023) fpp3
#Monthly expenditure ($AUD) on corticosteroid drugs that the Australian health system had between 1991 and 2008. Two additional variables (exog_1, exog_2) are simulated.
```
The above code will install the library and import anything we need to run inference. 
```python
data.plot()
```
here is how that plot should look like:
![img](assets/images/AutoCorr/data1.png)

For use to work with this data, we first need it to be in the format that we can work with (for example, converting fecha to date).
```python
# Data preparation
# ==============================================================================
data = data.rename(columns={'fecha': 'date'})
data['date'] = pd.to_datetime(data['date'], format='%Y-%m-%d')
data = data.set_index('date')
data = data.asfreq('MS')
data = data.sort_index()
data.head()
data.plot()
# Missing values
# ==============================================================================
print(f'Number of rows with missing values: {data.isnull().any(axis=1).mean()}')

# Verify that a temporary index is complete
# ==============================================================================
(data.index == pd.date_range(start=data.index.min(),
                             end=data.index.max(),
                             freq=data.index.freq)).all()
```

Okay, now for the fun part. To train our model, we first need to split our dataset into training and testing. We do this so that we can validate that our model performes well on new data (the testing set); because if we didn't do this, then we would have no way of knowing if our model actually learned or if it memorized the training set. 
```python
# Split data into train-test
# ==============================================================================
steps = 36
data_train = data[:-steps]
data_test  = data[-steps:]

print(f"Train dates : {data_train.index.min()} --- {data_train.index.max()}  (n={len(data_train)})")
print(f"Test dates  : {data_test.index.min()} --- {data_test.index.max()}  (n={len(data_test)})")

fig, ax = plt.subplots(figsize=(6, 2.5))
data_train['y'].plot(ax=ax, label='train')
data_test['y'].plot(ax=ax, label='test')
ax.legend();
```
![img](assets/images/AutoCorr/data2.png)

For our model, we will be implementing a RandomForestRegressor:
```python
# Create and train forecaster
# ==============================================================================
# this model uses the random forest regressor: https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html
# and this implements decision trees
# the lag time of 6 means the model will be trained off previous 6 months (forecast horizon)
#
# ==============================================================================
forecaster = ForecasterAutoreg(
                 regressor = RandomForestRegressor(random_state=123),
                 lags = 6)

forecaster.fit(y=data_train['y'])
forecaster
```


The second library I wanted to share is SKtime:
#### Using SKtime library
The Sktime library is another open-source Python Library used for implementing AI/ML models for forecasting, validation, training, etc. for time series data.

```python

```