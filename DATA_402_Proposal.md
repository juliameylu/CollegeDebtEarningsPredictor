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

This project is a supervised machine learning problem because we will use known college data and known financial outcomes to train models. Since our target variable will likely be a numeric value, such as median student debt or median earnings, this will be a regression task.


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

Since this project will focus on predicting continuous outcomes from the College Scorecard Dataset, the project will be evaluated using regression metrics. These metrics will measure how accurately the models predict post-graduation earnings based on institutional and demographic variables.

The dataset will be split into training and testing sets so that model performance can be evaluated on unseen data. Cross-validation may also be used when tuning hyperparameters for ridge and lasso regression.

1. Root Mean Squared Error (RMSE): RMSE will be one of the primary evaluation metrics because it measures the average magnitude of prediction error while penalizing larger errors more heavily. Since the target variable represents earnings in dollars, RMSE provides an interpretable measure of how far predictions are from actual earnings values. Lower RMSE values indicate better model performance.

2. Mean Absolute Error (MAE): MAE measures the average absolute difference between predicted and actual earnings values. Unlike RMSE, MAE is less sensitive to large outliers, making it useful for understanding the typical prediction error across institutions. Lower MAE values indicate more accurate predictions.

3. R2 : R2 measures the proportion of variation in post-graduation earnings that is explained by the predictors in the model. This metric helps evaluate how well variables such as tuition, graduation rate, admission selectivity, and student demographics explain differences in earnings outcomes across colleges. Higher R2 values indicate stronger explanatory power.

The project will compare linear regression, ridge regression, and lasso regression models using these evaluation metrics. Linear regression will serve as a baseline model, while ridge and lasso regression will help address multicollinearity and reduce overfitting in the large set of predictors.

## 7. Expected Challenges

One challenge we expect is missing data. The College Scorecard dataset has many values that are missing or privacy-suppressed, especially for earnings, debt, repayment, and smaller schools or programs. Some missing values may appear as NA, NULL, PS, or PrivacySuppressed, so we will need to clean these before building our models. This could also affect which target variable we choose, since we need enough complete data to train and evaluate the models.

Class imbalance could be a challenge if we decide to turn a numeric outcome into categories, such as high vs. low earnings or high vs. low default risk. Most schools may fall into the middle range, while extreme outcomes may be much less common. If we keep the project as a regression task, class imbalance will be less of an issue, but we may still need to watch for skewed target values and outliers.

Overfitting is another concern because the dataset has thousands of possible features but only several thousand schools per year. Many variables may also be closely related to each other, such as tuition, net price, debt, and financial aid measures. To reduce overfitting, we plan to select a smaller set of meaningful features and use regularized models like Ridge or Lasso regression.
There may also be computational limitations because the full raw dataset is large and includes many yearly and field-of-study files. Instead of loading everything at once, we plan to focus on the most recent institution-level file and only keep the columns that are useful for our project. This should make the dataset easier to work with and keep the project realistic for our timeline.

Finally, there may be dataset quality issues. Some features are not available for every year, some outcomes use different measurement windows, and privacy suppression may make the data less complete for smaller institutions. We will also need to be careful about target leakage, meaning we should avoid using variables that directly reveal or are measured after the outcome we are trying to predict.


## 8. Team Responsibilities

Julia will mainly work on the data side of the project. She will help download and understand the College Scorecard dataset, choose the most useful features, clean missing values, prepare the data for modeling, and create visualizations that explain the dataset.

Rhea will mainly work on the modeling side of the project. She will build and test the regression models, compare models like Linear Regression, Ridge Regression, and Lasso Regression, tune the models when needed, and create tables or graphs showing how well each model performs.

Both team members will work together on the final report, presentation, and GitHub submission. They will help interpret the results, explain the main challenges, discuss what the models did well or poorly, and make sure the code and final materials are organized and easy to follow.
