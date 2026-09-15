# Machine Learning Kepler KOI classification
## Goal:
Ce dépôt contient tout un processus de machine learning permettant de prédire, à partir de caractéristiques tabulaires d'un signal de transit `KOI (Kepler Object of Interest)` et des caractéristiques de l'étoile hôte, la classe de la cible `koi_disposition`.


  
### Input:
Une ligne de données décrivant : 
- Une étoile hôte et ses caractéristiques
- Les caractéristiques du signal `KOI` (détecté via la méthode des transits)
  
### Output:
Prédiction de la classe de la cible `koi_disposition` une parmi les trois classes possibles : 
- `CANDIDATE`
- `CONFIRMED`
- `FALSE POSITIVE`

## Structure :
 1) Exploratory data analysis 
 2) Preprocessing + Feature engineering
 3) Feature selection
 4) Modeling
 5) Pipeline

## Source :
Le dataset utilisé provient de Kaggle et les descriptions des colonnes du dataset ont été trouvées dans les archives de la NASA

Source dataset : https://www.kaggle.com/datasets/shashansai/kepler-exoplanet-search-results
Documentation officielle des variables : https://exoplanetarchive.ipac.caltech.edu/docs/API_kepcandidate_columns.html


