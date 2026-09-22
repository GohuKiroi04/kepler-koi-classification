# Machine Learning for Kepler KOI Classification

## Goal

This repository presents an end-to-end machine learning workflow for classifying **Kepler Objects of Interest (KOIs)** based on transit-signal features and host-star characteristics.

The target variable, `koi_disposition`, contains three possible classes:

* `CANDIDATE`
* `CONFIRMED`
* `FALSE POSITIVE`

### Input

A tabular observation describing:

* the host star and its characteristics;
* the detected KOI transit signal and its characteristics.

### Output

A prediction of the corresponding `koi_disposition` class.

## Project Structure

1. Exploratory Data Analysis
2. Data Preprocessing and Feature Engineering
3. Feature Selection
4. Model Training and Evaluation
5. Machine Learning Pipeline

## Results

Models were evaluated using **F1-macro** as the main metric so that the three target classes contribute equally to the evaluation. Hyperparameters were selected with 5-fold stratified cross-validation.

| Feature Selection | Model | CV F1-macro | Test F1-macro | Test Accuracy |
|---|---|---:|---:|---:|
| KBest | Decision Tree | 0.6916 | 0.6985 | 0.7292 |
| KBest | KNN | 0.7024 | 0.6988 | 0.7371 |
| Personal Selection | KNN | 0.6945 | 0.7042 | 0.7407 |
| Personal Selection | Random Forest | 0.7239 | 0.7131 | 0.7501 |
| Variance Threshold | Decision Tree | 0.7014 | 0.7045 | 0.7334 |
| **Variance Threshold** | **Random Forest** | **0.7482** | **0.7478** | **0.7805** |
| **Final Pipeline** | **Variance Threshold + Random Forest** | **0.7493** | **0.7518** | **0.7836** |

Among the models evaluated in the modeling phase, **Variance Threshold + Random Forest** achieved the strongest cross-validation performance. The final sklearn pipeline, which integrates feature engineering, preprocessing, feature selection and classification into a single workflow, reached a **test F1-macro of 0.7518** and an **accuracy of 0.7836**.

The `CANDIDATE` class remains the most difficult class to identify, while `CONFIRMED` and `FALSE POSITIVE` are classified more reliably.
## Data Sources

The dataset was obtained from Kaggle, while the variable descriptions were retrieved from the NASA Exoplanet Archive documentation.

* Dataset: Kepler Exoplanet Search Results : https://www.kaggle.com/datasets/shashansai/kepler-exoplanet-search-results
* Official variable documentation: NASA Exoplanet Archive : https://exoplanetarchive.ipac.caltech.edu/docs/API_kepcandidate_columns.html

