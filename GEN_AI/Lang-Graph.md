**LangGraph** is a framework built on top of **LangChain** that helps you create **stateful, multi-step workflows** using **graphs**.

> LangGraph = LangChain + Graph-based control flow

It allows you to:

- Define **nodes** (LLMs, tools, chains)
    
- Define **edges** (how the flow moves between steps)
    
- Handle **loops**, **branches**, and **memory** easily

### Features
 ✅ **1. Graph-based Workflow Design**

Define workflows as directed graphs for better control and clarity.

✅ **2. Stateful Execution**

Maintains memory and state across steps and iterations.

✅ **3. Loops and Branching**

Easily implement conditional logic and loops in your flows.

 ✅ **4. Modular Node Architecture**

Each step (node) can be an LLM, function, or tool.

 ✅ **5. Deterministic & Debuggable**

Predictable control flow ideal for testing and production.

✅ **6. LangChain Integration**

Works seamlessly with LangChain components like tools and memory.

✅ **7. Multi-agent Support**

Design agents that interact with each other in structured workflows.


### Workflows 
#### Agentic Workflows vs LLm Workflows 
| Feature                   | **LLM Workflows**                       | **Agentic Workflows**                          |
| ------------------------- | --------------------------------------- | ---------------------------------------------- |
| **Structure**             | Fixed, sequential steps                 | Dynamic, decision-based steps                  |
| **Control Flow**          | Predefined (linear or branching)        | Controlled by agent's internal reasoning       |
| **Flexibility**           | Low – follows exact steps               | High – adapts based on context and input       |
| **Tool Usage**            | Pre-scripted tool calls                 | Agent decides which tools to use and when      |
| **State/Memory Handling** | Basic or optional                       | Actively used and updated across steps         |
| **Behavior**              | Deterministic (predictable)             | Non-deterministic (varies per run)             |
| **Use Cases**             | Simple tasks (summarize, translate, QA) | Complex tasks (search, planning, multi-hop QA) |
| **Example Flow**          | Input → LLM → Output                    | Input → Agent → Think → Act → Reflect → Output |
#### **Why Transition from Workflows to Graphs?**
##### 📌 In short:

> **Workflows** = Easy, but limited  
> **Graphs** = Flexible, scalable, and powerful for real-world LLM applications

## Graphs 

## State Graph 
In **LangGraph**, a **State** is the structured data that flows through the graph — it holds both input, intermediate, and output values across nodes. It is defined using a **Pydantic model**, and each field in the model represents a **trackable variable** in the workflow.
#### Minimal Example to Define State

```python
from langgraph.graph import StateGraph
from pydantic import BaseModel
from typing import Optional

# Step 1: Define your custom state
class MyState(BaseModel):
    input: str
    processed: Optional[str] = None
    result: Optional[str] = None
```

>  This `MyState` holds:

- `input`: required string input.
    
- `processed`: intermediate value.
    
- `result`: final output value.
    

---

#### Registering State in Graph

```python
# Step 2: Create a graph and pass state
graph = StateGraph(MyState)
```
#### Important Notes

- **All node functions** in the graph take and return a **dictionary of values**, **not** the Pydantic model itself.
    

```python
def my_node(state: dict) -> dict:
    text = state['input']
    return {"processed": text.upper()}
```

- The returned dict keys must match the field names in your state.
    
- Unreturned fields retain their old values.
    

---

#### Full Tiny Flow Example

```python
from langgraph.graph import StateGraph
from pydantic import BaseModel
from typing import Optional

class MyState(BaseModel):
    input: str
    processed: Optional[str] = None
    result: Optional[str] = None

def process_text(state: dict) -> dict:
    return {"processed": state["input"].upper()}

def finalize(state: dict) -> dict:
    return {"result": f"Final: {state['processed']}"}

graph = StateGraph(MyState)
graph.add_node("process", process_text)
graph.add_node("finalize", finalize)

graph.set_entry_point("process")
graph.add_edge("process", "finalize")

app = graph.compile()

# Run it
out = app.invoke({"input": "hello world"})
print(out)
```


Output:

```python
{'input': 'hello world', 'processed': 'HELLO WORLD', 'result': 'Final: HELLO WORLD'}
```

---

Want me to show `State` in a conditional flow, looping flow, or one with memory/tool use next?
## Sequential Chain 
### 1. Lang_Graph Sequential Flow with Intermediate States

```python
from pydantic import BaseModel, Field
from langgraph.graph import StateGraph

# 1. Complex State Definition
class BookingState(BaseModel):
    user_name: str = Field(default="")
    destination: str = Field(default="")
    travel_date: str = Field(default="")
    confirmation_message: str = Field(default="")

# 2. Node: Collect User Name
def collect_name(state: BookingState) -> BookingState:
    state.user_name = "Nitish"  # Simulated input
    print("\n🟢 After collect_name:")
    print(state)
    return state

# 3. Node: Collect Destination
def collect_destination(state: BookingState) -> BookingState:
    state.destination = "Manali"  # Simulated input
    print("\n🟡 After collect_destination:")
    print(state)
    return state

# 4. Node: Collect Travel Date
def collect_travel_date(state: BookingState) -> BookingState:
    state.travel_date = "2025-08-01"  # Simulated input
    print("\n🔵 After collect_travel_date:")
    print(state)
    return state

# 5. Node: Confirm Booking
def confirm_booking(state: BookingState) -> BookingState:
    state.confirmation_message = (
        f"Booking confirmed for {state.user_name} to {state.destination} on {state.travel_date}."
    )
    print("\n🟣 After confirm_booking:")
    print(state)
    return state

# 6. Build LangGraph
builder = StateGraph(BookingState)
builder.add_node("collect_name", collect_name)
builder.add_node("collect_destination", collect_destination)
builder.add_node("collect_date", collect_travel_date)
builder.add_node("confirm", confirm_booking)

# 7. Set Sequential Flow
builder.set_entry_point("collect_name")
builder.add_edge("collect_name", "collect_destination")
builder.add_edge("collect_destination", "collect_date")
builder.add_edge("collect_date", "confirm")

# 8. Compile and Run
graph = builder.compile()
print("🚀 Starting LangGraph Execution...")
final_state = graph.invoke(BookingState())

# 9. Final Output
print("\n✅ Final State Snapshot:")
print(final_state.json(indent=2))
```

####  Sample Output Walkthrough

```text
🚀 Starting LangGraph Execution...

🟢 After collect_name:
user_name='Nitish' destination='' travel_date='' confirmation_message=''

🟡 After collect_destination:
user_name='Nitish' destination='Manali' travel_date='' confirmation_message=''

🔵 After collect_travel_date:
user_name='Nitish' destination='Manali' travel_date='2025-08-01' confirmation_message=''

🟣 After confirm_booking:
user_name='Nitish' destination='Manali' travel_date='2025-08-01' confirmation_message='Booking confirmed for Nitish to Manali on 2025-08-01.'

✅ Final State Snapshot:
{
  "user_name": "Nitish",
  "destination": "Manali",
  "travel_date": "2025-08-01",
  "confirmation_message": "Booking confirmed for Nitish to Manali on 2025-08-01."
}
```
### 2. Job Application Builder
Simulating a chatbot that helps a user **build a job application** in 4 steps:

1. Collect **name**
    
2. Collect **job role**
    
3. Collect **skills**
    
4. Generate **application letter**
    

---

##### Code with Intermediate State Flow

```python
from pydantic import BaseModel, Field
from langgraph.graph import StateGraph

# 1. Complex Pydantic State
class ApplicationState(BaseModel):
    applicant_name: str = Field(default="")
    job_role: str = Field(default="")
    skills: list[str] = Field(default_factory=list)
    application_letter: str = Field(default="")

# 2. Node 1: Collect Name
def collect_name(state: ApplicationState) -> ApplicationState:
    state.applicant_name = "Aman"  # Simulated
    print("\n🟢 After collect_name:")
    print(state)
    return state

# 3. Node 2: Collect Job Role
def collect_job_role(state: ApplicationState) -> ApplicationState:
    state.job_role = "Data Scientist"  # Simulated
    print("\n🟡 After collect_job_role:")
    print(state)
    return state

# 4. Node 3: Collect Skills
def collect_skills(state: ApplicationState) -> ApplicationState:
    state.skills = ["Python", "Machine Learning", "SQL"]  # Simulated
    print("\n🔵 After collect_skills:")
    print(state)
    return state

# 5. Node 4: Generate Application Letter
def generate_letter(state: ApplicationState) -> ApplicationState:
    skills_str = ", ".join(state.skills)
    state.application_letter = (
        f"Dear Hiring Team,\n\n"
        f"My name is {state.applicant_name}, and I am excited to apply for the {state.job_role} position. "
        f"I bring expertise in {skills_str} and am eager to contribute to your team.\n\n"
        f"Best regards,\n{state.applicant_name}"
    )
    print("\n🟣 After generate_letter:")
    print(state)
    return state

# 6. Build the Graph
builder = StateGraph(ApplicationState)
builder.add_node("collect_name", collect_name)
builder.add_node("collect_role", collect_job_role)
builder.add_node("collect_skills", collect_skills)
builder.add_node("generate_letter", generate_letter)

# 7. Define the flow
builder.set_entry_point("collect_name")
builder.add_edge("collect_name", "collect_role")
builder.add_edge("collect_role", "collect_skills")
builder.add_edge("collect_skills", "generate_letter")

# 8. Run the Graph
graph = builder.compile()
print("🚀 Starting Application Flow...")
final_state = graph.invoke(ApplicationState())

# 9. Final Output
print("\n✅ Final Application State:")
print(final_state.json(indent=2))
```
####  Sample Output

```text
🚀 Starting Application Flow...

🟢 After collect_name:
applicant_name='Aman' job_role='' skills=[] application_letter=''

🟡 After collect_job_role:
applicant_name='Aman' job_role='Data Scientist' skills=[] application_letter=''

🔵 After collect_skills:
applicant_name='Aman' job_role='Data Scientist' skills=['Python', 'Machine Learning', 'SQL'] application_letter=''

🟣 After generate_letter:
applicant_name='Aman' job_role='Data Scientist' skills=['Python', 'Machine Learning', 'SQL'] application_letter='Dear Hiring Team,...

✅ Final Application State:
{
  "applicant_name": "Aman",
  "job_role": "Data Scientist",
  "skills": [
    "Python",
    "Machine Learning",
    "SQL"
  ],
  "application_letter": "Dear Hiring Team,\n\nMy name is Aman, and I am excited to apply for the Data Scientist position. I bring expertise in Python, Machine Learning, SQL and am eager to contribute to your team.\n\nBest regards,\nAman"
}
```
### Example 
#### **LangGraph LLM QA Example – Organized Version**

```python
# === Imports ===
from langgraph.graph import StateGraph, START, END
from langchain_openai import ChatOpenAI
from typing import TypedDict
from dotenv import load_dotenv

# === Load environment variables (like OPENAI_API_KEY) ===
load_dotenv()

# === Initialize OpenAI Chat Model ===
model = ChatOpenAI()

# === Define State ===
class LLMState(TypedDict):
    question: str
    answer: str

# === Node Function ===
def llm_qa(state: LLMState) -> LLMState:
    question = state['question']
    prompt = f"Answer the following question: {question}"
    answer = model.invoke(prompt).content
    state['answer'] = answer
    return state

# === Create LangGraph ===
graph = StateGraph(LLMState)

# Add node
graph.add_node('llm_qa', llm_qa)

# Add edges
graph.add_edge(START, 'llm_qa')
graph.add_edge('llm_qa', END)

# Compile the workflow
workflow = graph.compile()

# === Execute the Workflow ===
initial_state = {'question': 'How far is the moon from the Earth?'}
final_state = workflow.invoke(initial_state)

# Print the result
print(final_state['answer'])

# === Optional: Direct Model Test ===
# If you want to invoke without graph
model.invoke('How far is moon from the earth?').content
```

---

##### Output Example:

```text
The average distance between the Moon and Earth is about 384,400 kilometers (238,855 miles).
```

## Prompt Chaining 
### Steps:

1. User asks a **vague question**
    
2. We **clarify the question**
    
3. We **answer the clarified question**
    
4. We **summarize the answer**
    
###  State Definition

```python
class LLMState(TypedDict):
    question: str
    clarified_question: str
    answer: str
    summary: str
```

### Node Functions (Prompt Chain)

```python
def clarify_question(state: LLMState) -> LLMState:
    prompt = f"Clarify this question for a better answer: {state['question']}"
    clarified = model.invoke(prompt).content
    state["clarified_question"] = clarified
    return state

def generate_answer(state: LLMState) -> LLMState:
    prompt = f"Answer the following clarified question: {state['clarified_question']}"
    answer = model.invoke(prompt).content
    state["answer"] = answer
    return state

def summarize_answer(state: LLMState) -> LLMState:
    prompt = f"Summarize this answer in one line: {state['answer']}"
    summary = model.invoke(prompt).content
    state["summary"] = summary
    return state
```

### Lang_Graph Setup

```python
from langgraph.graph import StateGraph, START, END
from langchain_openai import ChatOpenAI
from typing import TypedDict
from dotenv import load_dotenv

# Load API key from .env
load_dotenv()
model = ChatOpenAI()

# --- State ---
class LLMState(TypedDict):
    question: str
    clarified_question: str
    answer: str
    summary: str

# --- Nodes ---
def clarify_question(state: LLMState) -> LLMState:
    prompt = f"Clarify this question for a better answer: {state['question']}"
    state["clarified_question"] = model.invoke(prompt).content
    return state

def generate_answer(state: LLMState) -> LLMState:
    prompt = f"Answer the following clarified question: {state['clarified_question']}"
    state["answer"] = model.invoke(prompt).content
    return state

def summarize_answer(state: LLMState) -> LLMState:
    prompt = f"Summarize this answer in one line: {state['answer']}"
    state["summary"] = model.invoke(prompt).content
    return state

# --- Build Graph ---
graph = StateGraph(LLMState)
graph.add_node("clarify", clarify_question)
graph.add_node("answer", generate_answer)
graph.add_node("summarize", summarize_answer)

graph.add_edge(START, "clarify")
graph.add_edge("clarify", "answer")
graph.add_edge("answer", "summarize")
graph.add_edge("summarize", END)

workflow = graph.compile()
```

###  Run It

```python
input_state = {
    "question": "what's the big deal with the moon?",
}

final_state = workflow.invoke(input_state)

print("Clarified Question:", final_state["clarified_question"])
print("Answer:", final_state["answer"])
print("Summary:", final_state["summary"])
```

### Sample Output

```text
Clarified Question:
Why is the Moon considered significant or important?

Answer:
The Moon plays a crucial role in Earth's natural systems, influencing tides, stabilizing the planet's axial tilt, and inspiring cultural, scientific, and exploratory pursuits.

Summary:
The Moon affects Earth's tides, stability, and has deep cultural and scientific importance.
```
