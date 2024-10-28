
## 1. NLP with Python - Cheat Sheet  

### a. Importing Libraries  
```python
import numpy as np
import pandas as pd
import nltk
from nltk.tokenize import word_tokenize, sent_tokenize
from nltk.corpus import stopwords, wordnet
from sklearn.feature_extraction.text import CountVectorizer, TfidfVectorizer
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import MultinomialNB
from sklearn.metrics import classification_report, confusion_matrix, accuracy_score
import re
```

---

### 2. Text Preprocessing  

#### a. Tokenization  
- **Word Tokenization**: Splits text into individual words.
    ```python
    text = "Natural Language Processing is amazing!"
    word_tokens = word_tokenize(text)
    print(word_tokens)
    ```
- **Sentence Tokenization**: Splits text into sentences.
    ```python
    sent_tokens = sent_tokenize(text)
    print(sent_tokens)
    ```

#### b. Stopword Removal  
- **Use**: Removes common words that do not contribute to the meaning (e.g., 'is', 'the').
    ```python
    nltk.download('stopwords')
    stop_words = set(stopwords.words('english'))
    filtered_tokens = [w for w in word_tokens if w.lower() not in stop_words]
    ```

#### c. Lemmatization  
- **Use**: Reduces words to their base form.
    ```python
    from nltk.stem import WordNetLemmatizer
    nltk.download('wordnet')
    lemmatizer = WordNetLemmatizer()
    print(lemmatizer.lemmatize("running", pos='v'))  # 'run'
    ```

#### d. Regular Expression Cleaning  
- **Remove Special Characters and Numbers**:  
    ```python
    cleaned_text = re.sub(r'[^a-zA-Z\s]', '', text)
    print(cleaned_text)
    ```

---

### 3. Text Representation  

#### a. Bag of Words (BoW)  
- **Use**: Converts text into a frequency-based matrix.
    ```python
    vectorizer = CountVectorizer()
    X = vectorizer.fit_transform(["I love NLP", "NLP is cool"])
    print(X.toarray())
    ```

#### b. TF-IDF (Term Frequency-Inverse Document Frequency)  
- **Use**: Weighs terms based on their importance across multiple documents.
    ```python
    tfidf = TfidfVectorizer()
    X_tfidf = tfidf.fit_transform(["I love NLP", "NLP is cool"])
    print(X_tfidf.toarray())
    ```

---

### 4. NLP Models  

#### a. Sentiment Analysis using Naive Bayes  
- **Use**: Classifies text as positive/negative sentiment.
    ```python
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
    model = MultinomialNB()
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    print(accuracy_score(y_test, predictions))
    ```

#### b. Named Entity Recognition (NER)  
- **Use**: Detects entities like names, dates, etc.
    ```python
    import spacy
    nlp = spacy.load("en_core_web_sm")
    doc = nlp("Apple is looking at buying U.K. startup for $1 billion.")
    for ent in doc.ents:
        print(ent.text, ent.label_)
    ```

---

### 5. Word Embeddings  

#### a. Word2Vec  
- **Use**: Converts words into dense vectors.
    ```python
    from gensim.models import Word2Vec
    sentences = [["I", "love", "NLP"], ["NLP", "is", "fun"]]
    model = Word2Vec(sentences, vector_size=50, window=2, min_count=1, workers=4)
    print(model.wv['NLP'])
    ```

#### b. GloVe  
- **Use**: Pre-trained word embeddings.
    ```python
    !wget http://nlp.stanford.edu/data/glove.6B.zip
    ```

---

### 6. Transformers  

#### a. Text Generation with GPT-2  
- **Use**: Generate text based on input.
    ```python
    from transformers import GPT2Tokenizer, GPT2LMHeadModel
    tokenizer = GPT2Tokenizer.from_pretrained("gpt2")
    model = GPT2LMHeadModel.from_pretrained("gpt2")
    input_ids = tokenizer.encode("Once upon a time", return_tensors="pt")
    output = model.generate(input_ids, max_length=50)
    print(tokenizer.decode(output[0], skip_special_tokens=True))
    ```

#### b. Sentiment Classification with BERT  
- **Use**: Classifies text using BERT.
    ```python
    from transformers import pipeline
    sentiment_pipeline = pipeline("sentiment-analysis")
    result = sentiment_pipeline("I love NLP!")
    print(result)
    ```

---

### 7. Model Evaluation  

#### a. Confusion Matrix  
- **Use**: Shows predicted vs actual labels.
    ```python
    cm = confusion_matrix(y_test, predictions)
    print(cm)
    ```

#### b. Classification Report  
- **Use**: Displays precision, recall, F1-score.
    ```python
    print(classification_report(y_test, predictions))
    ```

---

### 8. NLP Libraries Overview  

| Library    | Purpose                       | Example Use Case               |
|------------|-------------------------------|--------------------------------|
| **nltk**   | Preprocessing & Tokenization  | Lemmatization, Tokenization    |
| **spaCy**  | Advanced NLP tasks            | NER, Dependency Parsing       |
| **gensim** | Word Embeddings               | Word2Vec, Topic Modeling      |
| **transformers** | Transformer models      | BERT, GPT-2, Text Generation  |

---

