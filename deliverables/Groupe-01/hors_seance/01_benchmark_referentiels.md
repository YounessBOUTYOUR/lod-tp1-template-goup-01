# Benchmark des référentiels externes

## Identification

- **Groupe** : Groupe 01
- **Jeu de données étudié** : Universités Publiques 2024-2025 (source officielle XLSX téléchargée depuis data.gov.ma)
- **Types d'entités retenus** : établissement, université, ville

## 1. Référentiels comparés

| Référentiel | URL | Types d'entités couverts | Intérêt potentiel | Limites observées |
| --- | --- | --- | --- | --- |
| Wikidata | [wikidata.org](https://www.wikidata.org/) | universités, certains établissements, villes | identifiants stables (QID), multilingue, riche pour l'alignement sémantique | couverture inégale sur certains établissements spécialisés, besoin de désambiguïsation manuelle |
| GeoNames | [geonames.org/countries/MA/morocco.html](https://www.geonames.org/countries/MA/morocco.html) | villes et hiérarchie géographique | identifiant géographique stable (geonameId), utile pour normaliser les localisations | ne couvre pas les établissements d'enseignement, seulement l'aspect géographique |
| DBpedia | [dbpedia.org](https://dbpedia.org/) | grandes universités, certaines villes | source linked data complémentaire, endpoint SPARQL disponible | couverture plus faible et parfois moins à jour que Wikidata |

### Vérification de couverture minimale par type d'entité

| Type d'entité retenu | Référentiel 1 | Référentiel 2 | Référentiel 3 (optionnel) | Condition "au moins 2" |
| --- | --- | --- | --- | --- |
| Etablissement | Wikidata | DBpedia | data.gov.ma (source officielle) | Respectée |
| Université | Wikidata | DBpedia | data.gov.ma (source officielle) | Respectée |
| Ville | GeoNames | Wikidata | DBpedia (partiel) | Respectée |

## 2. Critères de comparaison

Expliquez les critères utilisés pour comparer les référentiels :

Dans ce benchmark, les référentiels ont été comparés selon cinq critères opérationnels :

- **Couverture** : capacité du référentiel à contenir les entités du fichier réel (165 établissements, 12 universités, 38 villes).
- **Qualité des identifiants** : présence d'identifiants persistants et réutilisables (QID Wikidata, geonameId, URI DBpedia).
- **Précision sémantique** : clarté du type d'entité (université, école, ville), présence d'informations contextuelles et de propriétés descriptives.
- **Facilité d'appariement** : simplicité pour retrouver une entité locale via les champs disponibles dans le dataset (nom, abréviation, ville).
- **Richesse des informations disponibles** : quantité d'attributs exploitables ensuite en RDF (liens externes, hiérarchie géographique, alias, etc.).

Synthèse courte par critère :

- **Wikidata** est le meilleur compromis global pour établissements et universités.
- **GeoNames** est le meilleur choix pour normaliser les villes.
- **DBpedia** est utile en source secondaire de vérification, mais avec une couverture plus variable.

## 3. Cas d'appariement manuel

Documentez au moins `6` cas.

| Entité locale | Type | Référentiel cible | Correspondance candidate | Indices utilisés | Niveau de confiance | Décision |
| --- | --- | --- | --- | --- | --- | --- |
| Université Mohammed V - Rabat - | université | Wikidata | [Recherche candidate](https://www.wikidata.org/w/index.php?search=Universit%C3%A9+Mohammed+V+Rabat&title=Special%3ASearch&ns0=1) | nom université, ville Rabat, cohérence avec contexte national | Élevé | Retenu (appariement validé manuellement sur résultat principal) |
| Université Hassan II - Casablanca - | université | Wikidata | [Recherche candidate](https://www.wikidata.org/w/index.php?search=Universit%C3%A9+Hassan+II+Casablanca&title=Special%3ASearch&ns0=1) | nom, ville Casablanca, établissement de grande notoriété | Élevé | Retenu |
| Ecole Nationale Supérieure d'Informatique et d'Analyse des Systèmes Rabat (ENSIAS Rabat) | établissement | Wikidata | [Recherche candidate](https://www.wikidata.org/w/index.php?search=ENSIAS+Rabat&title=Special%3ASearch&ns0=1) | abréviation ENSIAS, ville Rabat, site institutionnel | Moyen à élevé | Retenu avec vérification du rattachement à l'université mère |
| Rabat | ville | GeoNames | [Recherche candidate](https://www.geonames.org/search.html?q=Rabat&country=MA) | exactitude du toponyme, pays MA, forte fréquence dans le dataset | Élevé | Retenu |
| Kénitra | ville | GeoNames | [Recherche candidate](https://www.geonames.org/search.html?q=Kenitra&country=MA) | variante d'accent (Kénitra/Kenitra), pays MA, présence de plusieurs établissements | Élevé | Retenu |
| Faculté Polydisciplinaire Kssar El Kébir | établissement | DBpedia | [Recherche candidate](https://lookup.dbpedia.org/index.html?query=Kssar+El+K%C3%A9bir) | nom établissement + ville, test de couverture DBpedia | Faible à moyen | Non retenu en appariement direct (couverture insuffisante, candidat non fiable) |

## 4. Synthèse

- Quel référentiel paraît le plus utile pour chaque type d'entité ?
- Quels cas restent ambigus ?
- Quels champs du dataset aident le plus à l'appariement ?

Réponses :

- **Référentiel le plus utile par type d'entité** :
  - Université : **Wikidata**
  - Etablissement : **Wikidata** (puis DBpedia en complément)
  - Ville : **GeoNames**
- **Cas ambigus** :
  - établissements rattachés à une université (risque de confusion entre entité autonome et composante interne)
  - villes avec variantes orthographiques/accents (Kénitra, Fès, Meknès)
  - établissements très spécifiques ou récents moins bien couverts dans DBpedia
- **Champs les plus utiles pour l'appariement** :
  - `Etablissement`
  - `Etablissement (Abr)`
  - `Université`
  - `Ville`
  - `Adresse` (en désambiguïsation)
