### **AI Evaluation Tool**
---
#### 5.1.1 **Import Test Data into Database**

Before running evaluations, you need to import test data points into the database.

**Run the Importer Script :**

```bash
python3 src/app/importer/main.py --config "src/app/importer/config.json"
```

After successful execution, you should see output similar to:

![Importing datapoints to database](../screenshots/importing%20data%20to%20database.png)

---

#### 5.1.2 **Start the InterfaceManager API Service**

The InterfaceManager handles communication with target platforms (API, WhatsApp, Web).

**Step 1: Navigate to InterfaceManager Directory and Start the Service**

```bash
cd src/app/interface_manager
python main.py
```

You should see output like:

![Interface Server Running](../screenshots/interface_manager_running.png)

---

#### 5.1.3 **Configure and Run Test Case Executor**

The Test Case Executor sends test prompts to your target application.

**Step 1: Update Executor Configuration**

As above, `src/app/testcase_executor/config.json` updated with your target details and database credentials.

**Step 2: View Available Options**

```bash
cd src/app/testcase_executor
python main.py --config "config.json" -h
```
![Arguments available in Testcase Executor](../screenshots/arguments%20of%20testcase%20executor.png)

**Step 3: Get Available Test Plans**

```bash
python main.py --config "config.json" --get-plans
```

Expected output:

![Plans](../screenshots/get_plans.png)

**Step 4: Get Available Metrics**

```bash
python main.py --config "config.json" --get-metrics
```

Expected output:

![Metrics](../screenshots/get_metrics.png)

**Step 5: Execute Test Cases**

```bash
python main.py --testplan-id <testplan-id> --testcase-id <testcase-id> --metric-id <metric-id> --max-testcases <max-testcases> --config "config.json" --execute
```

Replace placeholders with actual values from your test plan. The executor will run and display:

![TEM Running](../screenshots/Testcase_execution_manager_running.png)

The test execution interface will appear similar to:

![Interface](../screenshots/Interface.jpg)

---

#### 5.1.4 **Deploy LLM Models**

For evaluation using **LLM-as-Judge**, the following models must be available:

**Required Models**
1. `sarvamai/sarvam-2b-v0.5`
2. `google/shieldgemma-2b`
3. `sarvamai/sarvam-translate`
4. `qwen3:32b` (Default LLM-as-Judge)

> **Note**
> - Ollama’s default port **11434 is fixed**.
> - All other service ports (e.g., Sarvam AI) are **configurable** and can be changed to any free port.

LLM models seving can be done in following two ways :

**A. Local Serving**

Use this setup when running all services on the same machine.

- **Start Sarvam AI Service**
    ```bash
    cd src/app/sarvam_ai
    python main.py --port <free-port-local>
    ```

- **Pull and serve LLM-as-Judge**
    ```bash
    ollama pull qwen3:32b
    ollama serve
    ```
> Note: `ollama` serve usually runs by default and may not require manual execution.

**B. Remote GPU Serving(Port Forwarding)**</br>
Use this setup when models are hosted on a remote GPU machine.

- **Start Services on Remote GPU Machine** </br>
    Run the following commands on remote GPU machine-
    ```bash
    cd src/app/sarvam_ai
    python main.py --port <free-port-gpu>
    ```
    ```bash
    ollama pull qwen3:32b
    ```
- **Forward Remote Ports to Local Machine** 
    ```bash
    ssh gpu_machine_cred@machineIP \
    -L 21434:localhost:11434 \
    -L <free-local-port:localhost:<ollama-port> \
    -L <free-local-port:localhost:<gpu-port>
    ```
After serving sarvam ai, it will looks similar to following:

![Image](../screenshots/sarvam_ai.png)

There are other small sized models which gets downloaded while running this application. The models are - 

1. amedvedev/bert-tiny-cognitive-bias
2. LibrAI/longformer-harmful-ro
3. vectara/hallucination_evaluation_model
4. thenlper/gte-small
5. all-MiniLM-L6-v2
6. nicholasKluge/ToxiGuardrail
7. sentence-transformers/paraphrase-multilingual-mpnet-base-v2
8. google/flan-t5-large
9. holistic-ai/bias_classifier_albertv2
10. Human-CentricAI/LLM-Refusal-Classifier
11. cross-encoder/nli-deberta-base

#### 5.1.5 **Run Response Analysis**

After testcase execution completes and responses are collected, analyze them by getting run-name from Test runs table from DB OR from the testcase executor logs.

**Step 1: Start Response Analyzer**

```bash
cd src/app/response_analyzer
python analyze.py --config "path to config file" --run-name <run-name>
```

The analyzer will process responses and display:

![Response Analysis Image](../screenshots/Response_analyzer_running.png)

---

#### 5.1.6 **Generate Evaluation Report**

View comprehensive evaluation results and metrics.

```bash
cd src/app/response_analyzer
python report.py --config "path to config file" --run-name <run-name>
```

Use the same `run-name` from the analysis step.

The report will display detailed evaluation metrics:

![Evaluation Report](../screenshots/report_generation.png)

---

