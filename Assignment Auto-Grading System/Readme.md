# Automated Assignment Grading System — n8n Workflow

This **n8n workflow** functions as an **Automated Assignment Grading System**. It leverages AI and Google Drive integration to automatically evaluate student programming submissions based on a predefined rubric and assignment description.

## Key Workflow Steps

### 1. Initialization & Data Retrieval

* The workflow is **triggered manually** to start the grading process.
* Downloads the assignment instructions:

  * `Assignment.txt`
* Downloads the grading criteria:

  * `Rubric.txt`
* Searches a designated **Google Drive** folder for student assignment folder like: C++ source-code files (`.cpp`).

### 2. Data Preparation & Looping

* Extracts the text content from the assignment and rubric files.
* Combines the assignment description, grading rubric, and list of student submissions.
* Uses a **batch/loop controller** to process each student submission individually.

### 3. AI Evaluation — The Grading Agent

For each student submission:

1. Downloads the individual student's C++ source-code file.
2. Extracts the code content.
3. Sends the following information to an AI Agent:

   * Assignment description
   * Grading rubric
   * Student name
   * Student's C++ code
4. The AI Agent, powered by **OpenAI GPT-4o-mini**, acts as an expert programming instructor.
5. The agent evaluates the submission strictly against the predefined rubric.
6. It generates:

   * Criterion-by-criterion scores
   * Percentage calculations
   * Detailed grading justification
   * Strengths
   * Areas for improvement
   * Constructive feedback in **Arabic**

### 4. Results Processing & Storage

* Parses and cleans the structured **JSON response** returned by the AI Agent.
* Extracts and formats:

  * Student details
  * Criterion scores
  * Total grade
  * Percentage
  * Feedback
  * Strengths
  * Areas for improvement
* Formats the evaluation results according to the requirements of the results spreadsheet.
* Automatically appends each completed evaluation to the **Google Sheets** document named `Results`.

### 5. Continuous Processing

* After saving the evaluation, the workflow returns to the loop controller.
* The next student submission is processed automatically.
* This process continues until **all available `.cpp` submissions have been evaluated**.

## Workflow Architecture

```text
Manual Trigger
      │
      ▼
Google Drive
      │
      ├── Assignment.txt
      ├── Rubric.txt
      └── Student .cpp Files
              │
              ▼
      Data Preparation
              │
              ▼
       Loop / Batch Processing
              │
              ▼
      Download Student Code
              │
              ▼
       AI Grading Agent
        (GPT-4o-mini)
              │
              ▼
     Structured JSON Result
              │
              ▼
      Result Processing
              │
              ▼
       Google Sheets
         "Results"
              │
              ▼
       Next Student
              │
              ▼
       All Students Done
```

## Main Benefits

* **Automated grading:** Eliminates repetitive manual evaluation of programming assignments.
* **Rubric-based evaluation:** Ensures grading follows predefined assessment criteria.
* **Consistent assessment:** Applies the same evaluation framework to every submission.
* **Detailed feedback:** Provides students with actionable feedback in Arabic.
* **Scalable processing:** Can process multiple student submissions sequentially.
* **Centralized results:** Stores all evaluations automatically in Google Sheets.
* **Reduced instructor workload:** Automates the repetitive parts of programming assignment assessment while maintaining structured evaluation.
