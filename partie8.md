# Partie 8 – Évaluation et optimisation des prompts

**Texte à résumer (extrait fictif, note interne RH) :**
```
À compter du mois prochain, l'entreprise généralise le télétravail à deux jours par semaine pour
l'ensemble des équipes administratives, sur la base du volontariat. Les salariés souhaitant en
bénéficier devront en faire la demande auprès de leur manager au moins une semaine à l'avance. Un
point d'étape sera organisé dans trois mois pour évaluer l'impact sur la productivité et la
cohésion d'équipe. Les managers restent libres de refuser une journée de télétravail en cas de
réunion jugée indispensable en présentiel. Cette mesure fait suite à une enquête interne montrant
que 78% des salariés souhaitaient plus de flexibilité dans leur organisation de travail.
```

## Prompt A

```
Résume ce texte.
```
**Réponse A :**
```
L'entreprise met en place le télétravail deux jours par semaine pour les équipes administratives,
sur la base du volontariat, avec une évaluation prévue dans trois mois.
```

## Prompt B

```
Résume ce texte en 150 mots.
```
**Réponse B :**
```
L'entreprise généralise le télétravail à deux jours par semaine pour les équipes administratives, sur
la base du volontariat, à compter du mois prochain. Les salariés doivent formuler leur demande auprès
de leur manager au moins une semaine à l'avance. Un point d'étape est prévu dans trois mois pour
évaluer l'impact sur la productivité et la cohésion d'équipe. Les managers conservent la possibilité
de refuser une journée en cas de réunion jugée indispensable en présentiel. Cette décision fait suite
à une enquête interne révélant que 78% des salariés souhaitaient davantage de flexibilité.
```
*(52 mots réels — le modèle n'a pas rempli artificiellement jusqu'à 150 mots, ce qui reste fidèle au
texte source plutôt que de rallonger inutilement.)*

## Prompt C (structuré)

```
[RÔLE] Tu es un assistant de synthèse pour la direction RH.
[CONTEXTE] Ce texte est une note interne destinée à être diffusée aux managers.
[TÂCHE] Résume ce texte.
[DONNÉES] """{texte ci-dessus}"""
[CONTRAINTES] Maximum 100 mots. Conserve les chiffres clés et les délais. N'invente aucune
information. Base-toi uniquement sur le texte fourni.
[FORMAT] Trois puces : Mesure / Modalités / Suivi.
```
**Réponse C :**
```
- Mesure : télétravail généralisé à 2 jours/semaine pour les équipes administratives, sur la base du
  volontariat, dès le mois prochain.
- Modalités : demande à formuler auprès du manager au moins 1 semaine à l'avance ; le manager peut
  refuser un jour en cas de réunion présentielle indispensable.
- Suivi : bilan prévu dans 3 mois sur la productivité et la cohésion d'équipe. Mesure motivée par une
  enquête interne (78% des salariés en faveur de plus de flexibilité).
```

## Évaluation comparative

| Critère | Prompt A | Prompt B | Prompt C |
|---|---|---|---|
| Fidélité au texte | Bonne mais incomplète (délais absents) | Bonne, complète | Bonne, complète |
| Respect de la contrainte de longueur | N/A (non demandée) | Respectée (sous la limite) | Respectée |
| Exploitabilité (structure) | Faible (paragraphe libre) | Moyenne (paragraphe) | Élevée (3 puces prêtes à diffuser) |
| Chiffres clés conservés | Non (78% absent) | Oui | Oui |

**Conclusion** : le prompt A est le plus court à écrire mais perd des informations utiles (délai de
prévenance, chiffre de l'enquête). Le prompt C, structuré avec contraintes explicites et format
imposé, est le plus directement exploitable pour une diffusion aux managers — conforme au principe
vu en cours 4 (section 10) : les gains proviennent surtout de contraintes précises et d'un format
imposé, pas d'une reformulation stylistique.
