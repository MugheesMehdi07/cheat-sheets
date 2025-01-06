# Retrieval-Augmented Generation (RAG) Cheatsheet

RAG (Retrieval-Augmented Generation) is a technique for enhancing the capabilities of language models by combining them with a retrieval system. It retrieves relevant documents or data to provide context for the generation, improving accuracy and relevance.

---

## Key Components of RAG

### 1. **Retrieval System**
A system to search and fetch relevant information from a document store or database.

#### Example Tools:
- **Vector Databases**: Pinecone, Weaviate, FAISS
- **Traditional Search Engines**: Elasticsearch, Solr

### 2. **Document Store**
A repository where your documents are stored and indexed for efficient retrieval.

### 3. **Language Model**
An LLM like OpenAI GPT, Cohere, or Anthropic Claude processes the retrieved documents and generates a response.

---

## Steps to Implement RAG

### Step 1: Document Preprocessing
Prepare your documents for retrieval by cleaning and splitting them into chunks.

#### Code Example:
```python
from sklearn.feature_extraction.text import TfidfVectorizer

# Sample documents
documents = ["Document 1 content", "Document 2 content"]

# Preprocessing using TF-IDF
vectorizer = TfidfVectorizer()
tfidf_matrix = vectorizer.fit_transform(documents)
```

### Step 2: Create an Embedding and Index
Generate embeddings for your document chunks and store them in a vector database.

#### Code Example:
```python
from sentence_transformers import SentenceTransformer
import numpy as np

# Load a pre-trained model
model = SentenceTransformer('all-MiniLM-L6-v2')

# Generate embeddings
embeddings = model.encode(documents)

# Store in a NumPy array or vector database
vector_database = np.array(embeddings)
```

### Step 3: Query the Vector Database
Use a user query to fetch relevant chunks.

#### Code Example:
```python
from scipy.spatial.distance import cosine

query = "Explain the concept of RAG"
query_embedding = model.encode([query])[0]

# Find the closest document
closest_idx = np.argmin([cosine(query_embedding, doc) for doc in vector_database])
retrieved_doc = documents[closest_idx]
print(retrieved_doc)
```

### Step 4: Pass Retrieved Data to the Language Model
Combine the query with retrieved data and send it to the LLM.

#### Code Example:
```python
import openai

# OpenAI API call
response = openai.Completion.create(
    engine="text-davinci-003",
    prompt=f"Context: {retrieved_doc}\nQuestion: {query}\nAnswer:",
    max_tokens=150
)
print(response["choices"][0]["text"].strip())
```

---

## Integrating RAG into Existing LLM Applications

### 1. **Embedding Existing Workflows**
You can embed RAG in your current LLM app by replacing the static context with dynamically retrieved documents.

#### Code Example:
```python
context = f"Context: {retrieved_doc}\n"
user_input = "What is RAG?"
prompt = context + user_input

# OpenAI API call
response = openai.Completion.create(
    engine="text-davinci-003",
    prompt=prompt,
    max_tokens=100
)
print(response["choices"][0]["text"].strip())
```

### 2. **Combining RAG with Chatbots**
Enhance chatbots by adding retrieval to provide accurate and up-to-date responses.

#### Code Example:
```python
conversation_history = []
def chatbot_response(user_query):
    query_embedding = model.encode([user_query])[0]
    closest_idx = np.argmin([cosine(query_embedding, doc) for doc in vector_database])
    context = documents[closest_idx]

    prompt = f"Context: {context}\nUser: {user_query}\nChatbot:"
    response = openai.Completion.create(
        engine="text-davinci-003",
        prompt=prompt,
        max_tokens=100
    )
    answer = response["choices"][0]["text"].strip()
    conversation_history.append((user_query, answer))
    return answer

print(chatbot_response("Explain RAG"))
```

---

## Advanced RAG Use Cases

### 1. **Using External APIs for Retrieval**
Combine APIs like Google Search or Wikipedia with RAG to fetch live data.

#### Code Example:
```python
import requests

# Fetch data from Wikipedia API
response = requests.get("https://en.wikipedia.org/w/api.php", {
    "action": "query",
    "format": "json",
    "titles": "Retrieval-Augmented_Generation",
    "prop": "extracts",
    "explaintext": True
})
data = response.json()
print(data)
```

### 2. **Hybrid Retrieval**
Combine vector search and traditional keyword search for better results.

#### Code Example:
```python
from sklearn.metrics.pairwise import cosine_similarity

# Combine TF-IDF and embeddings
tfidf_query_vector = vectorizer.transform([query])
similarity_scores = cosine_similarity(tfidf_query_vector, tfidf_matrix)
hybrid_scores = similarity_scores[0] + [1 - cosine(query_embedding, doc) for doc in vector_database]

best_match_idx = np.argmax(hybrid_scores)
print(documents[best_match_idx])
```

### 3. **Multi-Document Summarization**
Summarize multiple retrieved documents to generate concise outputs.

#### Code Example:
```python
from transformers import pipeline

summarizer = pipeline("summarization")
retrieved_docs = [documents[i] for i in [0, 1, 2]]
summary = summarizer(" ".join(retrieved_docs), max_length=100, min_length=25, do_sample=False)
print(summary[0]["summary_text"])
```

---

## Best Practices

- **Optimize Chunks**: Ensure chunks are not too large to fit within the LLM’s context window.
- **Index Regularly**: Rebuild your vector index periodically for dynamic data.
- **Fine-Tune Models**: Fine-tune LLMs on domain-specific data for better performance.
- **Combine with Memory**: Use memory for conversational applications to maintain context.

---
