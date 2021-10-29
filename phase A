# ZJZ twitter sentiment analysis

# import
import tweepy
from textblob import TextBlob
#from wordcloud import WordCloud
import pandas as pd
import numpy as np
import re
import matplotlib.pyplot as plt

# keys and secrets
accessToken='xxxx'
accessTokenSecret='xxxx'
consumerKey='xxxx'
consumerSecret='xxxx'

#suthorization
auth = tweepy.OAuthHandler(consumerKey,consumerSecret)
auth.set_access_token(accessToken,accessTokenSecret)
api=tweepy.API(auth,wait_on_rate_limit=True)

# get n tweets 

posts = api.user_timeline(screen_name="BillGates",count=10,lang="en",tweet_mode="extended")
print(type(posts))
# put data into frame
df = pd.DataFrame([tweet.full_text for tweet in posts],columns=['Tweets'])

# filter some unnecessary words
def cleanTxt(text):
  text = re.sub(r'@[A-Za-z0-9]+','',text)
  text = re.sub(r'#','',text)
  text = re.sub(r'RT[\s]+','',text)
  text = re.sub(r'https:\/\/S+','',text)
  return(text)

df['Tweets']=df['Tweets'].apply(cleanTxt)

def getSubjectivity(text):
  return TextBlob(text).sentiment.subjectivity
def getPolarity(text):
  return TextBlob(text).sentiment.polarity
#NLP part
def getAnalysis(score):
  if score < 0:
    return 'Negative'
  elif score==0:
    return 'Middle'
  else:
    return 'Positive'


df['Subjectivity']=df['Tweets'].apply(getSubjectivity)
df['Polarity']=df['Tweets'].apply(getPolarity)
print(df)
df['Analysis']=df['Polarity'].apply(getAnalysis)
print(df)
