# Tweets-preprocessing-cleaning-for-text-mining-




#########   Date modifier

import time

OK=data_tweet['Time']

df = pd.DataFrame()

df['Time']=''

df['Time hour']=''

data_tweet['Year']=''

data_tweet['Month']=''

data_tweet['Day']=''

data_tweet['Hour']=''

for i in range(OK.shape[0]):

X=OK[i]

#Y= time.strftime('%Y%m%d%H', time.strptime(X,'%a %b %d %H:%M:%S +0000 %Y'))

Y= time.strftime('%Y%m%d', time.strptime(X,'%a %b %d %H:%M:%S +0000 %Y'))

df.at[i,'Time']=pd.to_numeric(Y)


   Y1= time.strftime('%Y', time.strptime(X,'%a %b %d %H:%M:%S +0000 %Y'))
   
   Y2= time.strftime('%m', time.strptime(X,'%a %b %d %H:%M:%S +0000 %Y'))
   
   Y3= time.strftime('%d', time.strptime(X,'%a %b %d %H:%M:%S +0000 %Y'))
   
   Y4= time.strftime('%H', time.strptime(X,'%a %b %d %H:%M:%S +0000 %Y'))
   
   data_tweet.at[i,'Year']=pd.to_numeric(Y1)
   
   data_tweet.at[i,'Month']=pd.to_numeric(Y2)
   
   data_tweet.at[i,'Day']=pd.to_numeric(Y3)
   
   data_tweet.at[i,'Hour']=pd.to_numeric(Y4)
   
   YY= time.strftime('%Y%m%d%H', time.strptime(X,'%a %b %d %H:%M:%S +0000 %Y'))
   
   data_tweet.at[i,'Time hour']=pd.to_numeric(YY)

data_tweet.drop(['Time'], axis=1, inplace=True)

data_tweet['time']=df['Time']

data_tweet=data_tweet.sort_values(by=['time'])

data_tweet.head(10)


   ![date_](https://user-images.githubusercontent.com/66491004/208567989-2bc3ad90-3cb5-4deb-89d9-7bd4585a7842.png)

#################### Mixing days/hours: text

#daily

data_tweet.drop(['id','user_followers_count','user_followee_count','lang','user_location',"Month","Day",'Hour','Year','Time hour'], axis=1, inplace=True)

data_tweet21 = data_tweet.groupby(["Month","Day",'Hour']).sum()

data_tweet21 = data_tweet.groupby(['time']).sum()

data_tweet21.head()

data_tweet2['text'][20170825]

#hourly

data_tweet=data_tweet3

data_tweet2=data_tweet4

data_tweet.drop(['id','user_followers_count','user_followee_count','lang','user_location',"Month","Day",'Hour','Year','time'], axis=1, inplace=True)

data_tweet1 = data_tweet.groupby(['Time hour']).sum()

data_tweet1.head()



####################  Text cleaning

import nltk

nltk.download('stopwords')

import re

import pandas as pd

import nltk

import string

from nltk.corpus import stopwords

#from nltk.tokenize import RegexpTokenizer

from nltk.tokenize import regexp

from nltk.stem import WordNetLemmatizer

from nltk.stem.porter import PorterStemmer

#import docx

#import docx2txt

ALL_Data['texte_cleaned']=''

#result = docx2txt.process("C:/Users/JabV/Desktop/DAta Cleaned/RD  monthly/Real/SF/7 July.docx")



def remove_html(text):

    """Remove special patterns - email, url, date etc."""
    
    email_regex = re.compile(r"[\w.-]+@[\w.-]+")
    
    url_regex = re.compile(r"(http|www)[^\s]+")
    
    date_regex = re.compile(r"[\d]{2,4}[ -/:]*[\d]{2,4}([ -/:]*[\d]{2,4})?") # a way to match date
    
    ## remove
    
    text = url_regex.sub("", text)
    
    text = email_regex.sub("", text)
    
    text = date_regex.sub("", text)
    
    return text


def remove_punctuation(text):

    no_punct="".join([c for c in text if c not in string.punctuation])
    
    return no_punct


#1 No tokenize

#tokenized_text=result2.lower()

#2 Tokenize

word_tokenizer = regexp.WhitespaceTokenizer()

#tokenized_text = [word.lower() for word in word_tokenizer.tokenize(result2)]


def remove_stopwords(text):

    words=[w for w in text if w not in stopwords.words('english')]
    
    return words

  
stemmer=PorterStemmer()

def word_stemmer(text):
  
    stem_text=" ".join([stemmer.stem(i) for i in text])
   
    return stem_text


for i in range(ALL_Data.shape[0]):
 
  j=ALL_Data.index[i]
  
  result=ALL_Data['text'][j]
  
  result1=remove_html(result)
  
  result2=remove_punctuation(result1)
  
  tokenized_text = [word.lower() for word in word_tokenizer.tokenize(result2)]
  
  result3=remove_stopwords(tokenized_text)
  
  result4=word_stemmer(result3)
  
  ALL_Data.at[j,'texte_cleaned']=result4

ALL_Data.head()

#mydoc = docx.Document()

#mydoc.add_paragraph(result4)

#mydoc.save("C:/Users/JabV/Desktop/DAta Cleaned/RD  monthly/Real/SF/7 July.docx")

   
