---
layout: page

title: stock price prediction using RNNs

description: building a simple web app for direct forecasting of stock prices using recurrent neural networks (RNNs)

img: 

importance: 5

category: work
---

Objective: Predict stock price for the next N days into the future.

<h4>Ingredients</h4>
1. Flask, 
2. AlphaVantage API
3. ML libraries (tensorflow, sklearn, etc.)
<br>

<img src="/assets/img/rnn.jpeg" width="500" height="250">

I'll be using an RNN to predict stock prices based on the past 60 days of stock price data. Note that weights and biases are going to be the same for each iteration unit of the RNN. 
However, when training on long-range dependencies, RNNs can suffer from the exploding/vanishing gradients problem. Exploding gradients cause extremely large learning steps during backprop so it would bounce around alot.
Conversely, vanishing gradients cause extremely tiny steps before it finds the optimal parameters. Therefore, I'll be using an LSTM, which can prevent these problems by a modification to the hidden layer that enables RNNs to remember
inputs over a longer time period. <br>

To summarize, there are 5 components of an LSTM:
1. Cell state: internal memory of the cell storing both STM and LTM
2. Hidden state: the output wrt to current input, current state, and previous hidden state
3. Input gate: weight of current input on current state
4. Forget gate: weight of previous state on current state
5. Output gate: weight of current state output into hidden state
<br><br>

An LSTM uses tanh and sigmoid activation functions. <br>
- Sigmoid: $$f(x) = \frac{e^x}{e^x+1} \rightarrow (0,1)$$
- Tanh: $$f(x) = \frac{e^x - e^-x}{e^x - e^-x} \rightarrow (-1,1)$$ <br>

Sigmoid is used in the in, out, and forget gate, which removes info by squashing values to 0, and keeping info with 1. Tanh is used to update the cell state and output the hidden state, creating candidate values between -1 and 1 that scale and normalize values. <br><br>


<h6><b>1. Data Preprocessing</b></h6>
To retrieve the data, I'm using the free AlphaVantage API to get the most recent prices of any stock. First, I'll fill in any missing values with the last known price (note that there are many different approaches to impute for missing data). I'm also applying log transform to the prices because it can better capture relative percentage changes in prices. 
For instance, a stock going from 10$ to 20$ should not be weighed the same as a stock going from 100$ to 110$ (weber's law!). Finally, normalize the data using min max scaling so that the range of values fall between 0 and 1. 

```python
import requests

def preprocess(ticker):
    url = f"https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol={ticker}&outputsize=full&apikey=Y8ZR7HEZ95DQQ9QH"
    r = requests.get(url)
    d = r.json()
    d1 = d['Time Series (Daily)']
    sorted_data = sorted(d1.items()) #ascending order
    last_date = [sorted_data[-1][0]] #retrieves the last date 
    data = []

    for index, (date, values) in enumerate(sorted_data):
        close = float(values['4. close'])
        if close == 0:
            data.append(data[index - 1]) #imputes missing value with last known price
        data.append(close)

    data = np.log(np.array(data) + 1) #log transform
    scaled = [ ((i - min(data)) / (max(data) - min(data))) for i in data ] #min max scaling
    
    return scaled, last_date

```
I want to create sets of 60 day batches to predict the price of next day. 
After doing so, I'll split the data into training and testing to see how to well the model performs, and tweak accordingly.

```python
from sklearn.model_selection import train_test_split

scaled = preprocess(ticker)
X = []
y = []
for i in range(60,len(scaled)):
  X.append(scaled[i-60:i])
  y.append(scaled[i])

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=42)
```
<br>

<h6><b>2. Building the Model</b></h6>
Now, to build the LSTM network. I'll use the most basic architecture, but note there are fancier things you can do (such as adding attention modules, etc).
There's two LSTM layers with 50 nodes each. I'm also adding dropout and batch norm to prevent the data from overfitting.

```python
from keras.models import Sequential
from keras.layers import LSTM, Dense, BatchNormalization, Dropout

model = Sequential()
model.add(LSTM(50, return_sequences=True, input_shape=(np.shape(X_train)[1], 1)))
model.add(LSTM(50))
model.add(Dropout(0.2))
model.add(BatchNormalization())
model.add(Dense(1))
model.compile(loss='mean_squared_error', optimizer='adam')
```
<br>

<h6><b>3. Trainings the Model</b></h6>








