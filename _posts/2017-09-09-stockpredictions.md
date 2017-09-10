---
layout: post
title:  "Stock Predictions through News Sentiment Analysis"
date:   2017-09-09
desc: "Stock Predictions through News Sentiment Analysis"
keywords: "stock predictions, machine learning, dinesh daultani, blog, sentiment analysis"
categories: [machine learning]
tags: [stockpredictions, machinelearning, dineshdaultani]
icon: icon-html
---
  
# Abstract:

Stock prices fluctuate rapidly with the change in world market economy. There are many techniques to predict the stock price variations, but in this project, New York Times’ news articles headlines is used to predict the change in stock prices. We are using NY Times Archive API to gather the news website articles data over the span of 10 years. Sentiment analysis of the headlines are going to be performed and then the output of the sentiment analysis is going to be fed into machine learning models to predict the price of DJIA stock indices.  
  
# Introduction

“According to the Efficient Market Hypothesis (EMH), stocks always trade at their fair value on stock exchanges, making it impossible for investors to either purchase undervalued stocks or sell stocks for inflated prices. As such, it should be impossible to outperform the overall market through expert stock selection or market timing, and the only way an investor can possibly obtain higher returns is by purchasing riskier investments.”[1]

Basically what that means is that the stock prices are hard to predict based on some expertise through previous trends and past stock prices. Stock price fluctuation represents the current market trends and business growth among other factors that could be considered to sell or buy stocks. To analyze the current trends, new company’s product information, business growth etc., we could take a look at the daily news which represents factual information about the companies which could be ultimately used to predict the stock prices. Hence, we will be using news articles to predict the change in stock indices rather than predicting the prices by historical stock prices.  
  
  
# Data Gathering

Two types of data gathered over the span of ten years from 2007-2016 as follows:

**1. Stock indices:** As in general, most researchers predict stock prices of composite index instead of predicting individual company’s stock prices. Because those composite index prices reflect the overall change in the stock market. We have used DJIA stock indices to predict the overall change in US top companies. Data is collected from Yahoo finance website [2]

**2. News data:** There is not a lot of article data available on Internet for public use. From our research the best openly available data which could be appropriately used in stock prediction was from the NY Times Archive API. [3]  
  
  
# Data Processing

### Article Filtering:

Articles collected from the NY Times archive API contain the data in the form of categories represented by sections. Some of the sections contains some irrelevant categories of articles, which are not related to stocks at all, such as Biography, Obituary, Schedule etc. Therefore, we have removed those kinds of articles from the lists. Article sections that are kept at the end for sentiment analysis are as follows: 'Business', 'National', 'World', 'U.S.' , 'Politics', 'Opinion', 'Tech', 'Science',  'Health' and 'Foreign'. Out of 1M articles, approximately 400k articles are filtered out after applying the above filters.  

### Merge stock indices with articles:

After filtering out the relevant articles, a single string was formed from concatenating all the articles headlines for a single day. After getting the single string for a day, it was merged with appropriate date (time series) and Dow Jones Industrial Average (DJIA) stock index value.  
  
  
# Sentiment Analysis

The Natural Language Toolkit (NLTK) package in python is the most widely used for sentiment analysis for classifying emotions or behavior through natural language processing. Vader Sentiment Analyzer, which comes with NLTK package, is used to score single merged strings for articles and gives a positive, negative and neutral score for that string.  

  
  
# Training models

Output of sentiment analysis is being fed to machine learning models to predict the stock prices of DJIA indices. We have used scikit-learn[4] library to train various machine learning models such as Random Forest, Logistic Regression and Multi-Layer Perceptron (MLP) Classifiers with different optimized values of hyper parameters to get the best optimized results.

Below are the results after applying various classifiers. Note: Orange line shows Exponentially Weighted Moving Average (EWMA) of actual price and blue line shows EWMA of predicted price.  
  
  

### Random Forest:  
<img src="{{ site.img_path }}/stockpredictions/random-forest.png" width="75%">  

### Logistic Regression:  
<img src="{{ site.img_path }}/stockpredictions/logistic-reasoning.png" width="75%">  

### MLP classifier:  
<img src="{{ site.img_path }}/stockpredictions/mlp-classifier.png" width="75%">  

  
  
# Challenges

1. Missing stock indices: As the stock market is closed on weekends and US holidays, there are no open/close prices for any of the stocks on those days. Which affects our DJIA values as well. We have used interpolation of the prices to fill in the missing values. For interpolation implementation, we have used the interpolate method from pandas[5] package.

2. High fluctuations in prices: As the prices of the stocks fluctuate a lot, we have used a technique called smoothing which is used in financial markets to take a moving average of the values, which results in comparatively smooth curves. For moving average implementation, we have used the EWMA method from pandas[5] package.  

  
  
# Conclusion

Our tests determined that using the MLP classifier (a.k.a. neural networks) showed better results than logistic regression and random forest trained models. Although the graphs generated does not shows satisfactory results, further research in the below mentioned areas could lead to better accuracy.  

  
  
# Further improvements

1. We were not able to find any corpse or sentiment analyzer which is designed specifically for news articles. We have used the Valence Aware Dictionary and sEntiment Reasoner (VADER) sentiment analyzer but it’s built specifically for social media text. We could develop a sentiment analyzer which could work better in news article situations. 
2. In our project we only considered news article sentiment analysis for prediction but in the real scenarios, stock fluctuations show trends which get repeated over a period of time. So there’s a lot of scope in merging the stock trends with the sentiment analysis to predict the stocks which could probably give better results.
3. Predict individual companies stocks based on optimized trained model and sentiment analysis of that specific company news articles.
4. Train Convolutional Neural Network (CNN) and Recurrent Neural Networks models.  

Github Project Link: https://github.com/dineshdaultani/StockPredictions  
  
  
# References:

1. Efficient Market Hypothesis (EMH): http://www.investopedia.com/terms/e/efficientmarkethypothesis.asp#ixzz4kq8u68hp  
2. https://finance.yahoo.com/quote/%5EDJI/history
3. https://developer.nytimes.com/archive_api.json
4. http://scikit-learn.org/stable/tutorial/basic/tutorial.html
5. http://pandas.pydata.org  
