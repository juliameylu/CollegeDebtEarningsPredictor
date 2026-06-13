# Predicting Post-Graduation Earnings from College Characteristics

**DATA 402/403 Final Project**

Julia Lu, Rhea Chellani

---

## Overview

Our project uses the U.S. Department of Education College Scorecard data to predict median earnings 10 years after enrollment based on college characteristics like tuition, admission rate, and graduation rate. We compare nine models across three families: linear regression (OLS, Ridge, Lasso), support vector regression (linear and RBF kernel), and a multilayer perceptron neural network. We also explore the effect of log-transforming the target variable on model performance.

---

## Getting the Data

The dataset is too large to include in this repository (~2.5 GB). You will have to download it directly from the U.S. Department of Education:

1. Go to: https://collegescorecard.ed.gov/data/
2. Under **"Download the Data"**, download the most recent **"College Scorecard Data"** zip file
3. Unzip it and rename the folder to:
   ```
   College_Scorecard_Raw_Data_03232026/
   ```
4. Place the folder in the same directory as `final_notebook.ipynb`
5. Make sure the file `Most-Recent-Cohorts-Institution.csv` is inside that folder

The directory should look like this in order to match our setup:
```
Final Project/
├── final_notebook.ipynb
├── mvp_notebook.ipynb
├── requirements.txt
├── README.md
└── College_Scorecard_Raw_Data_03232026/
    └── Most-Recent-Cohorts-Institution.csv
```

---

## Setup & Running

```bash
# Install dependencies
pip install -r requirements.txt

# Launch the final notebook
jupyter notebook final_notebook.ipynb
```

Once open, go to **Kernel → Restart & Run All**. All output figures will be saved as `.png` files in the `figures/` directory. Note: the SVR and MLP cross-validation steps may take a few minutes to run.

---

## Files

- `final_notebook.ipynb`: main Jupyter notebook with all the code (OLS/Ridge/Lasso, log-transform, SVR, MLP, learning curves)
- `mvp_notebook.ipynb`: original MVP notebook (OLS/Ridge/Lasso baseline)
- `requirements.txt`: Python package dependencies
- `figures/`: all output plots saved here when you run the notebook
  - `fig_target_distribution.png`: earnings distribution histogram
  - `fig_correlation_heatmap.png`: feature correlation heatmap
  - `fig_scatter_features_vs_target.png`: scatter plots of key features vs earnings
  - `fig_earnings_by_school_type.png`: earnings breakdown by school type
  - `fig_baseline_comparison.png`: train vs test RMSE for OLS, Ridge, Lasso
  - `fig_baseline_predicted_vs_actual.png`: OLS predicted vs actual
  - `fig_baseline_residuals.png`: OLS residual plot
  - `fig_log_model_diagnostics.png`: log-transform model diagnostics
  - `fig_svr_predicted_vs_actual.png`: LinearSVR and SVR-RBF predicted vs actual
  - `fig_mlp_diagnostics.png`: MLP predicted vs actual and residuals
  - `fig_all_models_comparison.png`: test RMSE bar chart for all 9 models
  - `fig_learning_curve.png`: bias-variance learning curve
  - `fig_residuals_vs_predicted.png`: residuals vs predicted for best model
  - `fig_rmse_by_school_type.png`: RMSE breakdown by school type
  - `fig_coefficients_comparison.png`: OLS/Ridge/Lasso coefficient comparison
