# TweetSentimentExtraction

### Problem Definition 
In this Kaggle challenge, a tweet and its corresponding sentiment are given. The task is to extract a part of the tweet that leads to the given sentiment.This problem,in common, can be posted as a Question Answering task wherein the sentiment acts as question, tweet as context from which answer is to be extracted and selected_text as the answer.

### Dataset
The data set provided by Kaggle had two files: train and test. The train file had 27,481 different tweets, one among the three sentiments (positive, negative or neutral) and their corresponding extracted text (selected_text). The challenge was to predict the selected_text for the 3534 tweets present in test data set.

### Performance Metric
The performance metric used for evaluation is word-level Jaccard score. It is calculated as follows:

![Performance Metric](https://github.com/VIVEK-JADHAV/TweetSentimentExtraction/blob/master/Images/performance.png)

### Exploratory Data Analysis
- There are large number of tweets with word length 5 to 7 irrespective of sentiment value.
- Positive and negative sentiment have similar distribution for difference in word length.
- Neutral sentiment has higher number of words in the selected_text compared to positive and negative sentiment. In fact, 92% of neutral tweets have equal word length and selected_text.Thus, neutral tweets can be returned as it is as the selected_text.

### BaseLine model
In this model, the tweet and its sentiment are given as input, and the start and end index of the selected text is returned by the model.

![BaseLineModel Archietecture](https://github.com/VIVEK-JADHAV/TweetSentimentExtraction/blob/master/Images/BaseLineModel.png)

This base line model has the following layers:
1. Input layer : The sentiment and the tweet are tokenized and the tokens are fed as input. 99.9 percentile of the tweets had less than 32 tokens. Hence, sequence_length was chosen as 33 (one for the sentiment) 
2.Embedding layer :This layer has pre-trained Glove word vectors of 100 dimension converting each token to 100 dimensional vector.
3. Conv1d Layer: 6 conv1d layers with kernel size 2 and stride=1
4. Dropout Layer: To prevent over-fitting.
5. Output layer: Two 32 neuron dense layer with soft-max activation function. One predicting the start index and other predicting the end index.

Loss function used was CategoricalCrossentropy and Adam optimizer with default learning rate.
The mean jaccard score for hold out test data-set was 0.59.The average jaccard score for positive sentiment is 0.35, for negative sentiment is 0.36 and for neutral sentiment is 0.92.

### Many To Many Model
In this model, the tweet is given as input to a LSTM layer and a time distributed dense layer is used to predict whether each of the input token must be present in selected_text or not.

![MantToManyModel Archietecture](https://github.com/VIVEK-JADHAV/TweetSentimentExtraction/blob/master/Images/ManyToManyModel.png)

This model has the following layers:
1. Input layer: This layer takes in token ids of the tweet as input.
2. Mask layer: This layer is masking the padded tokens.
3. Embedding Layer: Each token id is converted to 100 D vector using the pre-trained Glove vectors.
4. LSTM layer: This layer returns output at each time sequence. This is achieved by setting the parameter return sequences=True
5.Time distributed Dense Layer: This layer takes LSTM output at every time sequence and predicts whether that token must be present in the selected_text or not.

The model was trained with Adam optimizer with default learning rate. With 0.1 as the threshold, the predicted values were converted to binary(0's and 1's).Longest sub sequence algorithm was used to determine the tokens that would be part of the selected_text.
The mean jaccard score for hold out test data-set was 0.58.The average jaccard score for positive sentiment is 0.31, for negative sentiment is 0.33 and for neutral sentiment is 0.97. This model's performance did not improve from that of baseline model.

Medium Article: https://medium.com/@vivekjadhavr/tweet-sentiment-extraction-6cdf7a136fc3#6249
