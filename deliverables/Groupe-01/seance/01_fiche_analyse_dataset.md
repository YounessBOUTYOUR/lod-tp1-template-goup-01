# Fiche d'analyse du jeu de données

## Identification

- **Groupe** : 01
- **Date** : 18-04-2026
- **Nom du jeu de données** : Universités Publiques 2024-2025
- **Source / producteur** : Ministère de l'Enseignement Supérieur du Maroc
- **URL de la source** : [data.gov.ma - etablissement du superieur public](https://data.gov.ma/data/dataset/etablissements-de-l-enseignement-superieur-universitaire-public-ouverts)
- **Domaine métier** : Enseignement supérieur au Maroc

## Description générale

- **Objectif du jeu de données** : Lister les établissements de l'enseignement supérieur universitaire public ouverts au titre de l'année 2024-2025.
- **Format(s) disponible(s)** : XLSX
- **Langue(s)** : Français et Arabe
- **Licence** : ODbL (Open Data Commons Open Database License)
- **Fréquence de mise à jour** : Non précisée explicitement (métadonnées mises à jour le 19 février 2025)
- **Unité d'observation** : Chaque ligne représente un établissement d'enseignement supérieur.
- **Granularité des enregistrements** : Granularité fine

## Structure du jeu de données

| Champ / colonne | Signification | Exemple de valeur | Observation |
| --- | --- | --- | --- |
| Université | Nom de l'université de rattachement (français) | Université Mohammed V - Rabat - | 12 valeurs uniques, ponctuation hétérogène |
| Etablissement | Nom de l'établissement (français) | Faculté des Sciences Rabat | Très informatif mais sensible aux variations d'écriture |
| Etablissement (Abr) | Abréviation de l'établissement | FS Rabat | Champ candidat utile pour identifiant local |
| Effectifs des Etudiants 2023-2024 | Volume étudiants | 9895 | Majoritairement numérique, quelques valeurs non numériques (ex: -) |
| المؤسسة | Nom de l'établissement (arabe) | كلية العلوم الرباط | Riche sémantiquement, nécessite normalisation Unicode |
| الجامعة | Nom de l'université (arabe) | جامعة محمد الخامس  - الرباط- | Utile pour interopérabilité multilingue |
| Ville | Localisation de l'établissement | Rabat | 38 villes uniques, pas de code géographique externe |
| Adresse | Adresse postale de l'établissement | 4 avenue Ibn Battouta B.P 1014 – Rabat | Forte variabilité de forme |
| Téléphone | Contact téléphonique | 537771834 | Formats hétérogènes, 10 valeurs manquantes |
| Fax | Contact fax | 537774261 | Formats hétérogènes, 13 valeurs manquantes |

## Évaluation "Open Data"

| Critère | Observation | Score / 5 |
| --- | --- | --- |
| Accessibilité | Ressource accessible en ligne via portail national open data | 5 |
| Réutilisabilité | Données tabulaires riches, mais besoin de normalisation avant réutilisation intensive | 4 |
| Documentation | Description correcte sur le portail, schéma implicite | 3 |
| Format exploitable | XLSX structuré, exploitable mais moins direct qu'un CSV/API | 4 |
| Présence d'une licence | Licence ODbL explicitement indiquée | 5 |

## Évaluation "Linked Data readiness"

| Point observé | Oui / Non / Partiel | Commentaire |
| --- | --- | --- |
| Identifiants stables pour les enregistrements | Non | Pas d'ID pérenne officiel par établissement |
| Entités clairement distinguables | Oui | Université, établissement et ville sont bien séparés |
| Valeurs normalisées | Partiel | Données riches mais formats et ponctuation variables |
| Informations géographiques exploitables | Partiel | Champ Ville présent mais sans code GeoNames/ISO |
| Possibilité de lien vers des référentiels externes | Oui | Appariement possible vers Wikidata et GeoNames |
| Présence de clés candidates plausibles | Oui | Etablissement (Abr) + Ville + Université |
| Présence de codes ou nomenclatures réutilisables | Non | Pas de code territorial ou typologie normalisée |

## Maturité "5 étoiles"

| Niveau | Atteint ? | Justification |
| --- | --- | --- |
| 1 étoile : données disponibles sur le Web | Oui | Jeu de données publié en accès web |
| 2 étoiles : données structurées | Oui | Structure tabulaire claire |
| 3 étoiles : format non propriétaire | Non | XLSX reste un format propriétaire |
| 4 étoiles : usage d'URI pour identifier les choses | Non | Pas d'URI natives dans la source |
| 5 étoiles : liens vers d'autres données | Non | Aucun lien externe intégré nativement |

## Clés candidates et identifiants

| Objet ou entité cible | Champ(s) candidat(s) | Fiabilité | Limites | Recommandation |
| --- | --- | --- | --- | --- |
| Etablissement | Etablissement (Abr) + Ville | Moyenne à élevée | Risque de collision hors périmètre local | Ajouter Université ou suffixe anti-collision |
| Université | Université | Élevée | Variantes de ponctuation et espaces | Normaliser le libellé et associer QID Wikidata |
| Ville | Ville | Élevée | Variantes d'accents et translittération | Mapper chaque ville vers geonameId |

## Normalisation préalable nécessaire

| Champ | Problème observé | Impact pour le LOD | Action recommandée |
| --- | --- | --- | --- |
| Université | Espaces/ponctuation hétérogènes | Risque de faux doublons sémantiques | Trim + harmonisation de ponctuation |
| Etablissement | Variantes orthographiques et longueurs hétérogènes | Appariement externe moins fiable | Normaliser Unicode + dictionnaire d'alias |
| Ville | Variantes accentuées/non accentuées | Désambiguïsation géographique incomplète | Forme canonique + variante sans accents |
| Effectifs des Etudiants 2023-2024 | Présence de valeurs non numériques | Calculs statistiques et validation dégradés | Convertir en entier, marquer les manquants |
| Téléphone / Fax | Formats multiples + manquants | Vérification et matching technique limités | Nettoyage format + indicateur de complétude |

## Qualité des données

- **Forces observées** : couverture nationale large, structure tabulaire claire, présence bilingue français/arabe.
- **Faiblesses observées** : absence d'identifiant pérenne, hétérogénéité de formats texte et contacts.
- **Ambiguïtés ou doublons potentiels** : confusion possible entre composantes universitaires et entités autonomes.
- **Champs manquants pour une meilleure interconnexion** : type d'établissement normalisé, code ville/région, identifiant administratif officiel.
- **Risque principal pour une future mise en relation** : faux appariement dû aux variations de libellés si la normalisation n'est pas appliquée.

## Conclusion courte

En `8 à 12` lignes, expliquez si ce jeu de données constitue une bonne base pour une future publication en données ouvertes liées, à quelles conditions, et quelles actions techniques devraient être menées en priorité.

Le dataset officiel constitue une base solide pour une ouverture liée, car il couvre un périmètre national (165 établissements, 12 universités) avec une structure exploitable.
La richesse descriptive des colonnes permet de distinguer des entités centrales pertinentes (établissement, université, ville).
Cependant, la publication actuelle n'est pas encore prête pour un alignement automatique fiable.
La principale limite est l'absence d'identifiants techniques stables et de codes géographiques normalisés.
Le format XLSX nécessite aussi une étape de transformation avant pipeline LOD.
La priorité technique est de normaliser les libellés (université, établissement, ville) et de gérer explicitement les valeurs manquantes.
Ensuite, il faut construire des identifiants locaux cohérents, puis les aligner vers des référentiels externes.
Wikidata est adapté aux institutions, GeoNames aux villes, et DBpedia peut servir de source secondaire.
Avec ces prérequis, ce jeu de données peut devenir une bonne base pour TP2 et une future publication en RDF.
