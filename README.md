# Learning Progress Prediction – Academic Risk Management

## Project Overview
This project aims to predict students’ learning progress by forecasting the number of credits completed (`TC_HOANTHANH`) at the end of a semester.  
The primary objective is to support **early academic risk detection** and enable **proactive decision-making** in higher education management.

Instead of treating the task as a pure prediction problem, the project is designed as a **decision-support pipeline**, where model outputs are transformed into academic risk indicators that can be directly integrated into management dashboards.

---

## Dataset Description
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

## Problem Formulation
The task is formulated as a **regression problem**.
Instead of predicting completed credits directly, the model predicts the **credit completion rate (pass rate)**:

This approach:
- Normalizes targets across students with different credit loads
- Improves stability and generalization
- Allows direct interpretation as an academic risk score

Predicted pass rates are later converted back to completed credits.

---
## Recommended modules
The pipeline is modular by design. The following components are recommended to be kept when using or extending the system:

1. Feature engineering module
   Generates time-based historical features (lag, rolling statistics, cumulative statistics) while strictly preventing temporal data leakage.

2. Modeling module

   CatBoost Regressor as the primary nonlinear model

   Ridge Regression as a linear complementary model for stability

3. Explainability module

   CatBoost Feature Importance

   SHAP for global explanations

   LIME for instance-level explanations

Removing these modules may reduce prediction robustness or interpretability.

## Installation
Follow these steps to install and set up the project:
1. Clone or download this repository to your local machine
2. Install required Python packages
3. Prepare the input data files
4. Update file paths in the CONFIG section of the script:

## Contributing
After installation, follow these steps to run the pipeline
1. Run the main script
2. The pipeline will automatically:
  Load and preprocess data
  Generate historical and lag-based features
  Apply BTC (Back-Time Consistent) train/validation split
  Train CatBoost and Ridge models
  Optimize blending weight using validation RMSE
  Generate model explanations (Feature Importance, SHAP, LIME)
  Retrain on full data and predict test set results
3. The final prediction file will be saved

## Maintainers
### Step 1: 

