---
mindmap-plugin\: 
excalidraw-plugin:
---


### **1️⃣ Introduction & Purpose**


#### **Why this playlist?**

- Many people starting with Generative AI hear about **LangChain** early in the process.
    
- This playlist is aimed to **teach LangChain step by step**, covering both:
    
    - **What will be taught** (Curriculum)
        
    - **How and when videos will be released** (Schedule)
        

---

### **2️⃣ Recap of Generative AI Curriculum**

#### **Two Major Sides of Generative AI:**

|**Side**|**Description**|
|---|---|
|**Builder Side**|Involves building foundation models (transformers, pretraining, fine-tuning, optimization)|
|**User Side**|Building applications **using** foundation models|

- The **LangChain playlist** belongs to the **User Side**.
    
---

### **3️⃣ User Side Focus**

Key skills for user side:

- **Building LLM Applications**
    
- **Improving LLM Responses**
    
    - Prompt Engineering
        
    - Retrieval-Augmented Generation (RAG)
        
    - Fine-tuning
        
- **Learning Agentic AI**
    
- **Exploring LLM Ops**
    
- **Miscellaneous Application Development**
    

The **LangChain playlist** is the **starting point** to cover all these areas gradually.

---

## **4️⃣ What is LangChain?**

LangChain is:

- An **Open Source Framework** to build **LLM-based applications**.
    
- Helps create **chatbots, question-answering systems, RAG apps, autonomous agents**, and more.
    
- Provides **modular components** and **end-to-end tools** for developers.
    

---

### **5️⃣ Core Features of LangChain**

|**Feature**|**Details**|
|---|---|
|**LLM Support**|Supports **all major LLMs** (OpenAI GPT, Anthropic Claude, Google models, etc.). Both **open-source** and **closed-source**.|
|**Simplifies Development**|Provides **chains**, **wrappers**, and **components** to build complex applications easily.|
|**Multiple Integrations**|Integrates with **databases**, **remote data sources**, **APIs**, etc., reducing boilerplate code.|
|**Free & Open Source**|Actively developed, with multiple versions released in a short time.|
|**Covers Major Use Cases**|Chatbots, RAG apps, AI agents—all can be built with LangChain.|

---

### **6️⃣ Why Start with LangChain?**

LangChain serves as a **holistic entry point** because:

- It **touches almost every part of the user side ecosystem**:
    
    - LLM API usage (both open & closed source)
        
    - HuggingFace & Ollama integrations
        
    - Prompt Engineering exposure
        
    - RAG application building
        
    - Agent development
        
    - LLM Ops introduction
        

By learning LangChain first, you get a **broad practical exposure** to other Gen AI topics.

---

## **7️⃣ Curriculum of the Playlist**

The LangChain playlist is **divided into 3 main parts**:

### **Part 1: Fundamentals**

|**Video**|**Topic**|
|---|---|
|1|**What is LangChain?** (Overview + Why it’s needed)|
|2|**LangChain Components Overview**|
|3|**Working with Models** (Integration & Responses)|
|4|**Prompt Management & Techniques**|
|5|**Parsing LLM Outputs**|
|6|**Runnables & LCEL (LangChain Expression Language)**|
|7|**Advanced Prompting & Techniques**|
|8|**Integrating Memory in Chatbots**|

---

### **Part 2: Building RAG Applications**

|**Step**|**Topic**|
|---|---|
|1|**Document Loaders**|
|2|**Text Splitters**|
|3|**Embeddings**|
|4|**Vector Databases**|
|5|**Retrievers**|
|6|**Building a RAG Application from Scratch**|

---

### **Part 3: Building AI Agents**

|**Step**|**Topic**|
|---|---|
|1|**Tools & Toolkits**|
|2|**Tool Calling Concept**|
|3|**Creating an AI Agent End-to-End**|

---

## **8️⃣ Playlist Scope and Focus**

### **Coverage:**

- Planned: **17 Videos**
    
- Each video will be **30–40 minutes** (detailed and conceptual)
    
- Focus is on **LangChain v3** (Latest Version)
    

### **Goals:**

- Provide **updated information** (LangChain 3.x, not older versions like 0.x or 1.x).
    
- Ensure **conceptual clarity**, not just coding.
    
- Teach **under-the-hood mechanics**, so learners can adapt to future versions.
    
- Cover **80% of LangChain’s most useful features**.
    
- Additional content may be added if required.
    

---

## **9️⃣ Timeline & Release Plan**

|**Plan**|**Details**|
|---|---|
|**Start**|Within a day from the announcement|
|**Frequency**|**2 videos per week**|
|**Duration**|**8 weeks (Approx. 2 months)**|

Other projects (like **PyTorch playlist** and **builder side content**) will run in parallel.

---

## **🔟 Final Thoughts**

- Nitesh emphasizes **curiosity as his primary motivation**.
    
- LangChain is chosen because it’s **empowering**—once learned, you can build real human-facing applications.
    
- Learners are encouraged to share the playlist and help friends learn LangChain too.
    

---

## Introduction to LangChain

- LangChain is an **open-source framework for developing applications powered by LLMs (Large Language Models)**.
    
- It helps developers build LLM-powered apps by providing tools to **orchestrate complex workflows**.
    
- The video covers:
    
    - **What is LangChain?**
        
    - **Why do we need LangChain?**
        
    - **What can you build with LangChain?**
        
    - **Other alternatives to LangChain**
        

---

# LangChain: Components 
quick overview of LangChain’s **six core components**:

1. **Models**
    
2. **Prompts**
    
3. **Chains**
    
4. **Memory**
    
5. **Indexes**
    
6. **Agents**


### Models 

LangChain lets you **combine multiple models**—LLMs, embeddings, tools—into seamless pipelines.
#### Translation + Summarization Pipeline

Use **LLM 1** for translation and **LLM 2** for summarization.

```python
from langchain.chat_models import ChatOpenAI
from langchain.prompts import ChatPromptTemplate
from langchain.chains import SimpleSequentialChain
from langchain_core.output_parsers import StrOutputParser

# Translation Chain
translator = ChatOpenAI(model_name="gpt-3.5-turbo")
translation_prompt = ChatPromptTemplate.from_template("Translate this to Hindi:\n{input}")


translation_chain = translation_prompt | translator | StrOutputParser()


# Summarization Chain
summarizer = ChatOpenAI(model_name="gpt-3.5-turbo")
summarization_prompt = ChatPromptTemplate.from_template("Summarize in less than 100 words:\n{input}")



summarization_chain = summarization_prompt | summarizer | StrOutputParser()



# Sequential Chain
full_chain = SimpleSequentialChain(chains=[translation_chain, summarization_chain])


result = full_chain.run("Large language models are transforming AI by enabling complex interactions with text data.")
print(result)
```

---

| Feature                  | Benefit                                                             |
| ------------------------ | ------------------------------------------------------------------- |
| **Standardized API**     | Use different models (OpenAI, Anthropic, etc.) in the same pipeline |
| **Composable Chains**    | Easily build multi-step workflows                                   |
| **Minimal Code Changes** | Switch models by changing just the model name                       |

###🔗 Complete Sequential Progression**

#### **1️⃣ Simple LLM Call**

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-3.5-turbo", temperature=0)
response = llm.invoke("What is LangChain?")
print(response.content)
```

---

#### **2️⃣ Use PromptTemplate**

```python
from langchain.prompts import PromptTemplate

template = "Explain {concept} in simple terms."
prompt = PromptTemplate(template=template, input_variables=["concept"])

final_prompt = prompt.format(concept="Retrieval Augmented Generation")
print(final_prompt)
```

---

#### **3️⃣ Use LLMChain (Prompt + LLM Together)**

```python
from langchain.chains import LLMChain

chain = LLMChain(llm=llm, prompt=prompt)

result = chain.invoke({"concept": "Embeddings in AI"})
print(result["text"])
```

---

#### **4️⃣ Use SequentialChain (Multi-Step Workflow)**

```python
from langchain.chains import SequentialChain

# First chain: summarize
prompt1 = PromptTemplate(
    template="Give a short summary of {topic}.",
    input_variables=["topic"]
)
chain1 = LLMChain(llm=llm, prompt=prompt1, output_key="summary")

# Second chain: expand summary
prompt2 = PromptTemplate(
    template="Expand this summary into 3 points:\n{summary}",
    input_variables=["summary"]
)
chain2 = LLMChain(llm=llm, prompt=prompt2, output_key="bullets")

# Sequential Chain
overall_chain = SequentialChain(
    chains=[chain1, chain2],
    input_variables=["topic"],
    output_variables=["summary", "bullets"]
)

output = overall_chain.invoke({"topic": "LangChain Memory"})
print(output)
```

---

#### **5️⃣ Add Vector Search + RAG Retrieval**

```python
from langchain_openai import OpenAIEmbeddings
from langchain.vectorstores import FAISS
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain.docstore.document import Document

texts = [
    "LangChain is a framework for building LLM-powered apps.",
    "Embeddings convert text into vectors for similarity search.",
    "Retrieval Augmented Generation combines search with LLMs."
]

docs = [Document(page_content=t) for t in texts]

splitter = RecursiveCharacterTextSplitter(chunk_size=100, chunk_overlap=0)
chunks = splitter.split_documents(docs)

embed_model = OpenAIEmbeddings()
vectorstore = FAISS.from_documents(chunks, embed_model)

query = "What is RAG?"
retrieved_docs = vectorstore.similarity_search(query)

context = "\n".join([doc.page_content for doc in retrieved_docs])

prompt_rag = PromptTemplate(
    template="Use the following context to answer:\n{context}\n\nQuestion: {question}",
    input_variables=["context", "question"]
)

rag_chain = LLMChain(llm=llm, prompt=prompt_rag)

rag_result = rag_chain.invoke({"context": context, "question": query})
print(rag_result["text"])
```

---


### Prompts

LangChain provides a **powerful prompt management system**.  
It helps create **dynamic, reusable, and structured prompts** for LLMs.

#### Why Are Prompts Important?

- LLM output is **highly sensitive** to the prompt
    
- Well-structured prompts produce **better, more controllable results**
    
- Reusability reduces code repetition and errors
    

#### Types of Prompts in LangChain

|Prompt Type|Purpose|
|---|---|
|Static Prompt|Fixed instructions|
|Dynamic Prompt|Use variables/placeholders|
|Few-Shot Prompt|Include examples to guide the model|
|Role-Based Prompt|Set roles using system prompts|

#### Example: Static Prompt

```python
from langchain.chat_models import ChatOpenAI
from langchain.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

llm = ChatOpenAI()
prompt = ChatPromptTemplate.from_template("Tell me a joke.")

chain = prompt | llm | StrOutputParser()
print(chain.invoke({}))
```

#### Example: Dynamic Prompt

```python
from langchain.chat_models import ChatOpenAI
from langchain.prompts import ChatPromptTemplate

llm = ChatOpenAI()

template = "Explain {topic} in a {tone} tone."
prompt = ChatPromptTemplate.from_template(template)

inputs = {"topic": "Quantum Computing", "tone": "funny"}

chain = prompt | llm | StrOutputParser()
print(chain.invoke(inputs))
```

#### Example: Role-Based Prompt

```python
from langchain.chat_models import ChatOpenAI
from langchain.prompts import ChatPromptTemplate

llm = ChatOpenAI()

template = """
You are an expert {profession}.
Answer the following question:
{question}
"""

prompt = ChatPromptTemplate.from_template(template)

inputs = {"profession": "doctor", "question": "What is viral fever?"}

chain = prompt | llm | StrOutputParser()
print(chain.invoke(inputs))
```

#### Example: Few-Shot Prompt

```python
from langchain.chat_models import ChatOpenAI
from langchain.prompts import FewShotChatMessagePromptTemplate, ChatPromptTemplate, SystemMessagePromptTemplate, HumanMessagePromptTemplate

examples = [
    {"input": "I was charged twice.", "output": "Billing Issue"},
    {"input": "App crashes on login.", "output": "Technical Issue"},
]

example_prompt = ChatPromptTemplate.from_messages([
    HumanMessagePromptTemplate.from_template("{input}"),
    SystemMessagePromptTemplate.from_template("{output}")
])

few_shot_prompt = FewShotChatMessagePromptTemplate(
    example_prompt=example_prompt,
    examples=examples
)

main_prompt = ChatPromptTemplate.from_messages([
    SystemMessagePromptTemplate.from_template("Classify customer support tickets."),
    few_shot_prompt,
    HumanMessagePromptTemplate.from_template("{input}")
])

llm = ChatOpenAI()
chain = main_prompt | llm | StrOutputParser()

print(chain.invoke({"input": "I need help upgrading my plan."}))
```

#### Prompt Components in LangChain

| Component                        | Use                      |
| -------------------------------- | ------------------------ |
| ChatPromptTemplate               | For chat models          |
| PromptTemplate                   | For text models          |
| FewShotChatMessagePromptTemplate | For few-shot learning    |
| MessagesPlaceholder              | For conversation history |

#### Benefits of LangChain Prompt System

- **Reusability**: Write once, use anywhere
    
- **Dynamic Injection**: Easily insert variables at runtime
    
- **Cleaner Pipelines**: Separate prompt logic from LLM calls
    
- **Better Control**: Structured prompt management reduces errors
    

#### Retrieval + Generation (RAG)

Use **embeddings for search**, then **LLM for answering**.

```python
from langchain.chat_models import ChatOpenAI
from langchain.embeddings import OpenAIEmbeddings
from langchain.vectorstores import FAISS
from langchain.chains import RetrievalQA
from langchain.document_loaders import TextLoader

# Load documents
loader = TextLoader("my_docs.txt")
documents = loader.load()

# Create vector DB
embeddings = OpenAIEmbeddings()
db = FAISS.from_documents(documents, embeddings)

# LLM
llm = ChatOpenAI(model_name="gpt-3.5-turbo")

# RetrievalQA Chain
retriever = db.as_retriever()
qa_chain = RetrievalQA.from_chain_type(llm=llm, retriever=retriever)

result = qa_chain.run("What is LangChain?")
print(result)
```


## Chains

A **Chain** in LangChain is a **pipeline of steps** where the output of one step becomes the input of the next.

### Why Use Chains?

- **Break complex tasks into stages**
    
- **Combine multiple models, tools, or functions**
    
- Simplify workflows like **translation → summarization → storage**
    
- Avoid writing glue code manually
    

### Types of Chains in LangChain

|Chain Type|Purpose|
|---|---|
|**SimpleSequentialChain**|Run steps one after another, passing outputs|
|**LLMChain**|LLM + Prompt + Output|
|**SequentialChain**|Run steps sequentially with **named inputs/outputs**|
|**RouterChain**|Route to different chains based on conditions|
|**CustomChain**|Create your own pipeline logic|

---

#### Example: Simple Sequential Chain

Use two models:  
**English → Hindi translation → Summarization**

```python
from langchain.chat_models import ChatOpenAI
from langchain.prompts import ChatPromptTemplate
from langchain.chains import SimpleSequentialChain
from langchain_core.output_parsers import StrOutputParser

# Translation Chain
translator = ChatOpenAI(model_name="gpt-3.5-turbo")
translation_prompt = ChatPromptTemplate.from_template("Translate this to Hindi:\n{input}")
translation_chain = translation_prompt | translator | StrOutputParser()

# Summarization Chain
summarizer = ChatOpenAI(model_name="gpt-3.5-turbo")
summarization_prompt = ChatPromptTemplate.from_template("Summarize this in less than 100 words:\n{input}")
summarization_chain = summarization_prompt | summarizer | StrOutputParser()

# Combine into one chain
full_chain = SimpleSequentialChain(chains=[translation_chain, summarization_chain])

result = full_chain.run("Large language models are transforming AI.")
print(result)
```

---

#### Visual Flow: Sequential Chain

```text
[ User Input ]
       |
       v
[ Translator LLM ]
       |
       v
[ Summarizer LLM ]
       |
       v
[ Final Output ]
```

---

#### Example: LLMChain

Use a **prompt + LLM + output parser** as a single chain.

```python
from langchain.chat_models import ChatOpenAI
from langchain.prompts import ChatPromptTemplate
from langchain.chains import LLMChain
from langchain_core.output_parsers import StrOutputParser

llm = ChatOpenAI()
prompt = ChatPromptTemplate.from_template("Write a poem about {topic} in {tone} tone.")

chain = LLMChain(
    llm=llm,
    prompt=prompt,
    output_parser=StrOutputParser()
)

result = chain.invoke({"topic": "stars", "tone": "funny"})
print(result)
```

---

#### How Chains Work Internally

|Component|Role|
|---|---|
|**Prompt**|Structure the input|
|**Model**|Generate or process|
|**Parser**|Extract useful output|
|**Chain**|Connect the above steps|

---

#### Benefits of Using Chains

- **Simplifies multi-step tasks**
    
- **Reusable components** (prompts, models, parsers)
    
- **Easily replace models** (switch OpenAI → Anthropic etc.)
    
- **Readable pipeline logic**
    

---

#### Recap Visual

```text
[ Input ]
   |
   v
[ Chain Step 1 ]
   |
   v
[ Chain Step 2 ]
   |
   v
[ Chain Step N ]
   |
   v
[ Output ]
```

---

## Indexes

**Indexes** in LangChain help you **store, search, and retrieve data** for LLM applications.  
They are commonly used in **RAG (Retrieval-Augmented Generation)** workflows.

### Why Use Indexes?

- LLMs have **limited context windows**
    
- Indexes allow you to **search large documents, databases, or knowledge bases**
    
- Improve LLM responses by feeding it **relevant, retrieved context**
    

---

### What Do Indexes Do?

|Function|Purpose|
|---|---|
|**Store**|Save documents or data as searchable chunks|
|**Embed**|Convert text into vector embeddings|
|**Search**|Retrieve relevant chunks based on a query|

---

### Core Index Components in LangChain

|Component|Purpose|
|---|---|
|**Document Loaders**|Load PDFs, web pages, CSVs, etc.|
|**Text Splitters**|Break large texts into manageable chunks|
|**Embeddings**|Convert text to numerical vectors|
|**Vector Stores**|Store and search embeddings|

---

#### Example Workflow: LangChain Index

```text
[ Load Documents ]
        |
        v
[ Split into Chunks ]
        |
        v
[ Create Embeddings ]
        |
        v
[ Store in Vector DB ]
        |
        v
[ Retrieve Relevant Chunks ]
        |
        v
[ Use LLM with Retrieved Context ]
```

---

#### Example: Create a Simple Index with FAISS

```python
from langchain.document_loaders import TextLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain.embeddings import OpenAIEmbeddings
from langchain.vectorstores import FAISS

# Load your document
loader = TextLoader("my_notes.txt")
documents = loader.load()

# Split text into chunks
splitter = RecursiveCharacterTextSplitter(chunk_size=500, chunk_overlap=50)
docs = splitter.split_documents(documents)

# Generate embeddings
embeddings = OpenAIEmbeddings()

# Create FAISS index (in-memory vector store)
db = FAISS.from_documents(docs, embeddings)
```

#### Example: Retrieve Context from the Index

```python
query = "What is quantum computing?"
retrieved_docs = db.similarity_search(query, k=3)

for doc in retrieved_docs:
    print(doc.page_content)
```

---

#### Use Case: RAG Pipeline

1. **User Query** →
    
2. **Retrieve relevant documents** →
    
3. **Send documents + query to LLM** →
    
4. **LLM answers using the retrieved context**
    

---

#### Example: RAG with RetrievalQA

```python
from langchain.chat_models import ChatOpenAI
from langchain.chains import RetrievalQA

llm = ChatOpenAI()

qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    retriever=db.as_retriever()
)

result = qa_chain.run("Tell me about quantum computing.")
print(result)
```

---

#### Supported Vector Stores in LangChain

|Vector Store|Usage|
|---|---|
|**FAISS**|In-memory, local vector search|
|**Pinecone**|Cloud vector DB|
|**Weaviate**|Open-source vector search|
|**Chroma**|Local and persistent DB|
|**Milvus**|Scalable vector DB|

---

#### Benefits of LangChain Indexes

- **Easily search large text datasets**
    
- **Plug and play with multiple vector DBs**
    
- **Combine retrieval with generation (RAG)**
    
- **Efficient document QA systems**
    

---

#### Visual Recap: LangChain Index Flow

```text
[ Documents ]
    |
    v
[ Split Chunks ]
    |
    v
[ Embedding Model ]
    |
    v
[ Vector Store (Index) ]
    |
    v
[ Query Input ]
    |
    v
[ Retrieve Relevant Chunks ]
    |
    v
[ LLM Answer with Context ]
```


## Memory

### What is Memory?

In **LangChain**, **Memory** allows an LLM application to:

- **Remember previous interactions**
    
- Maintain **context over multiple conversations**
    
- Simulate **stateful dialogues**, like real human conversations
    

---

### Why is Memory Needed?

### Problem:

LLMs like GPT are **stateless** → They don’t remember past inputs unless you send **all context again**.

### Solution:

LangChain **Memory** solves this by:

- **Storing prior interactions**
    
- Automatically feeding the past context into future prompts
    
- Allowing agents and chatbots to act **context-aware**
    

---

#### Key Features of LangChain Memory

|Feature|Description|Use Case|
|---|---|---|
|**Store History**|Keeps track of chat exchanges|Chatbots|
|**Summarization**|Compresses long chats into summaries|Long conversations|
|**Context Management**|Uses only recent chats if needed|Token limits|
|**Semantic Memory**|Stores embeddings for search-based recall|Knowledge Assistants|

---

### Types of LangChain Memory (With Examples)

---

#### 1️⃣ ConversationBufferMemory

##### **What it Does:**

- Stores the **entire conversation** as raw text
    
- Sends the **full history** to the LLM in every prompt
    

##### **When to Use:**

- For **short conversations**
    
- When you need **exact history recall**
    

##### **Example:**

```python
from langchain.memory import ConversationBufferMemory
from langchain.chains import ConversationChain
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI()

memory = ConversationBufferMemory()

conversation = ConversationChain(
    llm=llm,
    memory=memory
)

conversation.predict(input="Hi, I am Alice.")
conversation.predict(input="What is my name?")  
# LLM will remember: "Alice"
```

---

#### 2️⃣ ConversationSummaryMemory

##### **What it Does:**

- Uses an **LLM to summarize the conversation so far**
    
- Stores a **compact summary** instead of full history
    

##### **When to Use:**

- **Long conversations** where you want to **reduce token usage**
    

##### **How it Works:**

|Step|Action|
|---|---|
|User input|Stored|
|LLM|Summarizes history|
|Memory|Stores updated summary|

---

##### **Example:**

```python
from langchain.memory import ConversationSummaryMemory
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI()

memory = ConversationSummaryMemory(llm=llm)

# Now use this memory in your chains or agents
```


---

#### 3️⃣ ConversationBufferWindowMemory

##### **What it Does:**

- Stores only the **last N messages** (e.g., last 3 exchanges)
    
- Old messages are **forgotten**
    

##### **When to Use:**

- You want **recent context only**
    
- Need to **control memory size**
    

---

##### **Example:**

```python
from langchain.memory import ConversationBufferWindowMemory

memory = ConversationBufferWindowMemory(k=3)

# This will store only the last 3 interactions
```


---

#### 4️⃣ VectorStoreRetrieverMemory

##### **What it Does:**

- Stores **interactions as vector embeddings**
    
- Allows **semantic search** to retrieve related memories
    

---

##### **When to Use:**

- **Long-term memory**
    
- Knowledge base recall
    
- Semantic similarity search
    

---

##### **Example:**

```python
from langchain.memory import VectorStoreRetrieverMemory
from langchain.vectorstores import FAISS
from langchain.embeddings import OpenAIEmbeddings

# Set up FAISS as vector store
embedding = OpenAIEmbeddings()
vectorstore = FAISS(embedding.embed_query, FAISS.IndexFlatL2(1536))

memory = VectorStoreRetrieverMemory(retriever=vectorstore.as_retriever())

# Now the memory can retrieve relevant past events via semantic search
```

---

### Comparison of Memory Types

| Memory Type            | Stores              | Use Case            |
| ---------------------- | ------------------- | ------------------- |
| **BufferMemory**       | Full chat logs      | Short chatbots      |
| **SummaryMemory**      | Summarized chat     | Long-term convo     |
| **BufferWindowMemory** | Last N messages     | Recent context only |
| **VectorStoreMemory**  | Semantic embeddings | Knowledge recall    |

---

### Real-Life Use Cases

|Application|Memory Type|
|---|---|
|**AI Customer Support Bot**|BufferWindowMemory|
|**Personal AI Assistant**|SummaryMemory|
|**FAQ Knowledge Bot**|VectorStoreMemory|
|**Role-play AI Chatbot**|BufferMemory|

---

### Visual Workflow of LangChain Memory

```text
+------------------+
|   User Input     |
+------------------+
         |
         v
+------------------+
|   Memory Lookup  |
+------------------+
         |
         v
+------------------+
|   LLM Response   |
+------------------+
         |
         v
+------------------+
| Memory Update    |
+------------------+
```

## Agents 
### LLM + Tool Use (Agent)

Link **LLM reasoning** with **external tools** like a calculator.

```python
from langchain.chat_models import ChatOpenAI
from langchain.tools import tool
from langchain.agents import AgentExecutor, create_openai_functions_agent
from langchain import hub

@tool
def calculator(expression: str) -> str:
    return str(eval(expression))

prompt = hub.pull("hwchase17/openai-functions-agent")
llm = ChatOpenAI(model="gpt-3.5-turbo-0613")

agent = create_openai_functions_agent(llm, [calculator], prompt)
executor = AgentExecutor(agent=agent, tools=[calculator], verbose=True)

executor.invoke({"input": "What is 45 * 19? Explain the result."})
```

---


### Why Do We Need LangChain?

#### Real-Life Use Case Example

- **Idea from 2014-15**: Create a PDF reader app where users can **chat with their PDFs**.
    
- Users could:
    
    - Ask for simplified explanations of specific pages.
        
    - Generate true/false questions on topics.
        
    - Summarize content into notes.
        

#### High-Level System Design

1. **User uploads PDF** → Stored in cloud (e.g., AWS S3).
    
2. **User asks a query** → e.g., "What are the parts of linear regression?"
    
3. **Search Process**:
    
    - **Keyword Search**: Matches exact words but may return irrelevant pages.
        
    - **Semantic Search**: Understands the **meaning** of the query to find relevant sections.
        

#### Why Semantic Search?

- It provides **contextual results** instead of just keyword matches.
    
- Reduces computational overhead by narrowing down relevant content before querying the LLM.
    

---

### How Semantic Search Works

1. Convert **all paragraphs and user queries into embeddings (vectors)**.
    
2. Use techniques like:
    
    - Word2Vec
        
    - Doc2Vec
        
    - Sentence Transformers
        
3. Perform **vector similarity comparison** to find the most relevant chunks.
    

---

### Detailed System Architecture

#### Components Involved

- **Document Loader**: Loads PDFs from the cloud.
    
- **Text Splitter**: Breaks PDF into smaller chunks (pages, paragraphs, etc.).
    
- **Embedding Model**: Converts each chunk into numerical vectors (embeddings).
    
- **Vector Database**: Stores embeddings for retrieval.
    
- **LLM (Large Language Model)**: Handles user queries and generates contextual responses.
    

#### Workflow

1. **Upload Document** → Stored on cloud.
    
2. **Split Document** → Into manageable chunks.
    
3. **Create Embeddings** → For each chunk and store them.
    
4. **Query Embedding** → User query is also embedded.
    
5. **Similarity Search** → Find closest matching document chunks.
    
6. **Send to LLM** → Provide user query + relevant document chunks to LLM.
    
7. **Generate Response** → LLM processes the input and responds.
    

---

### Challenges in Building This System

#### Challenge 1: Understanding & Text Generation

- Earlier, building a system that understands queries and generates answers was difficult.
    
- Solved by modern LLMs (e.g., GPT, BERT, etc.).
    

#### Challenge 2: Computation and Hosting

- LLMs are **large and costly** to host and run.
    
- Solved by **LLM APIs** like OpenAI’s API or Anthropic's Claude.
    
- Pay-as-you-use model reduces infrastructure burden.
    

#### Challenge 3: Orchestration of Components

- Many moving parts:
    
    - Cloud storage
        
    - Text splitters
        
    - Embedding models
        
    - Databases
        
    - LLMs
        
- Building all the glue code is **time-consuming and error-prone**.
    
- **LangChain solves this by providing built-in orchestration** with minimal boilerplate.
    

---

### Why LangChain?

#### Key Benefits

1. **Chains**
    
    - Create pipelines of tasks where output of one step becomes input for the next.
        
    - Supports sequential, parallel, and conditional chains.
        
2. **Model Agnostic Development**
    
    - Easily swap between OpenAI, Google, or open-source models without changing the core code.
        
3. **Rich Ecosystem**
    
    - Multiple document loaders
        
    - Various text splitters
        
    - Several embedding models
        
    - Compatibility with many vector stores
        
4. **Memory & State Handling**
    
    - Maintains conversational memory.
        
    - Can handle context across multiple queries.
        

---

### What Can You Build Using LangChain?

#### 1. Conversational Chatbots

- Handle customer queries at scale.
    
- Acts as a **first layer of customer interaction** before escalating to human agents.
    

#### 2. AI Knowledge Assistants

- Chatbots that **also know your data**.
    
- Example: A campus chatbot that answers questions based on course videos or notes.
    

#### 3. AI Agents

- Chatbots that **perform actions**, not just conversations.
    
- Example: Booking a flight or hotel directly through an AI assistant.
    

#### 4. Workflow Automation

- Automate personal or company workflows using LLMs.
    
- For example: Summarizing emails, generating reports, etc.
    

#### 5. Research & Summary Helpers

- Summarize large documents or research papers.
    
- Use within organizations for **private, secure document processing**.
    

---

### The Future of LLM-Powered Applications

- Just like websites and mobile apps, **LLM-based apps will see massive growth**.
    
- LangChain is set to become a **key tool in this revolution**.
    

---

### Alternatives to LangChain

1. **LlamaIndex**
    
    - Popular for **data indexing and retrieval with LLMs**.
        
    - Also covered in courses and tutorials.
        
2. **Haystack**
    
    - Another open-source framework for **building search and conversational apps** with LLMs.
        

---

### Summary

- LangChain simplifies building LLM applications by handling:
    
    - Workflow orchestration
        
    - Model integration
        
    - Memory management
        
- It enables rapid development of chatbots, AI agents, workflow automations, and knowledge assistants.
    
- The ecosystem is rich and growing, making it easier to focus on ideas instead of boilerplate code.

# Rag-Architecure 
![[Pasted image 20250720103904.png]]
![[Langchain-3.png]]


### High-Level RAG Architecture

```
User Query → Retriever → Relevant Documents → LLM Generator → Final Answer
```

---

### Components & Descriptions

#### 1. **User Query (Input Layer)**

- User asks a question in natural language.
    
- Example: "Explain linear regression from my notes."
    

---

#### 2. **Retriever (Retrieval Layer)**

- Finds **relevant documents or chunks** from a knowledge base.
    
- Uses **semantic search** (vector similarity).
    
- Example tools: FAISS, Pinecone, Weaviate.
    

##### Sub-Components:

- **Document Store**
    
    - Stores pre-processed documents in vector format.
        
- **Embeddings**
    
    - Converts text into numerical vectors using models like OpenAI, Sentence Transformers.
        

---

#### 3. **Relevant Documents (Contextual Knowledge)**

- Retrieved text chunks that are **most related to the query**.
    
- These become **external knowledge** for the LLM.
    

---

#### 4. **LLM Generator (Generation Layer)**

- Large Language Model (e.g., GPT, Claude, Llama) generates the response.
    
- **Input**: User query + relevant documents.
    
- **Output**: Contextually accurate and fluent response.
    

---

#### 5. **Final Answer (Output Layer)**

- The LLM returns a **context-aware answer** that combines retrieval + generation.
    
- User receives a complete, coherent response.
    

---

### Optional Enhancements

|Component|Purpose|
|---|---|
|**Memory**|Stores past interactions for conversational continuity.|
|**Tools / Agents**|Perform actions beyond text generation (e.g., API calls).|
|**Feedback Loop**|Improve system via user ratings or corrections.|

---

### Diagram (Textual)

```
User Query
     │
     ▼
Retriever ──> Vector DB ──> Relevant Chunks
     │
     ▼
LLM Generator (RAG)
     │
     ▼
Final Answer
```

---

### Summary

**RAG = Retrieval + Generation**

- **Retriever**: Fetches knowledge.
    
- **Generator (LLM)**: Forms the final answer using that knowledge.
    
- **Advantage**: Gives **factual, grounded, and up-to-date responses** without retraining the LLM.
    

### What is LangChain?

Let me explain LangChain in one sentence:

**LangChain is an open-source framework to develop applications powered by LLMs (Large Language Models).**

If you are building an LLM-powered app, LangChain helps you easily integrate all the components needed for that application.

But just knowing this is not enough. To truly understand **what LangChain is**, we need to first understand **why LangChain is needed**.

---

### Why Do We Need LangChain?

Let me give you an example from my personal experience.

In **2014-2015**, I came up with an idea. At that time, smartphones became popular, and people started reading PDFs instead of physical books.  
So I thought:

**What if I build an app where users can upload PDFs, read them, and also chat with them?**

For example:

- Upload a machine learning book
    
- Ask: "Explain page 5 like I’m 5 years old."
    
- Ask: "Generate true/false questions for linear regression."
    
- Ask: "Create notes on the decision tree section."
    

This app would allow users not just to read PDFs but **converse with them.**

---

### High-Level System Design

Let’s understand how such an application works:

#### Step 1: PDF Upload

- User uploads a PDF to the system (stored on the cloud, e.g., AWS S3).
    

#### Step 2: User Query

- User asks a question like:  
    _"What are the parts of linear regression?"_
    

#### Step 3: Search for Relevant Information

There are two ways to search:

1. **Keyword Search** – Matches exact words.  
    Inefficient because it may return irrelevant pages.
    
2. **Semantic Search** – Understands the meaning of the query and retrieves the most relevant content.  
    Much more efficient for context-based queries.
    

---

### Why Not Use the Whole Book?

A valid question is:  
**Why don’t we send the entire PDF to the LLM?**

Answer: **Efficiency.**  
Just like a student asking a teacher for help on a specific page instead of handing over the entire book,  
giving the LLM the relevant pages reduces computational load and improves the quality of the answer.

---

### How Does Semantic Search Work?

1. **Chunk the PDF:**  
    Break the document into small parts (pages, paragraphs, etc.).
    
2. **Generate Embeddings:**  
    Convert each chunk into a vector (numerical format representing meaning) using models like Word2Vec, Sentence Transformers, etc.
    
3. **Store Vectors:**  
    Save embeddings in a vector database (e.g., FAISS, Pinecone).
    
4. **Query Embedding:**  
    Convert user’s question into a vector.
    
5. **Similarity Search:**  
    Compare the query vector with all stored vectors to find the most similar chunks.
    

---

### Building the "Brain"

The **brain** of this system has two responsibilities:

1. **Natural Language Understanding (NLU):**  
    Understand the query properly.
    
2. **Context-Aware Generation:**  
    Use the retrieved content to generate a relevant answer.
    

Thanks to **LLMs**, both these tasks are now easy because models like **GPT, Claude, LLaMA** already have these capabilities.

---

### Using LLM APIs Instead of Hosting LLMs

Deploying LLMs locally is expensive and complicated.

Solution: Use APIs provided by companies like **OpenAI**, **Anthropic**, or **Google**.  
This solves the computation and cost challenges because you pay as you use.

---

### Challenge: Orchestration

The major challenge in building LLM-powered apps is orchestrating multiple components:

- **Document Loader**
    
- **Text Splitter**
    
- **Embedding Generator**
    
- **Vector Database**
    
- **Retriever**
    
- **LLM API**
    

Writing code for this **from scratch** is difficult, especially when components change (e.g., swapping OpenAI with Google Palm).

---

### How LangChain Helps

LangChain provides:

#### 1. **Chains**

- Create pipelines where the **output of one step is the input to the next**.
    
- Supports **parallel chains**, **conditional chains**, and **complex workflows**.
    

---

#### 2. **Model Agnostic Development**

- Easily switch between models (OpenAI, Anthropic, Google, etc.)
    
- Plug-and-play architecture with minimal code change.
    

---

#### 3. **Built-in Components**

- **Document Loaders** (PDFs, text, cloud storage)
    
- **Text Splitters**
    
- **Embedding Interfaces**
    
- **Vector Store Interfaces**
    

---

#### 4. **Memory and State Handling**

- Maintains context across multiple user queries (conversation memory).
    
- Handles follow-up questions intelligently.
    

---

### Use Cases of LangChain

Here are **popular applications** built using LangChain:

#### 1. **Conversational Chatbots**

- Customer support
    
- Internet-based companies scale customer conversations using chatbots powered by LangChain.
    

---

#### 2. **AI Knowledge Assistants**

- Personalized Q&A systems for private data (company documents, courses, etc.).
    

---

#### 3. **AI Agents**

- Perform actions beyond chat, like **booking tickets, running workflows, or making API calls**.
    

---

#### 4. **Workflow Automation**

- Automate repetitive business tasks with LLMs and tools.
    

---

#### 5. **Research and Summarization Tools**

- Summarize large documents
    
- Build research helpers without uploading sensitive data to public platforms.
    

---

### Alternatives to LangChain

LangChain is not the only option. Here are other popular frameworks:

- **LlamaIndex**
    
- **Haystack**
    

Both are good alternatives depending on your specific use case and pricing considerations.

---

### Conclusion

We’ve learned:

- **What LangChain is**
    
- **Why it is needed**
    
- **What you can build with it**
    
- **Its alternatives**
    


