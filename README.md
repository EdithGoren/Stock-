# Stock Market Prediction System

A comprehensive system for stock market analysis and prediction using LSTM neural networks, with additional features for news aggregation and visualization.

## Overview

This project combines machine learning with financial analysis to predict stock market trends. It consists of:

1. **Stock Price Prediction Model**: A deep learning LSTM-based model for time series prediction of stock prices
2. **Web Interface**: Streamlit dashboard for interactive stock analysis
3. **News Aggregation Service**: FastAPI backend service that collects relevant financial and tech news

## Technologies Used

### Programming Languages and Core Frameworks

- **Python 3.11**: Primary programming language
- **TensorFlow/Keras**: For building and training neural network models
- **FastAPI**: Backend API framework for news service
- **Streamlit**: Interactive web interface for stock visualization

### Data Processing and Analysis

- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computations
- **yfinance**: Yahoo Finance API for retrieving stock data
- **scikit-learn**: Data preprocessing (MinMaxScaler)

### Visualization

- **matplotlib**: Data visualization and plotting

### News Services

- **NewsAPI**: Commercial news API integration
- **feedparser**: RSS feed parser for news sources
- **aiohttp**: Asynchronous HTTP client/server

### Deployment

- **gunicorn**: WSGI HTTP Server for deploying FastAPI application
- **Procfile**: Heroku deployment configuration

## Neural Network Architecture

The stock prediction model uses a stacked LSTM (Long Short-Term Memory) architecture:

1. **Input Layer**: LSTM with 50 units, ReLU activation, and sequence return

   - Input shape: (lookback_window, 1) - 100 days of historical data
   - Dropout: 0.2 for regularization

2. **Hidden Layer 1**: LSTM with 60 units, ReLU activation

   - Dropout: 0.3

3. **Hidden Layer 2**: LSTM with 80 units, ReLU activation

   - Dropout: 0.4

4. **Hidden Layer 3**: LSTM with 120 units, ReLU activation

   - Dropout: 0.5

5. **Output Layer**: Dense layer with 1 unit (prediction value)

The model is compiled with:

- **Optimizer**: Adam
- **Loss Function**: Mean Squared Error

## Project Structure

```
Stock/
│
├── app.py                       # Main Streamlit application
├── Procfile                     # Heroku deployment configuration
├── requirements.txt             # Project dependencies
├── stocklab.ipynb               # Jupyter notebook with model development
│
└── stockmy/                     # Backend services
    ├── app/
    │   ├── main.py              # FastAPI main application
    │   ├── services/
    │   │   └── news_service.py  # News aggregation service
    │   └── static/
    │       └── index.html       # Static frontend
    │
    ├── README.md
    └── requirements.txt         # Backend dependencies
```

## Features

### Stock Analysis & Prediction

- Historical stock data visualization with moving averages (MA50, MA100, MA200)
- Price trend analysis
- Future price prediction using LSTM neural network

### News Aggregation

- Multi-source news collection (NewsAPI, RSS feeds, YouTube)
- Filtering by country, topic, and source
- Customizable timeframe for news retrieval

## Installation and Setup

1. Clone the repository

```bash
git clone <repository-url>
cd Stock
```

2. Install dependencies

```bash
pip install -r requirements.txt
```

3. Set up environment variables

```bash
# Create a .env file with the following variables
NEWS_API_KEY=your_newsapi_key
YOUTUBE_API_KEY=your_youtube_api_key
```

4. Run the Streamlit application

```bash
streamlit run app.py
```

5. Run the FastAPI backend (optional)

```bash
cd stockmy
uvicorn app.main:app --reload
```

## Model Training Process

The stock prediction model follows these steps:

1. **Data Collection**: Historical stock data from Yahoo Finance
2. **Data Preprocessing**:
   - Train/Test split (80/20)
   - Normalization using MinMaxScaler
   - Sequence creation (100 days lookback window)
3. **Model Training**: 50 epochs with batch size of 32
4. **Evaluation**: Comparison of predicted vs. actual stock prices

## Usage

### Stock Prediction Dashboard

1. Enter a stock symbol (default: GOOG)
2. View historical data and moving averages
3. Analyze prediction vs. actual price charts

### News Service API

- GET `/news?country=us&topics=technology,finance&days=3`
- GET `/sources` - List available news sources
- GET `/categories` - List available news categories

## Future Improvements

- Implement sentiment analysis on financial news
- Add more technical indicators for stock analysis
- Improve model accuracy with hyperparameter tuning
- Develop portfolio optimization features
- Implement real-time data streaming

## License

[MIT License](LICENSE)

## Contributors

- [Your Name]

## Acknowledgments

- Yahoo Finance for stock data
- NewsAPI for news data
- Various RSS feed providers
