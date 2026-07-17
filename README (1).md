# SpaceX Falcon 9 First-Stage Landing Prediction
### IBM Applied Data Science Capstone

> **Author:** Nandhakishore A &nbsp;•&nbsp; **Program:** IBM Applied Data Science Capstone &nbsp;•&nbsp; **Date:** 17-07-2026
> **Repository:** https://github.com/Nandhakishore-A/DATA_SCIENCE_CAPSTONE_PROJECT

---

## 1. Project Overview

SpaceX advertises Falcon 9 rocket launches at a fraction of the cost of competing providers, largely because SpaceX can reuse the rocket's first-stage booster instead of building a new one for every flight. If a booster's first stage does not land successfully, that saving disappears.

This project builds a complete, reproducible data-science pipeline to predict whether a Falcon 9 first-stage booster will land successfully, using historical launch data. The pipeline covers every stage required by the IBM Applied Data Science Capstone:

1. **Data Collection** via the public SpaceX REST API
2. **Data Collection** via web scraping (BeautifulSoup, Wikipedia launch records)
3. **Data Wrangling** — cleaning, missing-value handling, and outcome-label engineering
4. **Exploratory Data Analysis (SQL)** — 10 business questions answered against an IBM Db2 table
5. **Exploratory Data Analysis (Python)** — seaborn/matplotlib visualizations
6. **Interactive Visual Analytics** — Folium map of launch sites, landing outcomes, and proximities
7. **Interactive Dashboard** — Plotly Dash app for exploring launch records
8. **Machine Learning** — Logistic Regression, SVM, Decision Tree, and KNN classifiers tuned with `GridSearchCV`

**Best model:** a Decision Tree Classifier achieved **87.5% cross-validated accuracy** and **94.4% accuracy on the held-out test set** — the highest test-set accuracy of the four models compared.

This README, the accompanying `SpaceX_Capstone_Presentation.pptx`, and a rubric cross-check were generated directly from the contents of the project ZIP file — no notebooks, code, screenshots, or results were invented. Where required evidence (e.g. screenshots, a GitHub URL, some CSV data files) was **not found** in the ZIP, it is flagged below and in the presentation as a placeholder for you to supply.

---

## 2. Folder Structure

This is the structure of the files found in the uploaded ZIP archive:

```
Applied-Data-Science-Capstone-Project-main/
├── Data Collection API.ipynb                          # SpaceX REST API data collection
├── Data Collection with Web Scraping.ipynb             # BeautifulSoup scraping of Wikipedia launch tables
├── Data Wrangling lab week 1.ipynb                      # Cleaning, missing values, Class label engineering
├── Exploratory Data Analysis.ipynb                      # SQL EDA against an IBM Db2 table (Spacextbl)
├── EDA with Data Visualization.ipynb                    # seaborn/matplotlib visual EDA + feature engineering
├── interactive_visual_analytics_with_folium_final.ipynb # Folium map: launch sites, outcomes, distances
├── SpaceX_Machine Learning Prediction_Part_5.ipynb       # Model training, tuning, and evaluation
├── spacex_dash_app.py                                   # Plotly Dash interactive dashboard
├── ds-capstone-template-coursera.pdf                     # Original Coursera assignment/report template
└── README.md                                             # (original — minimal; this file replaces it)
```

> **Note:** No raw or processed dataset files (`.csv`) were found in the ZIP — including `spacex_launch_dash.csv`, which `spacex_dash_app.py` requires to run. Add your dataset CSVs to a `data/` folder and update the load paths before running the notebooks/app.

Recommended structure once you fill in the gaps:

```
├── notebooks/            # the 7 .ipynb files above
├── dashboard/
│   ├── spacex_dash_app.py
│   └── spacex_launch_dash.csv        # ⚠ currently missing — see Section 6
├── images/
│   ├── folium_map_screenshot.png     # ⚠ currently missing — see Section 6
│   └── dashboard_screenshot.png      # ⚠ currently missing — see Section 6
├── presentation/
│   └── SpaceX_Capstone_Presentation.pptx
├── README.md
└── ds-capstone-template-coursera.pdf
```

---

## 3. Technologies Used

Identified directly from the `import` statements and `%sql`/`pip install` cells across the notebooks and `spacex_dash_app.py`:

| Category | Libraries / Tools |
|---|---|
| Data collection | `requests`, SpaceX REST API (`api.spacexdata.com/v4`), `BeautifulSoup` (`bs4`) |
| Data handling | `pandas`, `numpy` |
| Database / SQL | `ibm_db_sa`, `sqlalchemy`, `ipython-sql` (`%sql` magic), IBM Db2 on IBM Cloud |
| Visualization | `matplotlib`, `seaborn`, `plotly.express` |
| Geospatial | `folium` (`folium.plugins.MarkerCluster`, `MousePosition`) |
| Dashboard | `dash`, `dash_html_components`, `dash_core_components` |
| Machine learning | `scikit-learn` — `train_test_split`, `StandardScaler`, `LogisticRegression`, `SVC`, `DecisionTreeClassifier`, `KNeighborsClassifier`, `GridSearchCV`, `confusion_matrix` |

---

## 4. Installation

```bash
# Clone your repository
git clone https://github.com/Nandhakishore-A/DATA_SCIENCE_CAPSTONE_PROJECT.git
cd DATA_SCIENCE_CAPSTONE_PROJECT

# Create and activate a virtual environment (recommended)
python -m venv venv
source venv/bin/activate                  # Windows: venv\Scripts\activate

# Install dependencies
pip install pandas numpy requests beautifulsoup4 \
            sqlalchemy==1.3.9 ibm_db_sa ipython-sql \
            matplotlib seaborn plotly \
            folium \
            dash dash-html-components dash-core-components \
            scikit-learn jupyter
```

> The SQL notebook (`Exploratory Data Analysis.ipynb`) connects to a specific IBM Db2 instance using a hard-coded connection string with credentials. **Rotate/replace those credentials** and point the `%sql` connection at your own Db2 (or other) database before re-running that notebook.

---

## 5. Usage

Run the notebooks in this order to reproduce the full pipeline:

1. **`Data Collection API.ipynb`** — pulls past Falcon 9 launches from the SpaceX API and builds the initial dataset.
2. **`Data Collection with Web Scraping.ipynb`** — scrapes Falcon 9/Heavy launch tables from Wikipedia as a secondary source.
3. **`Data Wrangling lab week 1.ipynb`** — cleans the collected data and engineers the binary `Class` (landing outcome) label.
4. **`Exploratory Data Analysis.ipynb`** — loads the wrangled data into a SQL table and answers 10 business questions.
5. **`EDA with Data Visualization.ipynb`** — produces the visual EDA plots (scatter, bar, line) and encodes features for modeling.
6. **`interactive_visual_analytics_with_folium_final.ipynb`** — builds the interactive Folium map of launch sites and proximities.
7. Run the dashboard:
   ```bash
   python spacex_dash_app.py
   ```
   then open the local URL Dash prints (typically `http://127.0.0.1:8050`). Requires `spacex_launch_dash.csv` in the same folder (⚠ not included — see Section 6).
8. **`SpaceX_Machine Learning Prediction_Part_5.ipynb`** — trains and tunes Logistic Regression, SVM, Decision Tree, and KNN classifiers, and compares their accuracy.

---

## 6. Known Gaps in This ZIP (please supply before final submission)

The following items were requested in the project rubric but were **not found** in the uploaded ZIP. Nothing was invented to fill these gaps — they're flagged here and as placeholders in the presentation:

- ❌ **`spacex_launch_dash.csv`** — required by `spacex_dash_app.py` but not included.
- ❌ **Raw/processed dataset CSVs** more generally — no `.csv` files exist in the ZIP.
- ❌ **Screenshot of the rendered Folium map** — the map is built as interactive HTML/JS inside the notebook; no static image output was found.
- ❌ **Screenshot of the running Dash dashboard** — no image of the app was found.
- ❌ **Pie chart in static EDA** — the only pie chart in the project is the *interactive* one inside `spacex_dash_app.py`; no static pie chart exists in the EDA notebooks.
- ❌ **Correlation plot / heatmap** in EDA — not present in any notebook.
- ❌ **`classification_report()` / ROC curve** for the ML models — only confusion matrices (`sns.heatmap` of `confusion_matrix`) were generated.
- ⚠ **Original `README.md`** contained only a single title line; it has been replaced by this file.

---

## 7. Results

| Model | Cross-Validated Accuracy (`best_score_`) | Test-Set Accuracy |
|---|---|---|
| **Decision Tree** | **0.8750** | **0.9444** |
| KNN | 0.8482 | 0.8333 |
| SVM | 0.8482 | 0.8333 |
| Logistic Regression | 0.8464 | 0.8333 |

- **Best model:** Decision Tree Classifier — `criterion='gini', max_depth=4, max_features='sqrt', min_samples_leaf=2, min_samples_split=10, splitter='best'`.
- **Dataset:** 90 Falcon 9 launches; overall historical landing success rate (`Class` mean) = **66.7%**.
- **Launch sites:** CCAFS SLC 40 (55 launches), KSC LC 39A (22), VAFB SLC 4E (13).
- **SQL EDA highlights:** total NASA (CRS) payload mass = 45,596 kg; first successful ground-pad landing = 2015-12-22; maximum payload mass = 15,600 kg (carried by 12 F9 B5 boosters); 100 successful vs. 1 failed overall mission outcome.
- **Visual EDA highlights:** landing success rate rose from 0% (2010/2013) to ~83–90% (2019–2020); ES-L1, GEO, HEO, and SSO orbits show a 100% observed success rate, while GTO is lowest at ~52%.

Full details, all 10 SQL query results, and every supporting chart are in `SpaceX_Capstone_Presentation.pptx`.

---

## 8. Conclusion

This project demonstrates a complete, end-to-end applied data science workflow — from raw API/web data through SQL and visual exploratory analysis, geospatial mapping, an interactive dashboard, and finally a tuned machine-learning classifier. The resulting Decision Tree model predicts Falcon 9 first-stage landing outcomes with 94.4% accuracy on unseen data, providing a concrete, data-driven estimate of launch cost risk tied to booster reusability.

**Suggested next steps:** add classification-report/ROC-AUC evaluation, capture the missing Folium/Dash screenshots, include the missing dataset CSVs, and evaluate ensemble methods (e.g. Random Forest, XGBoost) not present in the current notebooks.

---

## 9. Acknowledgements

Notebook templates and lab instructions originate from the **IBM Applied Data Science Capstone** on Coursera (see `ds-capstone-template-coursera.pdf` in this repository). © IBM Corporation, as noted in the original notebook headers.
