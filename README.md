# SleepScore-Metrics-and-Report-Workflow 😴😴😴

## Overview

This repository contains an **n8n-based automation pipeline** that calculates a user’s **SleepScore** and **sleep-related biological age impact**, then generates a **personalized, AI-written sleep health report**.

The workflow is designed to run continuously and autonomously, integrating data extraction, scoring, modeling, and natural language report generation into a single end-to-end system.

---

## Workflow Summary

The pipeline executes on a scheduled basis and processes all participants marked as **`Todo`** in the TruMe dataset.

### 1. Scheduled Trigger

- Uses n8n’s Schedule Trigger to run at fixed intervals  
- Enables fully automated, hands-off execution  

### 2. Data Ingestion (BigQuery)

- Queries Google BigQuery for participants with `Status = 'Todo'`  
- Extracts core sleep inputs:
  - Sleep duration
  - Trouble sleeping
  - Waking condition

### 3. Batch Processing

- Processes users in controlled batches  
- Ensures scalability and stability for larger datasets  

### 4. SleepScore Computation

- Calculates a **SleepScore (0–100)** using:
  - Sleep duration
  - Sleep quality indicators  
- Applies weighted logic to balance:
  - Duration (40%)
  - Sleep problems (60%)

### 5. BioAge Sleep Effect Modeling

- Standardizes SleepScore using population mean and standard deviation  
- Applies regression coefficients to estimate:
  - **Sleep-only biological age contribution**
  - **Full predicted biological age delta (years)**

### 6. AI-Generated Personalized Report

- Sends structured sleep metrics to **Google Gemini** via **LangChain**
- Produces a strict JSON-only report containing:
  - Headline summary
  - SleepScore category
  - BioAge impact (years and months)
  - Sleep pattern interpretation
  - Personalized recommendations

### 7. Merge & Output

- Merges numeric metrics with AI-generated narrative text  
- Output is structured for downstream storage in:
  - Google Sheets
  - Dashboards
  - APIs or reporting tools  

---

## Key Features

- Fully automated sleep analytics pipeline  
- Reproducible scoring and modeling logic  
- Scalable batch processing in n8n  
- Strict JSON-only AI outputs for reliability  
- Designed for health dashboards and personalized reports  

---

## Technology Stack

- **n8n** – workflow orchestration  
- **Google BigQuery** – data querying  
- **JavaScript (n8n Code Node)** – scoring and modeling  
- **Google Gemini** – LLM-based report generation  
- **LangChain** – prompt orchestration and output control  

---

---

## Notes

This workflow is designed for extensibility and can be adapted to include additional biological domains such as activity, diet, stress, or disease as new data sources become available.
