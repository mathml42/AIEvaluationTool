# Setup Manually

## Prerequisites and System Requirements

Before installing AIEvaluationTool, ensure your system meets the following requirements:

**Hardware Requirements:**
- Minimum 8GB RAM (24GB+ recommended for local LLM deployment)
- Multi-core processor (4+ cores)
- 50GB+ free disk space (for models and databases)
- GPU support recommended for faster model inference (NVIDIA CUDA compatible)

**Software Requirements:**
- **Python 3.10+**
- **Node.js 20.19+ or 22.12+**
- **MariaDB Server 10.5+**
- **Google Chrome Browser** (latest version)
- **ChromeDriver** (must match your Chrome version - critical dependency)
- **Ollama** (for local LLM deployment)
- **GPU drivers** (NVIDIA CUDA for accelerated processing)

---

## Step-by-Step Installation Instructions

### Step 1: Clone the Repository

```bash
git clone https://github.com/cerai-iitm/AIEvaluationTool
cd AIEvaluationTool
```
---

### Step 2: Set Up Virtual Environment & Install Dependencies

To ensure dependency isolation and reproducibility, create and use a Python virtual environment.

```bash
# Create virtual environment
python3 -m venv venv
```

Activate virtual environment
```bash
# Linux / macOS
source venv/bin/activate
```
```bash
# Windows
venv\Scripts\activate
```
Install all dependencies for each component using the provided `requirements.txt` files:
```bash
# Install required dependencies
pip install -r requirements.txt
```
---

### Step 3: Install ChromeDriver

ChromeDriver is essential for web and WhatsApp interface automation. So first check the version of google chrome and then install the respective version of chromedriver version.

---

### Step 4: Set up Database

#### 4.1 SQLite
By defaults, sqlite database will be used for ease to store small amount of data.
For large testcase datasets, set up the MariaDB Database.

#### 4.2 Set Up MariaDB Database

Create a new database and user:

```bash
# Login to MariaDB
mysql -u root -p

# Create database
CREATE DATABASE aievaluationtool;

# Create database user
CREATE USER 'aiet_user'@'localhost' IDENTIFIED BY 'secure_password';
GRANT ALL PRIVILEGES ON aievaluationtool.* TO 'aiet_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
---

### Step 5: Install Node.js Dependencies

With the version 20.19+ or 22.12+.

---

### Step 6: Strategy .env

Create `src/lib/strategy/.env` from `src/lib/strategy/.env.example`:

```bash
cp src/lib/strategy/.env.example src/lib/strategy/.env
```
---

### Step 7: Prepare Data Files

Ensure the `data/` directory contains the following files (already present in the repository):
- `DataPoints.json` (sample test dataset)
- `plans.json`
- `strategy_map.json`
- `strategy_id.json`
- `metric_strategy_mapping.json`
- **A detailed set of Seeding data points shall be provided upon request.**

---

### Test Ollama Setup (Optional)

If using local LLMs:

```bash
ollama pull qwen3:32b
ollama serve 
```

---

