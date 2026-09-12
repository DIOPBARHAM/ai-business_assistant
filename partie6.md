# Partie 6 – Prompt Engineering pour le Machine Learning

*Dataset fictif utilisé : capteurs d'un bâtiment — colonnes `timestamp, temperature, humidite,
consommation_kwh, type_piece (catégorielle)`.*

## 1) Préparation des données

```
Voici un extrait de mon dataset de capteurs (colonnes : timestamp, temperature, humidite,
consommation_kwh, type_piece). Le dataset contient des valeurs manquantes dans humidite et des
doublons de timestamp. Propose un plan de traitement (détection, méthode, risques associés) pour :
les valeurs manquantes, les doublons, les valeurs aberrantes, la variable catégorielle type_piece.
```
**Réponse :**
```
Plan de traitement des données
1. Valeurs manquantes – humidite
Détection : calculer le nombre et le taux de valeurs manquantes.
Méthode : interpolation temporelle pour les manques courts ; médiane par type_piece pour les cas plus longs.
Risque : créer des valeurs artificielles et fausser les analyses.
2. Doublons – timestamp
Détection : rechercher les timestamps identiques.
Méthode : vérifier les doublons, puis supprimer ou agréger les mesures si elles sont réellement identiques.
Risque : perte d’information ou masquage de variations.
3. Valeurs aberrantes
Détection : IQR, z-score et vérification des limites physiques.
Méthode : vérifier avant de supprimer ou corriger ; conserver les anomalies réelles.
Risque : supprimer une anomalie réelle ou modifier la variabilité.
4. type_piece (catégorielle)
Détection : vérifier les modalités, fautes et valeurs manquantes.
Méthode : standardiser puis appliquer un encodage one-hot.
Risque : perte d’information ou multiplication du nombre de variables.sentes peut lisser

```

## 2) Génération de visualisations

```
À partir du dataset de capteurs, propose une stratégie de visualisation exploratoire pour comprendre
la consommation énergétique d'un bâtiment. Pour chaque visualisation, indique : objectif, type de
graphique, variables utilisées, code Python (matplotlib/seaborn), précaution d'interprétation.
```
**Réponse :**
```
1. Évolution temporelle de la consommation
   Objectif : repérer les tendances et pics journaliers.
   Graphique : courbe (line plot), x=timestamp, y=consommation_kwh
   Code : sns.lineplot(data=df, x='timestamp', y='consommation_kwh')
   Précaution : vérifier l'échelle temporelle (agrégation horaire vs quotidienne) avant conclusion.

2. Consommation par type de pièce
   Objectif : comparer les usages énergétiques.
   Graphique : boxplot, x=type_piece, y=consommation_kwh
   Code : sns.boxplot(data=df, x='type_piece', y='consommation_kwh')
   Précaution : un déséquilibre du nombre d'observations par pièce peut fausser la comparaison.

3. Corrélation température / consommation
   Objectif : quantifier l'effet de la température sur la consommation.
   Graphique : nuage de points (scatter) + droite de régression
   Code : sns.regplot(data=df, x='temperature', y='consommation_kwh')
   Précaution : corrélation ≠ causalité ; d'autres facteurs (occupation) peuvent expliquer la relation.
```

## 3) Sélection de modèles

```
Je veux prédire la consommation énergétique horaire d'un bâtiment (régression) à partir de
température, humidité, type de pièce et heure de la journée, sur un dataset de 20 000 lignes.
Propose 4 modèles à comparer. Pour chacun : principe, avantages, limites, type de problème, métriques
pertinentes. Ne choisis pas le modèle final sans résultats expérimentaux.
```
**Réponse :**
```
1. Régression linéaire — principe : relation linéaire entre variables et cible. Avantage :
   interprétable, rapide. Limite : ne capture pas les relations non linéaires (ex. effet saturant de
   la température). Métriques : MAE, RMSE, R².

2. Random Forest Regressor — principe : ensemble d'arbres de décision. Avantage : robuste aux
   non-linéarités et aux outliers. Limite : moins interprétable, coût de calcul plus élevé.
   Métriques : MAE, RMSE, R².

3. Gradient Boosting (XGBoost/LightGBM) — principe : arbres construits séquentiellement pour corriger
   les erreurs précédentes. Avantage : très performant sur données tabulaires. Limite : sensible aux
   hyperparamètres, risque de surapprentissage. Métriques : MAE, RMSE, R².

4. Réseau de neurones (MLP) — principe : couches de neurones apprenant des représentations non
   linéaires. Avantage : puissant si beaucoup de données et de features. Limite : nécessite plus de
   données, peu interprétable, sensible au prétraitement. Métriques : MAE, RMSE, R².

Aucun de ces modèles n'est retenu par défaut : une validation croisée sur les données réelles est
nécessaire avant de choisir.
```

## 4) Interprétation des métriques de classification

```
Explique les métriques suivantes pour une tâche de classification : Accuracy, Precision, Recall,
F1-score, ROC-AUC. Pour chacune : définition, interprétation, exemple concret, contexte d'usage
privilégié.
```
**Réponse :**
```
- Accuracy : proportion de prédictions correctes sur l'ensemble. Ex : 94% de tickets bien classés.
  Utile si les classes sont équilibrées ; trompeuse sinon.
- Precision : parmi les prédictions positives, proportion réellement correcte. Ex : sur 100 alertes
  de fraude, 71 sont de vraies fraudes. Utile quand le coût d'un faux positif est élevé.
- Recall : parmi les cas réellement positifs, proportion détectée. Ex : sur 100 vraies fraudes, 62
  sont détectées. Utile quand manquer un cas positif est coûteux (santé, sécurité).
- F1-score : moyenne harmonique de precision et recall. Utile en cas de déséquilibre de classes et
  quand on veut un compromis entre les deux.
- ROC-AUC : capacité du modèle à distinguer les classes, indépendamment du seuil choisi. Utile pour
  comparer des modèles avant de fixer un seuil de décision opérationnel.
```

## 5) Interprétation des métriques de régression

```
Explique les métriques suivantes pour une tâche de régression : MAE, MSE, RMSE. Pour chacune :
définition, interprétation, exemple concret, contexte d'usage privilégié.
```
**Réponse :**
```
- MAE (Mean Absolute Error) : moyenne des écarts absolus entre prédiction et valeur réelle. Ex : une
  MAE de 2.3 kWh signifie qu'en moyenne, la prédiction s'écarte de 2.3 kWh de la consommation réelle.
  Facile à interpréter, peu sensible aux valeurs extrêmes.
- MSE (Mean Squared Error) : moyenne des écarts au carré. Pénalise fortement les grosses erreurs.
  Utile quand les erreurs importantes doivent être évitées à tout prix, mais moins interprétable
  (unité au carré).
- RMSE (Root Mean Squared Error) : racine carrée du MSE, ramène l'unité à l'échelle d'origine (kWh).
  Combine la sensibilité aux grandes erreurs du MSE et l'interprétabilité de la MAE. Souvent préféré
  en usage métier.
```
