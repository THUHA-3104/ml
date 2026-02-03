# Learning Progress Prediction – Academic Risk Management
## Project Overview
This project aims to predict students’ learning progress by forecasting the number of credits completed (`TC_HOANTHANH`) at the end of a semester.  
The primary objective is to support **early academic risk detection** and enable **proactive decision-making** in higher education management.
Instead of treating the task as a pure prediction problem, the project is designed as a **decision-support pipeline**, where model outputs are transformed into academic risk indicators that can be directly integrated into management dashboards.

---

## Features
The project focuses on three core objectives:
- Early Academic Progress Prediction : Predicts the number of credits a student is expected to complete (TC_HOANTHANH) at the end of a semester using historical academic records and registered credit load.
- Leakage-safe, Time-aware Modeling: Applies a strict time-based (BTC) train/validation/test split to ensure predictions rely only on past information and reflect real-world deployment conditions.
- Explainable Decision Support: Provides interpretable outputs using feature importance and explainable AI techniques (SHAP, LIME) to support early risk identification and academic intervention.
---

## Installation 
### Prerequisites
* Python 3.8+
* Libraries: `pandas`, `numpy`, `scikit-learn`, `catboost`, `matplotlib`.

### Steps
Follow these steps to install and set up the project:
### Step 1: Clone or download this repository to your local machine
> "git clone https://..."

### Step 2. Navigate to the project directory
>" cd ...."

### Step 3: Install required dependencies
> "pip install pandas numpy scikit-learn catboost shap lime"

### Step 4: Prepare the input datasets
>"admission.csv, academic_records.csv,test.csv, sample_submission.csv"
 
### Step 5: Update dataset paths in the configuration section of the source code:

---
## Usage
After installation, follow these steps to run the pipeline
1. Run the main script
2. The pipeline will automatically:
  - Load and preprocess data
  - Generate historical and lag-based features
  - Apply BTC (Back-Time Consistent) train/validation split
  - Train CatBoost and Ridge models
  - Optimize blending weight using validation RMSE
  - Generate model explanations (Feature Importance, SHAP, LIME)
  - Retrain on full data and predict test set results
3. The final prediction file will be saved

## Contributing
1. Fork the repository

2.Create a new branch:
   > git checkout -b feature/NewFeature
   
3.Commit your changes:
   > git commit -m "Add new feature"

4.Push the branch:
  > git push origin feature/NewFeature

5.Open a Pull Request

## Maintainers


