Yes. The reason it is not appearing correctly is that **Markdown formatting is sensitive to blank lines, indentation, and fenced code blocks**. In particular, the content after ````text` can get mixed with the surrounding Markdown if the fence is not separated cleanly.

For GitHub, the safest approach is to copy the **entire README below as one single block** and paste it directly into `README.md`.

````markdown
# 📧 AI Gmail Assistant

An intelligent Gmail assistant built using **Python, OpenAI GPT-4o-mini, LangChain, LangGraph, Gmail API, MCP, and Streamlit**.

The application allows users to interact with their Gmail inbox using natural language. Instead of manually searching through emails, users can ask questions such as:

- How many unread emails do I have?
- Show my recent emails.
- Summarize my latest email.
- Find emails from Google.
- Find emails containing invoices.
- Find unread emails.
- What action items are present in my emails?
- Are there any upcoming deadlines or meetings?
- What are the high-priority actions?
- Search my Gmail using natural language.
- Continue a conversation based on previous questions.

The project demonstrates how to build a **tool-enabled Agentic AI application** using LangGraph and Gmail APIs.

---

# 🚀 Project Overview

Traditional email applications require users to manually search, open, read, and analyze emails.

This project introduces an AI-powered Gmail assistant that acts as an intelligent interface over Gmail.

The user communicates with the application using natural language.

For example:

```text
User: Find unread emails from HDFC Bank.
````

The AI agent understands the user's request, selects the appropriate Gmail tool, retrieves the required emails, analyzes the results, and returns a natural-language response.

---

# 🏗️ Project Architecture

```text
                         ┌───────────────────────┐
                         │       User            │
                         │                       │
                         │ Natural Language Query│
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │     Streamlit UI      │
                         │                       │
                         │ Chat Interface        │
                         │ Gmail Dashboard       │
                         │ Quick Actions         │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │      LangGraph        │
                         │     Agent Workflow    │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │      GPT-4o-mini      │
                         │                       │
                         │ Understands Query     │
                         │ Selects Tools         │
                         └───────────┬───────────┘
                                     │
                       ┌─────────────┴─────────────┐
                       │                           │
                       ▼                           ▼
              ┌─────────────────┐        ┌─────────────────┐
              │   Gmail Tools   │        │ Conversation    │
              │                 │        │ Memory          │
              │ Search Gmail    │        │                 │
              │ Unread Count    │        │ Thread ID       │
              │ Recent Emails   │        │ Checkpoints     │
              │ Summarization   │        │                 │
              │ Action Items    │        └─────────────────┘
              │ Deadlines       │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │    Gmail API    │
              │                 │
              │ Google OAuth 2  │
              │ Gmail Messages  │
              │ Gmail Metadata  │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │   User Gmail    │
              │     Inbox       │
              └─────────────────┘
```

---

# 🔄 End-to-End Workflow

```text
User
  │
  ▼
Streamlit Chat UI
  │
  ▼
LangGraph Agent
  │
  ▼
GPT-4o-mini
  │
  ├── Direct Answer
  │
  └── Tool Call
        │
        ▼
   Gmail Tool
        │
        ▼
     Gmail API
        │
        ▼
     Gmail Inbox
        │
        ▼
     Tool Result
        │
        ▼
   GPT-4o-mini
        │
        ▼
 Natural Language Response
        │
        ▼
    Streamlit UI
```

---

# 🧠 Agentic AI Architecture

The application uses an **LLM-driven tool-calling architecture**.

The LLM does not directly access Gmail.

Instead, the LLM is connected to a set of controlled tools.

For example:

```text
User:
"Find unread emails from Google"

        ↓

GPT-4o-mini

        ↓

Tool Selection

        ↓

search_gmail(
    query="from:google is:unread"
)

        ↓

Gmail API

        ↓

Email Results

        ↓

GPT-4o-mini

        ↓

Final Answer
```

This architecture provides better control and separation of responsibilities.

---

# 🧩 Main Components

## 1. Streamlit

Streamlit provides the user interface.

Responsibilities include:

* Gmail account information
* Gmail connection status
* Unread email count
* Total email count
* Thread count
* Quick actions
* Chat interface
* Conversation history
* New conversation functionality

---

## 2. GPT-4o-mini

GPT-4o-mini acts as the reasoning and language-generation component.

It is responsible for:

* Understanding user questions
* Selecting appropriate tools
* Generating tool-call arguments
* Summarizing emails
* Extracting action items
* Identifying deadlines
* Identifying meetings
* Generating natural-language responses

---

## 3. LangChain

LangChain is used to:

* Integrate the LLM
* Define tools
* Bind tools to the model
* Manage messages
* Create reusable AI components

Example:

```python
agent = llm.bind_tools(TOOLS)
```

---

## 4. LangGraph

LangGraph manages the agent workflow.

The workflow contains:

```text
START
  ↓
Chatbot
  ↓
Tool Decision
  ↓
Tools
  ↓
Chatbot
  ↓
END
```

This enables the agent to perform multiple tool calls when required.

---

# 🛠️ Gmail Tools

The project provides several Gmail tools.

### Unread Email Count

```text
get_unread_email_count()
```

Returns the number of unread emails.

Example:

```text
User: How many unread emails do I have?
```

---

### Recent Emails

```text
get_recent_emails()
```

Returns recent emails with information such as:

* Sender
* Subject
* Date

---

### Latest Email Summary

```text
summarize_latest_email()
```

Uses GPT-4o-mini to summarize the latest email.

The summary includes:

* Sender
* Subject
* Main purpose
* Important dates
* Action items

---

### Unread Email Summarization

```text
summarize_unread_emails()
```

Retrieves unread emails and generates summaries.

---

### Gmail Search

```text
search_gmail(query)
```

Supports Gmail search operators.

Examples:

```text
from:google
from:hdfcbank
subject:invoice
has:attachment
is:unread
newer_than:1d
```

Users can therefore perform advanced Gmail searches.

---

### Action Item Extraction

```text
extract_action_items()
```

Analyzes emails and identifies tasks that require user action.

Example output:

```text
ACTION ITEMS

1. Complete a short form to indicate job preferences
   Sender: IBM Talent Acquisition
   Priority: Medium

2. Take action on the personal loan offer
   Sender: HDFC Bank
   Priority: High
```

---

### Deadline and Meeting Extraction

```text
extract_deadlines_and_meetings()
```

Analyzes emails to identify:

* Deadlines
* Meetings
* Important dates
* Events

---

# 🔍 Advanced Gmail Search

The application supports natural-language Gmail searching.

For example:

```text
Find unread emails from Google.
```

The agent can translate this into:

```text
from:google is:unread
```

Another example:

```text
Show emails from HDFC Bank containing loan offers.
```

The agent can construct an appropriate Gmail search query and call the Gmail API.

---

# 🧠 Conversation Memory

The application supports conversation-level memory using LangGraph checkpointing.

Each conversation receives a unique:

```text
thread_id
```

Example:

```text
thread_id = "550e8400-e29b-41d4-a716-446655440000"
```

This allows the application to maintain conversation state.

Example:

```text
User:
Find emails from HDFC Bank.

Assistant:
I found several HDFC Bank emails.

User:
Which ones are high priority?

Assistant:
Based on the HDFC Bank emails I found earlier...
```

The second question can use the context maintained by the conversation thread.

---

# 🔐 Gmail Authentication

The application uses the **Gmail API with OAuth 2.0**.

Authentication flow:

```text
Application
     │
     ▼
Google OAuth
     │
     ▼
User Login
     │
     ▼
Permission Grant
     │
     ▼
Access Token
     │
     ▼
Gmail API
```

Sensitive OAuth files are excluded from Git using `.gitignore`.

Examples:

```text
credentials/
credentials.json
token.json
token.pickle
```

These files should **never be committed to GitHub**.

---

# 📁 Project Structure

```text
AI_Gmail_Assistant/
│
├── agents/
│   ├── __init__.py
│   ├── agent.py
│   ├── graph.py
│   ├── nodes.py
│   └── state.py
│
├── config/
│
├── credentials/
│   ├── credentials.json
│   └── token.json
│
├── images/
│
├── mcp_server/
│
├── models/
│   ├── __init__.py
│   └── llm.py
│
├── prompts/
│
├── schemas/
│
├── services/
│   ├── __init__.py
│   ├── auth_service.py
│   ├── gmail_service.py
│   └── summary_service.py
│
├── tools/
│   ├── __init__.py
│   └── gmail_tools.py
│
├── utils/
│
├── app.py
│
├── requirements.txt
│
├── .gitignore
│
└── README.md
```

---

# 📂 Folder Responsibilities

## `agents/`

Contains the LangGraph agent implementation.

Main responsibilities:

* Agent creation
* LangGraph workflow
* Graph nodes
* Agent state
* Tool routing
* Conversation flow

---

## `services/`

Contains business logic for Gmail operations.

Examples:

```text
Gmail authentication
Gmail profile
Email retrieval
Email searching
Email body extraction
Email analysis
Email summarization
```

---

## `tools/`

Contains LangChain tools exposed to the AI agent.

The LLM can select these tools based on the user's request.

---

## `models/`

Contains LLM configuration.

The project currently uses:

```text
GPT-4o-mini
```

---

## `mcp_server/`

Contains the MCP-related implementation for extending the application with a Model Context Protocol based architecture.

---

## `prompts/`

Contains reusable prompt templates.

---

## `schemas/`

Contains structured data schemas used by the application.

---

## `credentials/`

Contains local Google OAuth credentials.

This folder must remain excluded from Git.

---

# 🧪 Testing

The project contains multiple test scripts for validating individual components.

Examples:

```text
test_auth.py
test_search.py
test_search_tool.py
test_search_full.py
test_agent.py
test_agent_search.py
test_agent_search_loop.py
test_graph_search.py
test_action_items.py
test_action_tool.py
test_deadlines.py
test_deadlines_tool.py
test_memory.py
test_graph_memory_action.py
```

Testing is performed at multiple levels:

```text
Unit Testing
     ↓
Service Testing
     ↓
Tool Testing
     ↓
Agent Testing
     ↓
LangGraph Testing
     ↓
Streamlit UI Testing
```

---

# 🧪 Example Test Flow

## Gmail Service

```text
test_search.py
       ↓
GmailService
       ↓
Gmail API
```

## Gmail Tool

```text
test_search_tool.py
       ↓
search_gmail()
       ↓
GmailService
```

## Agent

```text
test_agent_search.py
       ↓
GPT-4o-mini
       ↓
search_gmail tool
```

## LangGraph

```text
test_graph_search.py
       ↓
LangGraph
       ↓
Agent
       ↓
Tools
       ↓
Gmail API
```

---

# ⚙️ Installation

Clone the repository:

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

Navigate to the project:

```bash
cd AI_Gmail_Assistant
```

Create a virtual environment:

```bash
python -m venv gmail_ai_agent
```

Activate the environment on Windows:

```powershell
gmail_ai_agent\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# 🔑 Environment Configuration

Set the OpenAI API key as an environment variable.

Windows PowerShell:

```powershell
$env:OPENAI_API_KEY="your-api-key"
```

Alternatively, use a `.env` file if the project configuration loads environment variables through `python-dotenv`.

Never commit API keys to GitHub.

---

# 🔐 Google Gmail API Setup

The application requires Gmail API access.

High-level setup:

```text
Google Cloud Console
        ↓
Create / Select Project
        ↓
Enable Gmail API
        ↓
Configure OAuth Consent Screen
        ↓
Create OAuth Client
        ↓
Download credentials.json
        ↓
Place inside credentials/
        ↓
Run application
        ↓
Complete Google OAuth login
```

The generated OAuth token is stored locally and excluded from Git.

---

# ▶️ Running the Application

Activate the virtual environment:

```powershell
gmail_ai_agent\Scripts\activate
```

Run Streamlit:

```powershell
streamlit run app.py
```

The application will open in the browser.

---

# 💬 Example Questions

Once the application is running, users can ask:

```text
How many unread emails do I have?
```

```text
Show my latest 5 emails.
```

```text
Summarize my latest email.
```

```text
Find emails from Google.
```

```text
Find unread emails.
```

```text
Find emails from HDFC Bank.
```

```text
Find emails containing invoices.
```

```text
Show emails with attachments.
```

```text
What action items are present in my emails?
```

```text
What are the high-priority action items?
```

```text
Are there any upcoming deadlines?
```

```text
Are there any meetings mentioned in my emails?
```

```text
Find unread emails from Google and summarize them.
```

---

# 📊 Example User Interaction

```text
User:
Find unread emails from Google.

AI Gmail Assistant:
I found 3 unread emails from Google.

1. Security Alert
2. Account Notification
3. Google Account Update
```

Another example:

```text
User:
What are the high-priority actions in my emails?

AI Gmail Assistant:
I found the following high-priority action:

1. Review the HDFC Bank offer before the limited-time period expires.
```

---

# 🧱 Technology Stack

| Technology         | Purpose                      |
| ------------------ | ---------------------------- |
| Python             | Application development      |
| OpenAI GPT-4o-mini | LLM / reasoning              |
| LangChain          | LLM and tool integration     |
| LangGraph          | Agent workflow orchestration |
| Gmail API          | Gmail access                 |
| Google OAuth 2.0   | Authentication               |
| MCP                | Tool/context integration     |
| Streamlit          | User interface               |
| Pydantic           | Data validation              |
| Tiktoken           | Token handling               |
| Python-dotenv      | Environment configuration    |

---

# 🔄 Production-Oriented Architecture

The current project is designed with separation of responsibilities:

```text
Presentation Layer
        │
        ▼
Streamlit UI
        │
        ▼
Agent Layer
        │
        ▼
LangGraph
        │
        ▼
LLM Layer
        │
        ▼
Tool Layer
        │
        ▼
Service Layer
        │
        ▼
Gmail API
```

This separation makes the application easier to maintain and extend.

---

# 🚀 Future Enhancements

Potential future improvements include:

* Email sending through AI
* Email reply generation
* Draft email creation
* Email categorization
* Automatic priority classification
* Attachment analysis
* PDF/document extraction from attachments
* Calendar integration
* Meeting scheduling
* Gmail label management
* Email archiving
* Email deletion with confirmation
* Redis-based caching
* Async Gmail processing
* Background task processing
* Observability and logging
* LLM evaluation
* Prompt versioning
* Production deployment using Docker
* Cloud deployment
* Role-based access control
* Enterprise authentication

---

# 🔒 Security Considerations

The application handles sensitive email information, so security is important.

Important practices:

* Never commit OAuth credentials.
* Never commit API keys.
* Never expose `token.json`.
* Use environment variables for secrets.
* Use least-privilege Gmail scopes.
* Validate tool inputs.
* Avoid exposing sensitive email content in logs.
* Implement confirmation before destructive Gmail operations.
* Apply authentication and authorization for production deployments.

---

# 📈 Scalability Considerations

For production deployment, the architecture can be extended with:

```text
Load Balancer
      │
      ▼
Multiple Streamlit / API Instances
      │
      ▼
Agent Service
      │
      ├── LLM Service
      │
      ├── Gmail Service
      │
      ├── Redis Cache
      │
      └── Task Queue
```

For large-scale implementations, asynchronous processing and caching can reduce latency and API usage.

---

# 🎯 Key Learning Outcomes

This project demonstrates practical experience with:

* Generative AI
* LLM application development
* Agentic AI
* Function / Tool Calling
* LangChain
* LangGraph
* Gmail API integration
* OAuth 2.0
* Prompt Engineering
* Email summarization
* Information extraction
* Natural-language search
* Conversation memory
* MCP concepts
* Streamlit application development
* Modular Python architecture
* API integration
* AI application testing

---

# 👨‍💻 Project Highlights

The project demonstrates an end-to-end Agentic AI workflow:

```text
Natural Language
       ↓
LLM Reasoning
       ↓
Tool Selection
       ↓
Gmail API
       ↓
Email Retrieval
       ↓
Email Analysis
       ↓
LLM Response
       ↓
User
```

The main objective is to demonstrate how an LLM can interact with real-world external systems through controlled tools instead of simply generating text.

---

# 📌 Project Status

Current capabilities:

* ✅ Gmail OAuth authentication
* ✅ Gmail profile information
* ✅ Unread email count
* ✅ Recent email retrieval
* ✅ Full email retrieval
* ✅ Gmail search
* ✅ Natural-language Gmail search
* ✅ Email summarization
* ✅ Unread email summarization
* ✅ Action item extraction
* ✅ Deadline and meeting extraction
* ✅ Priority analysis
* ✅ LangChain tools
* ✅ LangGraph agent workflow
* ✅ Tool calling
* ✅ Conversation memory
* ✅ Thread-based conversations
* ✅ Streamlit UI
* ✅ New conversation support
* ✅ Modular project architecture
* ✅ Dependency version locking

---

# 📄 License

This project is intended for learning, demonstration, and portfolio purposes.

---

# ⭐ Author

**Nagaraj Kamale**

Generative AI Engineer | Machine Learning Engineer

Focused on:

* Generative AI
* LLM Applications
* RAG
* Agentic AI
* LangChain
* LangGraph
* Python
* Machine Learning

````
