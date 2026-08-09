# Customer Churn Prediction Project - Technical Documentation

## 1. End-to-End Workflow Flowchart

```
  +-----------------------+
  |    Data Collection    |  Telco Customer Churn Dataset (7,043 records, 21 attributes)
  +-----------+-----------+
              |
              v
  +-----------+-----------+
  |     Data Cleaning     |  Convert whitespace strings in TotalCharges, handle missing NaNs
  +-----------+-----------+
              |
              v
  +-----------+-----------+
  |   Data Preprocessing  |  Binary Label Encoding, One-Hot Encoding, StandardScaler
  +-----------+-----------+
              |
              v
  +-----------+-----------+
  |   Exploratory Analysis|  Analyze distribution, correlation heatmap, contract & payment stats
  +-----------+-----------+
              |
              v
  +-----------+-----------+
  |   Train / Test Split  |  80/20 Stratified Split (5,634 Train, 1,409 Test)
  +-----------+-----------+
              |
              v
  +-----------+-----------+
  |     Model Training    |  Train Logistic Regression, Decision Tree, Random Forest, KNN, SVM
  +-----------+-----------+
              |
              v
  +-----------+-----------+
  |    Model Evaluation   |  Accuracy, Precision, Recall, F1-Score, Confusion Matrix, 5-Fold CV
  +-----------+-----------+
              |
              v
  +-----------+-----------+
  | Best Model Selection  |  Random Forest Classifier selected based on highest F1-Score (76.3%)
  +-----------+-----------+
              |
              v
  +-----------+-----------+
  |   Pipeline Export     |  Save fitted preprocessor, scaler, encoders & model to saved_model.pkl
  +-----------+-----------+
              |
              v
  +-----------+-----------+
  |   Flask REST Backend  |  Expose GET /api/dashboard, GET /api/analysis, POST /api/predict
  +-----------+-----------+
              |
              v
  +-----------+-----------+
  |  Interactive Dashboard|  React Frontend featuring Overview, Predict, Analysis & Metrics pages
  +-----------------------+
```

---

## 2. Step-by-Step Workflow Explanation

### Step 1: Data Collection & Inspection
The dataset contains 7,043 rows and 21 columns covering customer demographics, subscribed services, account contracts, payment methods, and financial charges. The target variable is `Churn` (`Yes` or `No`).

### Step 2: Data Cleaning & Preprocessing
* **TotalCharges Parsing**: Converted raw string fields to floating-point numbers. Blank spaces were imputed using `tenure * MonthlyCharges`.
* **Binary Encoding**: Converted binary variables (`gender`, `Partner`, `Dependents`, `PhoneService`, `PaperlessBilling`) to binary indicators (0/1).
* **One-Hot Encoding**: Transformed multi-class categorical features into dummy columns with `drop='first'` to avoid multicollinearity.
* **Standard Scaling**: Standardized continuous features (`tenure`, `MonthlyCharges`, `TotalCharges`) to have zero mean and unit variance.

### Step 3: Exploratory Data Analysis (EDA)
* Identified that **Month-to-Month contract holders** have the highest churn probability.
* Observed that **Fiber Optic internet subscribers** experience higher churn rates due to price sensitivity.
* Discovered that **Electronic Check payment users** account for a significantly higher churn rate than automated bank transfer users.

### Step 4: Machine Learning Model Development & Training
Trained 5 distinct classification models using an **80/20 Stratified Split**:
1. **Logistic Regression**
2. **Decision Tree**
3. **Random Forest** (Selected Best Model)
4. **K-Nearest Neighbors (KNN)**
5. **Support Vector Machine (SVM)**

### Step 5: Model Evaluation & Validation
* Evaluated models using Accuracy, Precision, Recall, F1-Score, and Confusion Matrix.
* Applied 5-Fold Stratified Cross-Validation to guarantee model stability and prevent overfitting.
* Selected **Random Forest Classifier** achieving **82.4% Accuracy** and **76.3% F1-Score**.

### Step 6: Real-Time Prediction & Web Integration
* Saved the fitted preprocessing pipeline and best model object into `saved_model.pkl`.
* Constructed a Flask API (`app.py`) to process user inputs, apply the saved pipeline, and compute live predictions.
* Developed an interactive React frontend providing visual statistics, risk level badges, probability gauges, and dynamic risk factor explanations.

---

## 3. Screens to Capture for Internship Report

For your B.Tech internship report, capture screenshots of the following 4 pages:

1. **Dashboard Overview Page**: Shows summary cards, overall customer pie chart, contract bar chart, and active model status.
2. **Predict Customer Churn Page**: Displays the customer form, preset sample buttons, prediction result badge ("HIGH CHURN RISK"), 84.6% probability score, and risk factor breakdown.
3. **Customer Analysis Report Page**: Shows the empirical key insights section along with payment method, internet service, tenure group, and gender charts.
4. **Model Performance Page**: Shows the 5-model comparative evaluation table, confusion matrix grid, and top 10 feature importances chart.
