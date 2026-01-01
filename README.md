# 🚀 AI Impact on Jobs
## Predicting AI Risk, Job Resilience, and Safer Career Alternatives

This repository contains an end-to-end machine learning workflow that estimates how strongly AI may affect different jobs, groups jobs into risk levels, computes an interpretable resilience score, and recommends lower-risk alternatives for high-risk roles.

**Main questions this project answers:**
- How much AI impact (%) is expected for a given job?
- Is the job **Low / Medium / High** risk?
- How resilient is the job to AI disruption?
- If a job is high-risk, what **safer alternatives** are similar?

---

## 📦 What’s Inside 

| File | What it contains |
|---|---|
| `regression_output.csv` | Predicted AI impact score per job (`Predicted_AI_Impact`) |
| `final_risk_predictions.csv` | Risk labels + model predictions (`Risk_Category`, `Model_Prediction`) |
| `job_model_resilience_index.csv` | Resilience score & level (`Job_Resilience_Score`, `Resilience_Level`) |
| `final_hybrid_recommendations.csv` | Alternative job recommendations for high-risk jobs |

Visuals included:
- `Actual vs Predicted.png`
- `Resilience Distribution.png`
- `Top-10 Resilient Jobs.png`

Presentation:
- `AI Impact on Jobs Predicting Job Risk & Future Skills.pptx`
- `AI Impact on Jobs Predicting Job Risk & Future Skills (1).pdf`

---

## 🗂️ Dataset 

✅ The main dataset file is **`My_Data.csv`**.

It contains **4706** rows and the following columns (column names kept as-is):

| Column | Description |
|---|---|
| `Job titiles` | Job name *(note: dataset has a typo in the column name)* |
| `Domain` | Job domain / field |
| `Tasks` | Number of core tasks |
| `AI models` | Count/measure of relevant AI models/tools |
| `AI_Workload_Ratio` | Share of workload automatable by AI |
| `AI Impact` | Ground-truth AI impact percentage (stored like `85%`) |

> After preprocessing, **4699 jobs** remain in the modeling pipeline (7 records are removed during processing), and the outputs are produced for these 4699 jobs.

---

## 🧠 Method Summary

### 1) AI Impact Prediction (Regression)
- **Goal:** Predict a continuous **AI impact score (0–100)**.
- **Model:** Random Forest Regressor
- **Output column:** `Predicted_AI_Impact`
- **Saved to:** `regression_output.csv`

**Why Random Forest?**
- Handles non-linear patterns well
- Robust to noise/outliers
- Works well with mixed feature types

---

### 2) Risk Classification (Low / Medium / High)
- **Goal:** Turn AI impact into simple, interpretable risk categories.
- **Model:** Random Forest Classifier

Risk thresholds:

| AI Impact (%) | Risk |
|---:|---|
| 0–50 | Low |
| 50–70 | Medium |
| 70–100 | High |

- **Saved to:** `final_risk_predictions.csv`
- Key columns: `Risk_Category` (label), `Model_Prediction` (classifier output)

---

### 3) Job Resilience Index (Interpretability Layer)
A resilience metric is computed from model impact:

**Job_Resilience_Score = 100 − Model_AI_Impact**

Resilience interpretation:

| Score Range | Meaning |
|---:|---|
| 0–40 | Low Resilience |
| 40–70 | Medium Resilience |
| 70–100 | High Resilience |

- **Saved to:** `job_model_resilience_index.csv`

---

### 4) Hybrid Recommendation System (Safer Alternatives)
- **Goal:** For **High-risk** jobs, recommend **similar but safer** jobs.
- Only **Low/Medium risk** jobs are recommended.

Hybrid similarity is computed as:

| Component | Method | Weight |
|---|---|---:|
| Job title meaning | Sentence-BERT (MiniLM) | 0.45 |
| Domain similarity | One-hot + cosine similarity | 0.35 |
| Workload similarity | Scaled numeric cosine similarity | 0.20 |

- **Saved to:** `final_hybrid_recommendations.csv`
- Columns: `High_Risk_Job`, `Alternative_Job`, `Similarity`, etc.

---

## 📊 Evaluation & Visuals

Regression evaluation:
- MAE, RMSE, R²

Classification evaluation:
- Accuracy, Precision, Recall, F1-score

Included visual outputs:
- **Actual vs Predicted AI Impact**
- **Resilience Score Distribution**
- **Top-10 Most AI-Resilient Jobs**
