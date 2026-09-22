# Machine Learning for Kepler KOI Classification

This project presents an end-to-end machine learning workflow for classifying **Kepler Objects of Interest (KOIs)** using transit-signal features and host-star characteristics.

The objective is to predict the target variable `koi_disposition`, which contains three possible classes:

- `CANDIDATE`
- `CONFIRMED`
- `FALSE POSITIVE`

The project covers the complete machine learning workflow, from exploratory data analysis to the construction and evaluation of a final Scikit-learn pipeline.

---

## Project Objective

### Input

A tabular observation describing:

- the host star and its physical characteristics;
- the detected transit signal associated with the KOI.

### Output

A prediction of the corresponding `koi_disposition` class:

```text
CANDIDATE
CONFIRMED
FALSE POSITIVE
```

---

## Machine Learning Workflow

The project follows five main stages:

1. **Exploratory Data Analysis**
   - dataset structure analysis;
   - missing values;
   - target distribution;
   - feature distributions;
   - outlier and anomaly detection;
   - identification of potentially problematic variables.

2. **Data Preprocessing and Feature Engineering**
   - train/test split;
   - missing-value imputation;
   - categorical encoding;
   - robust scaling;
   - removal of identifiers and leakage-related variables;
   - transformation of skewed variables;
   - cyclic transformation of right ascension.

3. **Feature Selection**
   - manual domain-inspired selection;
   - `VarianceThreshold`;
   - `SelectKBest`.

4. **Model Training and Evaluation**
   - K-Nearest Neighbors;
   - Decision Tree;
   - Random Forest;
   - hyperparameter tuning;
   - stratified cross-validation;
   - evaluation using F1-macro and accuracy.

5. **Final Machine Learning Pipeline**
   - feature engineering;
   - preprocessing;
   - feature selection;
   - classification;
   - complete reproducible Scikit-learn workflow.

---

## Project Structure

```text
kepler-koi-classification/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── raw/
│   │   └── exoplanets_2018.csv
│   │
│   ├── processed/
│   │   ├── xtrain.csv
│   │   ├── xtest.csv
│   │   ├── ytrain.csv
│   │   └── ytest.csv
│   │
│   └── selected/
│       ├── xtrain_KB.csv
│       ├── xtest_KB.csv
│       ├── xtrain_P.csv
│       ├── xtest_P.csv
│       ├── xtrain_VT.csv
│       └── xtest_VT.csv
│
└── notebooks/
    ├── 01_eda.ipynb
    ├── 02_preprocessing.ipynb
    ├── 03_feature_selection.ipynb
    ├── 04a_kbest_decision_tree.ipynb
    ├── 04b_kbest_knn.ipynb
    ├── 04c_personnal_knn.ipynb
    ├── 04d_personnal_random_forest.ipynb
    ├── 04e_variance_threshold_decision_tree.ipynb
    ├── 04f_variance_threshold_random_forest.ipynb
    └── 05_pipeline.ipynb
```

The `data/` directory separates the dataset according to the different stages of the machine learning workflow:

```text
raw → processed → selected → modeling
```

The final pipeline directly starts from the raw dataset and reproduces the necessary preprocessing and feature-selection steps.

---

## Installation

Clone the repository:

```bash
git clone https://github.com/GohuKiroi04/kepler-koi-classification.git
cd kepler-koi-classification
```

Create a virtual environment:

### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

---

## Dependencies

The main libraries used in this project are:

- Python
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter

The exact package versions are available in:

```text
requirements.txt
```

---

## Running the Project

The notebooks can be followed in numerical order:

```text
01_eda.ipynb
        ↓
02_preprocessing.ipynb
        ↓
03_feature_selection.ipynb
        ↓
04a–04f_modeling.ipynb
        ↓
05_pipeline.ipynb
```

The final notebook:

```text
05_pipeline.ipynb
```

reconstructs the complete workflow using a single Scikit-learn pipeline.

---

## Evaluation Strategy

The main evaluation metric is **F1-macro**.

F1-macro computes the F1-score independently for each class and then averages the results.

This metric was selected because each target class should contribute equally to the final evaluation, independently of its frequency in the dataset.

Model selection was performed using **5-fold stratified cross-validation**.

The held-out test set was then used for the final evaluation.

---

## Results

| Feature Selection | Model | CV F1-macro | Test F1-macro | Test Accuracy |
|---|---|---:|---:|---:|
| KBest | Decision Tree | 0.6916 | 0.6985 | 0.7292 |
| KBest | KNN | 0.7024 | 0.6988 | 0.7371 |
| Personal Selection | KNN | 0.6945 | 0.7042 | 0.7407 |
| Personal Selection | Random Forest | 0.7239 | 0.7131 | 0.7501 |
| Variance Threshold | Decision Tree | 0.7014 | 0.7045 | 0.7334 |
| **Variance Threshold** | **Random Forest** | **0.7482** | **0.7478** | **0.7805** |
| **Final Pipeline** | **Variance Threshold + Random Forest** | **0.7493** | **0.7518** | **0.7836** |

Among the models evaluated during the modeling phase, the combination:

```text
Variance Threshold + Random Forest
```

obtained the strongest cross-validation performance.

The final Scikit-learn pipeline achieved:

- **F1-macro:** `0.7518`
- **Accuracy:** `0.7836`

on the held-out test set.

---

## Error Analysis

The `CANDIDATE` class remains the most difficult class to classify.

This class represents objects whose status has not yet been sufficiently established to classify them as either confirmed planets or false positives.

`CONFIRMED` and `FALSE POSITIVE` observations are classified more reliably by the final model.

The learning-curve analysis also indicates a remaining gap between training and validation performance, suggesting some degree of overfitting.

---

## Final Pipeline

The final pipeline integrates the complete machine learning workflow into a single Scikit-learn object:

```text
Raw data
   ↓
Feature engineering
   ↓
Missing-value handling
   ↓
Encoding
   ↓
Robust scaling
   ↓
Variance Threshold
   ↓
Random Forest
   ↓
KOI classification
```

This approach reduces the risk of applying inconsistent preprocessing steps between training and inference.

---

## Potential Improvements

Several extensions could be explored in future work:

- evaluate boosting algorithms such as XGBoost;
- investigate additional feature-engineering strategies;
- perform more extensive hyperparameter optimization;
- analyze feature importance and model interpretability;
- evaluate model calibration;
- investigate the errors made specifically on the `CANDIDATE` class.

---

## Data Sources

The dataset used in this project was obtained from Kaggle:

**Kepler Exoplanet Search Results**  
https://www.kaggle.com/datasets/shashansai/kepler-exoplanet-search-results

The variable definitions and scientific documentation were retrieved from the **NASA Exoplanet Archive**:

**Kepler Objects of Interest — Column Definitions**  
https://exoplanetarchive.ipac.caltech.edu/docs/API_kepcandidate_columns.html

---

## Author

**Hugo Fiévet**

Bachelor student in Computer Science — Artificial Intelligence.
