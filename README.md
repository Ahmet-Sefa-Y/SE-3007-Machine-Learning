# SE-3007-Machine-Learning# 🤖 AI Impact on Jobs
### Predicting Job Risk, Resilience & Future Career Alternatives

This project analyzes how **Artificial Intelligence (AI) impacts different professions** and provides a **fully reproducible, end-to-end machine learning pipeline**.

Instead of focusing only on job loss, it answers:

> **Which jobs are at risk, how resilient they are to AI, and which safer alternatives exist.**

---

## 📌 Problem Statement

AI is rapidly transforming the labor market. While some jobs are highly automatable, others remain resilient or evolve alongside AI.

The objectives of this project are:

- Predict the **degree of AI impact** on professions (regression)
- Classify jobs into **risk categories** (classification)
- Quantify **job resilience** against AI (index/score)
- Recommend **lower-risk alternative jobs** for high-risk professions (hybrid recommender)

---

## 📂 Dataset

Main input file:
- `My_Data.csv`

The dataset contains job-level information with attributes such as:

- **Job titiles** — Job name *(kept as the dataset column name)*
- **Domain** — Professional field
- **Tasks** — Number of core tasks
- **AI models** — Relevant AI tools/models count
- **AI_Workload_Ratio** — Share of tasks automatable by AI
- **AI Impact** — Ground-truth AI impact percentage

---

## 🧭 Project Pipeline (End-to-End)

This repository includes multiple notebooks that together form the pipeline:

1. **EDA (optional)**  
   - `eda.ipynb`

2. **AI Impact Prediction (Regression)**  
   - `AI_Risk_Prediction_Model.ipynb`  
   Output: `regression_output.csv`

3. **Job Vulnerability Classification (Low / Medium / High)**  
   - `Job_Vulnerability_Classification.ipynb`  
   Output: `final_risk_predictions.csv`

4. **Job Resilience Index (Interpretability Layer)**  
   - `Sector_AI_Resilience_Index.ipynb`  
   Output: `job_model_resilience_index.csv`

5. **Hybrid Recommendation System (Future-Proof Alternatives)**  
   - `Future-Proof_Skills_Recommender.ipynb`  
   Output: `final_hybrid_recommendations.csv`

---

## 🧹 Data Preprocessing

Key preprocessing steps:

- Removal of `%` symbols from `AI Impact`
- Conversion to numeric format
- Handling missing and infinite values
- Feature scaling using **StandardScaler**
- One-hot encoding for categorical variables when needed
- Post-processing regression outputs using clipping (`0–100`) for interpretability

---

## 🧠 Models & Methodology

### 1️⃣ AI Impact Prediction (Regression)

**Model:** Random Forest Regressor  
**Goal:** Predict AI impact as a continuous value (0–100%)

**Why Random Forest?**
- Handles non-linear relationships
- Robust to noise and outliers
- Performs well on mixed feature types

**Output file:**
- `regression_output.csv`

---

### 2️⃣ Risk Classification

**Model:** Random Forest Classifier  
**Goal:** Convert predicted AI impact into interpretable risk categories

| AI Impact (%) | Risk Category |
|--------------:|--------------|
| 0–50          | Low          |
| 50–70         | Medium       |
| 70–100        | High         |

**Output file:**
- `final_risk_predictions.csv`

---

### 3️⃣ Hybrid Job Recommendation System

**Goal:** Recommend safer alternatives for **high-risk** jobs.

Only **Low** and **Medium** risk jobs are suggested as alternatives.

Hybrid similarity combines:

| Component | Method | Weight |
|----------|--------|:------:|
| Job title semantics | Sentence-BERT (MiniLM) | 0.45 |
| Domain similarity | One-hot + cosine similarity | 0.35 |
| Workload similarity | Scaled numeric cosine similarity | 0.20 |

**Output file:**
- `final_hybrid_recommendations.csv`

---

### 4️⃣ Job Resilience Index

A final, interpretable metric is computed:

**Job Resilience Score = 100 − Model_AI_Impact**

| Score Range | Interpretation |
|------------:|----------------|
| 0–40        | Low Resilience |
| 40–70       | Medium Resilience |
| 70–100      | High Resilience |

**Output file:**
- `job_model_resilience_index.csv`

---

## 📊 Model Results & Evaluation

### Regression Metrics
The AI Impact prediction model is evaluated using:
- **MAE (Mean Absolute Error)**
- **RMSE (Root Mean Squared Error)**
- **R² Score (Coefficient of Determination)**

### Classification Metrics
The job risk classification model is evaluated using:
- **Accuracy**
- **Precision**
- **Recall**
- **F1-score**

---

## 🖼 Visualizations (Included)

The repository includes the following generated visuals:

- **Actual vs Predicted AI Impact** (`Actual vs Predicted.png`)
- **Job Resilience Score Distribution** (`Resilience Distribution.png`)
- **Top-10 Most AI-Resilient Jobs** (`Top-10 Resilient Jobs.png`)


