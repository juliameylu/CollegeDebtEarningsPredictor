# MVP Report: Predicting Post-Graduation Earnings from College Characteristics

Julia Lu, Rhea Chellani
DATA 402/403 Final Project
June 2026

---

## 1. Introduction

When students pick a college they're also making a long-term financial decision, but it's hard to know upfront how that choice will affect their earnings years later. We wanted to see if we could predict median earnings 10 years after enrollment just from publicly available information about the school itself.

We used the U.S. Department of Education's College Scorecard dataset and built a regression pipeline using three models we learned in class: linear regression, ridge, and lasso. This is our MVP submission, which means we have a working pipeline with baseline results and a plan for what comes next.

---

## 2. Dataset and Preprocessing

We used Most-Recent-Cohorts-Institution.csv from the College Scorecard, which has one row per institution with the most recent data available for each school. The dataset starts at 6,322 institutions across 3,308 columns. After dropping rows where our target variable was missing, we ended up with 5,173 schools.

The target variable is MD_EARN_WNE_P10, which is the median earnings of students who are working and not enrolled 10 years after first entering the school.

For features we picked 10 columns that seemed most related to earnings outcomes:

- ADM_RATE: admission rate (selectivity)
- SAT_AVG: average SAT of incoming students
- TUITIONFEE_IN and TUITIONFEE_OUT: in-state and out-of-state tuition
- UGDS: total undergrad enrollment
- C150_4: 4-year graduation rate
- PCTPELL: percent of students on Pell grants (low income indicator)
- PCTFLOAN: percent of students with federal loans
- CONTROL: school type (1=public, 2=private nonprofit, 3=for-profit)
- LOCALE: urban vs. rural classification

One of the bigger challenges was missing data. The Scorecard suppresses values when a student group is too small for privacy reasons, so a lot of columns have high missing rates. SAT_AVG was missing for 83.6% of schools and ADM_RATE for 69.5%. For the target variable we just dropped any school missing earnings data. For features we filled in missing values with the column median, which is a simple approach but it does mean those features are less useful for schools that didn't report.

We split 80/20 into train and test sets (4,138 training, 1,035 test) with random_state=42. We also standardized all features using StandardScaler fit only on the training set. This is important for ridge and lasso since they apply a penalty based on coefficient size, and if features are on different scales the penalty would be unfair.

---

## 2. Baseline Models

We trained three models, all covered in DATA 402:

Linear regression (OLS): no regularization, just minimizes squared error directly. This is our simplest baseline.

Ridge regression: adds an L2 penalty that shrinks all coefficients toward zero but never zeros them out. We used RidgeCV with 5-fold cross validation over 100 alpha values to find the best regularization strength. Best alpha: 27.83.

Lasso regression: adds an L1 penalty that can actually zero out coefficients completely, which does automatic feature selection. Same CV approach. Best alpha: 4.33.

---

## 3. Evaluation

Results on the test set:

- Linear OLS: train RMSE $12,139 / test RMSE $11,500 / MAE $8,209 / R2 0.47
- Ridge (alpha=27.83): train RMSE $12,140 / test RMSE $11,496 / MAE $8,200 / R2 0.47
- Lasso (alpha=4.33): train RMSE $12,139 / test RMSE $11,499 / MAE $8,207 / R2 0.47

All three models came out basically identical. Ridge is technically the best but by almost nothing. This tells us the features we chose probably aren't highly correlated with each other, so the regularization in ridge and lasso didn't have much to fix. Lasso also didn't zero out any features, meaning all 10 contributed at least something.

An R2 of 0.47 means we explain about 47% of the variation in earnings across schools. That's a reasonable starting point for this kind of prediction since earnings are also shaped by things we can't capture at the institution level, like what someone majors in or what job market they graduate into. The test RMSE of about $11,500 on a dataset where median earnings are around $40,750 is meaningful but not surprising given how limited our features are.

The largest coefficients (from ridge) were CONTROL (school type), PCTFLOAN (loan %), and PCTPELL (Pell grant %). For-profit schools predict lower earnings, which makes sense. The PCTFLOAN coefficient is positive, which seems counterintuitive but probably reflects a selection effect where students at more expensive, higher-quality schools take on more debt but also end up earning more.

Figures we generated: fig_target_distribution.png, fig_correlation_heatmap.png, fig_scatter_features_vs_target.png, fig_earnings_by_school_type.png, fig_model_comparison.png, fig_predicted_vs_actual.png, fig_residuals.png, fig_lasso_coefficients.png, fig_residuals_vs_predicted.png, fig_rmse_by_school_type.png

---

## 4. Error Analysis

59 schools had residuals bigger than $22,992 (2x the test RMSE), which is about 6% of the test set. Almost all of them are specialized health sciences schools:

- LA County College of Nursing: actual $115,318, predicted $51,095, off by $64,223
- West Coast University Texas: actual $102,672, predicted $38,790, off by $63,882
- Chamberlain University Indiana: actual $92,405, predicted $37,586, off by $54,819
- Oregon Health and Science University: actual $101,028, predicted $57,709, off by $43,319
- American Musical and Dramatic Academy: actual $26,975, predicted $69,173, off by -$42,198

Nursing and medical programs produce graduates who go straight into high-paying clinical careers, but nothing in our features captures what programs a school specializes in. The American Musical and Dramatic Academy is the opposite problem where our model sees a high tuition urban school and predicts high earnings, but arts conservatory graduates actually earn much less.

Breaking down RMSE by school type, public schools had the lowest error at $9,664, for-profit was $12,298, and private nonprofit was highest at $12,797. Public schools are more uniform so they're easier to predict consistently.

Train and test RMSE are almost identical across all three models (within about $650), which means we're not overfitting. The bigger problem is underfitting. An R2 of 0.47 means there's a lot of variance our 10 features can't explain. Some limitations:

- SAT_AVG and ADM_RATE had such high missing rates that most schools got the median imputed, so they end up being weak predictors
- We have no information about what programs a school offers, which is probably a major driver of earnings
- The residuals get larger at higher predicted earnings, which suggests log-transforming the target would help
- The schools we dropped for missing earnings data tend to be smaller and more specialized, so our model is probably better tuned to larger general-purpose institutions than it is to niche schools

---

## 5. Progress Toward Final Project

What we have working right now: a full end-to-end pipeline from raw data through preprocessing, model training, evaluation, and visualization. All three baseline models run with cross-validated hyperparameter tuning and we have a solid error analysis with per-school residuals and breakdowns by school type.

For the final project we're planning to:

- log-transform the target to address the heteroscedasticity in the residuals
- join with the field-of-study dataset to add program mix features (what % of students are in STEM, health, etc.)
- try SVM regression and MLP neural network, both from DATA 402
- also try predicting median debt (GRAD_DEBT_MDN) as a second target variable
- add state or region indicators to pick up on regional job market effects
- experiment with interaction terms between tuition and graduation rate

---

## How to Run

```
pip install -r requirements.txt
jupyter notebook mvp_notebook.ipynb
```

Run all cells with Kernel > Restart and Run All. Figures save to the figures/ folder automatically.

Data file needed: College_Scorecard_Raw_Data_03232026/Most-Recent-Cohorts-Institution.csv

---

## References

U.S. Department of Education. College Scorecard Data. https://collegescorecard.ed.gov/data/

Tibshirani, R. (1996). Regression Shrinkage and Selection via the Lasso. Journal of the Royal Statistical Society, 58(1), 267-288.

Hoerl, A. E. and Kennard, R. W. (1970). Ridge Regression: Biased Estimation for Nonorthogonal Problems. Technometrics, 12(1), 55-67.

Breiman, L. (2001). Statistical Modeling: The Two Cultures. Statistical Science, 16(3), 199-231.
