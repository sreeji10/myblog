---
title: "TFIDF keyword extractor deployed using Streamlit"
description: "compute top 5 tfidf keywords using tfidf & deployed using streamlit"
image: "images/post/post-6.jpeg"
date: 2022-01-25T18:19:25+06:00
categories: ["programming", "python"]
type: "featured" # available types: [featured/regular]
draft: false
---

TF-IDF stands for "Term Frequency–Inverse Document Frequency, is a numerical statistic that is intended to reflect how important a word is to a document in a collection or corpus. </br>
tf–idf value increases proportionally to the number of times a word appears in the document and is offset by the number of documents in the corpus that contain the word


#### Using Scikit learn library to compute tfidf scores on our training data.
-For this demo we will use Stackover posts related dataset which is available at archive.org
-Dataset is in XML format &comes out to be about 156 MB size.
```console
!wget https://archive.org/download/stackexchange/cs.stackexchange.com.7z/Posts.xml
```

#### Load the dataset using Pandas
```python
import pandas as pd
import re

data = pd.read_xml("Posts.xml")
data = data.Body #we are taking on the text body
data.fillna('', inplace=True)
```

#### Preprocess to remove unwanted tags
```python
def pre_process(text):
	'''Preprocess input text'''

	text=text.lower()
	text=re.sub("</?.*?>"," <> ",text) #remove html tags
	text=re.sub("(\\d|\\W)+"," ",text) # remove special characters and digits
	text = text.strip() #remove blank characters
	return text

data = data.apply(lambda x: pre_process(x))
```

#### Compute TF-IDF using Sklearn
```python
from sklearn.feature_extraction.text import TfidfVectorizer
tfidf_vectorizer = TfidfVectorizer(use_idf=True,max_df=0.7)
tfidf_vectorizer_vectors = tfidf_vectorizer.fit_transform(data)
```

#### Store the TF-IDF values for later use
```python
with open('tfidf.pickle', 'wb') as f:
    pickle.dump(tfidf_vectorizer, f, pickle.HIGHEST_PROTOCOL)
```


#### Now lets utilize Streamlit to create a UI
```python
#import necessary libraries
import streamlit as st
import pandas as pd
import pickle
import re
from sklearn.feature_extraction.text import TfidfVectorizer

#Setting up Streamlit configurations
st.set_page_config(layout='wide', initial_sidebar_state='expanded')
st.title('Keyword extraction using TFIDF')
st.markdown('Display top 5 keywords')
Text = st.text_input('Enter the sentence & press enter key')


@st.cache(allow_output_mutation=True)
def load():
	''' Load the calculated TFIDF weights'''

	data = None
	with open('tfidf.pickle', 'rb') as f:
		data = pickle.load(f)
	return data


def pre_process(text):
	'''Preprocess input text'''

	text=text.lower()
	text=re.sub("</?.*?>"," <> ",text) #remove html tags
	text=re.sub("(\\d|\\W)+"," ",text) # remove special characters and digits
	text = text.strip() #remove blank characters
	return text


def process(tfidf_vectorizer, text):
	'''Compute the Top 5 TFIDF scores'''

	if text is not None and text != '' and text != ' ':
		txt = tfidf_vectorizer.transform([text])
		df = pd.DataFrame(txt.T.todense(), index=tfidf_vectorizer.get_feature_names_out(), columns=["tfidf"])
		print(df)
		if len(text) >= 5:
			df = df.sort_values(by=["tfidf"],ascending=False)[:5]
		else:
			df = df.sort_values(by=["tfidf"],ascending=False)[:len(text)]
		return df
	return ''


def run():
	tfidf_vectorizer = load()
	text = pre_process(Text)
	val = process(tfidf_vectorizer, text)
	print(val, Text)
	st.write(val)

if __name__ == '__main__':
	run()
```

To check out a live demo, pls visit 
<a href="https://share.streamlit.io/sreeji10/tfidf-keyword-extractor-streamlit/main/src/streamlit_tfidf_keywordExtractor.py" target="_blank">here</a>