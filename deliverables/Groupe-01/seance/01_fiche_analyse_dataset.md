# Fiche d'analyse du jeu de données

## Identification

- **Groupe** : 01
- **Date** : 09-04-2026
- **Nom du jeu de données** : higher_education_sample
- **Source / producteur** : Ministère de l'Enseignement Supérieur du Maroc
- **URL de la source** : https://data.gov.ma
- **Domaine métier** : Enseignement supérieur au Maroc

## Description générale

- **Objectif du jeu de données** : Ce jeu de données sert à référencer et décrire les établissements d'enseignement supérieur au Maroc pour permettre à quelqu'un de les identifier, les localiser, et les comparer.
- **Format(s) disponible(s)** : CSV
- **Langue(s)** : Français et Anglais
- **Licence** : Aucune mentionnée
- **Fréquence de mise à jour** : Inconnue
- **Unité d'observation** : Chaque ligne représente un établissement d'enseignement supérieur.
- **Granularité des enregistrements** : Granularité fine

## Structure du jeu de données

| Champ / colonne | Signification | Exemple de valeur | Observation |
| --- | --- | --- | --- |
| record_id | Identifiant numérique unique de l'enregistrement | 1 | Simple entier séquentiel, pas un vrai identifiant stable |
| institution_name | Nom complet de l'établissement | Ecole Nationale Superieure d'Informatique... | Pas d'accents, mélange français/anglais |
| short_name | Sigle ou abréviation de l'établissement | ENSIAS | Utile comme clé candidate mais pas toujours unique |
| city | Ville où se trouve l'établissement | Rabat | Valeurs non normalisées, pas de code GeoNames |
| country | Pays de l'établissement | Morocco | Toujours "Morocco", pas de code ISO (MA ou MAR) |
| website | URL du site officiel | https://www.ensias.um5.ac.ma | Peut changer, instable comme identifiant |
| institution_type | Type d'établissement | public school | Vocabulaire non contrôlé, valeurs inconsistantes |
| main_field | Domaine principal d'enseignement | computer science | Vocabulaire libre, pas de thésaurus de référence |
| year_created | Année de création de l'établissement | 1992 | Format simple et cohérent |
| portal_hint | Portail Open Data suggéré pour la source | data.gov.ma | Même valeur pour tous les enregistrements |

## Évaluation "Open Data"

| Critère | Observation | Score / 5 |
| --- | --- | --- |
| Accessibilité |  |  |
| Réutilisabilité |  |  |
| Documentation |  |  |
| Format exploitable |  |  |
| Présence d'une licence |  |  |

## Évaluation "Linked Data readiness"

| Point observé | Oui / Non / Partiel | Commentaire |
| --- | --- | --- |
| Identifiants stables pour les enregistrements |  |  |
| Entités clairement distinguables |  |  |
| Valeurs normalisées |  |  |
| Informations géographiques exploitables |  |  |
| Possibilité de lien vers des référentiels externes |  |  |
| Présence de clés candidates plausibles |  |  |
| Présence de codes ou nomenclatures réutilisables |  |  |

## Maturité "5 étoiles"

| Niveau | Atteint ? | Justification |
| --- | --- | --- |
| 1 étoile : données disponibles sur le Web |  |  |
| 2 étoiles : données structurées |  |  |
| 3 étoiles : format non propriétaire |  |  |
| 4 étoiles : usage d'URI pour identifier les choses |  |  |
| 5 étoiles : liens vers d'autres données |  |  |

## Clés candidates et identifiants

| Objet ou entité cible | Champ(s) candidat(s) | Fiabilité | Limites | Recommandation |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |

## Normalisation préalable nécessaire

| Champ | Problème observé | Impact pour le LOD | Action recommandée |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

## Qualité des données

- **Forces observées** :
- **Faiblesses observées** :
- **Ambiguïtés ou doublons potentiels** :
- **Champs manquants pour une meilleure interconnexion** :
- **Risque principal pour une future mise en relation** :

## Conclusion courte

En `8 à 12` lignes, expliquez si ce jeu de données constitue une bonne base pour une future publication en données ouvertes liées, à quelles conditions, et quelles actions techniques devraient être menées en priorité.
