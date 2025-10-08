
# 🧠 Multi-Agent Collaborative Data Analyst using LangGraph

### 🚀 Project Overview
This project implements a **collaborative multi-agent chatbot system** using **LangGraph**.  
The system acts as an **intelligent Data Analyst Assistant**, capable of researching live data, analyzing it, and generating visualizations — all through **coordinating multiple AI agents**.

Unlike single-agent systems that struggle with multi-step reasoning or tool orchestration, this architecture follows a **divide-and-conquer approach**:
- Each agent specializes in a task.
- Agents communicate and coordinate via a **graph-based state machine**.
- Conditional routing logic dynamically determines which agent should handle the next step.

---

## 🧩 System Components

### 1. **Research Agent**
- Fetches and analyzes **live data** using the **Tavily Search API** (wrapped as a LangChain tool).
- Interprets user queries and retrieves relevant information for analysis.

### 2. **Chart Generator Agent**
- Executes **Python code** dynamically using the **PythonREPL** tool.
- Creates **visual charts and graphs** (e.g., GDP bar chart) from the fetched data.
- Marks completion with `"FINAL ANSWER"` when visualization is ready.

### 3. **Conditional Routing Edges**
- Implements logic-based transitions:
  - If a tool call is detected → routes to the **ToolNode**.
  - If `"FINAL ANSWER"` appears → terminates the graph.
  - Otherwise → switches agents for next execution.

### 4. **Graph State & Orchestration**
- Built using **LangGraph’s StateGraph**.
- Maintains a unified message state (`GraphState`) to allow multi-agent collaboration.
- Uses `"recursion_limit"` to control workflow depth.

---

## ⚙️ Tech Stack & Tools
| Component | Technology |
|------------|-------------|
| **Framework** | LangGraph |
| **LLM Backend** | OpenAI GPT models |
| **Tooling** | LangChain Tools, Tavily Search, PythonREPL |
| **Visualization** | Matplotlib (executed via Python code) |
| **Environment Variables** | `OPENAI_API_KEY`, `TAVILY_API_KEY` |

---

## 🧠 Project Flow

1. **User Input:**  
   User provides a query (e.g., “Fetch top 3 countries by GDP and visualize.”)

2. **Research Agent Execution:**  
   Fetches real-time GDP data using the **Tavily Search** tool.

3. **Conditional Routing:**  
   Graph logic decides whether to call tools, switch agents, or stop execution.

4. **Chart Generator Agent Execution:**  
   Runs Python code dynamically to create a **GDP bar chart**.

5. **Final Answer:**  
   Visualization and summarized insights are returned as `"FINAL ANSWER"`.

---

## 📊 Example Output

**User Prompt:**
> “Fetch the data of the top 3 countries with the highest GDP and draw a bar chart.”

**System Response:**
> ✅ *FINAL ANSWER:*  
> The bar chart displaying GDP of the top 3 countries in 2023 — United States ($27.72T), China ($17.79T), and Japan ($4.20T) — has been successfully created using Matplotlib.

---

## 🧩 Architecture Diagram
```mermaid
graph TD
    A[Research Agent] -->|Conditional Logic| B[ToolNode]
    B -->|Data Execution| C[Code Execution Agent]
    C -->|Generate Charts| A
    C -->|If FINAL ANSWER| D[End]
````

---

## 📚 What I Learned

| Concept                        | Description                                                                                                      |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| **LangGraph Fundamentals**     | Learned how to define nodes, edges, and state transitions to orchestrate agent workflows.                        |
| **State Management**           | Understood how messages become stateful objects shared among agents (`GraphState`).                              |
| **Tool Integration**           | Wrapped external utilities (like Tavily Search, PythonREPL) as LangChain tools for agent use.                    |
| **Prompt Engineering**         | Designed detailed multi-agent prompts to specify collaboration rules, responsibilities, and stopping conditions. |
| **Conditional Logic**          | Implemented dynamic routing (`TOOL_CALL`, `NEXT_AGENT`, `END`) to manage agent decisions.                        |
| **Multi-Agent Collaboration**  | Experienced real coordination between two AI agents exchanging intermediate results.                             |
| **Error Handling & Execution** | Managed Python code execution safely with `try-except` for runtime errors.                                       |
| **Graph Visualization**        | Visualized the agent flow using LangGraph’s `.draw_mermaid_png()` method.                                        |

---

## 🏭 Industry Applications

| Domain                          | How It’s Used                                                                    |
| ------------------------------- | -------------------------------------------------------------------------------- |
| **AI Data Analysis**            | Powering autonomous data assistants that fetch, analyze, and visualize insights. |
| **Enterprise Automation**       | Enabling multi-agent workflows for report generation and data-driven decisions.  |
| **RAG & Agentic Systems**       | Core architecture behind Retrieval-Augmented and Agentic LLM systems.            |
| **Business Intelligence**       | Automating dashboards that combine research and analytics agents.                |
| **AI Collaboration Frameworks** | Used in building AI teams that perform cross-domain collaborative reasoning.     |

---

## 🧑‍💻 How to Run

### 1️⃣ Set API Keys

```bash
export OPENAI_API_KEY="your_openai_key"
export TAVILY_API_KEY="your_tavily_key"
```

### 2️⃣ Install Dependencies

```bash
pip install langgraph langchain langchain-core langchain-tavily matplotlib
```

### 3️⃣ Run the Script


### 4️⃣ Example Output

A matplotlib-generated chart and printed “FINAL ANSWER” with GDP details.

---

## 🏁 Future Enhancements

* 🧠 Add more agents (e.g., Data Summarizer, Report Writer)
* ⚙️ Integrate vector database (like Weaviate or Pinecone) for memory
* 🌐 Deploy as web-based multi-user chatbot with Flask or FastAPI
* 📈 Real-time visualization dashboard with Streamlit

---

## 🧾 Author

👤 **Govinda Tak**
🎓 Full Stack & AI-ML Developer
💡 Passionate about building **Agentic AI Systems** for data analytics and automation.

```
