# Configuration

#### **Step 1: Update Database Configuration**

Update `src/app/importer/config.json`, `src/app/testcase_executor/config.json` & `src/app/response_analyzer/config.json` with your database credentials, and target if you are using MariaDB, else no changes required for database:

```json
{
    "db": {
        "engine":"sqlite",
        "file": "AIEvaluationData.db",
        "host": "localhost",
        "port": 3306,
        "user": "root",
        "password": "jarvis2025",
        "database": "AIEvaluationData"
    },
    "target": {
        "application_type": "WHATSAPP_WEB",
        "application_name": "Vaidya AI",
        "application_url": "https://web.whatsapp.com/",
        "agent_name": "Vaidya AI"
    }
}
```
---

#### **Step 2: Configure Environment Variables**

To use the LLM-as-a-judge mechanism for evaluation, you must have a language model available. You can either:
- **Run a model locally** (e.g., using Ollama, OpenAI-compatible local models, etc.), or
- **Provide API keys** for cloud-based models (e.g., OpenAI, Anthropic, etc.)

**Supported Models:**
- OpenAI GPT-3.5/4 (via API key)
- Anthropic Claude (via API key)
- Ollama (local)
- Any OpenAI-compatible local model

Ensure that `.env.example` in the root folder is initialized with appropriate values to create a `.env` file :

```bash
# Service Endpoints
OLLAMA_URL="http://localhost:11434"
GPU_URL="http://localhost:8000"

# Model Configuration
LLM_AS_JUDGE_MODEL="qwen3:32b"

# API Keys
PERSPECTIVE_API_KEY="your_perspective_api_key"
SARVAM_API_KEY="your_sarvam_api_key"
GEMINI_API_KEY="your_gemini_api_key"
OPENAI_API_KEY="your_openai_api_key"
```
- `OLLAMA_URL` points to the installed Ollama instance's endpoint address.  Typically it is `http://localhost:11434/`
- `LLM_AS_JUDGE_MODEL` points to the name of the LLM (loaded via Ollama) that we want to use as a judge.  Typically, it is `llama3.1:70b`.
- `PERSPECTIVE_API_KEY` should have the API KEY of Perspective service for toxicity detection.
- `GPU_URL` should point to the Sarvam AI RestAPI server (./src/app/sarvam_ai/) hosted elsewhere.  Typically, the URL is `http://localhost:8000`.
- For API-based models, set your API key in a `.env` file or as an environment variable (e.g., `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`).
- For local models, ensure the model server is running and accessible at the expected endpoint (see your model provider's documentation).

Ensure your model is accessible and properly configured before running the evaluation pipeline. Refer to the relevant documentation for your chosen model provider for setup instructions.

---
#### **Step 3: Configure XPath and Credentials**

XPath locators are used by automation frameworks (e.g., Selenium) to identify and interact with web elements.

- Locate the element in the web application (e.g., username field, password field, login button, prompt textbox and response element's xpath).
    - Right-click on the element → Inspect → Copy XPath.
    - Prefer relative XPath over absolute to avoid breakage when the DOM structure changes.
- Update the configuration file (`xpaths.json`).


``` json
{
  "applications": {
    "app_name_here": {
      "LoginPage": {
        "email_input": "xpath_for_email_input",
        "password_input": "xpath_for_password_input",
        "login_button": "xpath_for_login_button"
      },
      "LogoutPage": {
        "profile": "xpath_for_profile_icon",
        "logout_button": "xpath_for_logout_button"
      },
      "ChatPage": {
        "contact_search": "xpath_for_contact_search",
        "prompt_input": "xpath_for_prompt_input",
        "agent_response": "xpath_for_agent_response",
        "message_in": "xpath_for_incoming_message",
        "message_out": "xpath_for_outgoing_message"
      },
      "OtherPages": {
        "custom_element_1": "xpath_for_custom_element",
        "custom_element_2": "xpath_for_custom_element"
      }
    }
  }
}
```

To keep credentials secure and maintainable, here is the template of the `src/app/interface_manager/credentials.json`

```json
{
  "applications":
  {
    "cpgrams": {
      "username": "user_cpgrams",
      "password": "pass_cpgrams"
    },
    "openweb-ui": {
      "username": "user_openweb_ui",
      "password": "pass_openweb_ui"
    }
  }
}
```
---
#### **Step 4: Import the Target into the Database**

**Supported Target Types:**
- **API**: RESTful or custom API endpoints
- **WhatsApp**: WhatsApp Business API integration
- **Web Application**: Web-based interfaces

Add the following code to the end of `src/app/importer/main.py` to import your target application into the database:

```python
tgt = Target(
    target_name="your_agent_name", # Unique identifier for your agent
    target_type="API" # or "WhatsApp" or "WebApp"
    target_url="https://your-api-endpoint.com",  # Endpoint URL for the target service
    target_description="Your agent description",
    target_domain="Healthcare",  # or "Local API Interface"
    target_languages=["english"] # List of supported languages
)

target_id = db.add_or_get_target(target=tgt)
```

Replace the placeholder values with your actual target configuration details. The script will register your target and return its unique ID for use in subsequent operations.

---
#### **Step 5: Configure Test Data (TDMS)**

   Edit `src/app/TDMS/back-end/database/config.json`:
   
   **For SQLite (default, recommended for development):**
   ```json
   {
     "db": {
       "engine_type": "sqlite",
       "file": "TDMS.db"
     }
   }
   ```
   
   **For MariaDB (production):**
   ```json
   {
     "db": {
       "engine_type": "mariadb",
       "host": "localhost",
       "port": 3306,
       "user": "your_username",
       "password": "your_password",
       "database": "tdms_db"
     }
   }
   ```
---
#### **Step 6: Configure Database and ports for Test Case Execution Dashboard**

> src/app/TestCaseExecutorDashBoard/back-end/config.json

```json
   {
     "db": {
       "engine_type": "sqlite",
       "file": "AIEvaluationData.db"
     }
   }
   ```
   
   **For MariaDB (production):**
   ```json
   {
     "db": {
       "engine_type": "mariadb",
       "host": "localhost",
       "port": 3306,
       "user": "your_username",
       "password": "your_password",
       "database": "tdms_db"
     }
   }
   ```

  **For specifying the port of the back-end application:**
  ```json
    "port": {
      "back-end": "7000",
      "interface-manager": "8000"
    }
  ```

---
## 5. **Getting Started**
To getting started with tool following steps are provided for basics, for detailed documentation [click here](../docs/AI_Evaluation_Tool_Documentation.pdf).
