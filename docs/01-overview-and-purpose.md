# Overview & Purpose

### What is AIEvaluationTool?

AIEvaluationTool is a comprehensive, end-to-end framework designed to automate the evaluation of conversational AI systems across diverse real-world scenarios and quality metrics. It provides organizations with a robust mechanism to verify, test, and benchmark conversational agents—whether deployed as APIs, WhatsApp bots, or web applications—ensuring they meet high standards of accuracy, safety, and user experience.

### Target Audience

- **AI/ML Engineers** developing and deploying conversational AI systems
- **QA Teams** responsible for testing chatbots and virtual assistants
- **Product Managers** evaluating AI model performance before production deployment
- **Compliance Officers** ensuring responsible AI practices and ethical compliance

### Key Use Cases

- Automated testing of conversational agents across multiple platforms
- Performance benchmarking against predefined quality metrics
- Safety and toxicity evaluation of AI-generated responses
- Multi-language capability assessment
- Compliance verification for responsible AI standards

### Core Benefits

- **Automated Testing**: Eliminates manual testing through automated test case execution across WhatsApp, Web, and API interfaces
- **Comprehensive Evaluation**: Assesses 7 key dimensions including responsible AI, conversational quality, guardrails, language support, task understanding, performance, and privacy
- **End-to-End Pipeline**: Seamlessly integrates test execution, response analysis, and metric aggregation
- **LLM-as-Judge**: Leverages advanced language models for nuanced evaluation beyond rule-based metrics
- **Multi-Platform Support**: Evaluates agents across API, WhatsApp, and web application interfaces
- **Detailed Insights**: Generates comprehensive evaluation reports highlighting strengths and improvement areas

### Test Plans 

- **Responsible AI**: Evaluates ethical behavior by measuring fairness, bias, truthfulness, robustness, transparency, and cultural sensitivity in model responses.  
- **Conversational Quality**: Assesses coherence, fluency, relevance, and linguistic richness of responses using structural, semantic, and reference-based metrics.  
- **Guardrails and Safety**: Tests the model’s ability to detect, reject, and safely handle toxic, harmful, out-of-scope, hallucinated, and adversarial inputs.  
- **Language Support**: Measures multilingual capability with emphasis on Indian languages, including fluency, coverage, transliteration handling, and mixed-language contexts.  
- **Task Performance Metrics**: Quantifies task completion accuracy and correctness while accounting for valid rejections and failures.  
- **Performance and Scalability**: Evaluates system efficiency and reliability under load through latency, throughput, uptime, error rates, and failure resilience.  
- **Privacy and Safety**: Assesses resistance to misuse, jailbreaks, exaggerated safety behavior, and privacy leakage while ensuring appropriate privacy awareness.

### Supported Target Types
- **API**: RESTful or custom API endpoints
- **WhatsApp**: WhatsApp Business API integration
- **Web Application**: Web-based interfaces


### What is TDMS?

The **Test Data Management System (TDMS)** is a comprehensive web-based application designed to manage test data for AI evaluation workflows. It provides a centralized platform for creating, organizing, and managing test cases, prompts, responses, evaluation strategies, and related metadata required for testing conversational AI systems.

### System Architecture

TDMS follows a modern three-tier architecture:

```Architecture
┌─────────────────┐
│   Frontend      │  React + TypeScript + Vite
│   (React App)   │  Tailwind CSS + shadcn/ui
└────────┬────────┘
         │ HTTP/REST API
┌────────▼────────┐
│   Backend       │  FastAPI (Python)
│   (REST API)    │  SQLAlchemy ORM
└────────┬────────┘
         │
┌────────▼────────┐
│   Database      │  SQLite / MariaDB
│   (Data Store)  │
└─────────────────┘
```

### What is Prompt Quality Evaluation Tool?


The **Prompt Quality Evaluation Tool (PQET)** is a specialized module within the AIEvaluationTool designed to assess the quality of prompts and expected responses used in conversational AI systems. It leverages advanced evaluation strategies, including LLM-based judgment, to ensure that prompts are aligned with predefined metrics and submetrics. PQET provides a user-friendly interface for defining metrics, inputting test cases, and generating detailed evaluations. By automating the evaluation process, PQET helps identify critical flaws in prompts and suggests actionable improvements, ensuring that conversational agents meet high standards of accuracy, coherence, and safety.

### System Architecture

The PQET tool follows a modular architecture:

```Architecture
┌─────────────────┐
│   Frontend      │  Streamlit-based UI
│   (Streamlit)   │  Plotly for visualizations
└────────┬────────┘
         │
┌────────▼────────┐
│   Backend       │  Python-based logic
│   (FastAPI)     │  Async evaluation with LLMs
└────────┬────────┘
         │
┌────────▼────────┐
│   Database      │  SQLite or JSON-based
│   (Data Store)  │  Test cases and metrics
└─────────────────┘
```

### What is Test Case Execution Dashboard?

The **Test Case Execution Dashboard (TCED)** is a comprehensive web-based application designed to orchestrate, monitor, and manage the execution of test cases against conversational AI systems. It provides real-time visibility into test execution workflows, allowing teams to track progress, view detailed test results, and generate comprehensive evaluation reports. The dashboard supports multi-platform testing across APIs, WhatsApp integrations, and web applications, enabling seamless execution of test plans and metrics across diverse target systems.

### Key Features

- **Real-Time Execution Monitoring**: WebSocket-based live updates during test case execution with step-by-step progress tracking
- **Test Execution Orchestration**: Manage and execute test plans, metrics, and individual test cases with flexible filtering and selection
- **Comprehensive Test Run Management**: Create, continue, and track multiple test runs simultaneously with persistent state management
- **Advanced Filtering and Search**: Filter test runs by domain, target application, status, language, and metrics
- **Detailed Evaluation Reports**: Generate Excel-based reports with test summaries, evaluation details, metric scores, and execution timelines
- **Conversation Timeline**: View complete conversation history and evaluation reasoning for each test case
- **Resume Capability**: Continue interrupted or paused test runs without losing progress

### System Architecture

The TCED follows a modern three-tier architecture with WebSocket support for real-time updates:

```Architecture
┌─────────────────────────────┐
│   Frontend                  │  React + TypeScript + Vite
│   (React SPA)               │  Tailwind CSS + shadcn/ui
│   WebSocket Client          │  Real-time status updates
└────────┬────────────────────┘
         │ HTTP/REST API
         │ WebSocket (ws://)
         │
┌────────▼─────────────────────┐
│   Backend                    │  FastAPI (Python)
│   (REST API + WebSocket)     │  Async execution engine
│   Test Executor Service      │  Background task queue
└────────┬────────────────────┘
         │
┌────────▼─────────────────────┐
│   Database                   │  SQLite / MariaDB
│   (Data Store)               │  ORM: SQLAlchemy
│                              │  
│   Stores:                    │
│   - Test Runs & Details      │
│   - Conversations            │
│   - Evaluations              │
│   - Execution Timelines      │
└──────────────────────────────┘
```

### Core Components

**Frontend (React + TypeScript)**
- **Test Runs Page**: Display all test runs with filtering and sorting capabilities
- **Test Run Details**: View detailed evaluation results, metrics, and conversation history
- **New Test Run Page**: Create new test runs by selecting test plans, metrics, and test cases
- **Real-Time Updates**: WebSocket integration for live progress updates during execution
- **Report Download**: Generate and download Excel-based evaluation reports

**Backend (FastAPI)**
- **Test Execution Engine**: Orchestrates test case execution with async/await pattern
- **WebSocket Manager**: Broadcasts real-time status updates to connected clients
- **Interface Client**: Communicates with the InterfaceManager service to send prompts and receive responses
- **Database Management**: Handles CRUD operations for test runs, conversations, and evaluations
- **Report Generation**: Creates comprehensive Excel reports with multiple worksheets

**Database**
- **Test Runs**: Run metadata, status, timestamps, and target information
- **Run Details**: Test case mappings, metric associations, and status tracking
- **Conversations**: Agent responses, evaluation scores, and execution timelines
- **Evaluation Results**: Metric scores, reasoning, and detailed evaluation data


