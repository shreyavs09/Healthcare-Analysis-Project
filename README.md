# Healthcare Analytics Project

---

## 📄 Project Overview

This project performs a comprehensive data analysis of a healthcare dataset to uncover key insights into patient demographics, admission trends, and treatment costs. It also includes a machine learning component to predict the Length of Stay (LoS) for patients—a critical metric for hospital resource management and patient care planning. Finally, it presents important visuals and insights through interactive multi-page Power BI dashboards.

---

## 🎯 Problem Statement

Healthcare organizations generate vast amounts of data, but extracting actionable insights and predicting key operational metrics like patient Length of Stay remains a challenge. This project aims to:

- Analyze patient data to understand demographic distributions, common medical conditions, and billing patterns.
- Identify key trends in patient admissions and their impact on hospital operations.
- Develop a predictive model for Length of Stay to assist in resource allocation, discharge planning, and improving operational efficiency.

---

## 📊 Dataset

**File:** `Healthcare Analysis Dataset.xlsx - Data.csv`  
**Records:** ~55,500  
**Features:** 17

**Key Columns:**
- **Patient ID:** Unique identifier for each patient
- **Age:** Age of the patient (in years)
- **Gender:** Gender of the patient (e.g., Male, Female, Non-binary)
- **Medical Condition:** Primary medical condition diagnosed
- **Date of Admission, Discharge Date:** Dates of hospital admission and discharge
- **Doctor, Hospital:** Responsible doctor and treating hospital
- **Insurance Provider:** Patient's insurance company
- **Billing Amount:** Total billing amount for treatment (USD)
- **Admission Type:** Type of admission (e.g., Elective, Emergency, Urgent)
- **Test Results:** Outcome of medical tests (e.g., Normal, Abnormal, Inconclusive)
- **Hospital Latitude, Hospital Longitude:** Geographical coordinates of the hospital

---

## 🛠️ Tools & Technologies

- **Data Analysis & Preprocessing:** Python (Pandas, NumPy)
- **Data Visualization:** Python (Matplotlib, Seaborn), Power BI
- **Machine Learning:** Python (Scikit-learn, XGBoost)
- **Interactive Dashboard:** Power BI Desktop
- **Code Environment:** Google Colab, VS Code
- **Version Control:** Git, GitHub

---

## 📁 Project Structure

```
.
├── Healthcare_Analytics_EDA_&_Predictive_Modelling.ipynb   # Main notebook for EDA and  predictive modeling
├── Healthcare Analysis Dataset.xlsx                        # Cleaned healthcare dataset (Excel file)
├── Healthcare Analysis Dashboard.pbix                      # Power BI dashboard file (interactive visualization)
├── Healthcare Analysis Dashboard.pdf                       # PDF export of the Power BI dashboard
├── Healthcare Analysis Dashboard.pptx                      # PowerPoint for dashboard background design
├── BG1.jpg                                                # Dashboard background image 1
├── BG2.jpg                                                # Dashboard background image 2
├── README.md                                              # Project documentation
```

---

## 📈 Exploratory Data Analysis (EDA)

EDA was conducted using Python in Google Colab to understand the dataset's characteristics, identify patterns, and prepare the data for modeling.

### Data Overview

- 55,500 patient records with 17 features.
- No missing values—clean dataset.

### Data Cleaning & Feature Engineering

- Converted date columns to datetime objects.
- Calculated **Length of Stay (LoS)** in days:  
  `(Discharge Date - Date of Admission)`
- Negative LoS values (data errors) set to NaN, then filled with median LoS.
- Extracted time-based features: Admission Year, Month, Day of Week.
- Created Age Group bins (e.g., '18-24', '25-34', '80+').

### Key Univariate Insights

- **Age:** Broadly distributed across adult age groups.
- **Billing Amount & LoS:** Uniform distribution, suggesting diverse patient cases.
- **Gender:** Higher proportion of Female patients, followed by Male and Non-binary.
- **Medical Conditions:** Hypertension, Diabetes, and Obesity most prevalent.
- **Admission Types:** Balanced across Elective, Urgent, and Emergency.
- **Test Results:** Majority are 'Abnormal' or 'Inconclusive'.

### Key Bivariate Insights

- **Average Billing & LoS:** Consistent across medical conditions, admission types, and genders.
- **Test Results by Medical Condition:**  
  - Hypertension & Obesity: Predominantly 'Abnormal'
  - Arthritis: Higher proportion of 'Normal'
- **Monthly Admissions:** Stable trend, no significant seasonal spikes.

---

## 🤖 Predictive Modeling: Length of Stay Prediction

A machine learning model was developed to predict Length of Stay (regression problem).

- **Target Variable:** Length of Stay
- **Features Used:** Age, Gender, Medical Condition, Blood Type, Admission Type, Medication, Test Results, Insurance Provider, Hospital, Admission Year, Admission Month, Admission Day of Week
- **Preprocessing:** One-Hot Encoding via ColumnTransformer within a Pipeline
- **Model:** XGBoost Regressor (`xgb.XGBRegressor`)
- **Train/Test Split:** 80% training, 20% testing

**Performance Metrics:**
- **Mean Absolute Error (MAE):** 7.55 days
- **Root Mean Squared Error (RMSE):** 8.71 days
- **R-squared (R²):** -0.01

---

### Model Performance Discussion

The R-squared value of **-0.01** indicates that the current model's predictive capability is not yet robust, performing below a simple baseline model that would predict the average Length of Stay for all patients. This suggests that predicting Length of Stay is a complex challenge with the current dataset and features.

**Potential reasons for this initial performance:**
- The inherent variability and complexity of patient Length of Stay, influenced by numerous uncaptured factors (e.g., comorbidities, treatment complications, physician practices, hospital resource availability).
- Need for more advanced feature engineering or inclusion of additional, highly relevant data points.
- Initial hyperparameter settings for the XGBoost model might not be optimal.

Despite this, the modeling process successfully identified key features influencing the predictions, providing valuable insights for future improvements.

---

### Feature Importance

Despite the low R², analyzing feature importance provides insights into which variables the model attempted to leverage:

- **Top Predictors:** Insurance Provider (Medicare, Cigna), Test Results_Abnormal, Medical Condition (Asthma)
- **Hospital and Time Factors:** Hospital names and Admission Month (January, November, June)
- **Other Relevant Features:** Medication_Lipitor, Blood Type (O+, AB-), Age

This analysis suggests that while these features hold some individual predictive signal, the overall model needs further refinement to better capture the complex relationships within the data.

---

## 📊 Power BI Dashboard

An interactive Power BI dashboard was developed to provide a user-friendly interface for exploring the healthcare data. The dashboard consists of three main pages:

### 1. Patient Demographics

- Overview of patient counts, average age, billing, and length of stay
- Distribution by Age Group and Gender
- Test Results distribution by Age Group for selected medical conditions
- Top hospitals by patient count
- Filtering by Medical Condition, Month, and Year

### 2. Key Trends

- Trends in Admitted Patients, Avg Length of Stay, and Avg Billing Amount over time
- Breakdown by Day Type (Weekday/Weekend) and Length of Stay categories
- Monthly and daily admission breakdown tables

### 3. Treatment & Cost

- Total Billing Amount by Length of Stay and Admission Type
- Total Billing Amount by Hospital and Insurance Provider
- Prescription patterns for different Medical Conditions

---

## 💡 Key Findings & Recommendations

- **Prevalent Conditions:** Hypertension, Diabetes, and Obesity are most common—targets for public health initiatives.
- **Consistent Costs & Stays:** Average billing and LoS are consistent across conditions, genders, and admission types—warrants further investigation.
- **Distinct Test Result Patterns:** Strong relationship between Medical Condition and Test Results (e.g., Hypertension/Obesity: 'Abnormal'; Arthritis: 'Normal').
- **Hospital-Specific Influences:** Certain hospitals have higher patient volumes and unique influences on LoS.
- **LoS Prediction Challenges & Future Direction:** Feature importance analysis provides guidance; future efforts should focus on enriching the dataset and applying advanced modeling techniques.

---

## 🚀 Future Enhancements

- **Advanced Feature Engineering:** Create interaction terms (e.g., Age × Medical Condition), or features from external data (e.g., socioeconomic factors).
- **Hyperparameter Tuning:** Use GridSearchCV or RandomizedSearchCV for XGBoost.
- **Outlier Analysis & Treatment:** Deeper analysis of outliers in Billing Amount and LoS.
- **Alternative Models:** Try LightGBM, Random Forest, Neural Networks, etc.
- **Interactive Mapping:** Integrate an interactive map (e.g., Folium, Power BI map visuals) for hospital locations and patient distribution.
- **Deployment Simulation:** Plan for deploying the LoS prediction model as a web service (e.g., Flask/Streamlit).

---

## 🏃 How to Run Locally

**Clone the repository:**
```sh
git clone https://github.com/your-username/Healthcare-Analytics-Patient-Length-of-Stay.git
cd Healthcare-Analytics-Patient-Length-of-Stay
```

**Power BI Dashboard:**
- Ensure you have Power BI Desktop installed.
- Open `Healthcare Analysis Dashboard.pbix` in Power BI Desktop.

**Python EDA & Predictive Modeling:**
- Ensure Python is installed (preferably Python 3.8+).
- (Recommended) Use a virtual environment:
    ```sh
    python -m venv venv
    venv\Scripts\activate  # On Windows
    ```
- Install required libraries:
    ```sh
    pip install pandas numpy matplotlib seaborn scikit-learn xgboost
    ```
- Open `Healthcare_Analytics_EDA_&_Predictive_Modelling.ipynb` in Jupyter Notebook or VS Code with the Jupyter extension.
- Run all cells sequentially. Ensure `Healthcare Analysis Dataset.xlsx - Data.csv` is in the same directory.

---

## 📧 Connect with Me

- **LinkedIn:** [www.linkedin.com/in/shreyavs09](https://www.linkedin.com/in/shreyavs09)
- **Email:** sshreyavs@gmail.com