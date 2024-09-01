---
navigation: true
cover: assets/images/AutoCorr/ACmain.png
title: Part 2 - How do ARIMA Models Work? 
date: 2024-03-02
class: post-template
tags: arima
layout: post
current: post
subclass: 'post'
---

Here, we will build off the last lesson and properly implement an Autoregressive, Integrated, Moving Average Model. 


As usual, I will be using the same data as in the previous lesson. 

The fundamental change this time, is that we will have [NumPy](https://numpy.org/), an open-source numerical computation Python tool, handle all of these
multiplications for us. 

I believe that when running this algorithm, the problem would occur:
$$
  \frac{\partial \text{MSE}}{\partial b_i} = \frac{2}{n} \cdot \sum_{i=p}^n x_{t-i} \cdot (x_{t-p}\cdot b_{t-p} +\ldots +x_{t-i}\cdot b_{t-i} - y_t)
$$

Previously, we relied solely on Python arithmetic for this, but there is also an laternative method: **The Dot Product!**

$$
  \beta = (X^T \cdot X)^{-1} \cdot X^T \cdot y
$$

The above is a super simplified version of something called the [Moore-Penrose Inverse](https://en.wikipedia.org/wiki/Moore%E2%80%93Penrose_inverse). It is somewhat technical, so I decided to keep that out of this lesson.


### The Code

To keep this simple, I will first show you the new code:
```python
import math
def prepare_data(data, order):
  X, y = [], []
  for i in range(order, len(data)):
    X.append(data.iloc[i - order:i])
    y.append(data.iloc[i])
  return np.array(X), np.array(y)
def prepare_data_errors(data, order):
  X, y = [], []
  for i in range(order, len(data)):
    X.append(data.errors.iloc[i - order:i])
    y.append(data.y.iloc[i])
  return np.array(X), np.array(y)
def autoregressive_model (data, learning_rate, epoch, order, cost):
  #prepare data
  X, y = prepare_data(data, order)
  #weights = np.random.randn(order)
  weights = [0 for _ in range(order)]
  bias = 0

  for _ in range(epoch):
    predictions = np.dot(X, weights)
    error = predictions - y

    if cost == 'mse':
      gradient_weights = 2 * np.dot(X.T, error) / len(X)
      gradient_bias = 2 * np.sum(error) / len(X)
    elif cost == 'mae':
      #print(error/np.abs(error))
      gradient_weights = np.dot(X.T, error/np.abs(error)) / len(X)
      gradient_bias = np.sum(error/np.abs(error)) / len(X)
    elif cost == 'rmse':
      gradient_weights = (2 * np.dot(X.T, error) / len(X)) / 2 / np.sqrt(np.sum(np.square(error))/len(X))
      #gradient_bias = np.sum(error) / len(X) / np.sqrt(sum(error))
      gradient_bias = np.sum(error) / len(X) / np.sqrt(np.sum(np.square(error))/len(X))



    weights -= learning_rate * gradient_weights
    #bias -= learning_rate * gradient_bias

  return weights, bias
```
As you can see, it looks pretty similar to the previous function. However, each arithmetic operation (like calculating the error or running the gradient descent algorithm, is handled with NumPy):
```python
for _ in range(epoch):
  predictions = np.dot(X, weights)
  error = predictions - y
```

#### The Dot Product, Simplified 
If you don't know how a dot product works, please review this resource [here](https://www.mathsisfun.com/algebra/vectors-dot-product.html).

But if I were to explain it in simple terms, I would say that it is a method to finding the product of two vectors in space. When I say that, you might think to multiply their lengths, but this is false as it doesn't account for vectors that face different directions. Thus, there is a super simple method (which I will not explain right now; if you want, please view the source above) that looks like this for taking the dot product:

$$
let \vec{b} = \begin{bmatrix}b_1 \\ b_2 \\ \vdots \\ b_i\end{bmatrix}
$$

and 
$$
let \vec{X} = \begin{bmatrix}x_1 \\ x_2 \\ \vdots \\ x_i\end{bmatrix}
$$

Then, their dot product will be:
$$
  \vec{b} \cdot \vec{X} = (b_1 \cdot x_1 + b_2 \cdot x_2 + \ldots + b_i \cdot x_i)
$$

And you might be able to see, that this is actually the same operation we do when we calculate our error in the autoregressive function:
$$
  (x_{t-p}\cdot b_{t-p} +\ldots +x_{t-i}\cdot b_{t-i})
$$












### Cost Functions

There are many different cost functions out there, and each one can either help or hinder different models. In this lesson, we will show three main and common cost functions
_Mean Squared Error_(MSE), _Mean Absolute Error_(MAE), and _Root Mean Squared Error_(RMSE). 
