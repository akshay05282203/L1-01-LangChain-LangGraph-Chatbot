

# 🤖 LangChain + LangGraph Conversational Chatbot

A conversational AI chatbot built using **LangChain, LangGraph, and Google Gemini**. The project demonstrates how to build a stateful conversational application with message handling, workflow orchestration, conversation memory, and thread-based conversation management.

## ✨ Features

* Google Gemini LLM integration
* LangChain message handling
* LangGraph `StateGraph` workflow
* Multi-turn conversations
* Conversation state management
* `MemorySaver` checkpointing
* Thread-based conversation memory
* Separate conversation sessions using `thread_id`
* LangGraph workflow visualization
* Secure API key management using environment variables

## 🧰 Technologies

| Technology    | Purpose                         |
| ------------- | ------------------------------- |
| Python        | Application development         |
| LangChain     | LLM application framework       |
| LangGraph     | Stateful workflow orchestration |
| Google Gemini | Large Language Model            |
| python-dotenv | Environment variable management |
| IPython       | Workflow visualization          |

## 🏗️ Architecture

```text
                    User
                     |
                     v
              HumanMessage
                     |
                     v
          +---------------------+
          |     LangGraph       |
          |     StateGraph      |
          +----------+----------+
                     |
                     v
          +---------------------+
          |     Model Node      |
          |   Gemini 2.5 Flash  |
          +----------+----------+
                     |
                     v
               AIMessage
                     |
                     v
          +---------------------+
          |    MemorySaver      |
          |   Thread Checkpoint |
          +---------------------+
```

### 🔄 Workflow

The application follows a simple graph-based workflow:

```text
START
  |
  v
Model Node
  |
  v
END
```

The user message is passed to the LangGraph state. The model node sends the conversation to Gemini and returns an `AIMessage`. `MemorySaver` stores the state so that previous messages can be accessed within the same conversation thread.

## 🧠 Conversation Memory

The chatbot uses LangGraph's `MemorySaver` for conversation checkpointing.

A `thread_id` identifies a particular conversation.

```python
config = {
    "configurable": {
        "thread_id": "abc123"
    }
}
```

Using the same `thread_id` allows the chatbot to continue the previous conversation.

For example:

```text
Thread: abc123

User: I am Akshay.
AI: Hello, Akshay!

User: What is my name?
AI: Your name is Akshay.
```

A different `thread_id` represents another conversation session.

```text
Thread: abc124

User: What is my name?
AI: I don't have your name in this conversation yet.
```

## 📂 Project Structure

```text
L1-01-LangChain-LangGraph-Chatbot/
│
├── chatbot.py
├── requirements.txt
├── .gitignore
└── README.md
```

### 📄 File Description

| File               | Description                               |
| ------------------ | ----------------------------------------- |
| `chatbot.py`       | Main chatbot and LangGraph implementation |
| `requirements.txt` | Python dependencies                       |
| `.gitignore`       | Files excluded from Git                   |
| `README.md`        | Project documentation                     |

## ⚙️ Installation

### 1. Clone Repository

```bash
git clone https://github.com/akshay05282203/L1-01-LangChain-LangGraph-Chatbot.git
cd L1-01-LangChain-LangGraph-Chatbot
```

### 2. Create Virtual Environment

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

## 🔐 Configuration

Create a `.env` file in the project directory:

```env
GOOGLE_API_KEY=your_google_api_key
```

The application loads the API key using environment variables.

**Do not commit `.env` or expose your API key publicly.**

Recommended `.gitignore`:

```gitignore
.env
.venv/
__pycache__/
*.pyc
.ipynb_checkpoints/
```

## ▶️ Run the Application

After configuring the API key:

```bash
python chatbot.py
```

The application will execute the LangGraph workflow and demonstrate conversational memory using thread IDs.

## 🧩 Core Concepts

### 💬 Messages

The application uses LangChain message objects:

* `HumanMessage` — represents user input
* `AIMessage` — represents the model response

### 🗃️ MessagesState

`MessagesState` is used to maintain the conversation messages inside the LangGraph state.

### 🔀 StateGraph

`StateGraph` defines the workflow and controls how the conversation moves between nodes.

### 🧠 Model Node

The model node receives the current conversation state and invokes the Gemini model.

```python
def call_model(state: MessagesState):
    response = model.invoke(state["messages"])
    return {"messages": response}
```

### 💾 MemorySaver

`MemorySaver` provides in-memory checkpointing for conversation state.

```python
memory = MemorySaver()

app = workflow.compile(
    checkpointer=memory
)
```

## 📊 LangGraph Visualization

The workflow can be visualized using Mermaid:

```python
from IPython.display import Image, display

display(
    Image(
        app.get_graph().draw_mermaid_png()
    )
)
```

The generated graph represents:

```text
START → MODEL → END
```

## 🗨️ Example Conversation

```text
User: I am Akshay.

AI: Hello, Akshay! How can I assist you today?

User: What is my name?

AI: Your name is Akshay.
```

The conversation context is maintained when the same `thread_id` is used.

## 🎯 Learning Outcomes

This project provides practical experience with:

* Large Language Models
* LangChain
* LangGraph
* Gemini API integration
* Message-based conversations
* `MessagesState`
* `StateGraph`
* Nodes and edges
* Conversation memory
* Checkpointing
* Thread-based sessions
* Environment variables
* LLM workflow visualization

## 🚀 Future Improvements

Possible extensions include:

* Streamlit user interface
* FastAPI backend
* Persistent database memory
* RAG integration
* Vector database integration
* Tool calling
* Web search
* Long-term memory
* Conditional LangGraph workflows
* Multiple AI agents
* Docker deployment

## 👤 Author

**Akshay Chavan
 B.Tech CSE AI**

Interests: Artificial Intelligence, Machine Learning, Generative AI, Agentic AI, RAG, and Data Science.

## 📜 License

This project is created for educational and learning purposes.
# langchain-langgraph-conversational-chatbot
