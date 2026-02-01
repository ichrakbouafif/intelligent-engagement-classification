# Intelligent Engagement Classification in CRM Activities

## Project Overview

CRM systems log *actions*, not *outcomes*.
An email or call entry does **not** guarantee that a real human interaction occurred.

This project introduces an **AI-driven engagement classifier** that analyzes unstructured CRM activity logs to determine whether a **true human-to-human interaction** took place.

The solution combines:

* Rule-based heuristics
* Agentic LLM reasoning
* Cost-efficient bulk inference
* Structured, auditable outputs

---

## Objective

Classify CRM activities into:

* **ENGAGED**
  Verified interaction (e.g., email replies, real conversations, attended meetings)

* **NOT ENGAGED**
  One-way outreach, unanswered calls, automated sequences, internal tasks

* **ND (Non-Determinable)**
  Insufficient or ambiguous evidence

The result is stored in a new column:

```text
trueai_engaged  # Designed for sales performance analytics and reporting
```

---

## Dataset Description

The dataset contains **5,000 CRM activity records**, including:

* **Emails** – inbound & outbound, including automated sequences
* **Calls** – answered, missed, voicemails
* **Events** – scheduled meetings
* **Tasks** – internal reminders

### Schema

| Column          | Description                                   |
| --------------- | --------------------------------------------- |
| crm_subject     | Activity title, often with automation tags    |
| crm_description | Raw unstructured text of the interaction      |
| crm_subtype     | Type of activity: Email, Call, Task, or Event |

---

## Methodology

### 1. Data Cleaning

* Remove unsubscribe blocks
* Strip HTML/CSS formatting
* Remove URLs, email addresses, and boilerplate text
* Normalize whitespace

### 2. Heuristic Pre-Labeling

* Rule-based classification to capture obvious cases
* Reduces ambiguity before LLM processing

### 3. Agentic LLM Classification

* AI agent acts as a **Sales Operations Auditor**
* Analyzes:

  * Linguistic cues
  * Conversational evidence
  * Contextual engagement signals

### 4. Bulk Inference Optimization

* Batch processing to minimize API calls and cost
* Prediction isolation via `hs_object_id`
* Structured JSON output for traceability

---

## Model Evaluation

A **human-labeled evaluation set** of 200 CRM activities was created to assess model performance.

### Metrics

* Accuracy
* Precision / Recall / F1-score
* Confusion matrix

### Key Results

* High recall on **ENGAGED** interactions
* Strong precision on **NOT ENGAGED** classification
* **ND** class effectively captures ambiguity without forcing decisions

### Error Analysis

* Most errors occur in short or context-poor activity logs
* Highlights the importance of high-quality CRM descriptions

---

## LLM & Tooling

* **Model:** Google Gemini Flash
* **Prompting:** Agentic role-based reasoning
* **Output:** Strict JSON schema

**Frameworks & Libraries:**

* Python
* Pandas
* Google Generative AI SDK

---

## Output

The final dataset includes:

```text
hs_object_id | trueai_engaged
```

This enables:

* Accurate engagement filtering
* Sales funnel analytics
* CRM data quality audits

---

## Future Improvements

* Fine-tuned domain-specific LLM
* Active learning loop for continuous improvement
* Confidence scoring on predictions
* CRM-native deployment (HubSpot / Salesforce)
* Comprehensive evaluation against labeled ground truth

---

## Repository Structure

```
.
├── Intelligent_Engagement_Classification.ipynb
├── verifictus_activities.csv
├── human_annotation_labeled.csv
└── README.md
```

---

## Authors

**Eya Guerdelly & Echrak Bouafif**

Developed as an applied AI project focused on **sales intelligence, CRM analytics, and agentic AI systems**.

