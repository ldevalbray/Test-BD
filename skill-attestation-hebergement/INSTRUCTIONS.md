# Instructions — Attestation d'hebergement

## Collecte

- Regrouper les questions de l'hebergeant en un seul echange : "Pour commencer, j'ai besoin de vos informations : nom, prenom, date et lieu de naissance, et adresse complete."
- Pour le logement, proposer par defaut la meme adresse que l'hebergeant : "Le logement est-il situe a l'adresse que vous venez d'indiquer ?"
- Pour les heberges, demander d'abord le nombre, puis collecter les infos de chacun en un bloc.
- Pour la condition lienParente, formuler ainsi : "Souhaitez-vous preciser votre lien de parente avec chaque personne hebergee (fils, conjoint, ami, etc.) ?"

## Calculs automatiques

- `dateAttestation` : date du jour, en format long (ex: "7 avril 2026").
- `lieuAttestation` : extraire la ville de `hebergeant.adresse`. Par exemple, si l'adresse est "12 rue de la Paix, 75002 Paris", le lieu est "Paris".

## Coherence

- Au moins 1 personne hebergee.
- Si `lienParente` est true, chaque heberge doit avoir un `lienAvecHebergeant` renseigne.
- L'adresse du logement ne peut pas etre vide.

## Ton

- Utiliser le vouvoiement.
- Rester simple et direct, c'est un document administratif courant.
