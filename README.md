# Predicting Post-Graduation Earnings from College Characteristics

**DATA 402/403 Final Project**

Julia Lu, Rhea Chellani

---

## Overview

Our project uses the U.S. Department of Education College Scorecard data to predict median earnings 10 years after enrollment based on college characteristics like tuition, admission rate, and graduation rate. We compared three regression models: Linear Regression, Ridge, and Lasso.

---

## Getting the Data

The dataset is too large to include in this repository (~2.5 GB). You will have to download it directly from the U.S. Department of Education:

1. Go to: https://collegescorecard.ed.gov/data/
2. Under **"Download the Data"**, download the most recent **"College Scorecard Data"** zip file
3. Unzip it and rename the folder to:
   ```
   College_Scorecard_Raw_Data_03232026/
   ```
4. Place the folder in the same directory as `mvp_notebook.ipynb`
5. Make sure the file `Most-Recent-Cohorts-Institution.csv` is inside that folder

The directory should look like this in order to match our setup:
```
Final Project/
├── mvp_notebook.ipynb
├── mvp_report.md
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

# Launch the notebook
jupyter notebook mvp_notebook.ipynb
```

Once open, go to **Kernel → Restart & Run All**. All output figures should be saved as `.png` files in the same directory.

---

## Files

- `mvp_notebook.ipynb`: main Jupyter notebook with all the code
- `mvp_report.md`: written MVP report
- `requirements.txt`: Python package dependencies
- `DATA_402_Proposal.md`: original project proposal
- `figures/`: all output plots saved here when you run the notebook
