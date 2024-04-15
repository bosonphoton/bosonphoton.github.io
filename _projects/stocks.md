---
layout: page

title: stock price prediction using RNNs

description: building a simple online app for direct forecasting of stock prices using recurrent neural networks (RNNs)

img: 

importance: 5

category: work
---

<h4>Ingredients Used</h4>
1. Flask
2. AlphaVantage API
3. ML libraries (tensorflow, sklearn, etc.)
<br>

<img src="/assets/img/rnn.jpeg" width="500" height="250">

We will be using an RNN to predict stock prices based on the past 60 days of stock price data.
However, when training on long-range dependencies, RNNs suffer from the vanishing gradients problem.
Therefore, we will be using an LSTM, which is a modification to the RNN hidden layer that enables RNNs to remember
inputs over a longer time period. There are 5 components of an LSTM:

1. Cell state: internal memory of the cell storing both STM and LTM
2. Hidden state: the output wrt to current input, current state, and previous hidden state
3. Input gate: weight of current input on current state
4. Forget gate: weight of previous state on current state
5. Output gate: weight of current state output into hidden state

We want to predict a stock price N days into the future. So we want t o


<b>Data Cleaning & Preprocessing</b>




