# Sentiment-Analysis-for-IMDB-Movie-Reviews
Deep Learning application within the field of Natural Language Processing (NLP) in PyTorch

## Introduction
This project aims to train models to detect the sentiment of written text. More specifically, it will try to feed a movie review into a model and have it predict whether it is a positive or negative movie review.
The projects starts off with how to preprocess the dataset into a more appropriate format followed by three main parts. 
+ Part 1 deals with training basic Bag of Words models.
+ Part 2 will start incoporating temporal information by using LSTM layers.
+ Part 3 will show how to train a language model and how doing this as a first step can sometimes improve results for other tasks

## Data Source

## Preprocessing the Data

Each review is contained in a separate .txt file and organized into separate directories depending on if they’re positive/negative or part of the train/test/unlabeled splits. It’s easier to re-work the data before training any models for multiple reasons.

+ It’s faster to combine everything into fewer files. 
+ Need to tokenize the dataset (split long strings up into individual words/symbols). 
+ Need to know how many unique tokens there are to decide on our vocabulary/model size.
+ Don’t want to constantly be converting strings to token IDs within the training loop (takes non-negligible amount of time).  + Storing everything as token IDs directly leads to the 1-hot representation necessary for input into our model.

## Part 1 - Bag of Words
### 1a - Without GloVe Features
### 
## Summary
