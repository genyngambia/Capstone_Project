# Obesity Prediction Using Demographic and Lifestyle Factors

## 1. Business Understanding

**Goal**:  
The objective of this analysis is to predict obesity levels among adults in the United States based on demographic and lifestyle factors. By understanding how variables such as age, education, income, gender, and location contribute to obesity, we can better target public health campaigns toward high-risk groups, improving health outcomes and resource allocation.

### Key Business Questions:
- How do demographic and lifestyle factors (e.g., age, gender, education, income, race/ethnicity) predict obesity rates among adults in the U.S.?

### Business Impact:
- These predictors help public health organizations in formulating obesity-related policies, leading to better health outcomes and reduced healthcare costs.

---

## 2. Data Understanding

- **Source**: Behavioral Risk Factor Surveillance System (BRFSS) dataset.
- **Features**: `Age`, `Gender`, `Education`, `Income`, `Race/Ethnicity`, `Location`, and obesity-related measurements (`Data_Value`).
- **Target**: A binary target variable `Obese` (1 for obese if `Data_Value >= 30`, otherwise 0).

---

## 3. Data Preparation

### Data Cleaning:
- **Handling Missing Values**: Rows with missing target values (`Data_Value`) were removed. Missing values in categorical variables such as `Age(years)`, `Education`, `Income`, and `Gender` were filled using the mode.
- **Filtering for Obesity-Related Data**: Only records where the `Class` was related to "Obesity / Weight Status" were retained, resulting in 36,234 records after cleaning.
- **Feature Engineering**: Created a binary target variable, `Obese`, where individuals with `Data_Value >= 30` were labeled as obese (1), and others as non-obese (0).

### Feature Encoding:
- Categorical variables (`Age(years)`, `Education`, `Gender`, `Income`, `Race/Ethnicity`, and `LocationDesc`) were label-encoded for use in machine learning models.

### Splitting the Data:
- The data was standardized and split into training (70%) and testing (30%) sets for model evaluation.

---

## 4. Exploratory Data Analysis (EDA)

- **Obesity by Age**: Obesity increases with age, peaking between 45 and 64. Younger age groups have lower median obesity rates, with a few outliers.
- **Obesity by Education**: Higher education is linked to lower obesity rates, especially among college graduates, suggesting education influences healthier lifestyle choices.
- **Obesity by Gender**: Median rates are similar for males and females, but females show a wider range of values with more outliers, indicating higher variability.
- **Obesity by Income**: Obesity rates are inversely related to income, with lower-income groups showing higher rates. Higher income levels correlate with lower obesity rates.
- **Obesity by Race/Ethnicity**: Obesity rates vary across groups, with Non-Hispanic Black and American Indian/Alaska Native groups having higher median rates, while Asian individuals have the lowest. Other groups show moderate variability.

<p float="left">
  <img src="https://github.com/genyngambia/Capstone_Project/blob/capstone_project/Capstone_Project/images/obesity_by_age.png" width="300" />
  <img src="https://github.com/genyngambia/Capstone_Project/blob/capstone_project/Capstone_Project/images/obesity_by_education.png" width="300" /> 
  <img src="https://github.com/genyngambia/Capstone_Project/blob/capstone_project/Capstone_Project/images/obesity_by_gender.png" width="300" />
</p>

<p float="left">
  <img src="https://github.com/genyngambia/Capstone_Project/blob/capstone_project/Capstone_Project/images/obesity_by_income.png" width="300" />
  <img src="https://github.com/genyngambia/Capstone_Project/blob/capstone_project/Capstone_Project/images/obesity_by_race_ethnicity.png" width="300" />
</p>


---

## 5. Modeling

Multiple machine learning models were implemented, including:

- `Logistic Regression`
- `Decision Trees`
- `Support Vector Machines (SVM)`
- `K-Nearest Neighbors (KNN)`
- `Linear Regression`

Each model was evaluated for `accuracy`, `precision`, `recall`, and `F1-score`. Additionally, a tuned `Decision Tree` was trained using `GridSearchCV` to optimize hyperparameters.

### Model Comparison:
The comparison of each machine learning technique is based on accuracy, precision, recall, and F1-score.

![Model Comparison](https://github.com/genyngambia/Capstone_Project/blob/capstone_project/Capstone_Project/images/model_comparison.png)

### Feature Importance Visualization:
A key comparison was made between the default decision tree and the tuned decision tree model. The feature importance before and after tuning is displayed in a bar chart.
![Model Performance Comparison](https://github.com/genyngambia/Capstone_Project/blob/capstone_project/Capstone_Project/images/model_performance_comparison.png)

---

## 6. Insights and Recommendations:

- **Location**, **Race/Ethnicity**, and **Age** are key predictors of obesity. This suggests that public health policies targeting specific regions and demographics may be effective.
- **Education** and **Income** also play important roles, highlighting the socioeconomic dimensions of obesity.
- Further work could explore other lifestyle factors, such as physical activity and diet, to refine these predictions.
