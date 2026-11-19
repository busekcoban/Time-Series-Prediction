# Stock Price Prediction using LSTM and Prophet

This project demonstrates stock price prediction using two different models: Long Short-Term Memory (LSTM) and Prophet. The aim is to forecast NVIDIA's stock price and compare the performance of these models through various metrics.

### Features

- LSTM Model: A deep learning approach leveraging sequential data.

- Prophet Model: A statistical model designed for time series forecasting.

- Sliding Window Validation: Implemented for robust performance evaluation.

- Performance Metrics: Mean Absolute Error (MAE), Mean Squared Error (MSE), and Root Mean Squared Error (RMSE) are calculated to evaluate model accuracy.

- Data Preprocessing: Includes normalization, handling missing data, and ensuring valid trading days.

- Live data: prices are downloaded from Yahoo Finance on every run, up to the latest completed trading day.

- Reproducible training: a fixed random seed is used for the LSTM.

### Getting Started

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```

Tested with Python 3.13, TensorFlow 2.21 / Keras 3.15, Prophet 1.5 and yfinance 1.8.

Both notebooks download the prices from Yahoo Finance when they run.

### Dataset

Historical, split-adjusted daily close prices for NVIDIA (NVDA) are downloaded from Yahoo Finance (via `yfinance`) each time a notebook runs:

- LSTM Model: January 1, 2016 up to November 19, 2026.

- Prophet Model: the last 10 years up to November 19, 2026.

The results below come from a run on November 19, 2026 (data through November 18, 2026: 2,736 trading days for the LSTM, 2,512 for Prophet).

- Preprocessed Columns: Close prices are used for training and prediction.

### LSTM Model (`ltsm.ipynb`)

#### Workflow:

Preprocessing: Data is normalized using MinMaxScaler.

Data Preparation: Sequence of 30 days is used as input to predict the next day's price. The last 10% of the data is held out as the test set.

#### Model Architecture:

Three LSTM layers with dropout.

Fully connected layers for regression.

Training: Model is trained with 50 epochs and a batch size of 32.

Sliding Window Validation: A model is retrained on 80% windows shifted by 100 days; RMSE is calculated on the 30 days that follow each window.

#### Results:

| Metric | Value |
|---|---|
| Test MAE (Dec 1, 2025 – Nov 18, 2026) | 4.95 |
| Test RMSE (Dec 1, 2025 – Nov 18, 2026) | 6.40 |
| Sliding Window Average RMSE (6 windows) | 10.56 |

### Prophet Model (`prophet.ipynb`)

#### Workflow:

Preprocessing: Data is reformatted to Prophet's ds (date) and y (target) columns.

Training: Model is trained on historical data with daily seasonality enabled.

Cross-Validation: Performed using a 2-year initial window, 6-month step size, and a 1-year horizon (15 cutoffs).

Future Forecasting: Predicts the next 60 trading days.

#### Cross-Validation Results:

| Metric | Value |
|---|---|
| Mean Absolute Error (MAE) | 14.61 |
| Mean Squared Error (MSE) | 500.26 |
| Root Mean Squared Error (RMSE) | 22.37 |

### Note on comparing the models

The LSTM predicts one day ahead, while Prophet's cross-validation measures errors over a horizon of up to one year, so the metrics above are not directly comparable.
