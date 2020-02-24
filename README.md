# StockPrice

## Introduction
Stock price prediction is an intriguing and significant field in the financial world, due to its contribution of developing strategic ways to effectively predict future value of a company's stock and to benefit from stock exchange transactions. However, how the stock market will perform in the near future is somehow unpredictable as various factors and behaviours (both rational and irrational!) can make the share price volatile and thus hard to predict. 

Nowadays, with the development of machine learning techniques, it is easier to build deep learning models that well capture features of a certain stock and thus accurately predict the trend of that stock. Two popular stock prediction models include the ARIMA (Auto Regressive Integrated Moving Average) model which is purely mathematical and the LSTM model which is a special type of RNN using neural networks.

Moreover, since stock prices are constantly changing, the stock price prediction is only considered valuable when the prediction happens in real time. Therefore, for this Enterprise project, we will first train a model using various machine learning techniques, and then use the best model to predict price in real time.

Our project is done with the following steps:
1. Fetch data from API
2. Model Training
3. Model Selection
4. Predicting in real time with best model

Certainly, the model trained should be updated frequently, but this is out of our scope. We will assume that a model is re-trained using the most recent 5 days of data at the end of each trading day and then is used in next-day prediction.

## Step 1: Fetch data from API

For simplicity, we focused on a single stock AAPL and fetch the stock price per minute for date between Feb. 10, 2020 and Feb. 14, 2020. The dataset can be founded in "apple_5days_data.csv".

The data is fetched from [Wolrd Trading Data API](https://www.worldtradingdata.com/) and this is also where we got the real time data. Dataset includes five predictors: open, close, high, low, and volume. Our target variable is the close price.

## Step 2: Model Training

Due to time constraint, here we mainly tried two techniques: AutoML and RNN. We wanted to use data from the previous three minutes to predict for the next minute. 20% of the dataset is set as testing set, which means we are using the first four days of data to train a model that is tested on the last day.

### AutoML
Inspired by what we have learned in class, we first attempted AutoML from H2O platform. Since the data represents a time series, we manually add three lags for each predictors and feeding in total 15 lagged variables into AutoML model. AutoML then selects the top 10 models and we use XGBoost, the best model suggested by AutoML, to make predictions. 

Details can be found in "H2O_AutoML.ipynb".
 
### RNN (LSTM)

Intuitively speaking, RNN is a perfect model for sequential data such like stock prices. Unfortunately, RNN is not included in the current release of H2O and in such case, we will need to manually implement it in Keras.

Here we only use the last three close prices to predict for the next day, instead of using other predictors (e.g. open, volume, etc.). The future work can be incorporating all other predictors into the model.

We then saved the model and scaler in "model.h5" and "scaler.save", respectively. The saved model can be loaded in order to predict real time data.

Detailed code can be found in "RNN_Training_Testing.ipynb".
 
## Step 3: Model Selection

From Model_Comparison folder, we compare the model result from AutoML and RNN and concluded that RNN outperformed AutoML model with only some evidence of latency. We will then use the trained RNN model to do real time prediction on Feb. 18, 2020.

## Step 4: Predicting in real time with best model

We have written a while loop to keep calling API and fetch the latest data every minute. Predictions are then made and displayed in a live plot, along with the true price.

Detailed code can be found in "RNN_Testing_Real_Time.ipynb".

## Files uploaded

- Model_Comparison: comparing peformance of RNN and the best model selected by H2O
    - RNN_AutoML_Comparison_Plot.ipynb
    - 0214_true_vs_pred_automl.csv
    - 0214_true_vs_pred_rnn.csv
- AutoML_Model
    - H2O_AutoML.ipynb
    - apple_5days_lags.csv
- RNN_Model
    - RNN_Training_Testing.ipynb
    - RNN_Testing_Real_Time.ipynb
    - 0218_pred_rnn_real_time_sample.csv
    - scaler.save
    - model.h5
- GetDataFromAPI.ipynb
- LiveDemo.ipynb
- apple_5days_data.csv: Training dataset