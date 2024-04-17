---
layout: page

title: stock price prediction using RNNs

description: building a simple online app for direct forecasting of stock prices using recurrent neural networks (RNNs)

img: 

importance: 5

category: work
---

Objective: Predict stock price for the next N days into the future.

<h4>Ingredients Used</h4>
1. 
2. AlphaVantage API
3. ML libraries (tensorflow, sklearn, etc.)
<br>

<img src="/assets/img/rnn.jpeg" width="500" height="250">

We will be using an RNN to predict stock prices based on the past 60 days of stock price data. Note that weights and biases are going to be the same for each iteration unit of the RNN. 
However, when training on long-range dependencies, RNNs can suffer from the exploding/vanishing gradients problem. Exploding gradients cause extremely large learning steps during backprop so it would bounce around alot.
Conversely, vanishing gradients cause extremely tiny steps before it finds the optimal parameters. Therefore, we will be using an LSTM, which can prevent these problems by a modification to the hidden layer that enables RNNs to remember
inputs over a longer time period. An LSTM uses tanh and sigmoid activation functions. <br>
- Sigmoid: $$f(x) = \frac{e^x}{e^x+1} \rightarrow (0,1)$$
- Tanh: $$f(x) = \frac{e^x - e^-x}{e^x - e^-x} \rightarrow (-1,1)$$ <br>








To summarize, there are 5 components of an LSTM:

1. Cell state: internal memory of the cell storing both STM and LTM
2. Hidden state: the output wrt to current input, current state, and previous hidden state
3. Input gate: weight of current input on current state
4. Forget gate: weight of previous state on current state
5. Output gate: weight of current state output into hidden state
<br><br>

<h6>1. Data Preprocessing</h6>
First, we drop any rows with missing values. Then, we apply log transform to the prices because it can better capture relative percentage changes in prices. 
For instance, a stock going from 10$ to 20$ should not be weighed the same as a stock going from 100$ to 110$ (weber's law!). Then we normalize our data so that
the range of values fall between 0 and 1. 

```python
def preprocess(ticker):
    url = f"https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol={ticker}&outputsize=full&apikey=Y8ZR7HEZ95DQQ9QH"
    r = requests.get(url)
    d = r.json()
    d1 = d['Time Series (Daily)']
    sorted_data = sorted(d1.items()) #ascending order
    data = []

    for index, (date, values) in enumerate(sorted_data):
        close = float(values['4. close'])
        if close == 0:
            continue
        data.append(close)

    data = np.log(np.array(data) + 1)
    scaled = [ ((i - min(data)) / (max(data) - min(data))) for i in data ]
    
    return scaled

```

Now, we should split 







