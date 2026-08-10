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
User:
Find unread emails from HDFC Bank.
````

The AI agent determines that it needs to use the Gmail search tool and generates a Gmail query such as:

```text
from:hdfcbank is:unread
```

The Gmail API retrieves the matching emails.

The agent then processes the results and provides a natural-language response.

---

# 🎯 Business Requirement

The objective is to build an AI assistant that can help users manage large volumes of emails efficiently.

The assistant should be able to:

1. Connect securely to Gmail.
2. Retrieve Gmail account information.
3. Count unread emails.
4. Retrieve recent emails.
5. Search emails using Gmail search operators.
6. Read complete email content.
7. Summarize emails.
8. Summarize multiple unread emails.
9. Identify action items.
10. Identify deadlines and meetings.
11. Prioritize important actions.
12. Maintain conversation context.
13. Allow users to start a new conversation.
14. Provide a simple user interface.
15. Allow an LLM agent to decide which Gmail tool should be executed.

---

# 🏗️ High-Level Architecture

```text
                         ┌──────────────────────────┐
                         │        User              │
                         │                          │
                         │ Natural Language Query   │
                         └────────────┬─────────────┘
                                      │
                                      ▼
                         ┌──────────────────────────┐
                         │      Streamlit UI        │
                         │                          │
                         │ Chat Interface           │
                         │ Quick Actions            │
                         │ Gmail Account Info       │
                         └────────────┬─────────────┘
                                      │
                                      ▼
                         ┌──────────────────────────┐
                         │       LangGraph          │
                         │     Agent Workflow       │
                         │                          │
                         │  Chatbot Node            │
                         │        │                 │
                         │        ▼                 │
                         │   Tool Decision          │
                         │        │                 │
                         │        ▼                 │
                         │    Tool Node             │
                         └────────────┬─────────────┘
                                      │
                     ┌────────────────┼────────────────┐
                     │                │                │
                     ▼                ▼                ▼
              Gmail Tools       Analysis Tools    Search Tools
                     │                │                │
                     └────────────────┼────────────────┘
                                      │
                                      ▼
                         ┌──────────────────────────┐
                         │      Gmail Service       │
                         │                          │
                         │ Gmail API                │
                         │ OAuth Authentication     │
                         │ Email Retrieval          │
                         │ Search                   │
                         └────────────┬─────────────┘
                                      │
                                      ▼
                         ┌──────────────────────────┐
                         │       Gmail API          │
                         │                          │
                         │ Inbox                    │
                         │ Messages                 │
                         │ Threads                  │
                         └──────────────────────────┘


                         ┌──────────────────────────┐
                         │      OpenAI GPT-4o-mini  │
                         │                          │
                         │ Reasoning                │
                         │ Tool Selection           │
                         │ Summarization            │
                         │ Email Analysis            │
                         └──────────────────────────┘
```

---

# 🔄 End-to-End Request Flow

The application follows the following flow:

```text
User Question
     │
     ▼
Streamlit UI
     │
     ▼
LangGraph Agent
     │
     ▼
GPT-4o-mini
     │
     ├── Direct Answer
     │
     └── Tool Required
              │
              ▼
         Gmail Tool
              │
              ▼
         Gmail Service
              │
              ▼
          Gmail API
              │
              ▼
         Email Results
              │
              ▼
         GPT-4o-mini
              │
              ▼
       Final Response
              │
              ▼
        Streamlit UI
```

---

# 🧠 Agentic AI Architecture

The core of the application is an Agentic AI workflow.

The LLM is not restricted to answering questions directly.

Instead, it can decide whether a tool is required.

For example:

```text
User:
How many unread emails do I have?
```

The LLM identifies:

```text
Tool Required:
get_unread_email_count
```

The tool accesses Gmail.

The result may be:

```text
You have 7 unread emails.
```

The result is returned to the LLM, which generates the final response.

---

# 🔧 LangGraph Workflow

The LangGraph workflow contains two primary nodes.

```text
              START
                │
                ▼
          ┌─────────────┐
          │   Chatbot   │
          │     Node    │
          └──────┬──────┘
                 │
                 ▼
          Tool Required?
             /       \
           No         Yes
           │           │
           ▼           ▼
          END      ┌─────────┐
                   │  Tools  │
                   │   Node  │
                   └────┬────┘
                        │
                        ▼
                    Chatbot
                        │
                        ▼
                       END
```

The workflow uses:

```python
StateGraph
START
END
ToolNode
tools_condition
```

This enables the agent to dynamically select and execute Gmail tools.

---

# 🛠️ Gmail Tools

The application exposes Gmail functionality to the LangGraph agent through LangChain tools.

Current tools include:

### 1. Get Unread Email Count

```text
get_unread_email_count()
```

Example:

```text
User:
How many unread emails do I have?
```

---

### 2. Get Recent Emails

```text
get_recent_emails()
```

Example:

```text
User:
Show my latest emails.
```

---

### 3. Summarize Latest Email

```text
summarize_latest_email()
```

Example:

```text
User:
Summarize my latest email.
```

---

### 4. Summarize Unread Emails

```text
summarize_unread_emails()
```

Example:

```text
User:
Summarize my unread emails.
```

---

### 5. Gmail Search

```text
search_gmail(query)
```

This supports Gmail search operators.

Examples:

```text
from:google
```

```text
from:hdfcbank
```

```text
subject:invoice
```

```text
has:attachment
```

```text
is:unread
```

```text
newer_than:1d
```

---

### 6. Extract Action Items

```text
extract_action_items()
```

The tool analyzes emails and identifies tasks that require user action.

Example output:

```text
ACTION ITEMS

1. Action: Complete a short form to indicate job preferences
   Sender: IBM Talent Acquisition
   Priority: Medium

2. Action: Review the personal loan offer
   Sender: HDFC Bank
   Priority: High
```

---

### 7. Extract Deadlines and Meetings

```text
extract_deadlines_and_meetings()
```

This analyzes email content to identify:

* Meetings
* Deadlines
* Important dates
* Time-sensitive activities

---

# 🔎 Advanced Gmail Search

The assistant supports Gmail search operators.

Examples:

```text
from:google
```

Find emails from Google.

```text
from:hdfcbank
```

Find emails from HDFC Bank.

```text
subject:invoice
```

Find emails containing "invoice" in the subject.

```text
has:attachment
```

Find emails containing attachments.

```text
is:unread
```

Find unread emails.

```text
newer_than:7d
```

Find emails from the last seven days.

Multiple operators can also be combined.

Example:

```text
from:hdfcbank is:unread
```

---

# 🔐 Gmail Authentication

The application uses the Gmail API with OAuth 2.0.

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
Permission Approval
     │
     ▼
Access Token
     │
     ▼
Gmail API
```

OAuth files are stored locally under:

```text
credentials/
```

The following files are intentionally excluded from Git:

```text
credentials.json
token.json
```

They are included in `.gitignore` to prevent sensitive authentication information from being committed to GitHub.

---

# 🤖 LLM Configuration

The project uses:

```text
OpenAI GPT-4o-mini
```

The LLM is initialized through:

```text
models/llm.py
```

The model is configured with:

```python
ChatOpenAI(
    model="gpt-4o-mini",
    temperature=0
)
```

Temperature is set to `0` to provide more deterministic responses for email-related operations.

The API key is retrieved from:

```text
OPENAI_API_KEY
```

---

# 🧩 Conversation Memory

The application supports conversation memory using LangGraph checkpointing.

Each conversation receives a unique:

```text
thread_id
```

Example:

```text
550e8400-e29b-41d4-a716-446655440000
```

The thread ID allows the LangGraph workflow to maintain conversation state.

Example:

```text
User:
Find my HDFC emails.

Assistant:
I found several HDFC emails.

User:
Which of those are high priority?

Assistant:
The high-priority emails are...
```

The second question can use the context established during the conversation.

---

# 🆕 New Conversation

The Streamlit application provides a:

```text
🆕 New Conversation
```

button.

When clicked:

1. A new thread ID is generated.
2. Previous visible chat history is cleared.
3. Pending quick actions are cleared.
4. A new conversation starts.

---

# 🖥️ Streamlit Interface

The application provides:

### Gmail Account Information

The sidebar displays:

```text
Connected

Email
Unread Emails
Total Emails
Threads
```

---

### Quick Actions

The sidebar contains:

```text
📬 Unread Count
📩 Recent Emails
📝 Summarize Latest
```

These buttons automatically send predefined questions to the LangGraph agent.

---

### Chat Interface

Users can enter natural-language questions such as:

```text
Find emails from Google.
```

```text
Summarize my unread emails.
```

```text
What action items do I have?
```

```text
Are there any upcoming deadlines?
```

```text
Find unread emails from HDFC Bank.
```

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
│   └── ...
│
├── credentials/
│   ├── credentials.json
│   └── token.json
│
├── images/
│   └── ...
│
├── mcp_server/
│   └── ...
│
├── models/
│   ├── __init__.py
│   └── llm.py
│
├── prompts/
│   └── ...
│
├── schemas/
│   └── ...
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
│   └── ...
│
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
│
├── test_auth.py
├── test_search.py
├── test_search_tool.py
├── test_search_full.py
├── test_search_details.py
├── test_agent_search.py
├── test_agent_search_loop.py
├── test_graph_search.py
│
├── test_summary.py
├── test_unread_details.py
├── test_unread_summary.py
├── test_unread_tool.py
│
├── test_action_items.py
├── test_action_tool.py
├── test_deadlines.py
├── test_deadlines_tool.py
├── test_priority.py
│
├── test_email_analysis.py
├── test_multi_tool.py
├── test_memory.py
├── test_graph_action_search.py
└── test_graph_memory_action.py
```

> Note: `credentials/` exists locally but is excluded from version control using `.gitignore`.

---

# 📂 Folder Responsibilities

## `agents/`

Contains the Agentic AI and LangGraph workflow.

Important files:

```text
agent.py
```

Creates the LLM agent and binds Gmail tools.

```text
graph.py
```

Creates and compiles the LangGraph workflow.

```text
nodes.py
```

Contains LangGraph nodes.

```text
state.py
```

Defines the agent state.

---

## `services/`

Contains Gmail and business logic.

### `auth_service.py`

Responsible for Gmail OAuth authentication.

### `gmail_service.py`

Responsible for:

* Gmail API communication
* Profile retrieval
* Unread email retrieval
* Recent email retrieval
* Email search
* Full email retrieval
* Header extraction
* Email body extraction

### `summary_service.py`

Responsible for using GPT-4o-mini to summarize email content.

---

## `tools/`

Contains LangChain tools exposed to the AI agent.

```text
gmail_tools.py
```

Converts Gmail functionality into tools that the LLM can call.

---

## `models/`

Contains LLM configuration.

```text
llm.py
```

Creates the reusable GPT-4o-mini model instance.

---

## `mcp_server/`

Contains MCP-related components for exposing or integrating Gmail capabilities through the Model Context Protocol.

---

## `prompts/`

Contains reusable prompts used for email analysis and LLM processing.

---

## `schemas/`

Contains structured data definitions used by the application.

---

## `utils/`

Contains reusable utility functionality such as logging and helper functions.

---

# 🧪 Testing Strategy

The project follows incremental testing.

Individual components were tested before integrating them into LangGraph and Streamlit.

---

## Authentication Testing

```bash
python test_auth.py
```

Validates Gmail OAuth authentication.

---

## Gmail Search Testing

```bash
python test_search.py
```

Tests Gmail search functionality.

---

## Gmail Search Tool Testing

```bash
python test_search_tool.py
```

Tests the LangChain Gmail search tool.

---

## Full Email Search Testing

```bash
python test_search_full.py
```

Tests retrieval of complete email content.

---

## Agent Search Testing

```bash
python test_agent_search.py
```

Tests whether the LLM correctly identifies and calls the Gmail search tool.

---

## Agent Search Loop Testing

```bash
python test_agent_search_loop.py
```

Tests the complete:

```text
LLM → Tool → Result → LLM
```

cycle.

---

## LangGraph Search Testing

```bash
python test_graph_search.py
```

Tests the Gmail search capability through the LangGraph workflow.

---

## Action Item Testing

```bash
python test_action_items.py
```

Tests action-item extraction.

---

## Action Tool Testing

```bash
python test_action_tool.py
```

Tests the action-item LangChain tool.

---

## Deadline Testing

```bash
python test_deadlines.py
```

Tests deadline and meeting extraction.

---

## Deadline Tool Testing

```bash
python test_deadlines_tool.py
```

Tests the deadline/meeting LangChain tool.

---

## Memory Testing

```bash
python test_memory.py
```

Tests LangGraph conversation memory.

---

## Graph Memory Testing

```bash
python test_graph_memory_action.py
```

Tests memory together with Gmail analysis and action-item processing.

---

# ⚙️ Installation

## 1. Clone the Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

Navigate into the project:

```bash
cd AI_Gmail_Assistant
```

---

# 🐍 Create Virtual Environment

Windows:

```bash
python -m venv gmail_ai_agent
```

Activate it:

```bash
gmail_ai_agent\Scripts\activate
```

---

# 📦 Install Dependencies

Install the project dependencies:

```bash
python -m pip install -r requirements.txt
```

---

# 🔑 Configure OpenAI API Key

Set the OpenAI API key as an environment variable.

Windows PowerShell:

```powershell
$env:OPENAI_API_KEY="your-api-key"
```

Alternatively, configure it permanently through Windows Environment Variables.

Do not commit API keys to GitHub.

---

# 🔐 Configure Gmail API

Create a Google Cloud project and enable the Gmail API.

Create OAuth credentials for a desktop application.

Download the OAuth credentials file and place it locally as:

```text
credentials/credentials.json
```

Run:

```bash
python test_auth.py
```

Complete the Google OAuth authentication flow.

The application will create:

```text
credentials/token.json
```

The credentials directory must remain excluded from Git.

---

# ▶️ Run the Application

Use Streamlit:

```bash
python -m streamlit run app.py
```

or:

```bash
streamlit run app.py
```

If `streamlit` is not recognized on Windows, use:

```bash
python -m streamlit run app.py
```

This ensures Streamlit is executed from the active Python environment.

---

# 💬 Example Questions

After starting the application, users can ask:

### Basic Gmail Questions

```text
How many unread emails do I have?
```

```text
Show my latest emails.
```

```text
Summarize my latest email.
```

---

### Search Questions

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
Find emails with invoices.
```

```text
Find emails with attachments.
```

```text
Find emails received in the last 7 days.
```

---

### Email Analysis

```text
Summarize my unread emails.
```

```text
What action items do I have?
```

```text
What are my high-priority actions?
```

```text
Are there any deadlines in my emails?
```

```text
Do I have any upcoming meetings?
```

---

### Conversational Questions

```text
Find my HDFC emails.
```

Then:

```text
Which ones are important?
```

Then:

```text
Are there any actions I need to take?
```

This demonstrates the conversation-memory capability.

---

# 🔄 Example Agent Execution

Example:

```text
User:
Find unread emails from HDFC Bank.
```

The agent determines:

```text
search_gmail
```

with:

```text
from:hdfcbank is:unread
```

The tool calls Gmail API.

Gmail returns matching messages.

The results are passed back to the agent.

GPT-4o-mini generates:

```text
I found 3 unread emails from HDFC Bank.

1. Important Update on your HDFC Bank Account
2. Limited Time Personal Loan Offer
3. Your Monthly Statement
```

---

# 🧠 Example Action Item Flow

```text
User
 │
 │ "What action items do I have?"
 ▼
LangGraph Agent
 │
 ▼
extract_action_items
 │
 ▼
GmailService
 │
 ▼
Retrieve Emails
 │
 ▼
GPT-4o-mini
 │
 ▼
Analyze Email Content
 │
 ▼
Action Items
 │
 ▼
LangGraph
 │
 ▼
Final Response
```

Example:

```text
ACTION ITEMS

1. Complete a short form to indicate job preferences
   Sender: IBM Talent Acquisition
   Priority: Medium

2. Review the personal loan offer
   Sender: HDFC Bank
   Priority: High
```

---

# 🏆 Key Features

* Gmail API integration
* OAuth 2.0 authentication
* GPT-4o-mini integration
* LangChain tools
* LangGraph agent workflow
* Tool calling
* Gmail search operators
* Natural-language email search
* Email summarization
* Unread email analysis
* Action-item extraction
* Deadline detection
* Meeting detection
* Priority analysis
* Conversation memory
* Thread-based conversations
* Streamlit UI
* Quick actions
* New conversation support
* Modular architecture
* Component-level testing

---

# 🧰 Technology Stack

| Technology         | Purpose                             |
| ------------------ | ----------------------------------- |
| Python             | Application development             |
| OpenAI GPT-4o-mini | LLM                                 |
| LangChain          | LLM and tool integration            |
| LangGraph          | Agent workflow and state management |
| Gmail API          | Gmail access                        |
| Google OAuth 2.0   | Authentication                      |
| Streamlit          | Web UI                              |
| MCP                | Model Context Protocol integration  |
| Pydantic           | Data validation                     |
| Tiktoken           | Token processing                    |
| Pandas             | Data processing                     |

---

# 🔒 Security Considerations

Sensitive information should never be committed to GitHub.

The following files are excluded:

```text
credentials/
credentials.json
token.json
token.pickle
.env
.env.*
*.key
*.pem
```

API keys should be stored using environment variables or a secure secret-management solution.

For production deployment, additional security measures should be implemented, including:

* Secret management
* OAuth token encryption
* Access control
* Audit logging
* Least-privilege Gmail scopes
* Secure deployment configuration
* Rate limiting
* Monitoring

---

# 📈 Production Improvements

The current project provides a strong foundation for an Agentic AI Gmail assistant.

Potential future enhancements include:

### 1. Email Classification

Automatically classify emails:

```text
Important
Promotional
Financial
Work
Personal
Security
Newsletter
```

### 2. Priority Scoring

Automatically calculate:

```text
High
Medium
Low
```

priority.

### 3. Smart Inbox

Create an AI-powered inbox:

```text
🔥 Critical
⚡ Action Required
📅 Upcoming
📢 Notifications
📰 Newsletters
💰 Financial
```

### 4. Email Draft Generation

Allow the assistant to generate email replies.

Example:

```text
Reply to this email professionally.
```

### 5. Calendar Integration

Integrate Google Calendar to identify meetings and deadlines.

### 6. Background Processing

Process large numbers of emails asynchronously.

### 7. Caching

Use Redis or another caching layer to reduce repeated Gmail API calls.

### 8. Observability

Add:

* Structured logging
* Metrics
* Tracing
* Error monitoring
* Agent execution monitoring

### 9. Deployment

Potential deployment architecture:

```text
                    Internet
                       │
                       ▼
                 Load Balancer
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
        Streamlit App       Streamlit App
             │                   │
             └─────────┬─────────┘
                       ▼
                 Agent Service
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
       Gmail API    OpenAI API    Cache
```

---

# ⚠️ Important Limitations

This project currently focuses primarily on Gmail reading, searching, summarization, and analysis.

The assistant does not automatically:

* Send emails
* Delete emails
* Modify emails
* Move emails
* Mark emails as read
* Create calendar events

unless those capabilities are explicitly implemented and authorized.

This is intentional because Gmail write operations require additional safety controls and OAuth permissions.

---

# 📊 Project Architecture Summary

```text
┌──────────────────────────────────────────────────────────────┐
│                         USER                                 │
└────────────────────────────┬─────────────────────────────────┘
                             │
                             ▼
┌──────────────────────────────────────────────────────────────┐
│                      STREAMLIT UI                            │
│                                                              │
│ Chat │ Quick Actions │ Gmail Statistics │ New Conversation │
└────────────────────────────┬─────────────────────────────────┘
                             │
                             ▼
┌──────────────────────────────────────────────────────────────┐
│                       LANGGRAPH                              │
│                                                              │
│                    ┌──────────────┐                          │
│                    │   Chatbot    │                          │
│                    │     Node     │                          │
│                    └──────┬───────┘                          │
│                           │                                   │
│                    Tool Required?                            │
│                       /        \                              │
│                      /          \                             │
│                    No            Yes                          │
│                    │              │                           │
│                    ▼              ▼                           │
│                   END        ┌──────────┐                     │
│                              │ ToolNode │                     │
│                              └────┬─────┘                     │
│                                   │                           │
│                                   ▼                           │
│                               Chatbot                         │
└────────────────────────────────┬─────────────────────────────┘
                                 │
                ┌────────────────┼─────────────────┐
                │                │                 │
                ▼                ▼                 ▼
        Gmail Search       Email Summary     Email Analysis
                │                │                 │
                └────────────────┼─────────────────┘
                                 │
                                 ▼
                        ┌─────────────────┐
                        │  Gmail Service  │
                        └────────┬────────┘
                                 │
                                 ▼
                        ┌─────────────────┐
                        │    Gmail API    │
                        └─────────────────┘

                                 ▲
                                 │
                        ┌─────────────────┐
                        │   GPT-4o-mini   │
                        │                 │
                        │ Tool Selection  │
                        │ Summarization   │
                        │ Analysis        │
                        └─────────────────┘
```

---

# 🧑‍💻 Development Approach

The project was developed incrementally.

### Phase 1 — Gmail Authentication

```text
Google OAuth
     ↓
Gmail API Connection
```

### Phase 2 — Gmail Operations

```text
Profile
Unread Count
Recent Emails
Full Email
Search
```

### Phase 3 — AI Processing

```text
Email Summarization
Unread Email Summarization
Action Item Extraction
Deadline Extraction
Priority Analysis
```

### Phase 4 — LangChain Tools

Gmail operations were exposed as tools.

```text
Gmail Service
     ↓
LangChain Tools
     ↓
LLM
```

### Phase 5 — LangGraph Agent

The tools were connected to a LangGraph workflow.

```text
Chatbot
   ↓
Tool Decision
   ↓
Tool
   ↓
Chatbot
```

### Phase 6 — Advanced Search

Natural-language Gmail search was implemented using Gmail search operators.

### Phase 7 — Conversation Memory

Thread-based conversation state was introduced using LangGraph checkpointing.

### Phase 8 — Streamlit Integration

The complete AI Gmail assistant was integrated into a Streamlit UI.

---

# 🧪 Current Project Status

```text
✅ Gmail OAuth Authentication
✅ Gmail API Integration
✅ Gmail Profile
✅ Unread Email Count
✅ Recent Email Retrieval
✅ Full Email Retrieval
✅ Gmail Search
✅ Gmail Search Operators
✅ LangChain Tools
✅ GPT-4o-mini Integration
✅ Email Summarization
✅ Unread Email Summarization
✅ Action Item Extraction
✅ Deadline/Meeting Extraction
✅ Priority Analysis
✅ LangGraph Agent
✅ Tool Calling
✅ Agent Search Loop
✅ Conversation Memory
✅ Thread IDs
✅ New Conversation
✅ Streamlit UI
✅ Quick Actions
✅ Component Testing
✅ requirements.txt
✅ .gitignore
```

---

# 📌 Future Roadmap

```text
⬜ Email Reply Generation
⬜ Email Sending
⬜ Email Draft Creation
⬜ Gmail Labels
⬜ Email Classification
⬜ Calendar Integration
⬜ Redis Caching
⬜ Async Gmail Processing
⬜ Background Workers
⬜ Production Authentication
⬜ Monitoring
⬜ Tracing
⬜ Evaluation Framework
⬜ Docker Deployment
⬜ Cloud Deployment
```

---

# 👨‍💻 Author

**Nagaraj Kamale**

Generative AI Engineer

Areas of interest:

* Generative AI
* LLM Applications
* Agentic AI
* RAG
* LangChain
* LangGraph
* Prompt Engineering
* NLP
* Machine Learning
* AI Application Development

---

# ⭐ Project Highlights

This project demonstrates practical implementation of:

```text
LLM
 ↓
Tool Calling
 ↓
Agentic AI
 ↓
LangGraph
 ↓
Gmail API
 ↓
Email Analysis
 ↓
Conversation Memory
 ↓
Streamlit
```

It is designed as a practical example of how an LLM can interact with external APIs through tools and make decisions dynamically rather than simply generating text.

---

# 📜 License

This project is intended for educational, learning, and portfolio purposes.

Before deploying the application in a production environment, ensure that Gmail API usage, OAuth scopes, OpenAI API usage, privacy requirements, and organizational security policies are properly reviewed.

````

### One important GitHub note

Before pushing, keep these **out of GitHub**:

```text
credentials/credentials.json
credentials/token.json
.env
API keys
OAuth tokens
````

Your current `.gitignore` already covers the Gmail credentials directory, so **do not remove that rule**.

For your GitHub repository, I would also recommend that the repository contain the **README + source code + `requirements.txt` + `.gitignore`**, while the actual Gmail OAuth credentials remain only on your local machine.
