# Plan de normalisation et d'identification

## 1. Entités prioritaires

| Type d'entité | Pourquoi est-il prioritaire ? | Identifiant actuel | Stratégie proposée |
| --- | --- | --- | --- |
| Etablissement | C'est l'entité principale du jeu de données (165 lignes) et la plus fine pour un futur graphe RDF | Pas d'identifiant technique explicite, uniquement `Etablissement (Abr)` + nom + ville | Utiliser un identifiant composite canonique basé sur `Etablissement (Abr)` + `Ville` + préfixe pays (ex: ma-etab-emi-rabat) |
| Université | Permet de structurer le graphe (relation établissement -> université) | Valeur textuelle `Université` sans code stable | Créer un identifiant normalisé de l'université (slug du nom) et lier chaque établissement à sa ressource université |
| Ville | Nécessaire pour les liens géographiques externes et la désambiguïsation | Valeur textuelle `Ville` sans code externe | Mapper chaque ville à un identifiant GeoNames, puis stocker aussi la forme locale normalisée |

## 2. Champs à normaliser

| Champ | Problème observé | Règle de normalisation proposée | Impact attendu |
| --- | --- | --- | --- |
| `Université` | Variantes de ponctuation et espaces de fin (ex: " - "), encodage mixte | trim, réduction des espaces, suppression des suffixes décoratifs, conservation de la forme officielle | Réduction des faux doublons d'universités |
| `Etablissement` | Noms longs, variations orthographiques, ponctuation hétérogène | trim, normalisation Unicode NFC, table d'alias (forme officielle et forme normalisée) | Appariement plus robuste vers Wikidata/DBpedia |
| `Etablissement (Abr)` | Pas de problème majeur, mais possible ambiguïté à l'échelle nationale | uppercase forcé, suppression d'espaces doubles, contrôle d'unicité intra-université | Identifiant court exploitable pour URI |
| `Ville` | Accents et variantes possibles (Kénitra/Kenitra, Fès/Fes) | dictionnaire de formes canoniques + variante sans accents pour matching | Désambiguïsation géographique fiable |
| `Effectifs des Etudiants 2023-2024` | Valeurs non numériques présentes (ex: "-") | conversion numérique, mapping "-" vers valeur manquante, typage entier | Qualité statistique et exploitation analytique |
| `Adresse` | Forte hétérogénéité rédactionnelle (abréviations, ponctuation, ordre) | normalisation légère (espaces, ponctuation), sans perte d'information textuelle | Recherche textuelle et appariement assisté améliorés |
| `Téléphone` / `Fax` | Formats multiples (avec ou sans indicatif, espaces, slash) + valeurs manquantes | format canonique E.164 local si possible, sinon forme nettoyée + statut de validité | Meilleure qualité de contact et contrôle d'intégrité |
| المؤسسة / الجامعة | Sensibles à la normalisation Unicode et aux variantes graphiques | normalisation Unicode NFC, conservation de la graphie source + forme indexée | Interopérabilité multilingue préservée |

## 3. Stratégie d'identifiants

| Entité cible | Base de construction envisagée | Risque | Recommandation |
| --- | --- | --- | --- |
| Etablissement | `ma-etab-{abbr-normalisee}-{ville-normalisee}` | collision possible si même abréviation dans deux villes proches ou renommage | ajouter un suffixe court stable (hash du nom normalisé) si collision détectée |
| Université | `ma-univ-{nom-universite-normalise}` | renommage institutionnel dans le temps | stocker aussi un identifiant externe (Wikidata QID) quand disponible |
| Ville | `geonames:{id}` (si appariement validé), sinon `ma-city-{ville-normalisee}` | dépendance à la couverture GeoNames et ambiguïtés toponymiques | conserver double clé: identifiant local + référence GeoNames vérifiée |

## 4. Risques et limites

- Quels champs sont trop faibles pour servir d'identifiant ?
- Quelles collisions ou ambiguïtés sont possibles ?
- Quelles informations supplémentaires seraient nécessaires ?

Réponses :

- **Champs trop faibles pour servir d'identifiant seuls** :
  - `Adresse` (trop longue, sujette à changement)
  - `Téléphone` et `Fax` (manquants ou instables)
  - `Effectifs des Etudiants 2023-2024` (valeur métier non identifiante)
- **Collisions et ambiguïtés possibles** :
  - collision d'abréviations si extension future du périmètre
  - confusion entre établissement composant et université mère
  - variations d'accents et translittération arabe/français
- **Informations supplémentaires nécessaires** :
  - un identifiant administratif officiel pérenne par établissement
  - le type explicite d'établissement (faculté, école, institut) dans un champ dédié
  - un code territorial officiel pour la ville/région
  - un historique de changements de nom pour la traçabilité
