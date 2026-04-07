---
name: attestation-hebergement
description: Genere une attestation d'hebergement a partir des informations collectees aupres de l'utilisateur.
declencheurs:
  - "attestation d'hebergement"
  - "hebergement"
  - "attester que j'heberge"
  - "certificat d'hebergement"
famille: generation
---

# Skill — Attestation d'hebergement

## Objectif

Ce Skill produit le JSON structure necessaire a la generation d'une attestation d'hebergement. L'attestation certifie qu'une personne (l'hebergeant) accueille a son domicile une ou plusieurs personnes (les heberges).

## Architecture

Ce Skill fonctionne en trois etapes sequentielles :

### Etape 1 — Collecte

Lire le fichier `DATA_SCHEMA.json` ci-joint. Parcourir les sections dans l'ordre defini par `_collectOrder`. Pour chaque champ `required` non renseigne, poser la question a l'utilisateur en suivant les `_collectHint` quand ils sont presents.

Regles de collecte :
- Commencer par l'hebergeant (section `hebergeant`, _collectOrder: 1)
- Puis le logement (section `logement`, _collectOrder: 2)
- Puis les personnes hebergees (section `heberges`, _collectOrder: 3). Demander d'abord combien de personnes sont hebergees, puis collecter les infos de chacune.
- Les conditions (_collectOrder: 4) : pour `lienParente`, demander a l'utilisateur s'il souhaite preciser le lien de parente avec chaque heberge.
- Le champ `dateAttestation` doit etre la date du jour, ne pas le demander.
- Le champ `lieuAttestation` doit etre la ville extraite de l'adresse de l'hebergeant, ne pas le demander.

### Etape 2 — Transformation

Lire le fichier `REPLACEMENTS.json` ci-joint. Pour chaque condition, appliquer la `rule` pour determiner la valeur booleenne :
- `lienParente` : selon la reponse de l'utilisateur a l'etape 1.

Verifier la coherence :
- Au moins un heberge dans le tableau.
- Tous les champs required sont renseignes.

### Etape 3 — Production du JSON

Produire l'objet JSON complet conforme au DATA_SCHEMA.json. Le presenter a l'utilisateur pour validation.

Structure de sortie attendue :

```json
{
  "meta": {
    "skillName": "attestation-hebergement",
    "skillVersion": "1.0",
    "status": "success",
    "timestamp": "...",
    "warnings": []
  },
  "data": {
    "hebergeant": { ... },
    "logement": { ... },
    "heberges": [ ... ],
    "attestation": { ... },
    "conditions": { ... }
  },
  "deliverable": {
    "type": "json",
    "target": "processor",
    "templateRef": "drive://templates/attestation-hebergement-template.docx"
  }
}
```
