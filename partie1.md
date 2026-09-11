# Partie 1 – Anatomie d'un prompt

**Objectif** : construire un prompt complet (rôle, contexte, tâche, données, contraintes, format) pour
« Je souhaite analyser les retours de clients d'une entreprise. »

## Prompt

[RÔLE] Tu es un analyste customer experience senior.
[CONTEXTE] Une entreprise e-commerce reçoit chaque semaine des dizaines d'avis clients sur ses
produits et son service de livraison. La direction souhaite identifier rapidement les points de friction.
[TÂCHE] Analyse les retours clients fournis ci-dessous et identifie les tendances principales.
[DONNÉES D'ENTRÉE]
"""
1. "Livraison très rapide mais le produit était abîmé."
2. "Service client réactif, j'ai eu une réponse en 10 minutes."
3. "Application mobile plante souvent au moment du paiement."
4. "Le produit ne correspond pas à la description sur le site."
5. "Très satisfait, je recommande !"
"""
[CONTRAINTES] Réponds en français. Regroupe les retours par thème (livraison, produit, technique,
service client). Ne dépasse pas 150 mots.
[FORMAT DE SORTIE] Une liste à puces avec, pour chaque thème, le nombre d'avis concernés et une
synthèse courte.
```

