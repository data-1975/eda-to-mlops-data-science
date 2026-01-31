# 📊 End-to-End Data Science: EDA as the Foundation for Decision-Making, Scale, and MLOps

## 📌 Overview

This repository presents an **end-to-end Data Science project** where **Exploratory Data Analysis (EDA)** is treated not as an isolated initial step, but as the **foundation for technical, statistical, and operational decisions** throughout the entire analytical lifecycle.

The main goal is to demonstrate how decisions made **before the first model is trained** directly impact:

- analytical quality  
- reproducibility  
- scalability  
- governance  
- production reliability  

The project starts from **transactional accounting data** and evolves from **descriptive and diagnostic analysis** to a structure ready for **production and MLOps/DataOps practices**.

---

## 🎯 Problem Statement

In many Data Science projects, models fail not because of algorithmic limitations, but due to weak decisions in:

- missing value treatment  
- outlier handling  
- feature engineering  
- temporal understanding of data  

This project addresses the following question:

> **How can we design an analytical pipeline where EDA guides technical decisions, reduces production risk, and sustains models over time?**

---

## 🧠 Core Technical Principles

The project is guided by the following principles:

- **EDA as data governance**, not just visualization  
- **Business context over purely statistical decisions**  
- **Outliers treated as events**, not automatically as errors  
- **Domain-driven feature engineering**  
- **Explicit temporal analysis before modeling**  
- **Production and scalability mindset from day one**

---

## 🔍 Design Decisions (Selected Code Snippets)

The following excerpts highlight **high-impact design decisions** where EDA insights are transformed into **executable rules and deployable behavior**.

The goal is to show *how* analytical understanding becomes **operational reliability**.

---

### 🔹 Data Quality Gate: Domain-Driven Rule Enforcement

Instead of relying solely on schema validation, the pipeline enforces **explicit business rules** identified during EDA.

```python
# Conditional quality gate
if moeda != "BRL" and taxa_conversao is None:
    raise ValueError(
        "Non-BRL transactions require an exchange rate (taxa_conversao)"
    )
````

📌 **Why this matters**

* Prevents silent data corruption
* Encodes domain knowledge as executable contracts
* Fails fast before downstream processing

EDA findings are converted into **governance rules**, not just documentation.

---

### 🔹 Context-Aware Imputation (Not Statistical Guessing)

Missing values are handled using **business logic**, not blanket statistical defaults.

```python
# Context-aware imputation
is_brl = df["moeda"].eq("BRL")
df.loc[is_brl & df["taxa_conversao"].isna(), "taxa_conversao"] = 1.0
```

📌 **Why this matters**

* Avoids distortions from mean/median imputation
* Preserves financial semantics
* Makes assumptions explicit and auditable

EDA informs *when* a value should exist — not just *how* to fill it.

---

### 🔹 Outlier Handling as a Controlled Decision

Outliers are detected statistically but handled deliberately, with explicit intent.

```python
q1, q3 = valor.quantile([0.25, 0.75])
iqr = q3 - q1
df["valor"] = df["valor"].clip(
    lower=q1 - 1.5 * iqr,
    upper=q3 + 1.5 * iqr
)
```

📌 **Why this matters**

* Avoids naive removal of high-impact financial events
* Uses IQR-based capping as a controlled baseline
* Preserves distribution shape and pipeline stability

In production systems, this logic can be replaced by **flagging or review workflows**.

---

### 🔹 Pipeline Entrypoint: Deployable, Not Notebook-Driven

The workflow is exposed as a **CLI-driven pipeline**, enabling CI/CD, scheduling, and reproducibility.

```bash
python -m pipelines.run \
  --config deploy/config.prod.yaml \
  --input data/sample/dataset_sample.csv \
  --output out_prod \
  --date 2026-01-31
```

📌 **Why this matters**

* Eliminates manual notebook execution
* Enables automated runs via GitHub Actions
* Treats EDA and cleaning as a **deployable data product**

---

## 🧪 What Is Done in Practice

### 🔹 Diagnostic Exploratory Data Analysis (Pre-Cleaning)

* Structural inspection of the dataset
* Identification of skewness and long-tail distributions
* Outlier detection using the IQR method
* Missing data analysis (structural vs. accidental missingness)
* Semantic validation of variables

📌 **Goal:** understand the data before transforming it.

---

### 🔹 Context-Aware Data Treatment

* Business-driven imputation strategies
* Preservation of outliers when they represent legitimate events
* Selective handling of extreme values (capping vs. removal)
* Normalization aligned with data distribution

📌 **Goal:** clean the data without distorting reality.

---

### 🔹 Feature Engineering

* Creation of temporal components (month, accounting period)
* Domain-oriented aggregations (e.g., value × cost center)
* Preparation for downstream modeling

📌 **Goal:** convert implicit information into analytical signal.

---

### 🔹 Post-Cleaning Exploratory Analysis

* Reassessment of distributions
* Before vs. after comparisons
* Validation of the impact of cleaning decisions

📌 **Goal:** ensure that cleaning improved the data rather than biased it.

---

### 🔹 Scale and Production Perspective

* Modular code organization
* Clear separation between exploratory notebooks and reusable code
* Structure prepared for:

  * Spark / Databricks
  * Airflow orchestration
  * Versioning and CI/CD
  * Evolution toward MLOps and DataOps

📌 **Goal:** avoid isolated, non-reproducible notebooks.

---

## 🧰 Technology Stack

* **Python** (pandas, numpy, matplotlib, seaborn)
* **Statistical and visual EDA**
* **Modular Python architecture**
* **Spark / Databricks** (scalability perspective)
* **Airflow** (conceptual orchestration)
* **CI/CD and Infrastructure as Code** (MLOps vision)

> The focus is not on a specific tool, but on **decision architecture**.

---

## 📈 Who This Project Is For

* Senior / Specialist Data Scientists
* Professionals working with or transitioning into **MLOps / DataOps**
* Technical leaders seeking **sustainable Data Science systems**
* Anyone interested in treating **Data Science as a system, not an experiment**

---

## 🧭 Final Message

> Data Science is not about accurate models in notebooks.
> It is about **reliable, reproducible, and scalable decision-making in production**.

This project reflects that mindset.

```

---
