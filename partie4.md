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

## 2) Ajout des règles de validation

```
Règles de validation strictes à respecter avant de répondre :
- Le JSON doit être syntaxiquement valide.
- Aucune propriété supplémentaire n'est autorisée.
- sentiment doit être l'une des valeurs : positif, negatif, neutre.
- confiance doit être un nombre compris entre 0 et 1.
- urgence doit être l'une des valeurs : faible, moyenne, élevée.
Si une de ces règles n'est pas respectée dans ta première tentative, corrige silencieusement avant
de produire la réponse finale.
```
**Réponse (validée) :**
```json
{
  "sentiment": "negatif",
  "categorie": "technique",
  "urgence": "élevée",
  "probleme": "Plantages réguliers de l'application au moment du paiement",
  "confiance": 0.99
}
```
Validation manuelle : JSON parsable ✅ — 5 clés exactes, aucune en trop ✅ — `sentiment` ∈ énum ✅ —
`confiance` = 0.99 ∈ [0,1] ✅ — `urgence` ∈ énum ✅.
