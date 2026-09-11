# Partie 2 – Comparer les techniques de prompting

**Message à classer** : « Le service est rapide mais l'application plante régulièrement. »
**Classes possibles** : positif, négatif, neutre.

## Zero-shot

```
Classe le message suivant dans une des catégories : positif, négatif, neutre.
Message : « Le service est rapide mais l'application plante régulièrement. »
```
**Réponse :**
```
négatif
```
*(Justification implicite : le bug bloquant domine malgré la mention positive de rapidité.)*

## One-shot

```
Exemple : « Le produit est cher mais de bonne qualité. » → neutre
Nouveau message : « Le service est rapide mais l'application plante régulièrement. » → ?
```
**Réponse :**
```
negatif
```

## Few-shot

```
Exemple 1 : « Très satisfait du produit. » → positif
Exemple 2 : « Le produit ne fonctionne pas. » → négatif
Exemple 3 : « Livraison rapide mais SAV injoignable. » → négatif
Nouveau : « Le service est rapide mais l'application plante régulièrement. » → ?
```
**Réponse :**
```
négatif
```
*(Justification implicite :malgré la rapidité du service, le fait que l’application plante régulièrement constitue un problème important.)*


## Structured prompting

```
[ROLE] Tu es un système de classification de sentiment.
[TASK] Classe le message client suivant.
[DATA] """Le service est rapide mais l'application plante régulièrement."""
[CONSTRAINTS] Une seule catégorie parmi : positif, négatif, neutre. Réponds uniquement par le mot
de la catégorie, sans phrase.
[OUTPUT] Catégorie unique.
```

**Réponse :**
```
négatif

## Comparaison

| Technique | Résultat | Analyse |
|---|---|---|
| Zero-shot | négatif | Cohérent, mais aucune garantie de stabilité |
| One-shot | neutre | L'unique exemple (mixte → neutre) a biaisé la classification |
| Few-shot | négatif | Les exemples variés stabilisent le jugement vers le motif dominant |
| Structured | négatif | Résultat contraint, format garanti, cohérent avec le few-shot |

**Conclusion** : le one-shot est fragile car un seul exemple ambigu peut orienter le modèle dans la mauvaise direction. Le few-shot et le structured prompting convergent vers « négatif », qui semble le jugement le plus pertinent : un bug bloquant prime sur un point positif secondaire.
