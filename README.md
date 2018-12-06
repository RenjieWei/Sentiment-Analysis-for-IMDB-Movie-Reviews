# Sentiment-Analysis-for-IMDB-Movie-Reviews
Deep Learning application within the field of Natural Language Processing (NLP)

## Preprocessing the Data

Each review is contained in a separate .txt file and organized into separate directories depending on if they’re positive/negative or part of the train/test/unlabeled splits. It’s easier to re-work the data before training any models for multiple reasons.

+ It’s faster to combine everything into fewer files  
+ Need to tokenize the dataset (split long strings up into individual words/symbols)  
+ Need to know how many unique tokens there are to decide on our vocabulary/model size  
+ Don’t want to constantly be converting strings to token IDs within the training loop (takes non-negligible amount of time)  + Storing everything as token IDs directly leads to the 1-hot representation necessary for input into our model.
