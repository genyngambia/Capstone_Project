### Project Title
Obesity Prediction Using Demographic and Lifestyle Factors

**Author** Genevieve Ngambia

## Executive Summary
This project aims to predict obesity levels among adults in the United States using demographic and lifestyle factors like age, education, income, gender, and location. Leveraging machine learning, it provides insights to help public health organizations target high-risk groups and improve health outcomes.

According to recent data, nearly 1 in 3 adults (30.7%) in the U.S. are overweight, while more than 2 in 5 (42.4%) have obesity, including 9.2% who suffer from severe obesity. The prevalence of obesity and related conditions, such as diabetes and heart disease, continues to strain healthcare systems ([NIDDK Obesity Statistics](https://www.niddk.nih.gov/health-information/health-statistics/overweight-obesity#:~:text=the%20above%20table-,Nearly%201%20in%203%20adults%20(30.7%25)%20are%20overweight.,9.2%25)%20have%20severe%20obesity.)).


#### Rationale
Obesity is a significant public health concern, contributing to numerous chronic conditions such as diabetes, heart disease, and hypertension. 
Understanding the factors that contribute to obesity can enable policymakers and public health officials to design targeted interventions that improve health outcomes and reduce healthcare costs. 
By predicting obesity risk based on demographic and lifestyle factors, we can better direct public health resources to those who need them most.

#### Research Question
How do demographic and lifestyle factors, including age, education, income, gender, and location, predict obesity rates among adults in the United States?

#### Data Sources
- **Source**: Behavioral Risk Factor Surveillance System (BRFSS) dataset.
- **Features**: `Age`, `Gender`, `Education`, `Income`, `Race/Ethnicity`, `Location`, and obesity-related measurements (`Data_Value`).
- **Target**: A binary target variable `Obese` (1 for obese if `Data_Value >= 30`, otherwise 0).


#### Methodology
### Data Cleaning:
- **Handling Missing Values**: Rows with missing target values (`Data_Value`) were removed. Missing values in categorical variables such as `Age(years)`, `Education`, `Income`, and `Gender` were filled using the mode.
- **Filtering for Obesity-Related Data**: Only records where the `Class` was related to "Obesity / Weight Status" were retained, resulting in 36,234 records after cleaning.
- **Feature Engineering**: Created a binary target variable, `Obese`, where individuals with `Data_Value >= 30` were labeled as obese (1), and others as non-obese (0).
- **Distribution**: Obese (1): 23,187 instances (approx. 70%). Non-Obese (0): 9,493 instances (approx. 30%).
This class imbalance is addressed using SMOTE (Synthetic Minority Over-sampling Technique) to improve model performance and ensure the model doesn't overly favor the majority class.

### Feature Encoding:
- Categorical variables (`Age(years)`, `Education`, `Gender`, `Income`, `Race/Ethnicity`, and `LocationDesc`) were label-encoded for use in machine learning models.


### Exploratory Data Analysis (EDA):

- **Obesity by Age**: Obesity increases with age, peaking between 45 and 64. Younger age groups have lower median obesity rates, with a few outliers.
- **Obesity by Education**: Higher education is linked to lower obesity rates, especially among college graduates, suggesting education influences healthier lifestyle choices.
- **Obesity by Gender**: Median rates are similar for males and females, but females show a wider range of values with more outliers, indicating higher variability.
- **Obesity by Income**: Obesity rates are inversely related to income, with lower-income groups showing higher rates. Higher income levels correlate with lower obesity rates.
- **Obesity by Race/Ethnicity**: Obesity rates vary across groups, with Non-Hispanic Black and American Indian/Alaska Native groups having higher median rates, while Asian individuals have the lowest. Other groups show moderate variability.
- **Obesity by Geographic Location**: Obesity rates vary significantly across regions. Areas like Guam, Puerto Rico, and Mississippi show higher median rates, while District of Columbia and Colorado have lower rates. This highlights the need for region-specific health interventions to effectively address obesity in high-risk areas.


### Modeling:

#### Initial Classification Models:
In the initial phase of the analysis, we trained and evaluated four machine learning models: **Logistic Regression**, **K-Nearest Neighbors (KNN)**, **Support Vector Machine (SVM)**, and **Decision Tree**.

- **Decision Tree**: Achieved the highest accuracy at 71%, with an F1-score of 71%.
- **KNN**: Had a slightly lower accuracy at 67%, with an F1-score of 67%.

Due to their relatively better performance, we focused on tuning the **Decision Tree** and **KNN** models.

#### Model Tuning:

- **Decision Tree**: After hyperparameter tuning (e.g., `max_depth`, `min_samples_split`, `min_samples_leaf`), the performance metrics (accuracy and F1-score of 71%) remained unchanged, suggesting that the model's default settings were already close to optimal. The `LocationDesc` feature contributed significantly, accounting for 54% of feature importance, which may have restricted further performance improvements.
  
- **KNN**: Hyperparameter tuning of `n_neighbors`, `weights`, and `metric` resulted in a slight improvement, with accuracy increasing to 68% and an F1-score of 68%.

#### Exploring Ensemble Models:
Given the limited improvements from tuning **Decision Tree** and **KNN**, we explored ensemble models, including **Random Forest** and **XGBoost**. These models are known for their ability to reduce overfitting and generalize better by aggregating the results of multiple decision trees.

- **Random Forest**: Achieved the highest accuracy at 72%, along with well-balanced precision, recall, and F1-score, making it the best overall candidate.
- **XGBoost**: Achieved 71% accuracy, with strong precision and recall, but slightly underperformed compared to **Random Forest** in overall metrics.

#### Model Performance Comparison:
Here is a summary of the key performance metrics across all models:

| Model                | Accuracy | Precision | Recall | F1-Score |
|----------------------|----------|-----------|--------|----------|
| Logistic Regression   | 61%      | 62%       | 61%    | 60%      |
| Decision Tree         | 71%      | 72%       | 71%    | 71%      |
| SVM                   | 61%      | 62%       | 61%    | 60%      |
| KNN                   | 68%      | 68%       | 68%    | 68%      |
| Random Forest         | 72%      | 73%       | 72%    | 72%      |
| XGBoost               | 71%      | 71%       | 71%    | 70%      |

The image below provides a visual comparison of model performance across Accuracy, Precision, Recall, and F1-Score:

![Model Comparison: Accuracy, Precision, Recall, and F1-Score](https://github.com/genyngambia/Capstone_Project/blob/capstone_project/Capstone_Project/images/model_comparison_with_xgboost.png)


The Random Forest model outperformed the others with the highest accuracy and well-balanced metrics, making it the top candidate for predicting obesity.


#### Final Model Selection:
Based on the performance metrics, we selected **Random Forest** as the final model for predicting obesity due to its highest accuracy (72%) and balanced performance across precision, recall, and F1-score. **Random Forest** also offers robustness against overfitting, as it aggregates the results of multiple decision trees.

#### Random Forest Feature Importance:

| Feature          | Importance |
|------------------|------------|
| LocationDesc     | 0.572184   |
| Age (years)      | 0.140388   |
| Race/Ethnicity   | 0.109763   |
| Income           | 0.085819   |
| Education        | 0.073599   |
| Gender           | 0.018247   |

In conclusion, **Random Forest** emerged as the best model for obesity prediction due to its superior performance and its ability to drive future public health interventions aimed at reducing obesity.


#### Results

1. **Customizing Health Policies for High-Risk Locations**  
   - **Key Finding**: LocationDesc was the most important factor in the Random Forest model (importance score: 0.57). The EDA revealed significant variation in obesity rates across geographic regions, with areas like Guam, Puerto Rico, and Mississippi showing higher median obesity rates, while the District of Columbia and Colorado exhibited lower rates.
   - **Insight**: Public health interventions should focus on high-risk locations, particularly in regions with higher obesity rates. Region-specific strategies can effectively address the unique challenges in areas such as Guam, Puerto Rico, and Mississippi, while leveraging lower-risk regions like the District of Columbia and Colorado as models for best practices.

2. **Targeting Interventions for Specific Racial/Ethnic Groups**  
   - **Key Finding**: Race/Ethnicity was another critical factor (importance score: 0.11), with higher obesity rates in Non-Hispanic Black and American Indian/Alaska Native groups. Asian populations had the lowest obesity rates.
   - **Insight**: Public health interventions need to be culturally sensitive and customized to address the specific dietary habits, cultural practices, and healthcare access barriers faced by these groups.

3. **Addressing Obesity Across Age, Income, and Education Levels**  
   - **Key Finding**: EDA highlighted distinct patterns for age, income, and education levels. Obesity rates peak between ages 45-64, are higher among lower-income groups, and inversely correlated with education levels.
   - **Insight**: Middle-aged adults and low-income communities are high-priority groups. Educational interventions can be effective in reducing long-term obesity risks by promoting healthy habits early in life.

4. **High-Risk Group Interventions**  
   - **Low-Income Communities**: Subsidizing healthy food and offering fitness incentives can reduce obesity rates in these areas.
   - **Middle-Aged Adults**: Corporate wellness programs and preventative healthcare screenings can address obesity risks.
   - **Education-Based Interventions**: Introducing nutrition and fitness education early in schools can help prevent obesity.


### Potential Next Steps

1. **Localized Health Campaigns**  
   - Focus on regions with high obesity rates, such as Guam, Puerto Rico, and Mississippi, by directing resources like health screenings, fitness programs, and educational campaigns to these areas.
   - Tailor interventions to the specific challenges of these high-risk regions while also learning from lower-obesity areas like the District of Columbia and Colorado. Rural and inner-city regions with high obesity rates should also be prioritized for more effective resource allocation.

2. **Community-Based Programs**  
   - Build community centers for physical activities, offer nutritional classes, and collaborate with local businesses to promote healthier lifestyles in high-risk locations.

4. **Culturally Tailored Nutrition Programs**  
   - Implement nutrition programs that respect the dietary preferences of specific racial/ethnic groups, especially in African American and Hispanic communities.

5. **Improved Access to Healthcare**  
   - Expand healthcare services, such as mobile clinics or Medicaid coverage, in communities with higher obesity rates (Non-Hispanic Black, American Indian/Alaska Native groups).

6. **Targeted Exercise Programs**  
   - Introduce culturally appropriate exercise initiatives (e.g., music and dance) and encourage family or group-based activities to increase participation rates in diverse communities.

7. **Subsidized Healthy Foods for Low-Income Communities**  
   - Provide food vouchers or subsidies to make healthier food options affordable in low-income areas.

8. **Corporate Wellness Programs for Middle-Aged Adults**  
   - Promote healthier lifestyles in workplaces through corporate wellness initiatives that encourage regular exercise and preventative healthcare screenings.

9. **Education-Based Interventions**  
   - Promote nutrition and fitness education in schools and colleges to encourage healthy habits early in life. Public health campaigns targeting college graduates can also reinforce long-term healthy lifestyle practices.


#### Outline of project

- [Link to notebook 1]()


##### Contact and Further Information
For more information or collaboration, please contact gentsafack@gmail.com.
