# TweetSentimentExtraction

### Problem Definition 
In this Kaggle challenge, a tweet and its corresponding sentiment are given. The task is to extract a part of the tweet that leads to the given sentiment.This problem,in common, can be posted as a Question Answering task wherein the sentiment acts as question, tweet as context from which answer is to be extracted and selected_text as the answer.

### Dataset
The data set provided by Kaggle had two files: train and test. The train file had 27,481 different tweets, one among the three sentiments (positive, negative or neutral) and their corresponding extracted text (selected_text). The challenge was to predict the selected_text for the 3534 tweets present in test data set.

### Performance Metric
The performance metric used for evaluation is word-level Jaccard score. It is calculated as follows:

![Performance Metric](https://github.com/VIVEK-JADHAV/TweetSentimentExtraction/blob/master/Images/performance.png)


Medium Article: https://medium.com/@vivekjadhavr/tweet-sentiment-extraction-6cdf7a136fc3#6249
