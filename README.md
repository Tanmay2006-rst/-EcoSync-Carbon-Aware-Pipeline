# Real-Time Carbon-Aware Compute Optimization for Modern Data Infrastructure

**Author:** Rachamadagu Sai Tanmay  
**Program:** IBM SkillsBuild Data Analytics with AI — Academic Internship (AICTE)  
**Project:** Carbon-Aware Compute Scheduling using AI & Great Britain Grid Data

---

## Project Overview

This project builds an end-to-end AI pipeline that reads historical power grid generation data from Great Britain, calculates live grid carbon intensity (gCO₂/kWh), and trains a Random Forest Regressor to predict clean-energy windows. When intensity drops below the 200 gCO₂/kWh threshold, the system schedules heavy back-end compute jobs — reducing operational carbon emissions in data centres.

---

## Repository Structure

```
IBM_project/
├── RachamadaguSaiTanmay_CarbonAwareDataCompute.ipynb   ← Main Jupyter Notebook (run this first)
├── RachamadaguSaiTanmay_ProjectReport.docx             ← Project report with embedded chart
├── requirements.txt                                     ← Python dependencies
├── README.md                                            ← This file
├── analysis.py                                          ← Standalone Python script (same logic)
├── Dataset.csv                                          ← Raw Great Britain grid dataset
├── cleaned_dataset.csv                                  ← Auto-generated cleaned data
└── carbon_intensity_trend.png                           ← Auto-generated chart (insert in report)
```

---

## Prerequisites

- Python 3.9 or higher
- pip (comes bundled with Python)
- Jupyter Notebook or VS Code with the Jupyter extension

Install all required libraries in one command:

```bash
pip install -r requirements.txt
```

This installs:

| Package | Version | Purpose |
|---------|---------|---------|
| pandas | >=2.0.0 | Data loading and cleaning |
| numpy | >=1.24.0 | Numerical computation |
| matplotlib | >=3.7.0 | Chart generation |
| seaborn | >=0.12.0 | Statistical data visualisation |
| scikit-learn | >=1.2.0 | Random Forest ML model |

---

## Execution Guide

Follow these steps in order:

### Step 1 — Install dependencies

```bash
pip install -r requirements.txt
```

### Step 2 — Open the Jupyter Notebook

In VS Code, open `RachamadaguSaiTanmay_CarbonAwareDataCompute.ipynb`.  
Alternatively, launch from terminal:

```bash
jupyter notebook RachamadaguSaiTanmay_CarbonAwareDataCompute.ipynb
```

### Step 3 — Run all cells in order

Click **Run All** (or press `Shift + Enter` cell by cell):

| Cell | Action | Expected Output |
|------|--------|-----------------|
| Cell 1 | Load dataset | Shape printout + first 5 rows |
| Cell 2 | Clean data & engineer features | Missing value counts, feature confirmation |
| Cell 3 | Train Random Forest model | R² Score, RMSE, MAE printed |
| Cell 4 | Run optimization framework | Hour-by-hour GREEN / RED routing log |
| Cell 5 | Generate chart | `carbon_intensity_trend.png` saved + displayed |

### Step 4 — Review output logs

After **Cell 3**, look for:
```
R2  Score (Accuracy)       : XX.XX %
RMSE (Root Mean Sq. Error) : XX.XXXX gCO2/kWh
MAE  (Mean Absolute Error) : XX.XXXX gCO2/kWh
```

After **Cell 4**, look for the hour-by-hour routing table and the **EMISSION SAVINGS REPORT** block showing the optimal green window and estimated CO₂ saved.

### Step 5 — Insert chart into report

The file `carbon_intensity_trend.png` is auto-generated in your project folder after Cell 5 runs. It is already embedded in `RachamadaguSaiTanmay_ProjectReport.docx` under Section 4.

---

## How It Works

```
Raw CSV (Dataset.csv)
        │
        ▼
  Data Cleaning         ← dropna(), fillna(0), clip(lower=0)
        │
        ▼
Feature Engineering     ← carbon_intensity = (Coal×900 + Gas×400) / Total_MW
        │                  hour, day_of_week, month extracted
        ▼
  80/20 Train Split
        │
        ▼
RandomForestRegressor   ← 50 estimators, random_state=42
        │
        ▼
  Predict Intensity     ← for each hour of the day
        │
        ▼
  Threshold Check       ← < 200 gCO₂/kWh  →  GREEN SIGNAL → run jobs
                           >= 200 gCO₂/kWh →  RED SIGNAL   → defer jobs
```

---

## Key Results

- The model predicts hourly carbon intensity with measurable accuracy (see Cell 3 output).
- Early morning hours (00:00–04:00) and mid-day (10:00–14:00) consistently show lower intensity.
- By routing 1,000,000 compute rows to green windows, the pipeline demonstrates significant CO₂ emission savings versus running at peak hours (18:00–21:00).
- Estimated 25–40% reduction in operational carbon emissions achievable by shifting workloads to afternoon green windows.

---

## License

This project was created as part of the **AICTE–IBM SkillsBuild Academic Internship Program**.  
For educational and non-commercial use only.
