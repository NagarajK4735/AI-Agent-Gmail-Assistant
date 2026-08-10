Yes. Based on your **current project structure**, I would make one important adjustment to the README:

````markdown
# 📧 AI Gmail Assistant

### 🤖 Agentic AI-powered Gmail Assistant for intelligent email search, summarization, and analysis

The **AI Gmail Assistant** is a Generative AI application that allows users to interact with their Gmail inbox using natural language.

Instead of manually searching, opening, reading, and analyzing emails, users can simply ask questions and allow the AI assistant to retrieve and analyze the required information.

The application combines:

- Python
- OpenAI GPT-4o-mini
- LangChain
- LangGraph
- Gmail API
- Google OAuth 2.0
- MCP components
- Streamlit

to build a tool-enabled **Agentic AI Gmail Assistant**.

---

# ✨ Key Features

| Feature | Description |
|---|---|
| 📬 Unread Email Count | Get the number of unread emails |
| 📩 Recent Emails | Retrieve recent emails from Gmail |
| 🔍 Gmail Search | Search emails using Gmail search operators |
| 🧠 Email Summarization | Generate concise summaries of emails |
| 📋 Action Item Extraction | Identify tasks that may require user action |
| ⏰ Deadline Detection | Identify deadlines and time-sensitive information |
| 📅 Meeting Detection | Identify meetings mentioned in emails |
| ⭐ Priority Analysis | Identify high-priority actions |
| 💬 Conversation Memory | Maintain context across conversations |
| 🔐 Gmail OAuth | Authenticate securely with Gmail |
| 🤖 Tool Calling | Allow the LLM to select the appropriate Gmail tool |
| 🔄 LangGraph Workflow | Orchestrate agent and tool execution |
| 🖥️ Streamlit UI | Provide an interactive chat-based interface |
| 🆕 New Conversation | Start a fresh conversation using a new thread |
| 🔎 Natural-Language Search | Search Gmail using natural-language requests |

---

# 🚀 Project Overview

Traditional email applications require users to manually perform several steps:

```text
Search Email
     ↓
Open Email
     ↓
Read Content
     ↓
Understand Information
     ↓
Identify Important Actions
     ↓
Make a Decision
````

The **AI Gmail Assistant** simplifies this process by providing an AI-powered interface over Gmail.

The user communicates with the assistant using natural language.

### Example

```text
User:
Find unread emails from HDFC Bank.
```

The AI agent understands the user's intent, selects the appropriate Gmail tool, retrieves the required emails through the Gmail API, analyzes the results, and generates a natural-language response.

---

# 🧠 How the AI Gmail Assistant Works

```text
                         👤 User
                           │
                           │ Natural Language Query
                           ▼
                  ┌──────────────────┐
                  │   Streamlit UI   │
                  └─────────┬────────┘
                            │
                            ▼
                  ┌──────────────────┐
                  │    LangGraph     │
                  │  Agent Workflow  │
                  └─────────┬────────┘
                            │
                            ▼
                  ┌──────────────────┐
                  │   GPT-4o-mini    │
                  │   AI Agent / LLM │
                  └─────────┬────────┘
                            │
                     Tool Selection
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
       Gmail Search     Summarizer    Action Analyzer
             │              │              │
             └──────────────┼──────────────┘
                            ▼
                  ┌──────────────────┐
                  │    Gmail API     │
                  └─────────┬────────┘
                            │
                            ▼
                     📧 Gmail Inbox
                            │
                            ▼
                    Retrieved Emails
                            │
                            ▼
                     GPT-4o-mini
                            │
                            ▼
                      🤖 AI Response
                            │
                            ▼
                         👤 User
```

---

# 🤖 Agentic AI Architecture

The application follows a **tool-enabled Agentic AI architecture**.

The LLM does not directly perform Gmail operations. Gmail functionality is exposed through controlled tools that the LangGraph agent can invoke.

```text
User
 │
 ▼
Streamlit Application
 │
 ▼
LangGraph Agent
 │
 ▼
GPT-4o-mini
 │
 │ Determines required operation
 ▼
Tool Selection
 │
 ├── get_unread_email_count
 ├── get_recent_emails
 ├── summarize_latest_email
 ├── summarize_unread_emails
 ├── search_gmail
 ├── extract_action_items
 └── extract_deadlines_and_meetings
 │
 ▼
Gmail Service
 │
 ▼
Gmail API
 │
 ▼
Email Data
 │
 ▼
GPT-4o-mini
 │
 ▼
Final AI Response
 │
 ▼
Streamlit UI
```

The architecture separates:

* User Interface
* Agent Reasoning
* Tool Execution
* Gmail Service Logic
* Gmail API Communication
* Email Analysis
* Response Generation
* Conversation State

---

# 🔄 End-to-End Workflow

```text
1. User enters a natural-language question
                    ↓
2. Streamlit receives the request
                    ↓
3. LangGraph starts the agent workflow
                    ↓
4. GPT-4o-mini analyzes the user's intent
                    ↓
5. Agent selects the appropriate Gmail tool
                    ↓
6. Selected tool calls Gmail Service
                    ↓
7. Gmail Service communicates with Gmail API
                    ↓
8. Gmail data is retrieved
                    ↓
9. Tool returns the retrieved information
                    ↓
10. GPT-4o-mini analyzes the result
                    ↓
11. Final response is generated
                    ↓
12. Streamlit displays the response
```

---

# 🔍 Natural-Language Gmail Search

One of the important capabilities of the application is **AI-powered Gmail search**.

Users do not need to manually remember Gmail search operators.

### Example

```text
User:
Find unread emails from Google.
```

The agent can translate the user's intent into a Gmail search query such as:

```text
from:google is:unread
```

The workflow becomes:

```text
User Query
    ↓
GPT-4o-mini
    ↓
Understand User Intent
    ↓
Generate Gmail Search Query
    ↓
search_gmail Tool
    ↓
Gmail API
    ↓
Retrieve Matching Emails
    ↓
GPT-4o-mini
    ↓
Natural-Language Response
```

Examples of Gmail search operators supported by the search functionality include:

```text
from:google
from:hdfcbank
subject:invoice
has:attachment
is:unread
newer_than:1d
```

---

# 💬 Example User Queries

## 📬 Email Management

```text
How many unread emails do I have?
```

```text
Show my latest 5 emails.
```

```text
Show me my recent emails.
```

## 🔍 Email Search

```text
Find emails from Google.
```

```text
Find emails from HDFC Bank.
```

```text
Find unread emails.
```

```text
Find emails containing invoices.
```

```text
Find emails with attachments.
```

```text
Find emails from Google received recently.
```

## 📝 Email Analysis

```text
Summarize my latest email.
```

```text
Summarize my unread emails.
```

```text
What action items are present in my emails?
```

```text
What are the high-priority actions?
```

```text
Are there any upcoming deadlines?
```

```text
Are there any meetings mentioned in my emails?
```

---

# 📋 Action Item Extraction

The assistant can analyze retrieved emails and identify tasks that may require user action.

For example:

```text
User:
What action items are present in my emails?
```

The system retrieves relevant emails and analyzes their content using GPT-4o-mini.

The extracted information can include:

```text
Action
Sender
Subject
Deadline
Priority
```

### Example

```text
1. Action: Complete a short form to indicate job preferences
   Sender: IBM Talent Acquisition
   Subject: Stay Matched to the Right Opportunities at IBM
   Deadline: Not mentioned
   Priority: Medium
```

The assistant attempts to distinguish potential action items from general promotional or informational emails.

---

# ⏰ Deadline and Meeting Detection

The application can analyze email content to identify:

* Upcoming deadlines
* Important dates
* Meetings
* Scheduled events
* Time-sensitive activities

### Example

```text
User:
Are there any upcoming deadlines or meetings?
```

The assistant analyzes relevant email content and returns detected information when available.

---

# 📝 Email Summarization

The application uses GPT-4o-mini to summarize email content.

The summarization process considers:

* Sender
* Subject
* Main purpose
* Important dates
* Important action items

### Example

```text
User:
Summarize my latest email.
```

The assistant retrieves the latest email, extracts the relevant email content, and sends it to GPT-4o-mini for summarization.

---

# 💬 Conversation Memory

The application supports **conversation memory** using LangGraph checkpointing and thread-based conversations.

Each conversation is associated with a unique `thread_id`.

```text
Conversation
     │
     ▼
thread_id
     │
     ├── User Question 1
     ├── AI Response 1
     ├── User Question 2
     ├── AI Response 2
     ├── User Question 3
     └── AI Response 3
```

This allows the assistant to maintain context across multiple questions within the same conversation.

The Streamlit application also provides a **New Conversation** option.

When a new conversation is started:

```text
New Conversation
       ↓
Generate New thread_id
       ↓
Clear Visible Chat History
       ↓
Start Fresh Conversation
```

---

# 🧰 Gmail Tools

The LangGraph agent currently exposes the following Gmail-related tools:

```text
get_unread_email_count
get_recent_emails
summarize_latest_email
summarize_unread_emails
search_gmail
extract_action_items
extract_deadlines_and_meetings
```

The LLM determines which tool should be used based on the user's request.

### Example

```text
User:
How many unread emails do I have?
```

```text
        ↓
   GPT-4o-mini
        ↓
get_unread_email_count
        ↓
    Gmail API
        ↓
Unread Email Count
        ↓
   AI Response
```

---

# 🔐 Gmail Authentication

The application uses **Google OAuth 2.0** for Gmail authentication.

The authentication flow is:

```text
User
  ↓
Google OAuth
  ↓
Permission / Consent
  ↓
Gmail Authorization
  ↓
Access Token / Refresh Token
  ↓
Gmail API
```

OAuth-related files are stored locally and excluded from Git version control.

Sensitive files include:

```text
credentials/
credentials.json
token.json
token.pickle
```

These files must **not** be committed to GitHub.

---

# 🧩 Core Technologies

## 🐍 Python

Used as the primary programming language for the application.

## 🧠 OpenAI GPT-4o-mini

Used for:

* Natural-language understanding
* Tool selection
* Email summarization
* Action-item extraction
* Deadline detection
* Meeting detection
* Priority analysis
* Response generation

## 🔗 LangChain

Used for:

* LLM integration
* Tool creation
* Tool binding
* Message handling

## 🔄 LangGraph

Used for:

* Agent orchestration
* Workflow management
* Tool execution
* Conditional routing
* Agent state
* Conversation memory
* Checkpointing

## 📧 Gmail API

Used for:

* Gmail profile information
* Email retrieval
* Gmail search
* Email metadata
* Email content retrieval

## 🔐 Google OAuth 2.0

Used for secure authentication and authorization with Gmail.

## 🖥️ Streamlit

Used to build the interactive web-based chat interface.

## 🔌 MCP

The project contains an MCP component that provides an extensible foundation for connecting AI applications with external tools and context.

---

# 🗂️ Project Structure

The project follows a modular architecture:

```text
AI_Gmail_Assistant/
│
├── agents/
│   ├── agent.py
│   ├── graph.py
│   ├── nodes.py
│   └── state.py
│
├── config/
│
├── credentials/
│   └── (local OAuth files - NOT committed)
│
├── mcp_server/
│
├── models/
│   └── llm.py
│
├── services/
│   ├── auth_service.py
│   ├── gmail_service.py
│   └── summary_service.py
│
├── tools/
│   └── gmail_tools.py
│
├── tests/
│   ├── test_auth.py
│   ├── test_search.py
│   ├── test_search_tool.py
│   ├── test_search_full.py
│   ├── test_agent_search.py
│   ├── test_agent_search_loop.py
│   ├── test_graph_search.py
│   ├── test_action_items.py
│   ├── test_action_tool.py
│   ├── test_deadlines.py
│   ├── test_deadlines_tool.py
│   ├── test_email_analysis.py
│   ├── test_memory.py
│   ├── test_graph_memory_action.py
│   └── test_multi_tool.py
│
├── app.py
├── requirements.txt
├── .gitignore
└── README.md
```

> **Note:** The `credentials/` directory is used locally for Gmail OAuth files. Its contents are excluded from GitHub through `.gitignore`.

---

# 📁 Main Components

| Component                     | Responsibility                                              |
| ----------------------------- | ----------------------------------------------------------- |
| `app.py`                      | Streamlit application and chat interface                    |
| `agents/agent.py`             | Creates the LLM agent and binds Gmail tools                 |
| `agents/graph.py`             | Defines and compiles the LangGraph workflow                 |
| `agents/nodes.py`             | Defines chatbot and tool execution nodes                    |
| `agents/state.py`             | Defines the agent state                                     |
| `models/llm.py`               | Configures GPT-4o-mini                                      |
| `services/gmail_service.py`   | Handles Gmail API operations                                |
| `services/auth_service.py`    | Handles Gmail OAuth authentication                          |
| `services/summary_service.py` | Handles email summarization                                 |
| `tools/gmail_tools.py`        | Exposes Gmail operations as LangChain tools                 |
| `mcp_server/`                 | MCP-related project components                              |
| `tests/`                      | Component, tool, agent, graph, and memory testing           |
| `requirements.txt`            | Python dependencies                                         |
| `.gitignore`                  | Prevents secrets and unnecessary files from being committed |

---

# 🏗️ Application Architecture

```text
┌──────────────────────────────────────────────┐
│                 User / Browser               │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│                Streamlit UI                  │
│                                              │
│  • Chat Interface                            │
│  • Quick Actions                             │
│  • Gmail Statistics                          │
│  • Conversation Management                  │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│               LangGraph Agent                │
│                                              │
│  • Agent State                               │
│  • Conditional Routing                       │
│  • Tool Execution                            │
│  • Conversation Memory                       │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│                GPT-4o-mini                   │
│                                              │
│  • Intent Understanding                      │
│  • Tool Selection                            │
│  • Reasoning                                 │
│  • Response Generation                       │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│                Gmail Tools                   │
│                                              │
│  • Search                                    │
│  • Recent Emails                             │
│  • Unread Count                              │
│  • Summarization                             │
│  • Action Extraction                         │
│  • Deadline Detection                        │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│              Gmail Service                   │
│                                              │
│  • Authentication                            │
│  • Email Retrieval                           │
│  • Gmail Search                              │
│  • Header Extraction                         │
│  • Body Extraction                           │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│                 Gmail API                    │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
                  📧 Gmail Inbox
```

---

# 🧪 Testing Strategy

The project contains a dedicated `tests/` directory for validating different layers of the application.

The testing process was performed progressively:

```text
Gmail Authentication
        ↓
Gmail Service
        ↓
Individual Gmail Tools
        ↓
LLM Tool Calling
        ↓
Agent Tool Calling
        ↓
LangGraph Workflow
        ↓
Conversation Memory
        ↓
Streamlit Application
```

Examples of test categories include:

### Gmail Authentication

```text
test_auth.py
```

### Gmail Search

```text
test_search.py
test_search_tool.py
test_search_full.py
test_search_details.py
```

### Agent Search

```text
test_agent_search.py
test_agent_search_loop.py
```

### LangGraph Search

```text
test_graph_search.py
```

### Action Item Analysis

```text
test_action_items.py
test_action_tool.py
test_graph_action_search.py
test_graph_memory_action.py
```

### Deadline and Meeting Detection

```text
test_deadlines.py
test_deadlines_tool.py
```

### Email Analysis

```text
test_email_analysis.py
```

### Memory

```text
test_memory.py
test_graph_memory_action.py
```

### Multiple Tool Execution

```text
test_multi_tool.py
```

---

# 📊 Example Agent Execution

### User Query

```text
Find emails from Google.
```

### Agent Decision

```text
Intent:
Search Gmail

Tool:
search_gmail

Query:
from:google
```

### Gmail API

The Gmail API returns matching messages.

### AI Response

The retrieved email information is passed back through the agent workflow and GPT-4o-mini generates a natural-language response.

---

# 🎯 Project Goals

The main goals of this project are:

* Build a practical Agentic AI application
* Integrate an LLM with a real-world external API
* Implement Gmail tool calling
* Enable natural-language email search
* Automate email analysis
* Extract actionable information from emails
* Detect important deadlines and meetings
* Maintain conversation context
* Build a modular AI architecture
* Provide an intuitive Streamlit interface

---

# 📌 Current Capabilities

```text
✅ Gmail OAuth Authentication
✅ Gmail Profile Information
✅ Unread Email Count
✅ Recent Email Retrieval
✅ Gmail Search
✅ Natural-Language Gmail Search
✅ Email Summarization
✅ Unread Email Summarization
✅ Action Item Extraction
✅ Deadline Detection
✅ Meeting Detection
✅ Priority Analysis
✅ LangChain Tools
✅ LangGraph Agent
✅ Tool Calling
✅ Conversation Memory
✅ Thread-Based Conversations
✅ Streamlit Chat UI
✅ Gmail Quick Actions
✅ New Conversation Support
```

---

# 🚀 Future Enhancements

Potential future enhancements include:

```text
📤 Send Emails
↩️ Generate Email Replies
📝 Create Draft Emails
📎 Attachment Analysis
📄 PDF / Document Analysis
📅 Google Calendar Integration
🏷️ Gmail Label Management
🗄️ Email Archiving
🗑️ Email Deletion with Confirmation
⚡ Async Processing
🚀 Production Deployment
📊 LLM Evaluation
📈 Observability and Monitoring
🔐 Enterprise Authentication
```

---

# 💡 Why This Project?

This project demonstrates how **Generative AI and Agentic AI can interact with real-world APIs and applications**.

Instead of building a chatbot that only generates text, the application demonstrates an AI agent that can:

```text
Understand
   ↓
Reason
   ↓
Select a Tool
   ↓
Interact with an External System
   ↓
Retrieve Data
   ↓
Analyze Data
   ↓
Generate an Intelligent Response
```

This makes the application closer to a real-world **Agentic AI system** rather than a simple LLM chatbot.

---

# 📈 Learning Outcomes

This project provides practical experience with:

* Generative AI application development
* LLM integration
* Prompt engineering
* LangChain tool development
* LangGraph agent orchestration
* Agent state management
* Conversation memory
* Gmail API integration
* Google OAuth authentication
* Natural-language search
* Structured email analysis
* Streamlit application development
* Modular Python architecture
* Agentic AI design patterns

---

# 🛡️ Security Considerations

Sensitive credentials must never be committed to the repository.

The `.gitignore` file excludes sensitive files and directories such as:

```text
credentials/
credentials.json
token.json
token.pickle
.env
*.key
*.pem
```

Before pushing the project to GitHub, verify that no OAuth tokens, API keys, passwords, or other secrets are included.

The local `credentials/` directory may contain files required for Gmail authentication, but those files should remain on the developer's machine.

---

# ⚙️ Installation and Setup

## 1. Clone the Repository

```bash
git clone <your-github-repository-url>
cd AI_Gmail_Assistant
```

## 2. Create a Virtual Environment

On Windows:

```bash
python -m venv gmail_ai_agent
```

Activate the environment:

```powershell
gmail_ai_agent\Scripts\activate
```

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

## 4. Configure OpenAI API Key

Set the OpenAI API key as an environment variable.

For Windows PowerShell:

```powershell
$env:OPENAI_API_KEY="your-api-key"
```

Do not hard-code the API key in source code.

Do not commit API keys to GitHub.

## 5. Configure Gmail OAuth

Create/configure the required Gmail OAuth credentials locally.

Place the required OAuth files inside the local:

```text
credentials/
```

directory.

The credentials directory is excluded from Git version control.

## 6. Run the Application

Start the Streamlit application:

```bash
streamlit run app.py
```

The application will open in the browser.

---

# 🖥️ Streamlit Application

The Streamlit interface provides:

* Gmail connection status
* Gmail account information
* Unread email count
* Total email count
* Gmail thread count
* Quick actions
* Natural-language chat
* Conversation memory
* New conversation functionality

### Example Interface Flow

```text
┌────────────────────────────────────────────┐
│ 📧 AI Gmail Assistant                     │
├────────────────────────────────────────────┤
│                                            │
│ 👤 Find unread emails from Google.         │
│                                            │
│ 🤖 I found the following emails...         │
│                                            │
│                                            │
│ Ask about your emails...                   │
└────────────────────────────────────────────┘
```

---

# 📦 Dependencies

The project uses pinned Python dependencies defined in:

```text
requirements.txt
```

Major dependencies include:

```text
streamlit
openai
langchain
langchain-openai
langgraph
python-dotenv
google-api-python-client
google-auth
google-auth-oauthlib
google-auth-httplib2
pydantic
pandas
tiktoken
typing_extensions
```

---

# 🏆 Project Summary

The **AI Gmail Assistant** is an end-to-end Agentic AI application that combines:

```text
Python
   +
OpenAI GPT-4o-mini
   +
LangChain
   +
LangGraph
   +
Gmail API
   +
Google OAuth 2.0
   +
MCP Components
   +
Streamlit
```

The application demonstrates how an LLM can:

```text
Understand User Intent
        ↓
Select Appropriate Tool
        ↓
Interact with Gmail
        ↓
Retrieve Email Information
        ↓
Analyze Email Content
        ↓
Maintain Conversation Context
        ↓
Generate Intelligent Response
```

---

# 🔥 Final Architecture

```text
                         👤 USER
                           │
                           ▼
                  ┌─────────────────┐
                  │  Streamlit UI   │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │    LangGraph    │
                  │      Agent      │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │   GPT-4o-mini   │
                  │      LLM        │
                  └────────┬────────┘
                           │
                     Tool Calling
                           │
                           ▼
                  ┌─────────────────┐
                  │   Gmail Tools   │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ Gmail Service   │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │    Gmail API    │
                  └────────┬────────┘
                           │
                           ▼
                       📧 Gmail
                           │
                           ▼
                  Email Data / Results
                           │
                           ▼
                  ┌─────────────────┐
                  │   GPT-4o-mini   │
                  │ Analysis /      │
                  │ Response        │
                  └────────┬────────┘
                           │
                           ▼
                    🤖 AI Response
                           │
                           ▼
                         👤 USER
```

---

# 🛠️ Built With

**Python • OpenAI GPT-4o-mini • LangChain • LangGraph • Gmail API • Google OAuth 2.0 • MCP • Streamlit**

---

# 👨‍💻 Author

## Nagaraj Kamale

**Generative AI Engineer**

Python • Generative AI • LLMs • RAG • Agentic AI • LangChain • LangGraph

---

⭐ If you find this project useful, consider giving the repository a star.

````
Also, you **do not need to delete your `tests/` folder**. In fact, keeping the tests is a good practice because it demonstrates that you validated the Gmail service, tools, agent, LangGraph workflow, and memory separately.
