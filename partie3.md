# Partie 3 – Prompt Engineering et raisonnement

## 1) Décomposition

Prompt initial : « Analyse ces avis clients et donne-moi les problèmes les plus importants ainsi que les recommandations. »

**Décomposé en 3 prompts successifs :**
```
1. "Résume les tendances principales de ces avis clients."
2. "À partir de ce résumé, identifie les 3 problèmes les plus critiques, classés par gravité."
3. "Pour chacun de ces 3 problèmes, propose une recommandation concrète et réalisable."
```

## 2) Analyse avec contraintes + vérification

**Prompt A (analyse avec contraintes) :**
```
Analyse ces avis clients :
"""
1. "Livraison très rapide mais le produit était abîmé."
2. "Service client réactif, j'ai eu une réponse en 10 minutes."
3. "Application mobile plante souvent au moment du paiement."
4. "Le produit ne correspond pas à la description sur le site."
5. "Très satisfait, je recommande !"
"""
Identifie les 3 problèmes les plus critiques. Ne te base que sur les avis fournis. N'ajoute aucune
information absente du texte. Réponds en français, sous forme de liste.
```
**Réponse A :**
```
Application mobile qui plante au moment du paiement — problème technique récurrent.
Produit ne correspondant pas à la description du site — problème de conformité du produit.
Produit reçu abîmé — problème constaté malgré une livraison très rapide.
```

**Prompt B (self-check) :**
```
Relis ta réponse précédente et vérifie : as-tu utilisé uniquement les informations des avis fournis ?
Y a-t-il des contradictions ? As-tu inventé un problème absent des avis ? Corrige si nécessaire.
```
**Réponse B :**
```
Oui. J’ai utilisé uniquement les informations présentes dans les 5 avis.
Il n’y a pas de contradiction dans ma réponse précédente et je n’ai inventé aucun problème.
Application mobile qui plante au paiement — explicitement mentionné dans l’avis 3.
Produit ne correspondant pas à la description — explicitement mentionné dans l’avis 4.
Produit abîmé à la livraison — explicitement mentionné dans l’avis 1.
La réponse précédente est donc correcte.
```
