# Dentsu Smart Buddy

### AI-Powered Research & Data Analysis Assistant

Dentsu Smart Buddy is a **Streamlit-based AI research assistant** designed to help users research information, interact with documents, analyze CSV/Excel data, and retrieve information from web sources through a conversational interface.

The application combines **Azure OpenAI, LangChain, web search, document processing, data analysis, and conversational AI** into a single assistant.

---

## ✨ Features

### 🤖 AI Research Assistant

* Conversational AI interface powered by Azure OpenAI.
* Keyword-based routing for different types of user requests.
* Supports questions about research, analysis, current information, and general assistance.
* Designed to use web search for current events, news, sports, elections, rankings, and similar time-sensitive topics.

### 🌐 URL & Web Content Analysis

* Enter a blog or webpage URL directly into the application.
* Loads webpage content using web document loaders.
* Ask questions about the loaded webpage.
* Useful for research, article analysis, and information extraction.

### 📄 Document Q&A

Upload and interact with documents such as:

* PDF
* DOCX
* TXT
* Images

The assistant can process uploaded content and use it as context for conversational Q&A.

### 📊 CSV & Excel Analysis

Upload:

* `.csv`
* `.xlsx`
* `.xls`

The application uses **pandas** for data processing and can generate data-driven analysis and visualizations.

### 📚 Multi-Document Interaction

The application supports working with multiple uploaded documents and allows users to interact with their available document context through the assistant.

### 💬 Conversational Interface

* Chat-based user experience.
* Conversation history.
* New conversation functionality.
* Persistent user-related conversation metadata through SQLite.

### 🔐 Authentication

Includes:

* Sign In
* Create Account
* User sessions
* User-specific conversation metadata

### 🔎 Web Search & Tools

The AI agent can use external search/tool capabilities for requests where up-to-date information is required.

### 🌦️ Weather Information

The application includes weather lookup functionality through an external weather service.

---

## 🏗️ Technology Stack

| Technology          | Purpose                           |
| ------------------- | --------------------------------- |
| Python 3.11         | Application runtime               |
| Streamlit           | Web application framework         |
| Azure OpenAI        | LLM / conversational AI           |
| LangChain           | AI orchestration                  |
| LangChain Community | Document loaders and integrations |
| pandas              | Data analysis                     |
| SQLite              | User/conversation metadata        |
| Tavily / Web Search | Web research                      |
| Weather API         | Weather information               |

The application currently targets the following dependency versions:

```text
langchain==1.2.17
langchain-core==1.3.3
langchain-classic==1.0.5
langchain-community==0.4.1
langchain-openai==1.1.10
```

Python version:

```text
Python 3.11
```

---

## 📁 Suggested Project Structure

A recommended GitHub structure for the project is:

```text
dentsu-smart-buddy/
│
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
├── .env.example
│
├── data/
│   └── .gitkeep
│
└── tests/
    └── ...
```

> The current application is primarily contained in the Streamlit Python source file. As the project evolves, functionality can be separated into modules for authentication, document processing, AI agents, data analysis, and utilities.

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/dentsu-smart-buddy.git
cd dentsu-smart-buddy
```

### 2. Create a virtual environment

#### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

#### macOS / Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Create a `.env` file or configure Streamlit secrets for your deployment environment.

Example:

```env
AZURE_OPENAI_API_KEY=your_api_key
AZURE_OPENAI_ENDPOINT=your_endpoint
AZURE_OPENAI_API_VERSION=your_api_version
AZURE_OPENAI_DEPLOYMENT=your_deployment

TAVILY_API_KEY=your_tavily_key
WEB_SEARCH_API_KEY=your_web_search_key
WEATHER_API_KEY=your_weather_key
```

**Do not commit real API keys, passwords, or credentials to GitHub.**

---

## ▶️ Run the Application

Start the Streamlit application with:

```bash
streamlit run app.py
```

The application will provide a local URL that can be opened in your browser.

---

## 💡 Example Use Cases

### Research

```text
What are the latest trends in digital advertising?
```

### Webpage Analysis

Paste a webpage URL and ask:

```text
Summarize the key findings from this article.
```

### Document Analysis

Upload a PDF and ask:

```text
What are the main recommendations in this document?
```

### Data Analysis

Upload a CSV or Excel file and ask:

```text
Analyze the sales trend by month.
```

### Data Visualization

```text
Create a chart showing revenue by category.
```

### Current Information

```text
What are the latest developments in the industry?
```

---

## 🔄 Application Flow

```text
                    ┌──────────────────┐
                    │   User / Login   │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Streamlit UI     │
                    └────────┬─────────┘
                             │
                 ┌───────────┼───────────┐
                 ▼           ▼           ▼
             Documents      URLs       Data
                 │           │           │
                 ▼           ▼           ▼
              Loaders    Web Loader   pandas
                 │           │           │
                 └───────────┼───────────┘
                             ▼
                    ┌──────────────────┐
                    │ LangChain / LLM  │
                    │   AI Assistant   │
                    └────────┬─────────┘
                             │
                 ┌───────────┼───────────┐
                 ▼           ▼           ▼
              Answers     Analysis    Web Search
                 │           │           │
                 └───────────┼───────────┘
                             ▼
                    ┌──────────────────┐
                    │  Chat Response   │
                    └──────────────────┘
```

---

## 🔐 Security Considerations

Before deploying this application to production or making the repository public, review the application's security configuration carefully.

### Never commit secrets

API keys and credentials should be stored using:

* Environment variables
* Streamlit Secrets
* Azure Key Vault
* Another approved secrets-management solution

They should **never be hardcoded in source code**.

### Authentication

For production use, consider replacing simple application-level password handling with a production-ready authentication solution and a secure password hashing algorithm such as **bcrypt or Argon2**.

### LLM-generated code execution

The data-analysis functionality currently generates Python code through an LLM and executes it using Python `exec()`.

This should be treated as a significant security risk if users or model outputs cannot be fully trusted.

A production implementation should use a sandboxed execution environment with strict:

* File-system restrictions
* Network restrictions
* CPU limits
* Memory limits
* Execution timeouts
* Allowed-library controls

### URL loading

User-provided URLs should be validated before being requested to reduce the risk of SSRF and access to internal services.

---

## 🗄️ Data & Storage

The application currently uses **SQLite** for application/user-related metadata and conversation information.

Uploaded document content is also handled through the application's session state.

For a multi-user production deployment, consider moving persistent application data to a production database and using dedicated object storage for uploaded documents.

---

## ☁️ Deployment

The application can be deployed to a Streamlit-compatible hosting environment or another infrastructure capable of running Python and Streamlit.

For production deployment, configure:

1. Python 3.11
2. Required dependencies
3. Azure OpenAI credentials
4. Search API credentials
5. Weather API credentials
6. Persistent database/storage
7. Secure authentication
8. Appropriate network and execution restrictions

---

## 🧪 Testing

Recommended areas for automated testing include:

* Authentication
* User registration
* Login/logout
* Conversation creation
* Conversation history
* URL loading
* Document ingestion
* CSV/Excel processing
* Data analysis
* AI response routing
* External API failures
* Invalid uploads
* Invalid URLs
* Authentication/session edge cases

---

## 🛣️ Future Improvements

Potential improvements include:

* [ ] Move all secrets to environment variables / Streamlit Secrets
* [ ] Replace SHA-256 password storage with Argon2/bcrypt
* [ ] Improve authentication and authorization
* [ ] Sandbox LLM-generated Python execution
* [ ] Add comprehensive automated tests
* [ ] Add structured logging
* [ ] Improve error handling
* [ ] Separate application logic into modules
* [ ] Add vector database support for larger document collections
* [ ] Add document persistence
* [ ] Add production database support
* [ ] Add role-based access control
* [ ] Add Docker support
* [ ] Add CI/CD with GitHub Actions
* [ ] Add application monitoring and observability

---

## 📌 Project Status

**Version:** v5.1
**Status:** Production-oriented Streamlit application

This repository contains an AI-powered research assistant integrating conversational AI, web research, document Q&A, and data analysis capabilities.

---

## 🤝 Contributing

Contributions and improvements are welcome.

Before submitting a pull request:

1. Create a feature branch.
2. Make your changes.
3. Test the application locally.
4. Ensure no secrets or credentials are committed.
5. Submit a pull request with a clear description of the changes.

---

## ⚠️ Disclaimer

This application integrates external AI and web services. AI-generated responses and analyses should be reviewed by users before being relied upon for business-critical decisions.

External APIs may have their own usage limits, costs, availability requirements, and terms of service.

---

## 📄 License

Add the appropriate license for your organization/project before publishing the repository publicly.

For an internal/company repository, keep the repository private and follow your organization's software licensing and security policies.
