# Partie 7 – Prompt Engineering et RAG

**Document interne utilisé (extrait fictif de règlement intérieur) :**
```
Procédure de demande de congé : Tout salarié souhaitant poser un congé doit soumettre sa demande via
le portail RH au moins 15 jours avant la date souhaitée. Le manager dispose de 5 jours ouvrés pour
valider ou refuser la demande. En l'absence de réponse sous ce délai, la demande est considérée
comme acceptée.
```

**Question posée** : « Quel est le délai de préavis pour poser un congé, et que se passe-t-il si le
manager ne répond pas ? »

## Prompt A — sans document

```
Quel est le délai de préavis pour poser un congé dans mon entreprise, et que se passe-t-il si le manager ne répond pas ?
```
**Réponse A :**
```
Cela dépend généralement de la politique interne de chaque entreprise ; le délai habituel se situe
souvent entre 2 et 4 semaines. En l'absence de réponse du manager, les pratiques varient : certaines
entreprises considèrent la demande comme refusée par défaut, d'autres comme acceptée. Je ne peux pas
donner de réponse précise sans connaître votre règlement interne.
```
*(Réponse générique, non ancrée — risque d'hallucination si elle avait été formulée avec assurance.)*

## Prompt B — avec document, sans contraintes

```
Voici un extrait du règlement interne :
"""
Procédure de demande de congé : Tout salarié souhaitant poser un congé doit soumettre sa demande via
le portail RH au moins 15 jours avant la date souhaitée. Le manager dispose de 5 jours ouvrés pour
valider ou refuser la demande. En l'absence de réponse sous ce délai, la demande est considérée
comme acceptée.
"""
Quel est le délai de préavis pour poser un congé, et que se passe-t-il si le manager ne répond pas ?
```
**Réponse B :**
```
Le délai de préavis est de 15 jours avant la date souhaitée. Si le manager ne répond pas dans les
5 jours ouvrés suivant la demande, celle-ci est automatiquement considérée comme acceptée.
```

## Prompt C — avec document + règles RAG explicites

```
[RÔLE] Tu es un assistant documentaire interne.
[RÈGLES] Réponds uniquement à partir du CONTEXTE fourni. N'invente aucune information absente. Si
l'information n'est pas présente, dis-le clairement. Cite la source lorsque c'est possible.
[CONTEXTE]
"""
Procédure de demande de congé : Tout salarié souhaitant poser un congé doit soumettre sa demande via
le portail RH au moins 15 jours avant la date souhaitée. Le manager dispose de 5 jours ouvrés pour
valider ou refuser la demande. En l'absence de réponse sous ce délai, la demande est considérée
comme acceptée.
"""
[QUESTION] Quel est le délai de préavis pour poser un congé, et que se passe-t-il si le manager ne
répond pas ?
[FORMAT] Réponse directe, puis source utilisée.
```
**Réponse C :**
```
Réponse : Le délai de préavis est de 15 jours avant la date de congé souhaitée. Si le manager ne
répond pas dans les 5 jours ouvrés, la demande est considérée comme acceptée.
Source : extrait « Procédure de demande de congé » du règlement intérieur fourni.
```

## Comparaison

| Prompt | Ancrage | Fiabilité | Traçabilité |
|---|---|---|---|
| A (sans document) | Aucun | Faible, réponse générique | Aucune |
| B (avec document) | Oui | Bonne, réponse exacte | Implicite |
| C (avec document + règles) | Oui | Bonne et prudente | Explicite (source citée) |

**Conclusion** : sans document, le modèle produit une réponse plausible mais non fiable (risque
d'hallucination). Le RAG (B et C) ancre la réponse dans la réalité de l'entreprise ; l'ajout de
règles explicites (C) améliore encore la traçabilité et la prudence de la réponse.
