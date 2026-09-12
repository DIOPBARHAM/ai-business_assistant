# Partie 4 – Sorties structurées

## 1) Prompt JSON

```
Analyse le commentaire suivant et retourne un JSON strict avec les champs :
- sentiment (positif | negatif | neutre)
- categorie (chaîne libre décrivant le domaine concerné, ex : livraison, produit, technique)
- urgence (faible | moyenne | élevée)
- probleme (chaîne courte décrivant le problème)
- confiance (nombre entre 0 et 1)
Ne retourne que le JSON, sans texte avant ou après.
Commentaire : « Le service est rapide mais l'application plante régulièrement. »
```
**Réponse :**
```json
{
  "sentiment": "negatif",
  "categorie": "technique",
  "urgence": "élevée",
  "probleme": "L'application plante régulièrement, notamment lors du paiement",
  "confiance": 0.99
}
```


