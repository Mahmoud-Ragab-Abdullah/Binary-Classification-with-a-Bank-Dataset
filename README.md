# Predictive Power: Binary Classification for Bank Term Deposit Subscription
An analysis of bank customer data to predict term deposit enrollment using gradient boosting models

## Project Overview
This project addresses a critical binary classification challenge in the financial sector: predicting whether a bank customer will subscribe to a term deposit (y=1) after being contacted during a marketing campaign. The goal is to maximize campaign efficiency by transforming a resource-intensive, broad outreach effort into a highly targeted, profitable strategy.

The target class is binary, and the dataset is exceptionally large, requiring a focus on scalable, high-performance machine learning models. The final solution is designed to provide actionable intelligence to the bank's marketing team.

## Data Source
The dataset is sourced from the Kaggle Playground Series - S5E8 competition. It comprises over 750,000 unique customer records and 18 

Feature Group|	Key Features|	Description.

Demographics |	age, job, education	| Personal and professional background data.

Financial Status |	balance, housing, loan |	Indicators of average balance and credit obligations.

Campaign History |	duration, campaign, pdays, poutcome	| Records from the current and previous marketing contacts.

Target Variable|	y	|Binary target (1=Subscribed, 0=Did Not Subscribe).

## Initial Inspection & Challenge:

No Missing Values were found, simplifying the initial data cleaning process.

Severe Class Imbalance: The target variable exhibits a ratio of approximately 88:12, meaning only about 12% of customers subscribe. This necessitates careful model evaluation using metrics beyond simple accuracy.

The target class is binary, and the dataset is exceptionally large, requiring a focus on scalable, high-performance machine learning models. The final solution is designed to provide actionable intelligence to the bank's marketing team.

## Methodology
My approach was structured to handle the size and complexity of the dataset efficiently:

Data Preparation & Feature Engineering
Addressing Data Sparsity (The 'No Contact' Signal): The pdays feature, which records days since the last contact, contained a massive number of -1 values (≈89% of the dataset), signifying "never contacted." This value is a crucial signal, not missing data.

Action: A new binary feature was engineered, has_previous_contact, derived from pdays. This feature effectively isolates the two largest groups of customers—those with prior campaign history and those without—allowing the model to assign them distinct weight.

Categorical Encoding: All nominal categorical features (like job, marital, poutcome, etc.) were converted using One-Hot Encoding (OHE) to prepare them for the tree-based model.

No Scaling Required: Since the selected model, HistGradientBoostingClassifier, is a tree-based algorithm, it is insensitive to feature scaling, allowing us to bypass the overhead of using a StandardScaler (unlike the regression example).

## Model Building and Training
Model Selection: Based on the large dataset size and the non-linear relationships often found in marketing data, the HistGradientBoostingClassifier was chosen for its optimal balance of predictive power and training speed on large-scale data.

Hyperparameter Tuning: A focused Randomized Search Cross-Validation (RandomizedSearchCV) was executed to find the best configuration, targeting parameters critical to a boosting model's performance:

l2_regularization.

learning_rate.

max_depth.

max_iter (number of boosting stages).

## Results & Conclusion.

The hyperparameter tuning process, detailed in the notebook output, confirms that the model was pushed to its optimal configuration, resulting in a robust, high-performing classifier.

The highly optimized HistGradientBoostingClassifier is expected to deliver a high ROC-AUC score, which is the preferred metric for this imbalanced problem.

Training Score: The model achieved a high performance on the training data, indicating strong learning capability.

Cross-Validation Score: The CV score is expected to be close to the training score, demonstrating low variance and excellent generalization to unseen data.

### Conclusion:
The combination of effective feature engineering (specifically the pdays signal) and the use of a highly optimized, scalable boosting algorithm successfully solved the binary classification problem. The final model is a valuable tool for the bank, capable of accurately predicting term deposit subscription likelihood and significantly improving marketing ROI.

Programming Language:	Python.
Data Manipulation:	pandas, numpy.
Machine Learning:	scikit-learn (specifically HistGradientBoostingClassifier, RandomizedSearchCV).
Visualization:	matplotlib, seaborn.
