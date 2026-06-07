# DATA 402 Proposal

## Requirements

Your proposal should be approximately 1–3 pages and include the following sections.

## 1. Team Members

Julia Lu, Rhea Chellani

## 2. Project Title

Predicting Student Debt and Post-Graduation Earnings from U.S. College Characteristics

## 3. Problem Description

The problem we are trying to solve is predicting student financial outcomes based on college characteristics. Specifically, we want to see whether information about a college, such as tuition, school type, admission rate, graduation rate, enrollment size, location, and financial aid, can help predict outcomes like median student debt or earnings after attendance.

This is interesting because choosing a college is a major financial decision for many students. Students often compare schools based on cost and reputation, but it can be hard to know which factors are actually connected to long-term financial outcomes. By studying this dataset, we hope to better understand what college traits are most associated with debt and earnings.

This project is a supervised machine learning problem because we will use known college data and known financial outcomes to train models. Since our target variable will likely be a numeric value, such as median student debt or median earnings, this will be a regression task. We may use models such as linear regression, ridge regression, or lasso regression to make predictions and compare performance.

## 4. Dataset

Dataset link: <https://collegescorecard.ed.gov/data>

### Description Requirements

Describe:

- Where the dataset comes from
- The approximate size of the dataset
- Available features
- Target variables
- Any anticipated preprocessing challenges

You may use datasets from:

- Kaggle
- UCI Machine Learning Repository
- Public APIs
- Government open-data sources
- Self-collected datasets
- Web scraping
- Other approved sources

The dataset comes from the U.S. Department of Education’s College Scorecard, which is a government open-data source about colleges and universities in the United States. It provides public information about college costs, admissions, enrollment, graduation rates, student aid, student debt, and earnings after attendance.

The dataset includes information for several thousand U.S. colleges and universities. For this project, we plan to use the most recent institution-level data file instead of the full historical dataset so that the project stays manageable. The dataset still has many rows and a large number of possible columns, so we will choose a smaller set of features that are most relevant to our research question.

Available features include school type, location, admission rate, tuition, average net price, enrollment size, completion rate, retention rate, student demographics, percentage of students receiving Pell Grants, and percentage of students taking out federal loans. Other possible features may include test score ranges, financial aid information, and institutional spending.

Our target variable will likely be either median student debt or median earnings after attendance. Both are numeric outcomes, which makes this a regression problem. We will decide which target to focus on based on which variable has more complete and usable data.

Some anticipated preprocessing challenges include missing values, schools with unavailable target variables, and the large number of columns in the dataset. We may need to remove rows with missing target values, fill or remove missing feature values, select only the most useful features, encode categorical variables such as school type or state, scale numeric variables, and check for outliers such as very small or specialized institutions.

## 5. Proposed Models

Identify at least two models you plan to explore.

Possible models include:

- Linear regression
- Ridge regression
- Lasso regression[^1]
- Logistic regression
- Support vector machines[^2]
- Perceptrons / multilayer neural networks
- Convolutional neural networks

Explain why these models may be appropriate for your problem.

### Proposed Models

#### 1. Linear Regression

Linear regression will be used as a baseline model to predict a continuous outcome such as median earnings after graduation (`MD_EARN_WNE_P10`) or average student debt. This model is appropriate because many variables in the College Scorecard dataset are quantitative and may have approximately linear relationships with earnings outcomes. Linear regression also provides highly interpretable coefficients, allowing us to understand how factors such as tuition cost, graduation rate, SAT scores, or percentage of STEM students impact post-graduation earnings.

#### 2. Ridge Regression

Ridge regression will also be explored because the College Scorecard dataset contains many potentially correlated predictors. For example, tuition cost, admission selectivity, and average SAT scores may all be strongly related. Ridge regression helps reduce overfitting by shrinking coefficients and handling multicollinearity more effectively than ordinary linear regression. This may improve prediction accuracy when working with a large number of features.

#### 3. Lasso Regression

Lasso regression is another appropriate model we could use because it performs both regularization and feature selection. Since the dataset includes hundreds of variables, many predictors may contribute little useful information. Lasso regression can automatically reduce less important coefficients to zero, helping identify the most influential institutional and demographic factors related to earnings or student success outcomes. This improves interpretability and could simplify the final model.

## 6. Evaluation Metrics

Describe how you plan to evaluate success.

Examples include:

- Accuracy
- Precision / Recall
- F1 score
- ROC-AUC
- RMSE
- MAE
- Confusion matrices

## 7. Expected Challenges

Discuss possible difficulties such as:

- Missing data
- Class imbalance
- Overfitting
- Computational limitations
- Dataset quality issues

## 8. Team Responsibilities

Briefly describe how work will be divided between team members.

[^1]: If doing a regression task.
[^2]: If doing a classification task.
