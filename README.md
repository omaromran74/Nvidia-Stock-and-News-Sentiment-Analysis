# Nvidia Stock and News Sentiment Analysis

## Project Overview

This project looks at a pretty simple question:

**Can news sentiment help explain or predict Nvidia stock price changes?**

To test this, we used sentiment analysis on Nvidia-related news headlines and compared the results with Nvidia stock price movements from 2010 to 2022.

The full news dataset had around 4.5 million headlines from major news outlets, but we filtered it down to headlines that mentioned **Nvidia**. After filtering, we ended up with **455 Nvidia-related headlines**, which were then grouped into **232 daily sentiment scores**.

Basically, the goal was to see whether good or bad news lines up with stock movement — and whether that sentiment can be used to make even a basic prediction about the next market open.

---

## Tools and Libraries

This project was built using Python and a few common data science libraries:

* **Python** — main language for the whole project
* **pandas / NumPy** — cleaning, filtering, and transforming the data
* **HuggingFace Transformers** — used for BERT-based sentiment analysis
* **`cardiffnlp/twitter-roberta-base-sentiment`** — the sentiment model used on the headlines
* **scikit-learn** — logistic regression, decision tree, confusion matrices, and F1 scores
* **Matplotlib / Seaborn** — plots, heatmaps, and visualisations

---

## Datasets

| Dataset                            | Source                                                                                                                      |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| 4.5M news headlines from 2007–2022 | [Kaggle — jordankrishnayah](https://www.kaggle.com/datasets/jordankrishnayah/45m-headlines-from-2007-2022-10-largest-sites) |
| S&P 500 daily stock data           | [Kaggle — andrewmvd](https://www.kaggle.com/datasets/andrewmvd/sp-500-stocks)                                               |

The headline dataset was filtered to only include rows containing the word **"Nvidia"**. The stock dataset was filtered to only include **NVDA** stock prices from 2010 to 2022.

After cleaning and merging both datasets by date, we used the matched days for analysis and modelling.

---

## What the Code Does

### 1. Data Cleaning

First, the datasets were cleaned and prepared:

* Converted date columns into proper datetime format
* Filtered the stock dataset to only include Nvidia stock data
* Filtered the news dataset to only include Nvidia-related headlines
* Removed missing or incomplete stock data
* Matched headline dates with stock trading dates

One thing to note: weekend headlines were dropped during the merge because the stock market is closed on weekends.

---

### 2. Sentiment Analysis

Each Nvidia-related headline was classified as:

* **Negative**
* **Neutral**
* **Positive**

The model used was:

```python
cardiffnlp/twitter-roberta-base-sentiment
```

After classification, the sentiment labels were converted into numbers:

```text
negative = -1
neutral  =  0
positive =  1
```

Then, the scores were grouped by date to create a daily average sentiment score.

---

### 3. Feature Engineering

We created a few extra columns to compare sentiment with stock movement:

| Feature             | Meaning                                             |
| ------------------- | --------------------------------------------------- |
| `SentimentScore`    | Average sentiment score for that day                |
| `Open_vs_PrevClose` | Price change from previous close to today’s open    |
| `Close_vs_Open`     | Price change during the trading day                 |
| `NextOpen_vs_Close` | Price change from today’s close to next market open |

These features helped us check whether sentiment had any relationship with price movement before, during, or after the market day.

---

## Analysis

The analysis focused on two main things:

1. **Correlation**

   * We checked whether sentiment was connected to price movement.
   * Sentiment showed a positive correlation with premarket and post-market price changes.

2. **Prediction**

   * We tested whether sentiment and stock movement data could predict whether Nvidia would go up or down by the next market open.

For prediction, we used two simple models:

* Logistic Regression
* Decision Tree Classifier

Nothing too crazy, but good enough to test the idea.

---

## Results

| Model               | Accuracy | F1 Score | Notes                                                       |
| ------------------- | -------: | -------: | ----------------------------------------------------------- |
| Logistic Regression |   62.86% |     0.76 | Higher accuracy, but heavily biased toward predicting gains |
| Decision Tree       |   57.14% |     0.66 | Lower accuracy, but better at catching losses               |

The logistic regression model looked better at first because it had higher accuracy. But after checking the confusion matrix, it was clear that it mostly predicted the stock would go up. That worked okay because Nvidia generally performed well during the period, but it also meant the model missed most actual losses.

The decision tree had lower accuracy overall, but it was more balanced and did a better job detecting downside movement.

So yeah, the logistic regression had the better score, but the decision tree was arguably more useful if you care about spotting losses.

---

## Key Findings

* News sentiment had a positive relationship with Nvidia stock movement.
* Positive headlines were more often linked with gains, while negative sentiment appeared more around larger drops.
* The strongest relationship appeared around premarket and post-market price changes.
* Predicting stock movement is still hard, even with sentiment data.
* Same-day sentiment can be tricky because headlines might react to stock movement instead of causing it.

In other words, sentiment seems useful, but it is definitely not some magic stock prediction machine.

---

## Limitations

There were a few important limitations:

* The final dataset was small after filtering and merging.
* Only headlines containing the word **"Nvidia"** were used, so some relevant news was probably missed.
* Some headlines may mention Nvidia but not actually be mainly about Nvidia.
* Weekend headlines were removed because they could not be matched directly with trading days.
* Daily data makes it hard to know what happened first: the news or the price movement.
* The results are only based on Nvidia, so they may not apply to every company.

---

## Future Work

Some ways this project could be improved:

* Use a better keyword system or named entity recognition to find more relevant Nvidia headlines.
* Run the same process on more companies, or even the full S&P 500.
* Use intraday stock data to better understand timing and causality.
* Test time-lagged sentiment, like whether yesterday’s news affects today’s stock price.
* Try more advanced models and compare them with the basic ones used here.

---

## Authors

* Daniel Stevens
* Omar Omran
