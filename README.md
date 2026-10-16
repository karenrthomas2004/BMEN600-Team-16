# BMEN600-Team-16
## Group 16
## Abbey Currie, Danyang Chen, Kurt Yang, Karen Thomas
## Research Question

To what extent does chronic disease burden improve prediction of cognitive performance among adults aged 65 and older beyond demographic characteristics, smoking status, and BMI?

We compare models with and without a seven-condition disease count using linear regression, Random Forest, XGBoost, and CatBoost. The outcome is the official 0–27 cognition score.

## Dataset Access

Register through the University of Michigan’s HRS portal and download the Stata versions of:

1. [RAND HRS Longitudinal File 2022, Version 1](https://hrsdata.isr.umich.edu/node/38308): `randhrs1992_2022v1.dta`
2. [HRS Cross-Wave Imputation of Cognitive Functioning Measures 1992–2022, Final Version 2.0](https://hrsdata.isr.umich.edu/data-products/cross-wave-imputation-cognitive-functioning-measures-1992-2022): `cogimp9222a_r.dta`

Keep participant-level data in an authorized local location outside the repository. Follow the [HRS conditions of use](https://hrsdata.isr.umich.edu/data-products/conditions-of-use). Data exports currently listed under `Data/` require a sharing-permissions review; their presence does not authorize redistribution.

## File Map

| File or folder | Purpose |
|---|---|
| `Data Preparation/Extract Data Notebook.ipynb` | Extracts and links variables from the source datasets. |
| `Data Preparation/Data Cleaning Notebook.ipynb` | Cleans records, selects the latest eligible interview per participant, and generates demographic summaries. |
| `Machine Learning/linear regression.ipynb` | Runs the linear regression progress check. |
| `Machine Learning/Random Forest.ipynb` | Runs Random Forest models. |
| `Machine Learning/XGBoost.ipynb` | Runs baseline and tuned XGBoost models. |
| `Machine Learning/CatBoost.ipynb` | Runs baseline and tuned CatBoost models. |
| `Exploratory Analysis/` | Aggregate demographic tables and figure. |
| `Midterm Results/` | Model performance comparison, data summary, and diagnostic figures. |
| `Project Milestones.docx` | Project timeline and responsibilities. |
| `Data/` | Data exports; see the access notice above. |

## Run the Current Progress Check

**Software:** Python, Jupyter, pandas, NumPy, Matplotlib, scikit-learn, XGBoost and CatBoost.

```bash
python -m pip install jupyter pandas numpy matplotlib "scikit-learn>=1.2" xgboost catboost
jupyter notebook
```

1. Download the notebooks and obtain the source datasets through your authorized HRS account.
2. Open `Data Preparation/Extract Data Notebook.ipynb`. Update `folder`, `rand_file`, and `cog_file` to your local paths. Restart the kernel and run all cells to generate `hrs_full_data.csv`.
3. Open `Data Preparation/Data Cleaning Notebook.ipynb`. Update its input, RAND source, and output paths. Restart the kernel and run all cells to generate `cleaned_latest_data.csv` and demographic summaries.
4. Open `Machine Learning/linear regression.ipynb`. Point `input_file` to the generated `cleaned_latest_data.csv`, then restart the kernel and run all cells.
5. Review the displayed sample counts, MAE, RMSE, R², and diagnostic plots. Compare them with `Midterm Results/Model Performance Comparison.pdf`.

The documented sample contains **13,053 participants**, split into **9,137 training** and **3,916 test** participants using `random_state=3`. Reported linear regression benchmarks are:

| Predictor set | MAE | RMSE | R² |
|---|---:|---:|---:|
| Model 1: baseline predictors | 3.3485 | 4.2256 | 0.2818 |
| Model 2: baseline plus disease burden | 3.3383 | 4.2133 | 0.2860 |

Run the other modelling notebooks independently using the same cleaned file and row order. Each creates its own split. Generated filenames differ from some uploaded filenames, so check all paths before running.

**Current limitations:** Paths require local adjustment, package versions are not pinned, and the current split does not enforce household grouping. Clear participant-level notebook outputs before sharing.
