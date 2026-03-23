## Architecture & Design

### System Architecture

AIEvaluationTool follows a modular, layered architecture designed for scalability and extensibility:

![System Architecture](../screenshots/Arch.jpg)

### Core Components

**Data**
- Centralized MariaDB or SQLite database for storing test cases, configurations, and evaluation results
- JSON-based data files for test plans, strategies, and metric mappings

**Execution**
- **Test Case Executor**: Distributes and executes test cases across target platforms
- **Interface Manager**: Automates interactions with WhatsApp, web applications, and API endpoints using Selenium and ChromeDriver

**Analysis**
- **Response Analyzer**: Applies evaluation strategies to collected responses
- **Strategy Engine**: Implements model-based and rule-based evaluation techniques
- **LLM-as-Judge**: Leverages language models for nuanced conversational quality assessment

**Integration**
- **Sarvam AI Service**: Hosts multiple specialized models for text classification, translation, and toxicity detection
- **External APIs**: Perspective API for toxicity scoring, cloud LLM providers (OpenAI, Anthropic)

**Management**
- **TDMS (Test Data Management System)**: Web-based UI for managing test data, users, and permissions
- **ORM**: Abstracts database operations and data models


### Technology Stack

| Layer | Technology |
|-------|-----------|
| **Backend** | Python 3.10+, FastAPI |
| **Database** | MariaDB or sqlite |
| **Frontend** | Node.js 20.19+ or 22.14+ |
| **Web Automation** | ChromeDriver, Chrome Browser |
| **ML/AI Models** | Ollama, Hugging Face Transformers, OpenAI API |
| **APIs** | RESTful services, OpenAI-compatible endpoints |

### Key Dependencies

- **selenium**: Browser automation for web and WhatsApp interfaces
- **pydantic**: Data validation and ORM modeling
- **fastapi**: API server framework
- **requests**: HTTP client for API interactions
- **transformers**: Hugging Face model integration
- **ollama**: Local LLM deployment

### Project Layout

The AIEvaluationTool project is organized into a modular structure that separates concerns between data, application logic, libraries, and configuration files.

```tree
AIEvaluationTool/
├── data/
│   ├── DataPoints.json                 # Sample test dataset with evaluation prompts
│   ├── plans.json                      # Test plan definitions
│   ├── strategy_map.json               # Mapping of strategies to metrics
│   ├── strategy_id.json                # Strategy identifiers
│   ├── metric_strategy_mapping.json    # Metric to strategy associations
│   └── defaults.json                   # Default configuration values
│
├── src/
│   ├── app/
│   │   ├── importer/                   # Data import to database module
│   │   │   ├── main.py                 # Entry point for data import
│   │   │   └── config.json             # Database and file configurations
│   │   ├── interface_manager/          # Platform interaction automation
│   │   │   ├── main.py                 # FastAPI service for interface management
│   │   │   ├── credentials.json        # Secured account credentials
│   │   │   └── xpaths.json             # Locations to identify and interact with web elements
│   │   ├── testcase_executor/          # Test execution orchestration
│   │   │   ├── main.py                 # Test case execution manager
│   │   │   └── config.json             # Target and database configuration
│   │   ├── response_analyzer/          # Response analysis and evaluation
│   │   │   ├── analyze.py              # Main analysis script
│   │   │   ├── report.py               # Report generation
│   │   │   └── config.json             # Analyzer configuration
│   │   ├── sarvam_ai/                  # Local LLM model deployment
│   │   │   └── main.py                 # Model server entry point
│   │   ├── maintenance/                 # System maintenance and cleanup utilities
│   │   │   ├── config.json             # Maintenance configuration
│   │   │   └── fix_language.py         # Language correction and cleanup utility
│   │   ├── prompt_quality_evaluation_tool/  # Prompt Quality Evaluation Tool
│   │   │   ├── main.py                 # Streamlit application entry point
│   │   │   ├── API_keys.json           # LLM API credentials
│   │   │   └── metric_and_submetric.xlsx  # Metric definitions and submetrics
│   │   ├── TDMS/                       # Test Data Management System
│   │   │   ├── back-end/               # FastAPI backend service
│   │   │   │   ├── main.py             # TDMS API server
│   │   │   │   ├── database/           # Database layer
│   │   │   │       ├── config.json     # Database layer
│   │   │   └── front-end/              # React/Node.js frontend
│   │   └── TestCaseExecutorDashboard/  # Test Case Execution Dashboard
│   │       ├── back-end/               # FastAPI backend service
│   │       │   ├── .env                # DB configuration and Dev Configuration
│   │       │   ├── .env.example        # Environment template
│   │       │   ├── main.py             # TDMS API server
│   │       │   ├── config.json         # Configure Database and Ports
│   │       └── front-end/              # React/Node.js frontend
│   └── lib/
│       ├── strategy/..                 # Evaluation strategy implementations
│       │   ├── .env                    # Strategy configuration paths
│       │   └── .env.example            # Environment template
│       ├── orm/                        # Object-Relational Mapping layer
│       ├── data/                       # Pydantic data models
│       ├── interface_manager/          # Interface client library
│       │   └── client.py               # REST client for interface manager
│       └── utils/                      # Utility functions
├── requirements.txt                    # Python package dependencies
├── .env.example                        # Environment variables template
└── README.md                           # Project overview and quick start
```
---

### Module Descriptions

**data/** - Contains all test data, configurations, and reference materials
- Test datasets in JSON format
- Strategy mappings and metric definitions
- Default values and example data

---

**src/app/** - Application modules implementing core functionality
- `importer/` - Handles data import from JSON files to database
- `interface_manager/` - Manages automation across different platform types
- `testcase_executor/` - Orchestrates test execution workflow
- `response_analyzer/` - Analyzes responses and applies evaluation strategies
- `sarvam_ai/` - Hosts multiple specialized AI models for evaluation
- `TDMS/` - Web-based system for test data management and user access control
- `prompt_quality_evaluation_tool/` - Streamlit-based UI for assessing prompt and response quality using LLM-based evaluation
- `TestCaseExecutorDashboard/` - Web application for orchestrating, monitoring, and analyzing test case execution with real-time updates
- `maintenance/` - System utilities for database cleanup & language correction operations

---

**src/lib/** - Reusable libraries and shared components
- `strategy/` - Evaluation strategy implementations (model-based and rule-based)
- `orm/` - Database abstraction and entity models
- `data/` - Pydantic data validation classes
- `interface_manager/` - REST client for interface manager communication
- `utils/` - Common utilities across modules

---

