# StockPrice

## Introduction
The goal of this project is to predict the stock in real-time by utilizing [Wolrd Trading Data API](https://www.worldtradingdata.com/). We studied and experimented different models. We chose RNN in our final model and the result was pretty satisfying.

## Files

- Model_Comparison: comparing peformance of RNN and the best model selected by H2O
    - RNN_AutoML_Comparison_Plot.ipynb
    - 0214_true_vs_pred_automl.csv
    - 0214_true_vs_pred_rnn.csv
- AutoML_Model
    - H2O_AutoML.ipynb
    - 0214_apple_lags.csv
- RNN_Model
    - RNN_Training_Testing.ipynb
    - RNN_Testing_Real_Time.ipynb
    - 0218_pred_rnn_real_time_sample.csv
    - scaler.save
    - model.h5
- GetDataFromAPI.ipynb
- LiveDemo.ipynb
- apple_5days_data.csv: Training dataset
- Stock Price Prediction.pptx: Presentation Slides