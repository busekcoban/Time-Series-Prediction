# Stock Price Prediction using LSTM and Prophet

This project demonstrates stock price prediction using two different models: Long Short-Term Memory (LSTM) and Prophet. The aim is to forecast NVIDIA's stock price and compare the performance of these models through various metrics.

### Features

- LSTM Model: A deep learning approach leveraging sequential data.

- Prophet Model: A statistical model designed for time series forecasting.

- Sliding Window Validation: Implemented for robust performance evaluation.

- Performance Metrics: Mean Absolute Error (MAE), Mean Squared Error (MSE), and Root Mean Squared Error (RMSE) are calculated to evaluate model accuracy.

- Data Preprocessing: Includes normalization, handling missing data, and ensuring valid trading days.

### Dataset

Historical stock data for NVIDIA (NVDA) is retrieved using Yahoo Finance API:

- Time Period: January 1, 2016, to January 1, 2024.

- Prophet Model: Uses 10 years of historical data from Yahoo Finance for training and forecasting.

- Preprocessed Columns: Close prices are used for training and prediction.

### LSTM Model

#### Workflow:

Preprocessing: Data is normalized using MinMaxScaler.

Data Preparation: Sequence of 30 days is used as input to predict the next day's price.

#### Model Architecture:

Three LSTM layers with dropout.

Fully connected layers for regression.

Training: Model is trained with 50 epochs and a batch size of 32.

Sliding Window Validation: RMSE is calculated for multiple overlapping windows.

#### Key Metrics:

Sliding Window Average RMSE: Evaluates prediction stability.

### Prophet Model

#### Workflow:

Preprocessing: Data is reformatted to Prophet's ds (date) and y (target) columns.

Training: Model is trained on historical data with daily seasonality enabled.

Cross-Validation: Performed using a 2-year initial window, 6-month step size, and a 1-year horizon.

Future Forecasting: Predicts for the next 60 days.

#### Cross-Validation Results:

Mean Absolute Error (MAE): 10.95

Mean Squared Error (MSE): 466.83

Root Mean Squared Error (RMSE): 21.61
