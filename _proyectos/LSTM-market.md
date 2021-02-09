---
title: "LSTM to predict stock market prices"
excerpt: "Using a LSTM to predict the next close price for AAPL"

---

Investing in the stock market turned out to be something interesting. This is probably due to how easy it can be to earn money. However, this comes with a risk. In order to enter this world, a solid strategy is required that helps to foresee the gains, but also to mitigate the losses.

This is why, after a lot of investigation, I propose a LSTM model that will help to predict the next day close price for some ticker. On this case, I use the Apple Ticker (AAPL) for the first proves, but you can try other tickers and share your results. This is the first version of this model, so feel free to explore it, and improve it if necessary.

After this little introduction, let's talk about the model.

## LSTM: Long Short-Term Memory
LSTM is a type of Neural Network (a modified version) and his first objetive is to _remember_ data, that's why is called Long Short-Term memory. The idea is that LSTMs are explicitly designed to avoid the long-term dependency problem. This implementation is very usefull when we are trying to solve some time dependency problems. If you want more information, you can refer to this link http://colah.github.io/posts/2015-08-Understanding-LSTMs/

## Applying LSTM to stock markets.
Now, I want to explain you how to build and LSTM and how this will _predict_ stock prices.

First, import some libraries:

Pandas is for read and obtain the stock market information. The sklearn libreries contains all refers to the LSTM model and preprocessing functions.

```python
import pandas as pd
import datetime
import pandas_datareader.data as web
from pandas import Series, DataFrame
import math
import numpy as np
from sklearn.preprocessing import RobustScaler, MinMaxScaler
import matplotlib.pyplot as plt

# Neural Network library
from keras.models import Sequential
from keras.layers import LSTM, Dense, Dropout
from keras.optimizers import RMSprop
import math
import tensorflow as tf
from tensorflow.python.framework import ops
```

After importing the necessary libraries, is time to read the informations for the ticker. I used DataReader, but there is a library from Yahoo Finance that give the same information.

```python
start = datetime.datetime(2012, 1, 1)
end = datetime.datetime(2021, 1, 5)

df = web.DataReader("AAPL", 'yahoo', start, end)
df.tail()
#creating dataframe
data = df.sort_index(ascending=True, axis=0)
new_data = pd.DataFrame(index=range(0,len(df)),columns=['Date', 'Close'])
```

I dropped the irrelevant information and used only the Close price

```python
new_data = df.drop(['High','Low','Open','Volume','Adj Close'],axis=1)
```

The most important steps are __how to create the train and test dataset and create the model.__ For the first step I use this functions:

```python
def create_dataset(new_data):
    #creating train and test sets
    dataset = new_data.values

    train = dataset[0:987,:]
    valid = dataset[987:,:]

    #converting dataset into x_train and y_train
    scaler = MinMaxScaler(feature_range=(0, 1))
    scaled_data = scaler.fit_transform(dataset)

    x_train, y_train = [], []
    for i in range(60,len(train)):
        x_train.append(scaled_data[i-60:i,0])
        y_train.append(scaled_data[i,0])
    x_train, y_train = np.array(x_train), np.array(y_train)

    x_train = np.reshape(x_train, (x_train.shape[0],x_train.shape[1],1))
    return x_train,y_train,valid,scaler

def create_predict_data(new_data):
    #predicting 246 values, using past 60 from the train data
    inputs = new_data[len(new_data) - len(valid) - 60:].values
    inputs = inputs.reshape(-1,1)
    inputs  = scaler.transform(inputs)

    X_test = []
    for i in range(60,inputs.shape[0]):
        X_test.append(inputs[i-60:i,0])
    X_test = np.array(X_test)

    X_test = np.reshape(X_test, (X_test.shape[0],X_test.shape[1],1))
    return X_test
```
The general idea of this two functions is to separate the input data into train and test. I created 3 datasets: X_train, Y_train and the valid_dataset. This is going to be the information to feed the model. Now, is important to scale the data. Most of the AI models works better when data is between 0 and 1. Here I used the __MinMaxScaler__ to scale data in between this numbers.

The prediction data (or X_test) was created on the same way by cutting the main dataset into a smaller piece to obtain my information.

Now, another important step: Creating the model.
First, I created a Sequential object to add the different model features. I created a LSTM model with 70 units, and another with 50 units. Then I added a Dense layer. This combination is the one that had best performance, but you can try to change this and share your results.

```python
# create and fit the LSTM network
model = Sequential()
model.add(LSTM(units=70, return_sequences=True, input_shape=(x_train.shape[1],1)))
model.add(LSTM(units=50))
model.add(Dense(1))

model.compile(loss='mean_squared_error', optimizer='adam',metrics=['accuracy'])
model.fit(x_train, y_train, epochs=2, batch_size=1, verbose=1)
```

And here are some of the results. The RMS was near 1 so this is a good model, and the graph shows how accurates is the model.
![Grafico](/images/Grafico_ejemplo.png)

![rms](/images/rms.png)
