# Prédiction de résultats de matches

Résumé
- Notebook Jupyter qui prépare des données de matches et entraîne un RandomForest pour prédire si une équipe gagne (colonne `target`).

Fichiers
- `prediction.ipynb` : pipeline complet (prétraitement, features, entraînement, évaluation).
- `matches.csv` : jeu de données attendu (placer à la racine du projet).
- `README.md` : ce fichier.

Prérequis
- Windows, Python 3.8+
- Packages : pandas, scikit-learn, jupyter (ou utilisez l'environnement intégré VS Code)

Installation (Windows)
1. python -m venv venv
2. venv\Scripts\activate
3. pip install -r requirements.txt
   (si pas de requirements.txt : pip install pandas scikit-learn jupyter)

Exécution
- Ouvrir `prediction.ipynb` dans Jupyter ou VS Code et exécuter les cellules dans l'ordre.
- Commande Jupyter : jupyter notebook prediction.ipynb

Points importants du notebook
- Lecture : `matches = pd.read_csv("matches.csv", index_col=0)`
- Conversion date/time et création de features : `venue_code`, `opp_code`, `hour`, `day_code`
- Target : `matches["target"] = (matches["result"] == "W").astype("int")`
- Rolling features par équipe : fonction `rolling_averages(...)` (fenêtre 3, exclusif)
- Modèle : `RandomForestClassifier` (n_estimators=50, min_samples_split=10)
- Évaluation : précision / matrice de confusion / precision_score
- Fusion pour comparaison équipe vs adversaire via mapping de noms d'équipes

Reproduction rapide
- Exécuter les cellules jusqu'à la création de `matches_rolling`
- Appeler : `combined, error = make_predictions(matches_rolling, predictors + new_cols)`


