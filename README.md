# Machine Learning Kepler Koi classification
Ce dépôt contient tout un processus de machine learning permettant, à partir de caractéristiques d'un signal `KOI (Kepler Object of Interest)` détecté via la méthode de transit, déterminer la classe du signal `KOI` à savoir ;

la target : `koi_disposition` qui peut être classifié :
- `CANDIDATE`
- `CONFIRMED`
- `FALSE POSITIVE`
En entrée nous avons :
Une étoile hôte disponible dans le catalogue `KIC (Kepler )`
  
Il contient notamment les phases suivants :
- Exploratory data analysis 
- Preprocessing + Feature engineering
- Feature selection
- Modeling
- Pipeline

Le dataset utilisé provient de Kaggle qui lui même a été extrait des archives publiques de la NASA

