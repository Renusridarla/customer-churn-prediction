# Customer Churn Prediction and Customer Analysis Dashboard

> **An End-to-End Machine Learning Solution for Predicting Customer Churn**  
> *Artificial Intelligence & Machine Learning (AIML) Internship Capstone Project Report Implementation*

---

## 1. Project Title
**Customer Churn Prediction and Customer Analysis Dashboard**

---

## 2. Project Overview
This project presents an end-to-end predictive modeling application built to predict customer churn for telecommunications services. The solution encompasses data cleaning, feature preprocessing, exploratory data analysis (EDA), multi-algorithm model training, cross-validation, and an interactive React web dashboard backed by a Flask REST API.

---

## 3. Problem Statement
Customer attrition (churn) is one of the most critical challenges facing subscription-based business models. Acquiring new customers costs 5 to 25 times more than retaining existing ones. Predicting high-risk churn customers allows telecom providers to proactively deliver targeted retention incentives, reduce revenue loss, and maximize customer lifetime value.

---

## 4. Key Objectives
* Build a scalable dataset preprocessing pipeline preventing data leakage.
* Conduct comprehensive Exploratory Data Analysis (EDA) on customer attributes.
* Train and evaluate 5 Machine Learning classification models (Logistic Regression, Decision Tree, Random Forest, K-Nearest Neighbors, Support Vector Machine).
* Perform 5-Fold Stratified Cross-Validation for robust performance estimation.
* Expose real-time prediction and analytical endpoints via a Flask REST API.
* Present live metrics, interactive charts, and prediction tools on a modern React dashboard.

---

## 5. System Features
* **Dashboard Overview**: Key metrics summary cards, churn rate %, tenure distribution, contract breakdown.
* **Predict Customer Churn**: Real-time prediction form, probability score gauge (0-100%), risk level badges ("High Risk", "Medium Risk", "Low Risk"), and dynamic risk factor explanations.
* **Customer Analysis Report**: Empirical insights, EDA charts (payment method, internet service, tenure, gender).
* **Model Performance & Evaluation**: 5-model comparison table, confusion matrix grid, top 10 feature importances.
* **Preset Profiles**: 1-click loading of high-risk and low-risk customer profiles for quick evaluation.

---

## 6. Technologies Used

### Backend & Machine Learning
* **Language**: Python 3.14
* **Data Processing**: Pandas, NumPy
* **Machine Learning**: Scikit-Learn
* **Model Serialization**: Joblib
* **REST API**: Flask, Flask-CORS

### Frontend
* **Framework**: React 18, Vite
* **UI & Styling**: Custom Modern CSS Design System
* **Icons**: Lucide React
* **Charts**: Recharts

---

## 7. Dataset Description
The project uses a realistic Telco Customer Churn dataset containing **7,043 customer records** with 21 attributes:
* **Demographics**: `customerID`, `gender`, `SeniorCitizen`, `Partner`, `Dependents`
* **Account Info**: `tenure`, `Contract`, `PaperlessBilling`, `PaymentMethod`, `MonthlyCharges`, `TotalCharges`
* **Services**: `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`
* **Target Variable**: `Churn` (`Yes` / `No`)

---

## 8. Project Architecture

```
                                  +-----------------------+
                                  |   React Web Frontend  |
                                  |   (Vite / Recharts)   |
                                  +-----------+-----------+
                                              |
                                     HTTP REST API Requests
                                              |
                                              v
                                  +-----------+-----------+
                                  |   Flask Backend API   |
                                  |       (app.py)        |
                                  +-----------+-----------+
                                              |
                                              v
                                  +-----------+-----------+
                                  | Preprocessing Pipeline|
                                  |    (preprocess.py)    |
                                  +-----------+-----------+
                                              |
                                              v
                                  +-----------+-----------+
                                  | Trained ML Model  |
                                  |   (saved_model.pkl)   |
                                  +-----------------------+
```

---

## 9. Data Preprocessing Pipeline
1. **Raw Cleaning**: Converts whitespace strings in `TotalCharges` to float numbers and imputes missing values via `tenure * MonthlyCharges`.
2. **Binary Encoding**: Maps binary categorical attributes (`gender`, `Partner`, `Dependents`, `PhoneService`, `PaperlessBilling`) to 0/1 integers.
3. **One-Hot Encoding**: Applies `OneHotEncoder(drop='first')` to multi-class attributes (`Contract`, `PaymentMethod`, `InternetService`, `OnlineSecurity`, etc.).
4. **Feature Scaling**: Standardizes numeric attributes (`tenure`, `MonthlyCharges`, `TotalCharges`) using `StandardScaler`.
5. **Leakage Prevention**: Encoders and scalers are fitted exclusively on the training set and applied consistently during inference.

---

## 10. Exploratory Data Analysis (EDA) Highlights
* **Churn Distribution**: 26.5% Overall Churn Rate (1,869 churned vs 5,174 retained).
* **Contract Impact**: Month-to-Month contract holders display significantly higher churn rate compared to Two-Year contract holders.
* **Service Impact**: Fiber Optic internet subscribers experience higher churn rates due to price sensitivity.
* **Tenure Relationship**: Newer customers (< 12 months tenure) exhibit 3x higher churn risk than loyal customers (> 48 months).

---

## 11. Machine Learning Classification Algorithms
1. **Logistic Regression** (`LogisticRegression`)
2. **Decision Tree Classifier** (`DecisionTreeClassifier`)
3. **Random Forest Classifier** (`RandomForestClassifier`)
4. **K-Nearest Neighbors** (`KNeighborsClassifier`)
5. **Support Vector Machine** (`SVC`)

---

## 12. Model Evaluation Metrics

| Algorithm | Accuracy (%) | Precision (%) | Recall (%) | F1-Score (%) | 5-Fold CV Score (%) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Random Forest** (Selected Best) | **82.4%** | **78.5%** | **74.2%** | **76.3%** | **75.8% (±1.2%)** |
| Logistic Regression | 80.6% | 76.1% | 71.8% | 73.9% | 73.5% (±1.4%) |
| Support Vector Machine (SVM) | 79.8% | 75.0% | 69.5% | 72.1% | 71.8% (±1.5%) |
| Decision Tree | 78.2% | 71.4% | 68.1% | 69.7% | 69.1% (±1.8%) |
| K-Nearest Neighbors (KNN) | 76.5% | 68.2% | 64.3% | 66.2% | 65.8% (±2.0%) |

---

## 13. Real-Time Prediction Workflow
1. User enters customer parameters on the prediction UI or loads a preset.
2. Frontend dispatches `POST /api/predict` payload to Flask backend.
3. Backend converts input payload via `ChurnPreprocessor.transform_single_dict()`.
4. Saved ML model evaluates input feature vector and generates churn probability score.
5. Response payload returns `prediction` (`Yes`/`No`), `churn_probability` (%), `risk_level`, and risk factor explanations.

---

## 14. Dashboard Pages Overview
* **Page 1: Dashboard Overview** — Summary stats, churn pie chart, contract bar chart, active production model badge.
* **Page 2: Predict Customer Churn** — Interactive form, presets, live probability gauge, risk level badge, contributing factor breakdown.
* **Page 3: Customer Analysis Report** — Payment method, internet service, tenure, and gender EDA charts with dataset-backed insights.
* **Page 4: Model Performance** — 5-model comparative metrics table, confusion matrix grid, top 10 feature importances chart.

---

## 15. Installation Steps

### Prerequisites
* Python 3.10+
* Node.js 18+

### Step 1: Clone or Navigate to Project Folder
```bash
cd customer-churn-prediction
```

### Step 2: Install Backend Dependencies
```bash
cd backend
pip install pandas numpy scikit-learn flask flask-cors joblib matplotlib seaborn
```

### Step 3: Install Frontend Dependencies
```bash
cd ../frontend
npm install
```

---

## 16. How to Run the Backend API
```bash
cd backend
python app.py
```
* The backend runs on `http://127.0.0.1:5000`.
* Automatic Pipeline Check: If `saved_model.pkl` is missing, `app.py` automatically generates the dataset and trains all 5 models on startup!

---

## 17. How to Run the Frontend Dashboard
```bash
cd frontend
npm run dev
```
* Open your browser at `http://localhost:3000`.

---

## 18. Example Prediction API Request & Response

### Request (`POST /api/predict`)
```json
{
  "gender": "Female",
  "SeniorCitizen": 1,
  "Partner": "No",
  "Dependents": "No",
  "tenure": 2,
  "PhoneService": "Yes",
  "InternetService": "Fiber optic",
  "Contract": "Month-to-month",
  "PaymentMethod": "Electronic check",
  "MonthlyCharges": 98.75,
  "TotalCharges": 197.50
}
```

### Response
```json
{
  "prediction": "Yes",
  "churn_probability": 84.6,
  "risk_level": "High Risk",
  "status": "Customer is highly likely to churn",
  "risk_factors": [
    "Month-to-month contract increases churn risk",
    "Short tenure (< 12 months) indicates low retention commitment",
    "Fiber optic service exhibits higher churn rates due to price sensitivity",
    "Electronic check payment method is associated with higher churn"
  ]
}
```

---

## 19. Project Folder Structure

```
customer-churn-prediction/
│
├── backend/
│   ├── app.py                             # Flask API routes
│   ├── requirements.txt                   # Backend dependencies
│   ├── model/
│   │   ├── generate_dataset.py            # Generates Telco dataset
│   │   ├── preprocess.py                  # Preprocessing & encoding pipeline
│   │   ├── train_model.py                 # Multi-model training & evaluation
│   │   └── saved_model.pkl                # Trained model & pipeline dictionary
│   ├── data/
│   │   └── customer_churn.csv             # 7,043 customer records dataset
│   └── notebooks/
│       └── customer_churn_analysis.ipynb  # Capstone report Jupyter Notebook
│
├── frontend/
│   ├── package.json                       # React/Vite dependencies
│   ├── vite.config.js                     # Proxy configuration
│   ├── src/
│   │   ├── components/                    # Sidebar, Header, StatCard
│   │   ├── pages/                         # Overview, PredictChurn, CustomerAnalysis, ModelPerformance
│   │   ├── services/                      # Axios API service
│   │   ├── App.jsx                        # Main layout & router
│   │   ├── index.css                      # Custom design system
│   │   └── main.jsx                       # Entry point
│   └── public/
│
├── README.md                              # Comprehensive project documentation
└── PROJECT_DOCUMENTATION.md               # Internship report workflow documentation
```

---

## 20. Future Enhancements
* Incorporate deep learning binary classifiers (PyTorch / TensorFlow MLP).
* Implement automated hyperparameter tuning (GridSearchCV / Optuna).
* Add individual customer retention action recommendations (e.g. recommend contract upgrade discount).
