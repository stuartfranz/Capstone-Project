# Classification of Reddit Posts

---

### Introduction

---

Accross Reddit there are multiple different Subreddits Users will post to with a goal of determining one thing or another. r/AmITheAsshole is a subreddit that a user would go to in order to get other Users' opinions on their specific story with the goal of determining if they are in the right or the wrong.

A great feature about this subreddit is that Users' are encouraged to post their opinion in the comments in a standardised format. 'NTA' meaning that the commenter supports the User writing the story and 'YTA' meaning that they thought the User writing the story was in the wrong. This allows me to access the comments from each post and talley up they ammount of people voting either way and assign each of the posts a label of 'NTA' or 'YTA'

The goal of this model is to classify, using sentiment analysis on the post as well as variours traits about the post, weather or not the User posting the story is 'NTA' or 'YTA'

My metrics of success will be the percent of Classifications above the baseline model that I can predict correctly.

risks/limitations/assumptions

---

**[Data Collection and Data Dictiionary](./Data_Dict.md)**

**[Data Cleaning](./Sub2_Cleaning.ipynb)**

**[EDA (Pre Vader Sentiment Feature Engineering)](./Sub3_EDA.ipynb)**

**[Full EDA](./Sub5_Further_EDA.ipynb)**

**[Feature Engineering + Modelling](./Sub4_Vader_Sentiment.ipynb)**

#### Failed Models:

**[Regression Model](./Sub6_Regression_Analysis.ipynb)**

**[Tfidf Vectoriser](./Sub7_TFID_Vectoriser.ipynb)**

---

## [Summary](./Summary.md)
