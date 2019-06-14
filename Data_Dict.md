## Raw Data

All data for this project was collected using the [Reddit API](https://pushshift.io/). For this project I was collecting data from a subreddit called [r/AmITheAsshole](https://www.reddit.com/r/amitheasshole)

In order to collect the data I went through new posts every hour for the last month. This gave me in total about 14,000 different posts. I then went though each of these post and looked at their top 100 comments and based off this assigned them each a class of either 'NTA' or "YTA'. The whole data collection process can be found here: [Data Collection and Classification](./Sub1_Reddit_Data_Collection.ipynb)


## Data Dictonary: Post Cleaning and Sentiment Analysis

Below is the finaly data that was used in my modelling:

| Variable Name | Variable Type | Data Type | Variable Description |
| --- | --- | --- | --- |
| created_utc | Continuous | Integer | Time of Posting |
| gildings | Discrete | Integer | How many awards has this post got |
| is_crosspostable | Categorical | Boolean | Is this post crosspostable |
| is_robot_indexable | Categorical | Boolean | Is this post Robot Indexable |
| num_comments | Continuous | Integer | Number of Comments on post |
| over_18 | Categorical | Boolean | If an age filter is on |
| retrieved_on | Continuous | Integer | Time retrieved by API |
| score | Continuous | Integer | Score determined by Reddit |
| selftext | - | String | Text in post |
| send_replies | Categorical | Boolean | Can replies be sent |
| wls | Categorical | Integer | Advert White list status |
| vader_compound | Continuous | Float | Vader Sentiment Data |
| vader_neg | Continuous | Float | Vader Sentiment Data |
| vader_neu | Continuous | Float | Vader Sentiment Data |
| vader_pos | Continuous | Float | Vader Sentiment Data |
| quote_len | Continuous | Integer | Length of selftext |
| family? | Categorical | Boolean | Does post contain a reference to a family member |
| hour | Discrete | Integer | Hour in day of post |

[Next Section](./Sub2_Cleaning.ipynb)