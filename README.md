# Cognifyz Technologies — Data Science Internship Project

**Restaurant data analysis, feature analysis and predictive modeling across three levels and nine Jupyter notebooks.**

> **Status:** All nine notebooks have been executed with saved outputs. Every figure quoted in this README was read from those saved outputs (or from the two CSV files). This is a notebook-based analysis project; nothing here is deployed.

---

## Table of Contents

1. [Overview](#overview)
2. [Internship Context](#internship-context)
3. [Objectives](#objectives)
4. [Project Structure](#project-structure)
5. [Datasets](#datasets)
6. [Tasks at a Glance](#tasks-at-a-glance)
7. [Task Details](#task-details)
8. [Results and Key Findings](#results-and-key-findings)
9. [Technologies and Libraries](#technologies-and-libraries)
10. [Installation](#installation)
11. [How to Run the Notebooks](#how-to-run-the-notebooks)
12. [Limitations](#limitations)
13. [Conclusion](#conclusion)
14. [Suggested GitHub Topics](#suggested-github-topics)
15. [Author](#author)

---

## Overview

This repository contains the work completed for the **Cognifyz Technologies Data Science Internship**. It analyses a restaurant dataset of **9,551 records and 21 columns**, covering restaurant location, cuisines, price range, table-booking and online-delivery availability, aggregate rating, rating labels and votes.

The work is organised into three levels of increasing depth:

| Level | Theme | Tasks |
|---|---|---|
| **Level 1** | Data Analysis | Data Exploration and Preprocessing, Descriptive Analysis, Geospatial Analysis |
| **Level 2** | Feature Analysis | Table Booking and Online Delivery, Price Range Analysis, Feature Engineering |
| **Level 3** | Advanced Analysis | Predictive Modeling, Customer Preference Analysis, Data Visualization |

## Internship Context

The project was completed as the task submission for the Cognifyz Technologies Data Science Internship, using Jupyter Notebooks in VS Code. Each notebook is self-contained: it loads the dataset, documents its assumptions, produces tables and charts, and summarises findings from its own outputs.

## Objectives

- Explore and clean the restaurant dataset and understand the distribution of `Aggregate rating`.
- Describe the data with summary statistics, categorical distributions and geographic views.
- Study how restaurant services (table booking, online delivery) and price range relate to ratings.
- Engineer new, leakage-free features and export them as a separate dataset.
- Build and evaluate regression models that predict `Aggregate rating`.
- Analyse customer preferences by cuisine and communicate results through clear visualizations.

---

## Project Structure

```text
Cognifyz Intern/
├── README.md
├── dataset/
│   ├── Dataset.csv
│   └── engineered_restaurant_data.csv
├── Level1/
│   ├── Task1_Data_Exploration.ipynb
│   ├── Task2_Descriptive_Analysis.ipynb
│   └── Task3_Geospatial_Analysis.ipynb
├── Level2/
│   ├── Task1_Table_Booking_Online_Delivery.ipynb
│   ├── Task2_Price_Range_Analysis.ipynb
│   └── Task3_Feature_Engineering.ipynb
└── Level3/
    ├── Task1_Predictive_Modeling.ipynb
    ├── Task2_Customer_Preference_Analysis.ipynb
    └── Task3_Data_Visualization.ipynb
```

> **Path note:** The notebooks read the dataset from the relative path `../dataset/Dataset.csv`. The dataset folder is named `dataset` (lowercase), so the path matches the folder name and works on case-sensitive systems too. See [How to Run the Notebooks](#how-to-run-the-notebooks).

---

## Datasets

### `dataset/Dataset.csv` — original restaurant data

The raw input used by all nine notebooks. It has **9,551 rows × 21 columns** and no duplicate rows (checked in Level 1 Task 2). The notebooks do not state where the data was obtained, so no source is claimed here.

| Group | Columns |
|---|---|
| Identity | `Restaurant ID`, `Restaurant Name` |
| Location | `Country Code`, `City`, `Address`, `Locality`, `Locality Verbose`, `Longitude`, `Latitude` |
| Offering | `Cuisines`, `Average Cost for two`, `Currency`, `Price range` |
| Services | `Has Table booking`, `Has Online delivery`, `Is delivering now`, `Switch to order menu` |
| Ratings | `Aggregate rating`, `Rating color`, `Rating text`, `Votes` |

Points to be aware of (all observed in the notebook outputs):

- `Cuisines` is the only column with missing values: **9 rows (0.09%)**.
- Countries appear only as numeric `Country Code` values (15 distinct codes); the dataset has no country names.
- **2,148 restaurants (22.5%)** have an `Aggregate rating` of `0`. `Rating text` labels all of them *Not rated*, so the notebooks in Levels 2 and 3 treat `0` as "not rated" rather than as a poor score.
- `Average Cost for two` is recorded in local currencies and is therefore not directly comparable across countries.

### `dataset/engineered_restaurant_data.csv` — engineered copy

Produced by **Level 2 · Task 3: Feature Engineering**. It has **9,551 rows × 30 columns**: the 21 original columns, unchanged and in the same order, followed by 9 engineered features. The export was re-read and its shape checked inside the notebook, and `Dataset.csv` was not modified. As inspected, no other notebook loads this file.

| Engineered feature | Rule |
|---|---|
| `Restaurant Name Length` | Number of characters in `Restaurant Name` |
| `Address Length` | Number of characters in `Address` |
| `Has Table Booking` | `Yes` → 1, `No` → 0, unknown → missing |
| `Has Online Delivery` | `Yes` → 1, `No` → 0, unknown → missing |
| `Cuisine Count` | Number of distinct comma-separated cuisines; missing if `Cuisines` is missing |
| `Restaurant Name Word Count` | Number of words in the name |
| `Address Word Count` | Number of words in the address |
| `Is Multi Cuisine` | 1 if more than one cuisine is listed, otherwise 0 |
| `Services Offered Count` | Sum of the two service flags (0–2) |

No engineered feature uses `Aggregate rating`, `Rating color`, `Rating text` or `Votes`.

---

## Tasks at a Glance

| # | Level | Task | Notebook | Purpose |
|---|---|---|---|---|
| 1 | Level 1 | Data Exploration and Preprocessing | `Level1/Task1_Data_Exploration.ipynb` | Dataset size, missing values, data types, rating distribution and imbalance |
| 2 | Level 1 | Descriptive Analysis | `Level1/Task2_Descriptive_Analysis.ipynb` | Summary statistics; country, city and cuisine distributions |
| 3 | Level 1 | Geospatial Analysis | `Level1/Task3_Geospatial_Analysis.ipynb` | Restaurant locations and coordinate–rating association |
| 4 | Level 2 | Table Booking and Online Delivery | `Level2/Task1_Table_Booking_Online_Delivery.ipynb` | Service availability and its relation to rating and price range |
| 5 | Level 2 | Price Range Analysis | `Level2/Task2_Price_Range_Analysis.ipynb` | Price-range mix, ratings by price range, rating colour |
| 6 | Level 2 | Feature Engineering | `Level2/Task3_Feature_Engineering.ipynb` | Create, validate and export new features |
| 7 | Level 3 | Predictive Modeling | `Level3/Task1_Predictive_Modeling.ipynb` | Regression models for `Aggregate rating` |
| 8 | Level 3 | Customer Preference Analysis | `Level3/Task2_Customer_Preference_Analysis.ipynb` | Cuisine popularity (votes) and cuisine–rating relationship |
| 9 | Level 3 | Data Visualization | `Level3/Task3_Data_Visualization.ipynb` | Rating distributions, group comparisons, feature–rating relationships |

---

## Task Details

### Level 1 — Data Analysis

#### Task 1: Data Exploration and Preprocessing
**Purpose:** Establish the shape and quality of the dataset and examine the target variable.

**Analysis performed:** row and column counts; data-type profile; missing-value counts and percentages; filling missing `Cuisines` with `Unknown` on a working copy (`df_clean`) so the original data stays untouched; numeric coercion of `Aggregate rating`; rating counts and percentages with a descriptive class-imbalance check.

#### Task 2: Descriptive Analysis
**Purpose:** Summarise the dataset with statistics and frequency tables.

**Analysis performed:** `describe()`-style statistics plus medians for numeric columns; top-10 tables for `Country Code`, `City` and `Cuisines`; top-10 cities and top-10 individually counted cuisines (multi-cuisine cells are split); average rating for the ten cities with the most records; auto-generated insights.

#### Task 3: Geospatial Analysis
**Purpose:** Explore where restaurants are located and whether coordinates relate to ratings.

**Analysis performed:** coordinate validation; restaurant counts by country code and city; a longitude/latitude scatter plot coloured by rating; Pearson correlation between coordinates and rating; average rating for the top-10 cities by record count. The notebook also contains an interactive Folium map for a 2,500-record sample, but Folium was not installed when the notebook was run, so the map was not produced (the output shows an installation hint).

### Level 2 — Feature Analysis

#### Task 1: Table Booking and Online Delivery
**Purpose:** Measure how common the two services are and how they relate to ratings and price.

**Analysis performed:** counts and percentages for each service; rating mean, median and standard deviation with and without table booking (rated restaurants only); online-delivery counts and within-price-range percentages; labelled tables and charts.

#### Task 2: Price Range Analysis
**Purpose:** Understand how restaurants and ratings are distributed across the four price ranges.

**Analysis performed:** inspection of `Price range`; counts and shares per range; rating statistics per range (rated restaurants only, with unrated counts shown); identification of the highest-rated range; analysis of `Rating color` bands and their mix within each price range.

#### Task 3: Feature Engineering
**Purpose:** Create reusable, leakage-free features and export them.

**Analysis performed:** nine engineered features (see [Datasets](#datasets)); original-versus-engineered comparison; descriptive statistics, distributions and a correlation heatmap; **19 automatic validation checks** (independent recomputation, original data unchanged, no leakage in feature names); export to `engineered_restaurant_data.csv`.

### Level 3 — Advanced Analysis

#### Task 1: Predictive Modeling
**Purpose:** Predict `Aggregate rating` with regression models and evaluate them honestly.

**Analysis performed:** `Rating color` and `Rating text` excluded as direct encodings of the target; modeling restricted to rated restaurants; 80/20 train–test split (`random_state=42`) before computing any feature statistics; features include country, city, multi-hot encoding of the 40 most frequent cuisines, price range, service flags, `log(1 + Votes)`, name/address length and a country-relative cost; comparison of a mean baseline, Linear, Ridge, two Decision Trees, Random Forest and Gradient Boosting using 5-fold cross-validation on the training set; a small randomised search for Random Forest; permutation importance; robustness checks without `Votes` and with unrated restaurants included.

#### Task 2: Customer Preference Analysis
**Purpose:** Find which cuisines are most popular and whether some cuisines are rated higher.

**Analysis performed:** cuisine explosion (a restaurant counts toward each cuisine it lists); popularity by total and average votes; mean rating per cuisine with 95% confidence intervals for cuisines with at least 30 rated restaurants; Welch t-tests against all other restaurants with Benjamini–Hochberg false-discovery-rate adjustment; a country-adjusted rating; cross-validated Ridge models comparing the explanatory power of cuisine and country.

#### Task 3: Data Visualization
**Purpose:** Present the rating distribution, group comparisons and feature relationships visually.

**Analysis performed:** distribution views (histograms, box plot, cumulative distribution, rating-category bars); mean ratings with confidence intervals by country, cuisine and city; rating against price range, service flags, name length and address length; a geographic scatter view; a Spearman correlation heatmap.

---

## Results and Key Findings

All values below come from the saved notebook outputs. Unless stated, "rated" means `Aggregate rating > 0`.

### Dataset and ratings (Level 1)

| Item | Result |
|---|---|
| Dimensions | 9,551 rows × 21 columns; row count preserved after cleaning |
| Missing values | `Cuisines`: 9 (0.09%); all other columns complete |
| `Aggregate rating` (all rows) | mean 2.67, median 3.20, std 1.52, range 0.0–4.9 |
| Unrated (rating 0) | 2,148 restaurants (22.49%) — the most frequent value; least frequent is 1.8 (1 restaurant) |
| Votes | median 31, mean 156.9 (right-skewed) |
| Countries (by code) | Code 1: 8,652 records; Code 216: 434; Code 215: 80 |
| Cities | New Delhi 5,473; Gurgaon 1,118; Noida 1,080; Faridabad 251; Ghaziabad 25 |
| Most listed cuisines | North Indian 3,960; Chinese 2,735; Fast Food 1,986; Mughlai 995; Italian 764 |
| Coordinates vs rating (Pearson) | Latitude 0.001; Longitude −0.117 |

> Level 1 statistics include the unrated `0` values, which is why the mean rating here (2.67) is lower than the rated-only mean in Levels 2 and 3 (3.44).

### Services and price range (Level 2)

| Item | Result |
|---|---|
| Table booking | 1,158 restaurants (12.12%) |
| Online delivery | 2,451 restaurants (25.66%) |
| Mean rating, with vs without table booking (rated only) | 3.59 (n = 1,111) vs 3.41 (n = 6,292) |
| Online delivery by price range 1 / 2 / 3 / 4 | 15.77% / 41.31% / 29.19% / 9.04% |
| Restaurants by price range 1 / 2 / 3 / 4 | 4,444 (46.53%) / 3,113 (32.59%) / 1,408 (14.74%) / 586 (6.14%) |
| Mean rating by price range 1 / 2 / 3 / 4 (rated only) | 3.24 / 3.38 / 3.78 / 3.89 |
| Highest-rated colour | Dark Green (mean 4.66); colours are fixed rating bands, so this follows from how colours are assigned, not from price |
| Engineered dataset | 9,551 × 30; all 19 validation checks passed |

### Predictive modeling (Level 3 · Task 1)

Setup: 7,403 rated restaurants; 5,922 for training and 1,481 for testing. The model was selected by cross-validated R² on the training set only.

| Model | CV R² (mean) | Test R² | Test MAE | Test RMSE |
|---|---|---|---|---|
| **Random Forest (tuned)** | **0.621** | **0.666** | **0.237** | **0.321** |
| Gradient Boosting | 0.617 | 0.653 | 0.245 | 0.328 |
| Random Forest | 0.610 | 0.660 | 0.239 | 0.324 |
| Ridge Regression | 0.580 | 0.632 | 0.252 | 0.338 |
| Linear Regression | 0.579 | 0.634 | 0.251 | 0.337 |
| Decision Tree (depth 8) | 0.528 | 0.573 | 0.268 | 0.363 |
| Decision Tree (unpruned) | 0.233 | 0.241 | 0.347 | 0.484 |
| Baseline (mean) | −0.002 | −0.000 | 0.455 | 0.556 |

- The selected model's predictions fall within ±0.5 rating points of the true rating for **88.2%** of test restaurants.
- Its training R² is 0.885 versus a cross-validated R² of 0.621, which indicates noticeable overfitting.
- Permutation importance is dominated by `Votes (log)` (0.625), followed by `Cuisines` (0.088) and `Longitude` (0.063).
- **Without `Votes`**, test R² falls to 0.551 (MAE 0.290, RMSE 0.373). `Votes` accumulate after a restaurant has been rated, so it would not be available as a pre-launch predictor.
- A third robustness run that includes unrated restaurants reports R² 0.964, but it uses a different test set and treats "not rated" as a numeric 0, so it is **not comparable** with the figures above.

### Customer preferences (Level 3 · Task 2)

| Item | Result |
|---|---|
| Cuisines analysed | 145 distinct; 39 have ≥ 30 rated restaurants |
| Most-voted cuisine | North Indian — 595,981 votes across 3,960 restaurants |
| Overall mean rating (rated) | 3.440 |
| Highest / lowest mean rating (≥ 30 rated) | Indian 4.16 (n = 66) / Raw Meats 3.07 (n = 80) |
| Significant vs rest (FDR 5%) | 23 cuisines above, 10 below, of 39 tested |
| Country-adjusted top cuisine | Mediterranean (+0.534 vs country mean) |
| Cross-validated R², Ridge | cuisine only 0.248; country only 0.193; both 0.325 |

### Visualization insights (Level 3 · Task 3)

| Item | Result |
|---|---|
| Rated restaurants | 7,403 (mean 3.44, median 3.40, std 0.552) |
| Strongest rating correlations (Spearman) | `Votes (log)` 0.682; `Price range` 0.402; relative cost 0.247; table booking 0.126 |
| Weak correlations | online delivery −0.039; name length 0.012 |
| Most common 15 cuisines | highest American (3.76); lowest Mithai (3.14) |
| Cities (min. 20 rated restaurants) | highest London (4.54); lowest Ghaziabad (3.10) |

---

## Technologies and Libraries

Verified from the notebook imports and kernel metadata:

| Category | Tools |
|---|---|
| Language | Python 3.11 (kernel `tf_env`, Python 3.11.16) |
| Environment | Jupyter Notebooks in VS Code |
| Data handling | `pandas`, `numpy` |
| Visualization | `matplotlib`, `seaborn`; `folium` (optional, Level 1 Task 3 only) |
| Machine learning | `scikit-learn` (models, pipelines, preprocessing, model selection, metrics, permutation importance) |
| Statistics | `scipy` (Welch t-test, Spearman correlation) |
| Notebook display | `IPython` |

Standard-library modules used: `pathlib`, `warnings`.

---

## Installation

The package names below were confirmed from the notebook imports. **Exact package versions were not recorded in the notebooks**, so none are pinned here.

```bash
# 1. Create and activate a virtual environment (recommended)
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS / Linux:
source .venv/bin/activate

# 2. Install the dependencies
pip install -r requirements.txt
```

**Recommended `requirements.txt`** (place in the repository root):

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
scipy
ipykernel
jupyter
folium
```

`ipykernel` and `jupyter` are needed to run the notebooks; `folium` is only needed for the interactive map in Level 1 Task 3. For a reproducible setup, run `pip freeze` in the environment that produced your outputs and pin those versions.

---

## How to Run the Notebooks

### In VS Code

1. Install the **Python** and **Jupyter** extensions.
2. Open the `Cognifyz Intern` folder via *File → Open Folder*.
3. Open any notebook from `Level1/`, `Level2/` or `Level3/`.
4. Select the Python environment that has the dependencies installed (*Select Kernel* in the top-right corner).
5. Choose **Run All**, or run cells one at a time.

### In Jupyter

```bash
cd "Cognifyz Intern"
jupyter notebook
```

Open a notebook and use *Run → Run All Cells*.

### Important notes

- **Working directory:** each notebook loads `../dataset/Dataset.csv`, so it must run with its own level folder as the working directory. VS Code and Jupyter do this by default when a notebook is opened directly.
- **Folder-name case:** The dataset folder is named `dataset/` (lowercase), and the notebooks use `../dataset/Dataset.csv`. Keep these names consistent when running the notebooks on case-sensitive systems.
- **Order:** the notebooks are independent of each other. Only Level 2 · Task 3 writes a file (`engineered_restaurant_data.csv`), and no other notebook reads it.
- **Folium map:** install `folium` and re-run the interactive-map cell in Level 1 Task 3 if you want the map.

---

## Limitations

- **Single, geographically skewed dataset.** Country code 1 accounts for 8,652 of 9,551 records (about 90.6%), and a few Delhi-area cities dominate the city counts. Results for other countries rest on very small samples.
- **Unrated restaurants are handled differently across levels.** Level 1 statistics include the 2,148 zero ratings; Levels 2 and 3 exclude them. The two sets of averages are therefore not directly comparable.
- **Placeholder coordinates in Level 1 Task 3.** Level 3 identifies 499 rows with a zero longitude or latitude that behave as placeholders (excluded from the Level 3 maps and treated as missing in the model). Level 1 Task 3 only checks that coordinates lie within valid bounds, so these rows remain in its scatter plot and in the reported coordinate–rating correlations. Those correlations should be read with that in mind.
- **Country names are an assumption.** The dataset provides only `Country Code`. The Level 3 notebooks map codes to names with a dictionary written inside the notebooks; this mapping is not supplied by the dataset.
- **Mixed currencies.** `Average Cost for two` is in local currencies, so its raw descriptive statistics (Level 1 Task 2) mix currencies. Level 3 uses a country-relative cost instead.
- **`Votes` is not a pre-launch signal.** It dominates the predictive model; performance without it is noticeably lower (test R² 0.551).
- **Overfitting and validation scope.** The tuned Random Forest shows a large gap between training and cross-validated R², and results come from one random 80/20 split plus cross-validation on this dataset only. There is no external validation.
- **Association, not causation.** Differences by cuisine, price range, table booking or location are observational. Cuisine groups overlap because multi-cuisine restaurants count toward each cuisine they list.
- **Rating colour is not an independent variable.** It is a direct bucketing of the rating, so "the colour with the highest rating" follows from its definition.
- **Interactive map not generated.** Folium was unavailable when Level 1 Task 3 was run.
- **Notebook execution does not guarantee analytical correctness.** The outputs document what the code produced; they have not been independently audited.

---

## Conclusion

The project takes a restaurant dataset from basic exploration through feature analysis to predictive modeling. The main takeaways from the saved outputs are that about 22.5% of restaurants are unrated and must be handled explicitly; that price range and vote count are the strongest correlates of rating among rated restaurants; and that a tuned Random Forest reaches a test R² of 0.666 (MAE 0.237) on rated restaurants, though that result depends heavily on `Votes` and shows some overfitting. The analysis is observational and bounded by the limitations listed above.

---

## Suggested GitHub Topics

`data-science` · `data-analysis` · `exploratory-data-analysis` · `feature-engineering` · `machine-learning` · `regression` · `random-forest` · `scikit-learn` · `pandas` · `matplotlib` · `seaborn` · `jupyter-notebook` · `data-visualization` · `geospatial-analysis` · `internship-project` · `restaurant-data`

---

## Author

**Harsh** — B.Tech CSE student focused on data science and machine learning.

- GitHub: [harshantla-cloud](https://github.com/harshantla-cloud)
- LinkedIn: [linkedin.com/in/harsh-5694b13ab](https://www.linkedin.com/in/harsh-5694b13ab)
