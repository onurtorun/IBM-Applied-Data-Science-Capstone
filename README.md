# IBM Applied Data Science Capstone: SpaceX Falcon 9 First Stage Landing Prediction

**Author:** Mustafa Onur Torun  
**GitHub Profile:** [@onurtorun](https://github.com/onurtorun)

---

## Executive Summary
This repository contains the complete end-to-end data science capstone project for the **IBM Data Science Professional Certificate**. The primary objective is to predict whether the SpaceX Falcon 9 first stage booster will land successfully, allowing commercial competitors to assess launch costs ($62M vs. up to $165M+ for non-reusable options).

---

## Project Methodology & Architecture

1. **Module 1: Data Collection & Wrangling**
   - Extracted historical launch records via the SpaceX REST API.
   - Filtered dataset specifically for Falcon 9 launches and wrangled missing landing pad/payload metrics into a structured binary target (`Class = 1` for successful recovery, `Class = 0` for landing failure).

2. **Module 2: Exploratory Data Analysis (EDA)**
   - **SQL Analytics:** Queried unique launch sites, total payloads, booster versions carrying maximum payload, failure outcomes by date, and landing success distributions using SQLite.
   - **Data Visualization:** Built exploratory scatter, bar, and trend visualizations to analyze relationships between payload mass, launch sites, flight numbers, orbit types, and year-over-year recovery progression.

3. **Module 3: Interactive Visual Analytics**
   - **Folium:** Constructed interactive geographic maps plotting launch complexes (CCAFS, KSC, VAFB), proximity markers (coastlines, railways, highways), and outcome clusters.
   - **Plotly Dash:** Developed an interactive web dashboard allowing dynamic filtering of launch sites and payload mass ranges with automated pie and scatter updates.

4. **Module 4: Machine Learning Classification**
   - Standardized one-hot encoded feature matrices using `StandardScaler`.
   - Trained, cross-validated (10-fold CV), and fine-tuned four classification algorithms using `GridSearchCV`:
     - Logistic Regression
     - Support Vector Machine (SVM)
     - Decision Tree Classifier
     - K-Nearest Neighbors (KNN)

---

## Machine Learning Results & Model Evaluation

All models were evaluated on an unseen test dataset (20% split, 18 samples). The hyperparameter optimization and test accuracy results:

| Model | Best Validation Score (CV) | Test Accuracy | Optimal Hyperparameters |
| :--- | :---: | :---: | :--- |
| **Logistic Regression** | ~0.846 | **83.33%** | `C=0.01`, `penalty='l2'`, `solver='lbfgs'` |
| **Support Vector Machine** | ~0.848 | **83.33%** | `C=1.0`, `gamma=0.0316`, `kernel='sigmoid'` |
| **Decision Tree** | ~0.859 | **83.33%** | `criterion='entropy'`, `max_depth=14`, `max_features='sqrt'`, `min_samples_leaf=2`, `splitter='random'` |
| **K-Nearest Neighbors** | ~0.848 | **83.33%** | `algorithm='auto'`, `n_neighbors=10`, `p=1` |

### Key Insights
- **Predictive Accuracy:** All four fine-tuned models achieved a test accuracy of **83.33%** (misclassifying only 3 out of 18 test records).
- **Yearly Success Progression:** Booster recovery rates demonstrated a steep upward trajectory after 2013, surpassing an 80% success rate by 2020 due to iterated landing protocols.
- **Payload & Orbit Sensitivity:** Payloads deployed to lower-altitude orbits (LEO, ISS) exhibited higher recovery consistency compared to high-energy geostationary transfer orbits (GTO).
- **Geographic Proximity:** Launch sites closer to coastal boundaries (notably CCAFS LC-40 and KSC LC-39A) accommodated the highest mission frequency and operational drone ship recovery logistics.

---

## Repository Structure

```text
.
├── README.md
├── SpaceX_Capstone_Presentation.pdf
│
├── 1-1_Complete_the_Data_Collection_API_Lab/
│   ├── jupyter-labs-spacex-data-collection-api.ipynb
│   ├── Task 2 Filter the dataframe to only include Falcon 9 launches.png
│   └── Task 3 Data Wrangling.png
│
├── 2-1_Exploratory_Data_Analysis_with_SQL/
│   ├── jupyter-labs-eda-sql-coursera_sqllite.ipynb
│   ├── my_data1.db
│   ├── Task 1 Unique Launch Sites.png
│   ├── Task 2 Launch Sites Begin with CCA.png
│   ├── Task 3 Total Payload Mass.png
│   ├── Task 4 Average Payload Mass.png
│   ├── Task 5 First Successful Landing.png
│   ├── Task 6 Boosters between 4000 and 6000.png
│   ├── Task 7 Total Number of Successful and Failure Missions.png
│   ├── Task 8 Booster Versions that Carried the Maximum Payload.png
│   ├── Task 9 Month_Booster_Failure.png
│   └── Task 10 Count of Landing Outcomes.png
│
├── 2-2_Exploratory_Data_Analysis_with_Visialization/
│   ├── edadataviz.ipynb
│   ├── dataset_part_3.csv
│   ├── Task 1 RS b FN_LS.png
│   ├── Task 2 RS b PM_LS.png
│   ├── Task 3 RD b SR_OT.png
│   ├── Task 4 RS b FN_OT.png
│   ├── Task 5 RS b PM_OT.png
│   ├── Task 6 LS rate trend.png
│   ├── Task 7 Create Dummy Variables to Categorical Columns.png
│   └── Task 8 Cast all numeric columns to float64.png
│
├── 3-1_Interactive_Visual_Analytics_with_Folium_lab/
│   ├── lab_jupyter_launch_site_location.ipynb
│   ├── Task 1.png
│   ├── Task 2.png
│   └── Task 3.png
│
├── 3-2_Build_an_Interactive_Dashboard_with_Plotly_Dash/
│   ├── spacex-dash-app.py
│   ├── total-success-launches-by-site.png
│   ├── total-success-launches-for-site-ksc-lc-39a.png
│   └── correlation-between-payload-and-success.png
│
└── 4-1_Complete_the_Machine_Learning_Prediction_lab/
    ├── SpaceX_Machine Learning Prediction_Part_5.ipynb
    ├── Task 5 accuracy using the method score.png
    ├── Task 9 accuracy tree_cv using the method score.png
    └── Task 12 best performing method.png
