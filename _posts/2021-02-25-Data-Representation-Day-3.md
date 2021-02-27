---
title: 'Big Data Analysis Day 3: How to Collect Data '

date: 2021-2-25

---

**How do we collect Data?**

- We could download raw data files
    * Kaggle other sites

- We could crawl a website
    * Run a program that automatically traverses the web for us
    * Many Python Libraries that help with that (Beautiful Soup)

- We could use the Application Programming Interface (API)
    * Way for a program to request services from another program



### Lets work with Twitters API

[Heres a Link to my Twitter Web Scraper](https://github.com/devinpowers/twitter)


**Simple Twitter Search API**

```python
import tweepy
from tweepy import OAuthHandler
from tweepy import API

```
After you Create a App in Twitter you enter these values in for the X's:
```python
C_KEY = 'XXX'
C_SECRET = 'XXX'
A_TOKEN_KEY = 'XXX'
A_TOKEN_SECRET = 'XXX'

```

```python
auth = tweepy.OAuthHandler(C_KEY, C_SECRET)
auth.set_access_token(A_TOKEN_KEY, A_TOKEN_SECRET)
api = tweepy.API(auth)
```

Lets **search** for a specfic keyword

```python
keyword = 'Whatever keyword we enter'
posts = api.search(q=keyword,count=10)
for tweet in posts:
    print("* "+str(tweet.text.encode("utf-8")))

```

Output:

Will output a bunch of JSON code



## Lets work on an Exercise using Python Tweepy

[Read the Tweepy Documentation](https://docs.tweepy.org/en/latest/)

Using the Twitter Search (REST) API in order to download the 10 most recent tweets from the twitter feed containing whatever **keyword** we decide.

APIs do have rate limitation which is how many requests can be made per day or per hour, if the rate is exceeded, the API returns an error. (possibly blocks IP address if abused)

Twitters REST API limit is 180 queries per 15 minute window

Replace the XXX's with your own consumer tokens and access tokens

Let's extract the **screen name** of the user who posts the tweet of our keyword and the tweet message as well, and store the results in a DataFrame object.

**Search Methods** (from tweepy documentation)

```python
api.search(q,[,geocode][,lang] [,locale][,result_type][,count][,until] [,since_id][,max_id] [,include_entities] )
```
This will return a relevant Tweets matching a specified query.

**Parameters:**

* q : The search query string
* geocode : Returns tweets by users location (lat/long)
* lang : Restricts tweets to a given language
* locale : Specify the language of the Query we sent
* result_type : Specifies what type of search results you would prefer to receive
* count : The number of results to try and retrieve
* until : Returns tweets created before a given data
* since_id : Returns only statuses with an ID greater than the specified ID
* mad_id :  Returns only statuses with an ID less than or equal to the specified ID
* include_entities : he entities node will not be included when set to false. Defaults to true

In our case, were only intrested in using the **q** (query for our keyword) and  **count** to limit the number of tweets to search for. 

The keyword to search for in this example will be: **Michigan State Spartans**v(Go Green!)

```python
import tweepy
from tweepy import OAuthHandler
from tweepy import API

import pandas as pd


consumer_key = 'XXX'
consumer_secret = 'XXX'
access_token = 'XXX'
access_token_secret = 'XXX'

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.API(auth)

## Search Method
keyword = "Michigan State Spartans"

post = api.search(q = keyword, count = 10 )

# now lets save the data of the tweet and the username

data = pd.DataFrame(columns = ["Tweet", "UserName"])

## Lets add the stuff to our DataFrame

for tweet in post:

    data = data.append( {"Tweet":tweet.text. "UserName":tweet.user.screen_name }, ignore_index = True)

```
Lets see our DataFrame:
```python
data
```
Output:

```python

	Tweet	                                            UserName
0	RT @chrissolari: Michigan State basketball's F...	TheAndyKatz
1	Michigan State basketball's Foster Loyer could...	chrissolari
2	@PekalaLaw Truly another crazy story. I guess ...	LoganSimios
3	Michigan State Women’s Basketball: Nebraska Co...	SpartyOnHuskers
4	Late-night shooting pays off as Gabe Brown tur...	SpartansMLive
5	Late-night shooting pays off as Gabe Brown tur...	MLive
6	Late-night shooting pays off as Gabe Brown tur...	MLiveSports
7	RT @SportsCenter: THE SPARTANS HANDLE BUSINESS...	Krueger24Kyle
8	RT @onlinelisting: #RecentSportNews #sportcap ...	onlinelisting
9	RT @Graham_Couch: I pity the 2-seed that faces...	RyanMSU21


```

COOL