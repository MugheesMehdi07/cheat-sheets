# LangChain Cheatsheet

LangChain is a framework designed for developing applications powered by language models. It allows chaining together components like prompt templates, language models, memory, and more, making it easier to build robust and efficient AI applications.

---

## Key Concepts

### 1. **Prompt Templates**
Prompt templates allow you to standardize and reuse the input to your language model.

#### Code Example:
```python
from langchain.prompts import PromptTemplate

# Define a prompt template
template = "Translate the following English text to French: {text}"
prompt = PromptTemplate(
    input_variables=["text"],
    template=template
)

# Format the prompt
formatted_prompt = prompt.format(text="How are you?")
print(formatted_prompt)
# Output: Translate the following English text to French: How are you?
```

---

### 2. **Chains**
Chains are sequences of actions combining prompts, models, and outputs.

#### Code Example:
```python
from langchain.chains import SimpleSequentialChain
from langchain.prompts import PromptTemplate
from langchain.llms import OpenAI

# Define two prompts
prompt1 = PromptTemplate(input_variables=["text"], template="Summarize this: {text}")
prompt2 = PromptTemplate(input_variables=["summary"], template="What are the key takeaways from this summary: {summary}")

# Initialize LLM
llm = OpenAI(temperature=0)

# Create Chains
chain1 = LLMChain(llm=llm, prompt=prompt1)
chain2 = LLMChain(llm=llm, prompt=prompt2)

# Combine Chains
sequential_chain = SimpleSequentialChain(chains=[chain1, chain2])
result = sequential_chain.run("LangChain simplifies AI workflows.")
print(result)
```

---

### 3. **Memory**
Memory enables chains to remember information across calls, useful for chatbots or sequential tasks.

#### Code Example:
```python
from langchain.memory import ConversationBufferMemory
from langchain.chains import ConversationChain
from langchain.llms import OpenAI

# Initialize memory and LLM
memory = ConversationBufferMemory()
llm = OpenAI(temperature=0)

# Create conversation chain
conversation = ConversationChain(llm=llm, memory=memory)

# Simulate a conversation
conversation.predict(input="Hello, who are you?")
conversation.predict(input="What's my name?")

# The second response will consider the context of the first message.
```

---

### 4. **Tools and Agents**
Agents use tools to perform specific tasks like querying APIs, searching, or calculations.

#### Code Example:
```python
from langchain.agents import load_tools, initialize_agent
from langchain.llms import OpenAI

# Load tools
llm = OpenAI(temperature=0)
tools = load_tools(["serpapi", "calculator"])

# Initialize an agent
agent = initialize_agent(tools, llm, agent="zero-shot-react-description", verbose=True)

# Run a query
result = agent.run("What's the weather in New York and what is 5 times 7?")
print(result)
```

---

### 5. **Document Loaders and Indexes**
Load, parse, and index documents for question answering or retrieval-based tasks.

#### Code Example:
```python
from langchain.document_loaders import TextLoader
from langchain.indexes import VectorstoreIndexCreator

# Load a document
loader = TextLoader("example.txt")
documents = loader.load()

# Create an index
index = VectorstoreIndexCreator().from_documents(documents)

# Query the index
query = "What is LangChain?"
response = index.query(query)
print(response)
```

---

### 6. **Custom Chains**
Build custom logic by combining multiple components.

#### Code Example:
```python
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain
from langchain.llms import OpenAI

# Define prompt
prompt = PromptTemplate(
    input_variables=["name"],
    template="Write a poem about {name}."
)

# Create chain
llm = OpenAI(temperature=0.7)
chain = LLMChain(llm=llm, prompt=prompt)

# Run chain
result = chain.run("LangChain")
print(result)
```

---

## Advanced Topics

### 7. **Callbacks**
Callbacks allow monitoring and debugging during chain execution.

#### Code Example:
```python
from langchain.callbacks import StdOutCallbackHandler
from langchain.chains import SimpleSequentialChain

# Define callback
callback = StdOutCallbackHandler()

# Attach callback to chain
chain = SimpleSequentialChain(chains=[chain1, chain2], callbacks=[callback])
result = chain.run("LangChain helps build AI tools.")
```

---

### 8. **Async Support**
Run chains asynchronously for better performance in certain scenarios.

#### Code Example:
```python
import asyncio
from langchain.llms import OpenAI
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

async def async_chain():
    llm = OpenAI(temperature=0)
    prompt = PromptTemplate(
        input_variables=["question"],
        template="Answer concisely: {question}"
    )
    chain = LLMChain(llm=llm, prompt=prompt)
    result = await chain.apredict(question="What is LangChain?")
    print(result)

asyncio.run(async_chain())
```

---

### 9. **Integration with Other Tools**
LangChain integrates seamlessly with tools like Pinecone, Weaviate, and more for advanced workflows.

#### Example:
```python
from langchain.vectorstores import Pinecone
import pinecone

# Initialize Pinecone
pinecone.init(api_key="your-api-key", environment="your-environment")
index = Pinecone.from_existing_index("your-index-name")

# Use the index in LangChain
response = index.query("Explain LangChain.")
print(response)
```

---

### 10. **LangGraph**
LangGraph provides a visual representation of chains and workflows for debugging and optimization.

#### Code Example:
```python
from langchain.visualization import visualize_chain

# Visualize a chain
visualization = visualize_chain(sequential_chain)
visualization.render()
```

---

### 11. **LangSmith for Logging and Monitoring**
LangSmith helps track execution, logs, and performance metrics across workflows.

#### Code Example:
```python
from langchain.smith import LangSmith

# Initialize LangSmith logger
logger = LangSmith(log_file="chain_logs.json")

# Attach logger to chain
sequential_chain.add_logger(logger)
result = sequential_chain.run("Test input")

# View logs
print(logger.get_logs())
```
