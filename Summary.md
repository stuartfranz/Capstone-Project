<!--
 .tab { margin-left: 40px; }
-->

# Summary

- [Data Collection](#Data0)
    - [Reddit API](#Data1)
    - [Post Collection](#Data2)
    - [Comment Collection](#Data3)
- [Cleaning](#Clean0)
    - [Convert Dates](#Clean1)
    - [Columns to Drop](#Clean2)
    - [Drop NA](#Clean3)
    - [Convert all to Float](#Clean4)
- [Feature Engineering](#FE)
- [Models](#Model0)
    - [TFIDF](#Model1)
    - [Vader Sentiment](#Model2)
        - [Linear Regression](#Model3)
        - [Logistic Regression](#Model4)
        - [Decision Tree Classification](#Model5)
        - [Bagged DTC](#Model6)
- [Limitations](#Lim0)
- [Next Steps](#NS)

---

<h1><a id = 'Data0' href = './Data_Dict.md'>
Data Collection</a></h1>

<h3><a id = 'Data1' href = 'https://pushshift.io/'>
Reddit API:</a></h3>

<p>All data for this project was collected the Reddit API. On this there are three area that you can search: Comments, Submissions and Subreddits. For this project I solely searched through Submissions and Comments. The Reddit API has a feature that you can search with a delay and therefore can seach over an extended period of time. This made it perfect for large scale rapid data collection.</p>

<h3><a id = 'Data2'></a>
Post Collection Method:</h3>

<p>Collecting Data was made very easy and fast by the Submissions portion of the Reddit API. The API gave around 50 different peatures of each post. I collected all of these as it did not effect the speed of collection. It was easy to get rid of a certain ammount of these features straight off the bat. For example there were a few features that were traits of the author. While this could have been useful they were all either too specific like the name of the author or they were very generic and did not change between different authors. Quickly sifting through the features it was easy to make decisions about if features were necessary. If I was not 100% sure about dropping a feature I would leave it in and let the model decide weather or not to keep it.</p>

<p>Some cleary relevant features that were given by the API included the Text in the post and the number of comments. I will dulve further into these in the modelling section.</p>

<h3><a id = 'Data3'></a>
Comment Collection:</h3>

<p>In order to collect the comments I looped through all of the different ID's that I had collected as features of the posts. For each of the comments in this subreddit commenters will vote using a standardised format for weather or not they thought that the poster was in the right. This made it easy to sift through all of the comments for each post and Identify what the community thought was the correct answer to a subjective question. This gave a dominant class for each post and allowed me assign each post into one of 'NTA' and 'YTA'</p>

<h1><a id = 'Clean0' href = './Sub2_Cleaning.ipynb'>
Cleaning</a></h1>

<a id = 'Clean1'></a>
- **Convert Dates**
    - All of the dates were given in UTC which is just a number that represents the number of seconds since the 1st of Januray 1970. I used a library called time to convert all times to a datetime format.
    
<a id = 'Clean2'></a>
- **Columns to Drop**
    - After looking through some of the columns in more detail there were a few which either were all null or a large percentage of them were null. I dropped all of the columns.

<a id = 'Clean3'></a>
- **Drop NA**
    - Certain Columns only had a small number of nulls. For these I simply dropped the rows with any nulls. This sacrificed only a small percentage of my data.

<a id = 'Clean4'></a>
- **Convert all to Float**
    - At this point I ensured that all columns that were meant to be floats were in the right format so they would not cause problems further down the line.
    
<h1><a id = 'FE' href = './Sub4_Vader_Sentiment.ipynb'>
Feature Engineering</a></h1>

<p>Due to the fact that a few of the colums were in a format that were not easy to model with I decided to manufacture a couple of features. These included the hour of the day in which the post was made (Which was subsequently dopped due to the fact that the times did not account for timezone and hence was meaningless), weather of not the text contained certaing keywords (which was emitted during TFIDF modelling phase to avoid overfitting) and collating the awards into one collums so that they could be put through a model.</p>

<h1><a id = 'Model0' href = './Sub4_Vader_Sentiment.ipynb'>
Modelling</a></h1>

<h3><a id = 'Model1' href = './Sub7_TFID_Vectoriser.ipynb'>
TFIDF:</a></h3>

<p class="tab">Score: 0.57243195785777</p>
<p class="tab">Baseline: 0.57243195785777</p>
<p class="tab">As you can see with the scores above my model did not improve the baseline at all. This can be seen in the <a href='./Sub5_Further_EDA.ipynb'>Cloudmaps</a> where there are a lot of overlaps between the top words for each class. This lead me towards sentiment analysis as just using NLP was not working.</p>

<h3><a id = 'Model2' href = './Sub4_Vader_Sentiment.ipynb'>
Vader Sentiment:</a></h3>

<h5><a id = 'Model3' href = './Sub6_Regression_Analysis.ipynb'>
Linear Regression:</a></h5>

<p class="tab">R Squared Score: 0.059378183682180</p>
<p class="tab">For the linear regrssion model I used the percentage of comments voting for 'NTA' as the target. As you can tell by the score this did not work very well at all and barely beat a completely random model.</p>

<h5><a id = 'Model4'></a>
Logistic Regression:</h5>

<p class="tab">Test Score: 0.6066725197541704</p>
<p class="tab">Baseline: 0.57243195785777</p>
<p class="tab">Basic Logistic regression was the first model that had a significant improvement from the baseline. It was still not great and so I kept searching</p>

<h5><a id = 'Model5'></a>
Decision Tree Classification:</h5>

<p class="tab">Test Score: 0.6084284460052678</p>
<p class="tab">Baseline: 0.57243195785777</p>
<p class="tab">This model only slightly improved on the Logistic Regression Model. But it did show movment in the right direction which was not the case for many other models tested.</p>

<h5><a id = 'Model6'></a>
Bagged DTC:</h5>

<p class="tab">Test Score: 0.655838454784899</p>
<p class="tab">Baseline: 0.57243195785777</p>
<p class="tab">After the slight improvement from Logistic regression to DTC I decided that if I were to used bagging then I could reduce a large amount of the varience that was arising in my models and sure enough the model score shot up to 8% above the baseline. Since I have attempted to improve this score using neural networks and thus far have been unsuccessfull. This is most likely due the the <a href = #Lim0> limitations</a> detailed below</p>

<h1><a id = 'Lim0'></a>
Limitations</h1>

<p>Whilst the Reddit API did provide a very quick and easy way to collect data and also provide a large amount of features of each post the usefulness of a lot of the features was non existant. There are various fatures of the submissions that the API missed out that I would have liked to explore. This would include features including but not limited to: The timezone of the post, the location of the post and various information about the user. I understand that the some of these may cause issues due to privacy concerns and therefore are alimitation to my model</p>

<h1><a id = 'NS'></a>
Next Steps</h1>

<p>There are many different subreddits that involve some kind of voting in the comments. I think that it would be interesting to apply different methods to multiple different subreddits. I think that there would be some that would work very well with sentiment analysis.I could even extend the way in which I found the targets by using tags on the posts.</p>
    
<p>There are endless paths to go down and I would be interested to find out what types of predictions I could come up with</p>


[Return Home](./ReadMe.md)
