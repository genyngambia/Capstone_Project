Portuguese Bank Marketing Campaign Analysis
Business Understanding
The goal of this analysis was to predict whether a client would subscribe to a term deposit based on data collected from a Portuguese bank's marketing campaigns. The data consists of personal, financial, and campaign-related features, which are used to model and predict customer behavior. The aim is to improve the bank’s marketing strategy by understanding key factors influencing customer decisions, thus optimizing future campaigns.
 2.  Data Understanding & Preparation
Data Description: The dataset contains information from multiple telemarketing campaigns, including features such as age, job, education, duration of the call, and other personal and campaign-specific attributes.
Cleaning & Transformation: There was no cleaning performed as none was needed. We  handled categorical variables through one-hot encoding. Numerical variables were standardized to ensure better model performance.
Modeling Approach
We implemented four different classification models to predict customer subscriptions:
Logistic Regression
K-Nearest Neighbors (KNN)
Decision Tree
Support Vector Machine (SVM)
Each model was trained and evaluated on the cleaned dataset, and hyperparameter tuning was performed (especially for KNN and Decision Tree) to optimize their performance.
Model Comparison and Performance with no tuning parameters
Model
Train Time (s)
Train Accuracy
Test Accuracy
Logistic Regression
0.2467
0.9119
0.9114
K-Nearest Neighbors
0.0157
0.9286
0.9030
Decision Tree
0.1822
1.0000
0.8866
Support Vector Machine (SVM)
12.6516
0.9217
0.9111




Interpretation of the findings:
Logistic Regression and SVM are the best-performing models, with strong generalization and consistent accuracy on both training and test data. While SVM delivers excellent performance, it comes at the cost of significantly longer training time (12.65 seconds), making it the slowest of the models. If time and computational resources are a concern, Logistic Regression offers similar accuracy but with much faster training time (0.25 seconds).
K-Nearest Neighbors (KNN) is the fastest model to train (0.02 seconds) but shows a slight drop in test accuracy compared to the training data, indicating some room for improvement. 
Decision Tree overfits the training data, with a perfect accuracy of 100% but a significant drop in test accuracy (88.66%). 

Model Performance Improvement Efforts
In this project, we attempted several strategies to improve the performance of the models, including feature selection and hyperparameter tuning for K-Nearest Neighbors (KNN) and Decision Tree models. Here’s an overview of the steps taken and the outcomes of each attempt:

1. Feature Selection: Logistic Regression
To improve model performance, we attempted to remove irrelevant features based on feature importance values. Despite this effort, Logistic Regression showed only marginal performance changes. The results were as follows:
Accuracy: 0.9097
Precision: 0.6702
Recall: 0.4021
F1-Score: 0.5027
Observation: Removing less relevant features did not lead to significant improvements in the model’s performance. The Logistic Regression model maintained similar accuracy, but the recall was low, indicating the model struggled to identify true positives.

2. Hyperparameter Tuning: K-Nearest Neighbors (KNN)
We slightly improved the K-Nearest Neighbors (KNN) model through hyperparameter tuning. Specifically, we focused on adjusting the number of neighbors (n_neighbors) to optimize the model's performance. The best result was found with 19 neighbors:
Best KNN Parameters: {'n_neighbors': 19}
Best Cross-Validated Accuracy: 0.9106
Tuned KNN Test Accuracy: 0.9088
Comparison with Pre-Tuning Values:
Pre-Tuning Test Accuracy: 0.9030
Post-Tuning Test Accuracy: 0.9088
Observation:
After tuning, the KNN test accuracy improved slightly, increasing from 90.30% to 90.88%. This indicates a small but noticeable enhancement in model performance after adjusting the number of neighbors, though the overall improvement is modest. The KNN model remains competitive but does not show a drastic change in accuracy as a result of the tuning process.
ill underperforming in identifying true positives, even though precision is moderately high.

3. Hyperparameter Tuning: Decision Tree
We applied extensive hyperparameter tuning for the Decision Tree model, optimizing parameters such as the criterion, max depth, min samples split, and min samples leaf. The best parameters were:
Best Decision Tree Parameters: {'criterion': 'gini', 'max_depth': 5, 'min_samples_leaf': 3, 'min_samples_split': 2}
Best Cross-Validated Accuracy: 0.9131
Tuned Decision Tree Test Accuracy: 0.9148
Comparison with Pre-Tuning Values:
Pre-Tuning Test Accuracy: 0.8866
Post-Tuning Test Accuracy: 0.9148
Observation:
After tuning, the Decision Tree test accuracy improved significantly from 88.66% to 91.48%. This indicates that hyperparameter tuning had a substantial positive impact on the model's ability to generalize and make accurate predictions. Compared to both the default Decision Tree and the tuned KNN model, the tuned Decision Tree showed a better balance.
Summary of Efforts
Feature Selection for Logistic Regression: Minimal improvement was observed in model performance, with accuracy remaining around 90.97%, and recall being particularly low at 40.21%. Feature selection did not lead to significant gains in performance.
Hyperparameter Tuning for KNN: Tuning the n_neighbors parameter improved test accuracy slightly, from 90.30% to 90.88%
Hyperparameter Tuning for Decision Tree: Decision Tree tuning yielded the best results, with test accuracy increasing significantly from 88.66% to 91.48%. 
Findings and Insights
Key Predictors:
Features like duration, age, nr.employed, and euribor3m were identified as the most impactful on customer behavior.
Less relevant features (e.g., day of the week) were removed during feature selection, but this led to minimal improvements in performance for Logistic Regression.
Actionable Insights:
Call Duration: Longer call duration significantly increases the likelihood of subscription, indicating that more meaningful and engaging conversations positively influence customer decisions.
Economic Indicators: Features such as nr.employed and euribor3m reflect broader market conditions that also affect customer behavior, implying that economic factors play a crucial role in decision-making.
Recommendations and Next Steps
Targeted Marketing: Focus on customers who are more engaged in longer conversations, as they have a higher likelihood of subscribing. Tailor customer interactions based on age, employment status, and financial indicators to further personalize the marketing approach.
Refining Campaigns: Optimize future marketing campaigns by tailoring strategies to individuals who are more likely to respond positively, using personal attributes such as job type, education level, and financial standing. This will help improve conversion rates and customer engagement.


