# Cadrage : TestRank

Sélection et priorisation prédictives de tests pour projets Java / Maven.

## Problème

Les suites de tests en intégration continue sont longues, et la plupart des tests ne détectent rien pour un changement donné. L'objectif est d'exécuter en premier les tests les plus susceptibles d'échouer, afin d'obtenir un retour plus rapide, et de pouvoir ne lancer qu'un sous-ensemble quand c'est acceptable.

Travaux connexes : Develocity Predictive Test Selection (solution commerciale pour Gradle et Maven), l'article de Facebook sur la sélection prédictive de tests, et le benchmark RTPTorrent. Ce projet est une alternative open-source, transparente et évaluée de façon reproductible, pas une nouveauté de recherche.

## Objectifs mesurables

| # | Objectif | Valeur cible |
|---|---|---|
| O1 | Rappel des échecs en exécutant au plus X % des tests | 95 % de rappel avec X = *à remplir avec les résultats réels* |
| O2 | Amélioration de l'APFD par rapport à la meilleure baseline | *à remplir* |
| O3 | Surcoût ajouté par le plugin à un build | *à remplir (en secondes)* |
| O4 | Généralisation : résultats sur un projet jamais vu à l'entraînement | *à remplir* |

Les valeurs entre étoiles sont remplies uniquement avec des mesures réelles. Aucune valeur n'est fixée à l'avance.

## Hypothèses

- H1 : l'historique d'échecs récents d'un test est prédictif de ses échecs futurs.
- H2 : la proximité entre les fichiers modifiés et un test (nom, package, co-échecs passés) est prédictive.
- H3 : un modèle combinant ces signaux bat des heuristiques simples.
- H4 : un modèle entraîné sur certains projets garde une partie de ses performances sur un projet nouveau.

## Métriques

- APFD (Average Percentage of Faults Detected) : `1 − (TF1 + … + TFm) / (n·m) + 1/(2n)`.
- Rappel des échecs en exécutant 10 %, 20 % et 30 % des tests.
- Pourcentage de tests à exécuter pour atteindre 95 % de rappel.
- Temps jusqu'au premier échec.
- Intervalles de confiance par bootstrap, résultats rapportés par projet.

## Baselines

1. Ordre original de la suite.
2. Ordre aléatoire (moyenne sur plusieurs tirages).
3. `failedfirst` de Maven Surefire.
4. Tests les plus échoués récemment.
5. Heuristique par nom de fichier (`Foo` / `FooTest`).

## Données

- Source principale : RTPTorrent, 3 à 5 projets choisis parmi les 20 après exploration (critère : assez d'échecs réels).
- Source complémentaire : 2 dépôts Maven choisis pour tester le plugin de bout en bout (exécution de commits successifs dans Docker, lecture des rapports Surefire).
- Option : fautes injectées avec PIT, toujours rapportées séparément des échecs réels.
- Découpage temporel uniquement (entraînement sur le passé, test sur le futur). Aucune feature n'utilise de données postérieures au commit.

## Livrables

1. Pipeline de données et de features reproductible (DVC, MLflow).
2. Modèle de classement et rapport d'évaluation.
3. Service de ranking (FastAPI).
4. Plugin Maven (ordre et filtre des tests, mode sécurité).
5. Backend Spring Boot et dashboard React.
6. Boucle MLOps : réentraînement planifié, mode ombre champion/challenger, surveillance de la dérive.

## Hors périmètre

- Sélection au niveau méthode (le niveau classe de test d'abord).
- Projets Maven multi-modules.
- Autres langages et autres outils de build.
- Déploiement en production réelle.

## Risques et parades

| Risque | Parade |
|---|---|
| Peu d'échecs réels dans certains projets | Choisir les projets après exploration, compléter avec des fautes injectées rapportées à part |
| Tests instables qui polluent les labels | Relancer les échecs, calculer un score d'instabilité, exclure ou pondérer |
| Commits qui ne compilent pas | Images Docker avec plusieurs JDK, mesurer et documenter le taux de commits exploitables |
| Fuite temporelle dans les features | Test automatique qui vérifie les dates, découpage temporel strict |
| Écart entre entraînement et service | Un seul module de features, partagé |
| Projet trop ambitieux | Chemin minimal : étapes 0 à 5 avec seulement le mode de réordonnancement |

## Plan

| Étape | Contenu | Durée estimée |
|---|---|---|
| 0 | Cadrage et préparation | 8 h |
| 1 | Données | 25 h |
| 2 | Features | 12 h |
| 3 | Modèle et évaluation hors ligne | 15 h |
| 4 | Service de ranking et registry | 12 h |
| 5 | Plugin Maven | 15 h |
| 6 | Backend et dashboard | 15 h |
| 7 | Boucle MLOps | 15 h |
| 8 | Évaluation finale | 12 h |
| 9 | Finalisation et publication | 10 h |
