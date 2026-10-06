# LangGraph Course — CampusX

A hands-on learning repository for **LangGraph and Agentic AI**, following the CampusX *Agentic AI using LangGraph* YouTube curriculum.

The goal of this repository is to learn LangGraph by implementing workflows from scratch, understanding state management and graph execution, and gradually moving toward production-oriented agentic systems.

## 🚀 What I'm Learning

- Agentic AI fundamentals
- Generative AI vs Agentic AI
- LangChain vs LangGraph
- LangGraph state, nodes, edges, and reducers
- Sequential workflows
- Parallel workflows
- Conditional workflows
- Iterative workflows
- LLM-powered workflows
- Chatbots with LangGraph
- Persistence and memory
- Streaming
- Streamlit UI integration
- SQLite integration
- Structured LLM output with Pydantic
- Tools and tool-calling
- MCP integration
- RAG with LangGraph
- Human-in-the-loop (HITL)
- Subgraphs
- Short-term and long-term memory
- LangSmith observability
- Building larger agentic applications

## 🧠 Core LangGraph Concepts

### State

State is the shared data structure passed between nodes.

```python
from typing import TypedDict

class State(TypedDict):
    input: str
    output: str
```

### Nodes

Nodes are Python functions that perform individual pieces of work.

```python
def process(state: State):
    return {"output": "Processed"}
```

### Edges

Edges control how execution moves through the graph.

```python
graph.add_edge(START, "process")
graph.add_edge("process", END)
```

### Graph

A basic LangGraph workflow:

```text
START
  ↓
Node 1
  ↓
Node 2
  ↓
END
```

## 📚 Course Roadmap

### 1. Foundations

- [ ] Agentic AI using LangGraph — Introduction
- [ ] Generative AI vs Agentic AI
- [ ] What is Agentic AI?
- [ ] LangChain vs LangGraph
- [ ] LangGraph Core Concepts

### 2. Workflow Patterns

- [ ] Sequential Workflows
- [ ] Parallel Workflows
- [ ] Conditional Workflows
- [ ] Iterative Workflows
- [ ] Prompt Chaining
- [ ] Routing
- [ ] Orchestrator-Worker
- [ ] Evaluator-Optimizer

### 3. Practical LangGraph Workflows

- [x] BMI Workflow
- [x] Simple LLM Workflow
- [x] Prompt Chaining
- [x] Batsman Statistics Workflow
- [x] UPSC Essay Evaluation Workflow
- [x] Quadratic Equation Workflow
- [x] Review Reply Workflow
- [x] X/Tweet Generator Workflow

### 4. Chatbots

- [ ] Basic LangGraph Chatbot
- [ ] Persistence
- [ ] Memory
- [ ] Streaming
- [ ] Streamlit UI
- [ ] Resume Chatbot
- [ ] SQLite-backed Chatbot

### 5. Observability

- [ ] LangSmith fundamentals
- [ ] LangSmith tracing
- [ ] LangGraph observability
- [ ] Debugging and monitoring agentic workflows

### 6. Tools and Agentic Systems

- [ ] Tools in LangGraph
- [ ] Tool calling
- [ ] MCP Client with LangGraph
- [ ] RAG with LangGraph
- [ ] Human-in-the-loop
- [ ] Subgraphs

### 7. Memory

- [ ] Understand LLM memory limitations
- [ ] Short-term memory
- [ ] Long-term memory
- [ ] Persistent conversations

### 8. Final Agentic AI Project

- [ ] Planning
- [ ] Research
- [ ] Content generation
- [ ] Evaluation
- [ ] Memory
- [ ] Tool usage
- [ ] Observability

## 🗂️ Repository Structure

```text
Langraph/
│
├── notebooks/
│   ├── 01_bmi_workflow.ipynb
│   ├── 02_simple_llm_workflow.ipynb
│   ├── 03_prompt_chaining.ipynb
│   ├── 04_batsman_workflow.ipynb
│   ├── 05_upsc_essay_workflow.ipynb
│   ├── 06_quadratic_equation_workflow.ipynb
│   ├── 07_review_reply_workflow.ipynb
│   ├── 08_x_post_generator.ipynb
│   └── ...
│
├── .env.example
├── .gitignore
├── requirements.txt
└── README.md
```

> Notebook names can be adjusted to match the actual files in this repository.

## 🛠️ Tech Stack

- Python
- LangGraph
- LangChain
- Google Gemini
- Pydantic
- Python `typing`
- Streamlit
- SQLite
- LangSmith
- MCP
- Jupyter Notebook

## ⚙️ Installation

Create a virtual environment:

```powershell
python -m venv myenv
```

Activate it on Windows:

```powershell
myenv\Scripts\Activate
```

Install dependencies:

```powershell
pip install -U langgraph langchain langchain-google-genai python-dotenv pydantic
```

For additional projects, install the required dependencies listed in `requirements.txt`.

## 🔐 Environment Variables

Create a local `.env` file:

```env
GOOGLE_API_KEY=your_api_key_here
```

Never commit `.env` to GitHub.

The repository should contain `.env` in `.gitignore`:

```text
.env
```

## ▶️ Basic LangGraph Example

```python
from typing import TypedDict
from langgraph.graph import StateGraph, START, END

class State(TypedDict):
    message: str

def process(state: State):
    return {
        "message": state["message"].upper()
    }

graph = StateGraph(State)

graph.add_node("process", process)

graph.add_edge(START, "process")
graph.add_edge("process", END)

workflow = graph.compile()

result = workflow.invoke({
    "message": "hello langgraph"
})

print(result)
```

## 🔀 Workflow Patterns

### Sequential

```text
START → Node A → Node B → Node C → END
```

Used when each step depends on the previous step.

### Parallel

```text
             → Node A →
START ───────→ Node B →→ Summary → END
             → Node C →
```

Used when independent operations can execute in parallel.

### Conditional

```text
START
  ↓
Router
  ├──→ Path A
  └──→ Path B
```

Used when the next node depends on the current state.

### Iterative

```text
START → Generate → Evaluate
             ↑        │
             └────────┘
```

Used when a workflow needs repeated improvement until a condition is satisfied.

## 🧩 Structured LLM Output

Pydantic can be used to make LLM responses predictable:

```python
from pydantic import BaseModel, Field

class TweetEvaluation(BaseModel):
    evaluation: str
    feedback: str

structured_model = model.with_structured_output(TweetEvaluation)
```

This is useful for routing and evaluation workflows.

## 💾 Persistence and Memory

LangGraph can maintain state across interactions using a checkpointer.

Example configuration:

```python
config = {
    "configurable": {
        "thread_id": "1"
    }
}
```

The `thread_id` identifies a conversation/thread when persistence is enabled.

## 🔍 Learning Goals

By completing this repository, I aim to be able to:

- Design stateful LLM workflows
- Build multi-step AI applications
- Implement routing and conditional execution
- Run independent graph branches in parallel
- Build evaluator-optimizer loops
- Add persistence and memory
- Integrate tools and external systems
- Build RAG workflows with LangGraph
- Implement human-in-the-loop workflows
- Debug agentic applications with LangSmith
- Understand how LangGraph differs from simple LLM chains

## 📈 Progress

| Area | Status |
|---|---|
| LangGraph fundamentals | 🟢 |
| State / Nodes / Edges | 🟢 |
| Sequential workflows | 🟢 |
| Parallel workflows | 🟢 |
| Conditional workflows | 🟡 |
| Iterative workflows | 🟡 |
| Structured output | 🟢 |
| Chatbots | 🟡 |
| Persistence | 🟡 |
| Streaming | 🔴 |
| SQLite | 🔴 |
| Tools | 🔴 |
| MCP | 🔴 |
| RAG | 🔴 |
| HITL | 🔴 |
| Subgraphs | 🔴 |
| LangSmith | 🔴 |
| Long-term memory | 🔴 |
| Final agentic project | 🔴 |

Legend:

- 🟢 Completed
- 🟡 In progress
- 🔴 Not started

## 📌 Learning Approach

For each topic:

1. Understand the concept
2. Implement the smallest possible example
3. Modify the example independently
4. Debug common LangGraph errors
5. Visualize the graph
6. Build a slightly larger workflow
7. Add the concept to a practical project

## 🎯 Next Steps

After completing the fundamentals:

1. Build a production-style LangGraph application
2. Integrate tools and MCP
3. Add RAG
4. Add persistence and memory
5. Add LangSmith observability
6. Deploy the application
7. Document the architecture and design decisions

## 📖 Course Reference

This repository follows the CampusX *Agentic AI using LangGraph* YouTube curriculum.

- CampusX LangGraph course: https://learnwith.campusx.in/courses/LangGraph-YouTube-69145df5c26d79058b698748
- CampusX LangGraph tutorial repository: https://github.com/campusx-official/langgraph-tutorials

This repository contains my own implementations and learning exercises rather than reproducing the course's proprietary notes.

---

## 👨‍💻 Author

**Rohan Patil**

BE Artificial Intelligence & Machine Learning — 2027

Interested in:

- Generative AI
- AI Agents
- RAG
- LangGraph
- MCP
- FastAPI
- Machine Learning
- MLOps
