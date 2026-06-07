# Predicting Post-Graduation Earnings from College Characteristics

**DATA 402/403 Final Project — Cal Poly SLO**
**Team:** Julia Lu, Rhea Chellani

---

## Overview

This project uses U.S. Department of Education College Scorecard data to predict median earnings 10 years after enrollment based on college characteristics like tuition, admission rate, and graduation rate. We compare three regression models: Linear Regression, Ridge, and Lasso.

---

## Getting the Data

The dataset is too large to include in this repository (~2.5 GB). Download it directly from the U.S. Department of Education:

1. Go to: https://collegescorecard.ed.gov/data/
2. Under **"Download the Data"**, download the most recent **"College Scorecard Data"** zip file
3. Unzip it and rename the folder to:
   ```
   College_Scorecard_Raw_Data_03232026/
   ```
4. Place the folder in the same directory as `mvp_notebook.ipynb`
5. Make sure the file `Most-Recent-Cohorts-Institution.csv` is inside that folder

Your directory should look like this:
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

Once open, go to **Kernel → Restart & Run All**. All output figures will be saved as `.png` files in the same directory.

---

## Files

| File | Description |
|---|---|
| `mvp_notebook.ipynb` | Main Jupyter notebook — all code |
| `mvp_report.md` | Written MVP report |
| `requirements.txt` | Python package dependencies |
| `DATA_402_Proposal.md` | Original project proposal |
