# Learning Progress Prediction – Academic Risk Management

## 1. Project Overview
This project aims to predict students’ learning progress by forecasting the number of credits completed (`TC_HOANTHANH`) at the end of a semester.  
The primary objective is to support **early academic risk detection** and enable **proactive decision-making** in higher education management.

Instead of treating the task as a pure prediction problem, the project is designed as a **decision-support pipeline**, where model outputs are transformed into academic risk indicators that can be directly integrated into management dashboards.

---

## 2. Dataset Description
The project uses three main datasets provided by the organizer:

### `admission.csv`
- One row per student
- Provides background information before enrollment
- Key columns:
  - `MA_SO_SV`: Student ID
  - `NAM_TUYENSINH`: Admission year
  - `PTXT`: Admission method
  - `TOHOP_XT`: Subject combination
  - `DIEM_TRUNGTUYEN`: Admission score
  - `DIEM_CHUAN`: Major cutoff score

### `academic_records.csv`
- One row per student per semester
- Contains historical academic performance
- Key columns:
  - `MA_SO_SV`: Student ID
  - `HOC_KY`: Semester (e.g. HK1 2023-2024)
  - `GPA`, `CPA`
  - `TC_DANGKY`: Registered credits
  - `TC_HOANTHANH`: Completed credits (target for train/validation)

### `test.csv`
- Semester: HK1 2024–2025
- Provided columns:
  - `MA_SO_SV`
  - `TC_DANGKY`
- Objective: predict `TC_HOANTHANH`

---

## 3. Problem Formulation
The task is formulated as a **regression problem**.
Instead of predicting completed credits directly, the model predicts the **credit completion rate (pass rate)**:

This approach:
- Normalizes targets across students with different credit loads
- Improves stability and generalization
- Allows direct interpretation as an academic risk score

Predicted pass rates are later converted back to completed credits.

---

## 4. Methodology and Pipeline

### 4.1 Time-aware Data Split
To avoid data leakage and reflect real-world deployment, data is split strictly by time:
- **Train**: 2020–2021 → HK1 2023–2024
- **Validation**: HK2 2023–2024
- **Test**: HK1 2024–2025

### 4.2 Feature Engineering
Historical features are constructed per student using only past information:
- Lag features (GPA, completed credits, pass rate)
- Rolling statistics (mean, std)
- Cumulative statistics (historical averages and sums)
- Trend indicators (recent performance vs historical average)
- Workload indicators (registered credits vs historical capacity)
- Admission score gap (`DIEM_TRUNGTUYEN - DIEM_CHUAN`)

All features are designed to be **time-safe** and deployment-ready.

### 4.3 Models
Two complementary models are used:
- **CatBoost Regressor** for capturing non-linear relationships and feature interactions
- **Ridge Regression** as a stable linear baseline

Final predictions are obtained via **model blending**, where blending weights are optimized on the validation set.

---

## 5. Academic Risk Scoring and Application
The predicted pass rate serves as a **continuous Academic Risk Score** ranging from 0 to 1.  
Students can be grouped into risk levels using adjustable business thresholds, for example:
- High risk: pass rate < 0.70
- Medium risk: 0.70–0.90
- Low risk: ≥ 0.90

Predictions are converted back to completed credits and clipped to ensure:


This design allows direct integration into academic management dashboards, enabling early identification of students who require closer monitoring or intervention.

---

## 6. Project Structure

---

## 7. How to Run

### Step 1: Install dependencies
```bash
pip install -r requirements.txt

Instead of predicting completed credits directly, the model predicts the **credit completion rate (pass rate)**:

