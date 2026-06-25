
# Financial Inclusion in Africa – Machine Learning Project

## Project Overview

This project was developed as part of the Data Science & AI Engineering Bootcamp.

The objective is to predict whether a respondent owns or uses a bank account based on demographic and socio-economic information.

The project is based on the **Zindi Financial Inclusion in Africa** competition.

---

## Project Goal

Financial inclusion plays an important role in economic development.

The goal of this project is to develop a supervised machine learning model that predicts bank account ownership using survey data collected in four African countries.

---

## Dataset

The dataset contains information from respondents in

- Kenya
- Rwanda
- Tanzania
- Uganda

Each observation includes features such as

- Country
- Age
- Household Size
- Cellphone Access
- Education Level
- Job Type
- Marital Status
- Relationship to Household Head
- Location Type

The target variable is

```text
bank_account
```

with the classes

```text
Yes
No
```

---

## Project Workflow

The notebook follows a complete end-to-end machine learning workflow.

### 1. Data Loading

- Import datasets
- Initial inspection
- Missing value analysis

### 2. Exploratory Data Analysis (EDA)

Analysis of

- Target distribution
- Cellphone access
- Education level
- Location type
- Age
- Country
- Household size

### 3. Data Preparation

- Target encoding
- One-Hot Encoding
- Train/Test Split
- Preprocessing Pipeline

### 4. Machine Learning

The following models were evaluated:

- Dummy Classifier (Baseline)
- Logistic Regression
- Decision Tree
- Random Forest

### 5. Model Evaluation

Evaluation metrics include

- Accuracy
- Mean Absolute Error (MAE)
- Precision
- Recall
- F1 Score
- Confusion Matrix
- Cross Validation

### 6. Model Interpretation

The Random Forest model was further analysed using

- Feature Importance
- Grouped Feature Importance
- Correlation Matrix

### 7. Final Model

The best-performing Random Forest model was trained using the complete training dataset.

Predictions were generated for the Zindi test dataset.

---

## Results

The final submission achieved a public Zindi score of

**MAE = 0.13345231**

The Random Forest classifier showed the best overall performance among all evaluated models.

---

## Repository Structure

```text
├── data/
├── models/
├── notebooks/
│   └── financial-inclusion-africa.ipynb
├── requirements.txt
├── README.md
└── Plan.md
```

---

## Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- Jupyter Notebook

---

## Running the Project

Create a virtual environment

```bash
python -m venv .venv
```

Activate it

Windows PowerShell

```powershell
.venv\Scripts\Activate.ps1
```

Install the dependencies

```bash
pip install -r requirements.txt
```

Open the notebook

```bash
jupyter notebook
```

---

## Future Improvements

Possible future work includes

- Advanced Feature Engineering
- Larger Hyperparameter Search
- XGBoost
- LightGBM
- CatBoost
- Ensemble Learning

---

## Author

Sebastian Bentzien

Data Science & AI Engineering Bootcamp

2026