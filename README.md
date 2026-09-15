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

## Data Sources

The dataset was obtained from Kaggle, while the variable descriptions were retrieved from the NASA Exoplanet Archive documentation.

* Dataset: Kepler Exoplanet Search Results : https://www.kaggle.com/datasets/shashansai/kepler-exoplanet-search-results
* Official variable documentation: NASA Exoplanet Archive : https://exoplanetarchive.ipac.caltech.edu/docs/API_kepcandidate_columns.html

