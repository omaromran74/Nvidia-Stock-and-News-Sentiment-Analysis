# Nvidia Stock and News Sentiment Analysis

This project explores the link between news sentiment and stock prices for Nvidia. We analyze news headlines about Nvidia and predict stock price changes using sentiment analysis and machine learning.

## Features
- **Sentiment Analysis**: Using BERT to analyze news headlines about Nvidia.
- **Stock Prediction**: Predicts stock price movement with logistic regression and decision trees.
- **Market Data**: Nvidia stock data from 2010 to 2022.

## Data
Two datasets were used:
1. **News Headlines**: 4.5 million headlines covering Nvidia from 2007-2022.
2. **Stock Prices**: Nvidia stock data from 2010-2022, focusing on open and close prices.

These datasets are merged to explore if sentiment influences stock movements.

## Method
1. **Sentiment Extraction**: Classifies each headline as negative, neutral, or positive.
2. **Price Analysis**: Compares stock price changes with sentiment on the same day.
3. **Modeling**: Uses logistic regression and decision trees to predict stock price movement the next day.

## Results
- **Logistic Regression**: 62.86% accuracy, F1 score of 0.76.
- **Decision Tree**: 57.14% accuracy, F1 score of 0.66. Better at predicting stock losses.

## Future Work
- Expand dataset to include broader market news.
- Test more advanced models for better sentiment prediction.
- Add time-lagged data for longer-term predictions.
