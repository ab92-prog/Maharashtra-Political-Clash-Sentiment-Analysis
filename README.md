# Maharashtra-Political-Clash-Sentiment-Analysis
I have scrapped data from news API on the Verdict of Honorable Supreme Court on the Maharashtra political Condition . I have tried to create an easy model of sentiment Analysis
Absolutely, you can include the code snippet and explanation in your README file to help others understand how to perform sentiment analysis on news articles using TextBlob and the NewsAPI. Here's how you can structure it in your README:

## Sentiment Analysis of News Articles using TextBlob

This code snippet demonstrates how to perform sentiment analysis on a set of news articles using the TextBlob library and data obtained from the NewsAPI. Sentiment analysis helps us understand the emotional tone conveyed in the articles, whether it's positive, negative, or neutral.

### Installation

Before getting started, ensure you have the required libraries installed. You can do this using pip:

```bash
pip install newsapi-python textblob
```

### Code Explanation

1. **Import Required Libraries:**

```python
import requests
import re
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import WordNetLemmatizer
from textblob import TextBlob
```

2. **Define NewsAPI Endpoint and Parameters:**

```python
url = "https://newsapi.org/v2/everything"
params = {
    "q": "Supreme Court verdict on Maharashtra Political Crisis",
    "language": "en",
    "sortBy": "relevancy",
    "apiKey": "YOUR_NEWSAPI_API_KEY"
}
```

3. **Make a Request to NewsAPI:**

```python
response = requests.get(url, params=params)
articles = response.json()["articles"]
```

4. **Preprocess Text:**

```python
def preprocess_text(text):
    text = text.lower()
    text = re.sub(r"[^a-zA-Z0-9\s]", "", text)
    text = re.sub(r"\s+", " ", text)
    words = word_tokenize(text)
    words = [word for word in words if word not in stopwords.words("english")]
    lemmatizer = WordNetLemmatizer()
    words = [lemmatizer.lemmatize(word) for word in words]
    preprocessed_text = " ".join(words)
    return preprocessed_text

preprocessed_articles = []
for article in articles:
    text = article["description"]
    preprocessed_text = preprocess_text(text)
    preprocessed_articles.append(preprocessed_text)
```

5. **Perform Sentiment Analysis:**

```python
sentiment_scores = []
for article in preprocessed_articles:
    blob = TextBlob(article)
    sentiment_scores.append(blob.sentiment.polarity)
```

6. **Print Sentiment Scores:**

```python
for i, score in enumerate(sentiment_scores):
    print(f"Article {i+1} Sentiment Score: {score}")
```

This code snippet showcases the sentiment analysis process using TextBlob on a collection of news articles, allowing you to gauge the overall sentiment conveyed in the articles. Replace `YOUR_NEWSAPI_API_KEY` with your actual NewsAPI API key.

Feel free to use and modify this code to analyze sentiments in your own datasets of news articles.

---

Feel free to include this comprehensive code explanation in your README file to provide others with a clear understanding of how to utilize the provided code snippet for sentiment analysis.
