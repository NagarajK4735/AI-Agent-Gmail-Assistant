````markdown
# 📧 AI Gmail Assistant

An AI-powered Gmail assistant that allows users to interact with their Gmail inbox using natural language.

The application combines the Gmail API, OpenAI GPT-4o-mini, LangChain, LangGraph, and Streamlit to provide an intelligent conversational interface for email management and analysis.

---

## 🚀 Project Overview

Managing a large number of emails manually can be time-consuming.

Users typically need to:

- Check unread emails
- Search emails
- Find emails from specific senders
- Find emails based on subjects
- Read recent emails
- Summarize emails
- Identify action items
- Identify deadlines and meetings
- Analyze email content
- Ask follow-up questions

The AI Gmail Assistant provides a conversational interface where users can ask questions such as:

> How many unread emails do I have?

> Show my latest emails.

> Find emails from Google.

> Show emails from HDFC Bank.

> Find emails containing invoices.

> Summarize my latest email.

> What action items are present in my emails?

> Do I have any upcoming deadlines or meetings?

The application determines which Gmail operation is required and invokes the appropriate tool.

---

# 🏗️ Architecture

The application follows an agentic architecture using LangGraph.

```mermaid
flowchart TD

    A[User] --> B[Streamlit UI]

    B --> C[LangGraph Agent]

    C --> D[GPT-4o-mini]

    D --> E{Tool Required?}

    E -->|No| F[Generate Response]

    E -->|Yes| G[Gmail Tools]

    G --> H[GmailService]

    H --> I[Gmail API]

    I --> J[Gmail Account]

    J --> H
    H --> G
    G --> C

    C --> K[Conversation Memory]

    K --> C

    C --> B

    B --> F
````

---

# 🔄 Application Flow

The high-level request flow is:

```text
User
  │
  ▼
Streamlit UI
  │
  ▼
LangGraph
  │
  ▼
GPT-4o-mini
  │
  ├── Direct answer
  │
  └── Tool call
          │
          ▼
      Gmail Tool
          │
          ▼
      GmailService
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
      LangGraph
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

# 🧩 Main Components

## 1. Streamlit UI

File:

```text
app.py
```

Responsibilities:

* Provide the chat interface
* Display Gmail account information
* Display unread email count
* Display total emails
* Provide quick actions
* Maintain conversation state
* Maintain conversation/thread ID
* Display assistant responses
* Send user requests to LangGraph

---

## 2. Gmail Authentication

File:

```text
services/auth_service.py
```

Responsibilities:

* Authenticate with Google
* Handle Gmail OAuth
* Create Gmail API credentials
* Reuse the OAuth token when available
* Establish an authenticated Gmail API service

OAuth files are stored locally:

```text
credentials/
├── credentials.json
└── token.json
```

These files are excluded from Git using `.gitignore`.

---

# 3. Gmail Service

File:

```text
services/gmail_service.py
```

This layer acts as the interface between the application and Gmail API.

Responsibilities include:

* Retrieve Gmail profile
* Count unread emails
* Retrieve recent emails
* Retrieve complete email details
* Search Gmail
* Extract email headers
* Extract email body
* Retrieve email metadata
* Retrieve email content

Example Gmail search:

```text
from:google
```

or:

```text
subject:invoice
```

or:

```text
is:unread
```

or:

```text
has:attachment
```

---

# 4. Gmail Tools

File:

```text
tools/gmail_tools.py
```

This layer exposes Gmail operations to the LangChain/LangGraph agent.

Current tools include functionality such as:

```text
get_unread_email_count
get_recent_emails
summarize_latest_email
summarize_unread_emails
search_gmail
extract_action_items
extract_deadlines_and_meetings
```

The tools act as the bridge between the LLM and Gmail services.

---

# 5. LLM Layer

File:

```text
models/llm.py
```

The project uses:

```text
GPT-4o-mini
```

The LLM is configured as a reusable model instance.

Example configuration:

```python
ChatOpenAI(
    model="gpt-4o-mini",
    temperature=0
)
```

Temperature is set to `0` to make responses more deterministic.

---

# 6. LangGraph Agent

Files:

```text
agents/
├── agent.py
├── graph.py
├── nodes.py
└── state.py
```

LangGraph controls the agent workflow.

The agent can:

1. Receive the user's request.
2. Send the request to GPT-4o-mini.
3. Determine whether a tool is required.
4. Invoke the appropriate Gmail tool.
5. Receive the tool result.
6. Send the result back to the LLM.
7. Generate the final response.

---

# 7. Agent State

File:

```text
agents/state.py
```

The application maintains the conversation messages inside the LangGraph state.

Conceptually:

```text
AgentState
    │
    └── messages
          │
          ├── HumanMessage
          ├── AIMessage
          ├── ToolMessage
          └── AIMessage
```

This allows the agent to maintain conversational context.

---

# 8. LangGraph Workflow

File:

```text
agents/graph.py
```

The graph contains:

```text
START
  │
  ▼
chatbot
  │
  ▼
Tool required?
  │
 ┌┴───────────┐
 │            │
No           Yes
 │            │
 ▼            ▼
END         tools
              │
              ▼
           chatbot
```

The important advantage of this design is that the LLM can perform multiple reasoning/tool steps before producing the final answer.

---

# 🧠 Agentic Behavior

The assistant does not require a separate hard-coded function for every natural-language question.

For example, the user can ask:

```text
Find emails from Google.
```

The LLM can determine that:

```text
search_gmail
```

is required and generate:

```text
query = "from:google"
```

The tool executes the Gmail API search.

The result is returned to the agent.

The LLM then converts the result into a human-readable response.

---

# 🔍 Gmail Search

The assistant supports Gmail search operators.

Examples:

| User Request            | Gmail Query       |
| ----------------------- | ----------------- |
| Emails from Google      | `from:google`     |
| Unread emails           | `is:unread`       |
| Emails with attachments | `has:attachment`  |
| Invoice emails          | `subject:invoice` |
| Recent emails           | `newer_than:1d`   |
| Emails from HDFC        | `from:hdfcbank`   |

The LLM converts the natural-language request into an appropriate Gmail search query.

---

# 📝 Email Summarization

The application can summarize email content using GPT-4o-mini.

The summarization process is:

```text
Gmail Email
    │
    ▼
Extract sender
    │
    ▼
Extract subject
    │
    ▼
Extract body
    │
    ▼
Build summarization prompt
    │
    ▼
GPT-4o-mini
    │
    ▼
Concise summary
```

The summary can contain:

* Sender
* Subject
* Main purpose
* Important dates
* Action items

---

# ✅ Action Item Extraction

The assistant can analyze email content and identify tasks that require user action.

Example:

```text
ACTION ITEMS

1. Complete the IBM job preference form
   Priority: Medium

2. Review the HDFC personal loan offer
   Priority: High
```

The system attempts to distinguish actual actions from general informational or promotional content.

---

# 📅 Deadline and Meeting Detection

The assistant can analyze emails for:

* Meetings
* Interviews
* Appointments
* Submission deadlines
* Payment deadlines
* Important dates

Example:

```text
DEADLINES AND MEETINGS

Meeting:
Technical Interview

Date:
August 15, 2026

Action:
Attend the scheduled interview
```

---

# 💬 Conversation Memory

The application maintains a conversation/thread ID.

Example:

```text
thread_id
    │
    ▼
LangGraph Checkpointer
    │
    ▼
Conversation State
```

This enables follow-up questions.

Example:

```text
User:
Show me emails from HDFC.

Assistant:
Here are the HDFC emails...

User:
Which of those require action?

Assistant:
The HDFC emails containing the following action items...
```

The second question can be interpreted in the context of the conversation.

---

# 🔐 Security

Sensitive Gmail OAuth files are not committed to the repository.

The following directory is excluded:

```text
credentials/
```

Sensitive files include:

```text
credentials.json
token.json
```

The `.gitignore` also excludes:

```text
.env
*.key
*.pem
```

API keys should be supplied through environment variables rather than hard-coded in source code.

---

# 📦 Installation

## 1. Clone the repository

```bash
git clone <your-github-repository-url>
```

```bash
cd AI_Gmail_Assistant
```

---

## 2. Create a virtual environment

Windows:

```powershell
python -m venv gmail_ai_agent
```

Activate it:

```powershell
gmail_ai_agent\Scripts\activate
```

---

## 3. Install dependencies

```powershell
python -m pip install -r requirements.txt
```

---

# 🔑 Configuration

Set the OpenAI API key as an environment variable.

Windows PowerShell:

```powershell
$env:OPENAI_API_KEY="your-api-key"
```

Alternatively, use a `.env` file if your configuration supports it.

Do not commit API keys to GitHub.

---

# 📧 Gmail API Configuration

The application requires Gmail API access.

High-level setup:

```text
Google Cloud Project
        │
        ▼
Enable Gmail API
        │
        ▼
Configure OAuth Consent
        │
        ▼
Create OAuth Client
        │
        ▼
Download credentials.json
        │
        ▼
credentials/
        │
        ▼
Run application
        │
        ▼
Google OAuth Login
        │
        ▼
token.json
```

The generated OAuth token should remain local and should never be committed to GitHub.

---

# ▶️ Running the Application

Start the Streamlit application using:

```powershell
streamlit run app.py
```

If `streamlit` is not recognized, use:

```powershell
python -m streamlit run app.py
```

The second form is especially useful when working inside a Python virtual environment.

---

# 🧪 Testing

The project contains multiple test scripts covering different components.

Examples:

```text
test_auth.py
test_search.py
test_summary.py
test_action_items.py
test_deadlines.py
test_memory.py
test_graph_search.py
test_graph_action_search.py
test_graph_memory_action.py
```

Testing covers:

* Gmail authentication
* Gmail search
* Email retrieval
* Email summarization
* Action-item extraction
* Deadline detection
* Agent tool selection
* LangGraph execution
* Conversation memory

---

# 🛠️ Technology Stack

| Technology         | Purpose                            |
| ------------------ | ---------------------------------- |
| Python             | Application development            |
| Streamlit          | User interface                     |
| OpenAI GPT-4o-mini | LLM                                |
| LangChain          | LLM/tool integration               |
| LangGraph          | Agent workflow                     |
| Gmail API          | Gmail access                       |
| Google OAuth       | Authentication                     |
| Pydantic           | Data validation                    |
| tiktoken           | Token processing                   |
| MCP                | Model Context Protocol integration |
| Git/GitHub         | Version control                    |

---

# 📂 Project Structure

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
│   ├── credentials.json
│   └── token.json
│
├── images/
│
├── mcp_server/
│
├── models/
│   └── llm.py
│
├── prompts/
│
├── schemas/
│
├── services/
│   ├── auth_service.py
│   ├── gmail_service.py
│   └── summary_service.py
│
├── tools/
│   └── gmail_tools.py
│
├── utils/
│
├── .gitignore
├── app.py
├── requirements.txt
└── README.md
```

> `credentials/` is intentionally excluded from version control.

---

# 🎯 Key Features

* Gmail OAuth authentication
* Gmail profile information
* Unread email count
* Recent email retrieval
* Natural-language Gmail search
* Gmail search operators
* Full email retrieval
* Email body extraction
* Email summarization
* Unread email summarization
* Action-item extraction
* Deadline detection
* Meeting detection
* LangChain tools
* LangGraph agent
* Tool calling
* Conversation memory
* Streamlit chat interface
* Quick Gmail actions
* New conversation support
* Gmail API integration
* Secure credential handling

---

# 🔮 Future Enhancements

Potential future improvements include:

* Email categorization
* Priority classification
* Spam detection
* Attachment analysis
* PDF/document extraction from attachments
* Email drafting
* Reply generation
* Email sending with confirmation
* Calendar integration
* Gmail label management
* Advanced multi-step agents
* Redis-backed conversation memory
* Production logging
* Monitoring and observability
* Automated evaluation
* Docker deployment
* Cloud deployment
* Role-based access control

---

# ⚠️ Security Notes

Never commit:

```text
credentials.json
token.json
.env
API keys
private keys
OAuth secrets
```

Always verify `.gitignore` before pushing the repository.

---

# 👨‍💻 Author

Nagaraj Kamale

Generative AI Engineer

Skills demonstrated in this project:

* Python
* Generative AI
* LLMs
* LangChain
* LangGraph
* OpenAI
* Gmail API
* Agentic AI
* Tool Calling
* Prompt Engineering
* Streamlit
* OAuth

````

---

# 3. Architecture You Can Explain in an Interview

This is the **most important part** for you because this project can now become one of your strongest GenAI project explanations.

### High-level architecture

```text
                         ┌─────────────────────┐
                         │       USER          │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    STREAMLIT UI     │
                         │                     │
                         │ Chat + Quick Action │
                         └──────────┬──────────┘
                                    │
                                    ▼
                    ┌─────────────────────────────┐
                    │        LANGGRAPH            │
                    │                             │
                    │  ┌───────────────────────┐  │
                    │  │       Chatbot         │  │
                    │  └───────────┬───────────┘  │
                    │              │              │
                    │       Tool required?       │
                    │          /       \           │
                    │        No         Yes       │
                    └───────┬────────────┬─────────┘
                            │            │
                            │            ▼
                            │     ┌──────────────┐
                            │     │ Gmail Tools  │
                            │     └──────┬───────┘
                            │            │
                            │            ▼
                            │     ┌──────────────┐
                            │     │ GmailService │
                            │     └──────┬───────┘
                            │            │
                            │            ▼
                            │     ┌──────────────┐
                            │     │  Gmail API   │
                            │     └──────┬───────┘
                            │            │
                            │            ▼
                            │     ┌──────────────┐
                            │     │ Gmail Inbox  │
                            │     └──────────────┘
                            │
                            ▼
                    ┌───────────────────┐
                    │   GPT-4o-mini     │
                    │ Response          │
                    │ Generation        │
                    └─────────┬─────────┘
                              │
                              ▼
                       ┌────────────┐
                       │  Response  │
                       │     UI     │
                       └────────────┘
````

---

# 4. Component Responsibilities

A very easy way to remember the architecture is:

| Layer                  | Responsibility                         |
| ---------------------- | -------------------------------------- |
| **Streamlit**          | User interface                         |
| **LangGraph**          | Agent orchestration                    |
| **GPT-4o-mini**        | Reasoning and response generation      |
| **Tools**              | Expose Gmail capabilities to the agent |
| **GmailService**       | Gmail business/API operations          |
| **Gmail API**          | Access actual Gmail data               |
| **AuthService**        | OAuth authentication                   |
| **SummaryService**     | LLM-based email summarization          |
| **State/Checkpointer** | Conversation memory                    |

---

# 5. The Interview Story

If the interviewer says:

> **"Explain your Gmail AI Assistant project."**

You can answer:

> "I developed an AI-powered Gmail assistant using Python, Streamlit, OpenAI GPT-4o-mini, LangChain, LangGraph and Gmail API. The objective was to allow users to interact with their Gmail inbox using natural language instead of manually searching through emails."

Then continue:

> "The user interacts through a Streamlit chat interface. The request is passed to a LangGraph agent powered by GPT-4o-mini. Based on the user's request, the agent decides whether it can answer directly or needs to invoke a Gmail tool."

Then explain the important part:

> "For example, if the user asks 'Find emails from HDFC Bank', the LLM selects the `search_gmail` tool and generates an appropriate Gmail search query such as `from:hdfcbank`. The tool calls the GmailService, which communicates with the Gmail API. The retrieved emails are then returned to the LangGraph agent, and GPT-4o-mini converts the results into a natural-language response."

Then mention memory:

> "I also implemented conversation memory using LangGraph's checkpointer and thread IDs, which allows the assistant to maintain context across follow-up questions."

Finally:

> "I also implemented capabilities such as email summarization, unread email analysis, action-item extraction, deadline and meeting detection, and natural-language Gmail search."

That's a **much stronger project explanation** than simply saying:

> "I created a chatbot for Gmail."

---

## One important GitHub step before you push

Because your project contains:

```text
credentials/
    credentials.json
    token.json
```

**do not push those files.**

Your `.gitignore` is already configured correctly.

Also, before the first GitHub push, I strongly recommend moving the development test scripts into:

```text
tests/
```

so your final repository becomes:

```text
AI_Gmail_Assistant/
│
├── agents/
├── config/
├── images/
├── mcp_server/
├── models/
├── prompts/
├── schemas/
├── services/
├── tools/
├── utils/
├── tests/
│
├── .gitignore
├── app.py
├── requirements.txt
└── README.md
```

That is the structure I'd use for your **final GitHub version**.
