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


