
#### Overview

The TestCase Evaluation Dashboard is a web-based application for
configuring, starting, monitoring, and analyzing AI model evaluations.
Users can initiate test runs directly from the interface, track
execution status in real time, and review detailed evaluation results
with full explainability. For the user manual, [click here](../docs/Testcase_execution_dashboard_doc.pdf).

------------------------------------------------------------------------

#### 5.4.1 Start the Front-end Application

#### Step 1: Navigate to the Application Directory

``` bash
cd src/app/TestCaseExecutorDashboard
```

#### Step 2: Start the FrontEnd application

``` bash
cd front-end
npm install
npm start
```

> Ensure all required dependencies are installed.

After running the command, open the URL shown in the terminal (e.g.,
http://localhost:3000).

![TRDB application](../screenshots/TRDB_without_back_end.png)

------------------------------------------------------------------------

#### 5.4.2 Start the backend application [In a separate terminal]

``` bash
cd ../back-end/
python main.py
```

--------------

#### Key Features

**1. Monitor Test Runs**

-   View Run ID, Name, Target, Status, Duration, and Domain.
-   Filter by Domain, Target, or Status.
-   Access detailed reports for completed runs.

![TRDB application](../screenshots/TRDB_first_page.png)

**2. Create a New Test Run**

-   Configure target model, test plan, domain, language, and metrics.
-   Optionally limit test cases or specify a test case ID.
-   Click **Start Run** to initiate evaluation directly from the app.

![TRDB application](../screenshots/TRDB_add_test_run.png)

**3. View Test Run Details**

-   Execution timeline visualization.
-   Results table with test cases, metrics, scores, and status.
-   Filter results by metric or status.

![TRDB application](../screenshots/TRDB_test_run_details.png)

**4. Inspect Individual Test Cases**

-   Numerical score with visual indicator.
-   Detailed evaluation reasoning.
-   Conversation ID and metadata.
-   Full conversation details : User Prompt, System Prompt, and Agent Response.

![TRDB application](../screenshots/TRDB_single_testcase_eval_details.png)

This application provides an end-to-end workflow for transparent and
structured AI evaluation.

-------------

