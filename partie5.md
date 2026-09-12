# Partie 5 – Prompts pour les applications métier

## 1) Résumé de document

```
[RÔLE] Tu es un analyste de documents professionnels.
[TÂCHE] Résume le document suivant en maximum 250 mots.
[CONTRAINTES] Conserve toutes les informations factuelles. Identifie clairement les objectifs, les
résultats et les recommandations. N'invente aucune information absente du texte. Base-toi
uniquement sur le texte fourni.
[DONNÉES] """{document à coller ici}"""
[FORMAT] Trois sections : Objectifs / Résultats / Recommandations.
```

**Réponse (exemple appliqué à Rapport sur la satisfaction des clients fictif) :**
```
Objectifs
Améliorer la satisfaction globale des clients.
Réduire les réclamations liées aux produits et au paiement.
Résultats
75 % des clients sont satisfaits.
60 % apprécient particulièrement la rapidité de livraison.
25 % signalent des problèmes concernant l’état des produits à la réception.
15 % rencontrent des difficultés lors du paiement sur l’application mobile.
Recommandations
Renforcer l’emballage des produits avant expédition.
Corriger les problèmes techniques liés au paiement.
Assurer un suivi mensuel de la satisfaction des clients.
```

## 2) Traduction FR → EN

```
Traduis ce texte du français vers l'anglais, dans un registre professionnel. Conserve le sens et la
structure. Garde les termes techniques et noms d'entreprise tels quels. Ne résume pas, ne rajoute
aucune information, ne traduis pas littéralement les expressions idiomatiques.
Texte : """Notre nouvelle solution SaaS de gestion de stock permet aux PME de gagner un temps
précieux sur leurs inventaires."""
```
**Réponse :**
```
Our new SaaS inventory management solution enables SMEs to save valuable time on their inventory counts.
```

## 3) Classification de ticket informatique

```
Classe le ticket suivant dans une des catégories : réseau, logiciel, matériel, sécurité, accès, autre.
Réponds uniquement en JSON avec les champs categorie et justification.
Ticket : « Mon imprimante réseau ne répond plus depuis ce matin. »
```
**Réponse :**
```json
{
  "categorie": "réseau",
  "justification": "L’imprimante est connectée au réseau et ne répond plus, ce qui indique un problème de connectivité réseau."
}
```

## 4) Extraction d'informations d'une facture

```
Extrais du texte suivant : numéro_facture, date, client, montant_ht, tva, montant_ttc. Retourne
uniquement un JSON valide, avec null si une information est absente.
Facture : « Facture n°F-2026-0456 du 03/09/2026, client : Société Diallo & Fils, montant HT :
450.00€, TVA 18% : 81.00€, montant TTC : 531.00€. »
```
**Réponse :**
```json
{
  "numero_facture": "F-2026-0456",
  "date": "03/09/2026",
  "client": "Société Diallo & Fils",
  "montant_ht": 450.00,
  "tva": 81.00,
  "montant_ttc": 531.00
}
```

## 5) Email de retard de livraison

```
Rédige un email destiné à un client dont la livraison a pris du retard. Objectifs : reconnaître le
retard, présenter des excuses, expliquer la situation sans inventer de cause précise, proposer une
solution. Ton : professionnel, courtois, rassurant. Longueur maximale : 150 mots.
```
**Réponse :**
```
Madame, Monsieur,

Nous vous présentons nos sincères excuses pour le retard pris par votre livraison. Nous comprenons les désagréments que cette situation peut occasionner et regrettons de ne pas avoir pu respecter le délai initialement prévu.

Votre commande est toujours en cours de traitement, et nous mettons tout en œuvre pour que sa livraison intervienne dans les meilleurs délais.

Nous vous tiendrons informé(e) de l’évolution de la situation et vous communiquerons toute nouvelle information concernant l’acheminement de votre commande.

Nous vous remercions pour votre patience et votre compréhension, et restons à votre disposition pour toute question complémentaire.

Cordialement,

L’équipe Service Client

```
