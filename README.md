# Sentiment-Analysis-for-IMDB-Movie-Reviews
Deep Learning application within the field of Natural Language Processing (NLP) in PyTorch.

## 1.Introduction
Sentiment analysis is contextual mining of text which identifies and extracts subjective information in source material, and helping a business to understand the social sentiment of their brand, product or service while monitoring online conversations.

This project aims to train models to detect the sentiment of written text. More specifically, it will try to feed a movie review into a model and have it predict whether it is a positive or negative movie review.
The projects starts off with how to preprocess the dataset into a more appropriate format followed by three main parts. 
+ Part 1 deals with training basic Bag of Words models.
+ Part 2 will start incoporating temporal information by using LSTM layers.
+ Part 3 will show how to train a language model and how doing this as a first step can sometimes improve results for other tasks

## 2.Data Source
This project will work with the [Large Movie Review Dataset](http://ai.stanford.edu/~amaas/data/sentiment/) of IMDB movie reviews. This is a dataset for binary sentiment classification with a collection of 75,000 .txt files.
## 3.Code Implementation
### 3.1 Preprocessing the Data

Each review is contained in a separate .txt file and organized into separate directories depending on if they’re positive/negative or part of the train/test/unlabeled splits. It’s easier to re-work the data before training any models.

Example before and after tokenization
```
"`Mad Dog' Earle is back, along with his sad-sack moll Marie, and that fickle clubfoot Velma. So are Babe and Red, Doc and Big Mac, and even the scenery-chewing mutt Pard. The only thing missing is a good reason for remaking Raoul Walsh's High Sierra 14 years later without rethinking a line or a frame, and doing so with talent noticeably a rung or two down the ladder from that in the original. (Instead of Walsh we get Stuart Heisler, for Humphrey Bogart we get Jack Palance, for Ida Lupino Shelley Winters, and so on down through the credits.) The only change is that, this time, instead of black-and-white, it's in Warnercolor; sadly, there are those who would count this an improvement.<br /><br />I Died A Thousand Times may be unnecessary \x96 and inferior \x96 but at least it's not a travesty; the story still works on its own stagy terms. Earle (Palance), fresh out of the pen near Chicago, drives west to spearhead a big job masterminded by ailing kingpin Lon Chaney, Jr. \x96 knocking over a post mountain resort. En route, he almost collides with a family of Oakies, when he's smitten with their granddaughter; the smiting holds even when he discovers she's lame. Arriving at the cabins where the rest of gang holes up, he finds amateurish hotheads at one another's throats as well as Winters, who throws herself at him (as does the pooch). Biding time until they get a call from their inside man at the hotel, Palance (to Winter's chagrin) offers to pay for an operation to cure the girl's deformity, a gesture that backfires. Then, the surgical strike against the resort turns into a bloodbath. On the lam, Palance moves higher into the cold Sierras....<br /><br />It's an absorbing enough story, competently executed, that lacks the distinctiveness Walsh and his cast brought to it in 1941, the year Bogie, with this role and that of Sam Spade in the Maltese Falcon, became a star. And one last, heretical note: Those mountains do look gorgeous in color.<br /><br />"
```
```
['`', 'mad', 'dog', "'", 'earle', 'is', 'back', ',', 'along', 'with', 'his', 'sad-sack', 'moll', 'marie', ',', 'and', 'that', 'fickle', 'clubfoot', 'velma', '.', 'so', 'are', 'babe', 'and', 'red', ',', 'doc', 'and', 'big', 'mac', ',', 'and', 'even', 'the', 'scenery-chewing', 'mutt', 'pard', '.', 'the', 'only', 'thing', 'missing', 'is', 'a', 'good', 'reason', 'for', 'remaking', 'raoul', 'walsh', "'s", 'high', 'sierra', '14', 'years', 'later', 'without', 'rethinking', 'a', 'line', 'or', 'a', 'frame', ',', 'and', 'doing', 'so', 'with', 'talent', 'noticeably', 'a', 'rung', 'or', 'two', 'down', 'the', 'ladder', 'from', 'that', 'in', 'the', 'original', '.', '(', 'instead', 'of', 'walsh', 'we', 'get', 'stuart', 'heisler', ',', 'for', 'humphrey', 'bogart', 'we', 'get', 'jack', 'palance', ',', 'for', 'ida', 'lupino', 'shelley', 'winters', ',', 'and', 'so', 'on', 'down', 'through', 'the', 'credits', '.', ')', 'the', 'only', 'change', 'is', 'that', ',', 'this', 'time', ',', 'instead', 'of', 'black-and-white', ',', 'it', "'s", 'in', 'warnercolor', ';', 'sadly', ',', 'there', 'are', 'those', 'who', 'would', 'count', 'this', 'an', 'improvement', '.', 'i', 'died', 'a', 'thousand', 'times', 'may', 'be', 'unnecessary', 'and', 'inferior', 'but', 'at', 'least', 'it', "'s", 'not', 'a', 'travesty', ';', 'the', 'story', 'still', 'works', 'on', 'its', 'own', 'stagy', 'terms', '.', 'earle', '(', 'palance', ')', ',', 'fresh', 'out', 'of', 'the', 'pen', 'near', 'chicago', ',', 'drives', 'west', 'to', 'spearhead', 'a', 'big', 'job', 'masterminded', 'by', 'ailing', 'kingpin', 'lon', 'chaney', ',', 'jr.', 'knocking', 'over', 'a', 'post', 'mountain', 'resort', '.', 'en', 'route', ',', 'he', 'almost', 'collides', 'with', 'a', 'family', 'of', 'oakies', ',', 'when', 'he', "'s", 'smitten', 'with', 'their', 'granddaughter', ';', 'the', 'smiting', 'holds', 'even', 'when', 'he', 'discovers', 'she', "'s", 'lame', '.', 'arriving', 'at', 'the', 'cabins', 'where', 'the', 'rest', 'of', 'gang', 'holes', 'up', ',', 'he', 'finds', 'amateurish', 'hotheads', 'at', 'one', 'another', "'s", 'throats', 'as', 'well', 'as', 'winters', ',', 'who', 'throws', 'herself', 'at', 'him', '(', 'as', 'does', 'the', 'pooch', ')', '.', 'biding', 'time', 'until', 'they', 'get', 'a', 'call', 'from', 'their', 'inside', 'man', 'at', 'the', 'hotel', ',', 'palance', '(', 'to', 'winter', "'s", 'chagrin', ')', 'offers', 'to', 'pay', 'for', 'an', 'operation', 'to', 'cure', 'the', 'girl', "'s", 'deformity', ',', 'a', 'gesture', 'that', 'backfires', '.', 'then', ',', 'the', 'surgical', 'strike', 'against', 'the', 'resort', 'turns', 'into', 'a', 'bloodbath', '.', 'on', 'the', 'lam', ',', 'palance', 'moves', 'higher', 'into', 'the', 'cold', 'sierras', '...', '.', 'it', "'s", 'an', 'absorbing', 'enough', 'story', ',', 'competently', 'executed', ',', 'that', 'lacks', 'the', 'distinctiveness', 'walsh', 'and', 'his', 'cast', 'brought', 'to', 'it', 'in', '1941', ',', 'the', 'year', 'bogie', ',', 'with', 'this', 'role', 'and', 'that', 'of', 'sam', 'spade', 'in', 'the', 'maltese', 'falcon', ',', 'became', 'a', 'star', '.', 'and', 'one', 'last', ',', 'heretical', 'note', ':', 'those', 'mountains', 'do', 'look', 'gorgeous', 'in', 'color', '.']
```
### 3.2 Bag of Words
I implemented the basic bag of words model to extract the sentiment information. Note that the bag of words method utilizes all of the tokens in the sequence but loses all of the information about when the tokens appear within the sequence. 
### 3.3 RNN with LSTM
A recurrent neural network can be used to maintain the temporal information and process the data as an actual sequence. This part consists of training recurrent neural networks built with LSTM layers. I trained two separate models, one from scratch with a word embedding layer and one with GloVe features.
### 3.4 Language Model
This part is about training a language model by leveraging the additional unlabeled data and showing how this pretraining stage typically leads to better results on other tasks like sentiment analysis.
Here is a sample of text produced by the trained language model.
```
# temperature 1.3
a crude web backdrop from page meets another eastern story ( written by an author bought ) when it was banned months , i am sure i truly are curiosity ; i have always been the lone clumsy queen of the 1950 's shoved director richard `` an expert on target '' . good taste . not anything report with star 70 's goods , having it worked just equally attractive seem to do a moving train . memorable and honest in the case of `` ross , '' you find it fantasy crawford is strong literature , job suffering to his a grotesque silent empire , for navy turns to brooklyn and castle of obsession that has already been brought back as welles ' anthony reaches power . it 's totally clearly staged , a cynical sit through a change unconscious as released beer training in 1944 with mickey jones 
```
```
# temperature 1.3
i wanted to walk out on featuring this expecting even glued and turd make . he genius on dialog , also looking good a better opportunity . anyway , the scene in the ring where christopher wallace , said things giving the least # 4 time anna hang earlier too leaves rick the blond doc from , walter from leon . is ironic until night with rob roy , he must 've been a mother . which are images striking to children while i think maybe this is not mine . but not in just boring bull weather sake , which set this by saying an excellent episode about an evil conspiracy monster . minor character with emphasis for blood deep back and forth between hip hop , baseball . as many red light figure hate americans like today 's life exercise around the british variety kids . nothing was added 
```


## 4.Summary
### 4.1 Test Accuracy 
* Trained the bag of words model and achieved 87.74% accuracy in the test dataset
* Trained the recurrent neural network model built with LSTM layers and achieved 92.31% accuracy in the test dataset
* Trained the language model and achieved 93.01% accuracy in the test dataset
* To put this in perspective, the state of the art on the IMDB sentiment analysis is around 94.1%.



### 4.2 Further Improvement
There are several ways in which I can build the model. I will continue trying and improving the accuracy of the model by experimenting with different architectures, layers and parameters.



