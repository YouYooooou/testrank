# Journal de bord : TestRank

Règle : j'écris ici chaque jour ce que j'ai fait, ce qui a marché, ce qui a échoué et pourquoi. Je note mes chiffres réels au moment où je les obtiens.

---

## Fiches de lecture (Étape 0, jour 2)

Pour chaque lecture : 5 lignes maximum par rubrique. Les lignes marquées « à compléter » sont à écrire avec mes propres mots après avoir lu.

### 1. RTPTorrent : An Open-source Dataset for Evaluating Regression Test Prioritization (MSR 2020)

**Lien :** page MSR 2020 de l'article (recherche « RTPTorrent MSR 2020 »)

**Ce qu'ils font (repères déjà identifiés)**
- Un jeu de données public de 20 projets Java open-source, avec des résultats de tests issus de builds CI automatisés sur environ 9 ans.
- Il sert de benchmark pour comparer des méthodes de priorisation de tests.
- À compléter : comment les données sont construites (source CI, granularité des tests).
- À compléter : la liste des projets et leurs tailles (nombre de builds, de tests, d'échecs).
- À compléter : les baselines et métriques qu'ils fournissent ou utilisent.

**Ce que je reprends**
- À compléter.

**Ce que je ferai différemment**
- À compléter.

**Questions à vérifier en lisant**
- [ ] Quel est le format des fichiers et comment les charger ?
- [ ] Quelles conditions d'utilisation (licence) ?
- [ ] Quels projets ont le plus d'échecs réels ?

---

### 2. Develocity Predictive Test Selection (gradle.com)

**Lien :** gradle.com, page « Predictive Test Selection » et son manuel utilisateur

**Ce qu'ils font (repères déjà identifiés)**
- Un modèle de ML appris sur l'historique des changements de code et des résultats de tests, qui sélectionne les tests pertinents pour un changement.
- Compatible Gradle et Maven, pour les tests exécutés sur la JUnit Platform.
- Ils filtrent les résultats de tests instables de l'entraînement.
- Un simulateur compare les prédictions aux résultats réels avant d'activer la fonction.
- Des profils de sélection permettent de régler le compromis vitesse / confiance, et un mode « remaining tests » existe (à relire dans le manuel).

**Ce que je reprends**
- À compléter (idées : simulateur avant activation, filtrage des tests instables, profils de sélection).

**Ce que je ferai différemment**
- À compléter (idées : projet open-source, évaluation reproductible sur RTPTorrent, explications SHAP, mode ombre champion/challenger).

**Questions à vérifier en lisant**
- [ ] Comment fonctionne exactement le mode « remaining tests » ?
- [ ] Quelles informations le plugin envoie-t-il au serveur ?
- [ ] Quelles limites sont indiquées (compatibilité, cas non supportés) ?

---

### 3. Facebook : Predictive Test Selection (Machalica et al., ICSE-SEIP 2019)

**Lien :** à rechercher (titre : « Predictive Test Selection », arXiv ou ICSE-SEIP 2019)

**Ce qu'ils font**
- À compléter : le problème posé et l'approche du modèle.
- À compléter : les features utilisées (changement, test, historique).
- À compléter : comment ils définissent et mesurent le rappel des échecs.
- À compléter : le compromis annoncé entre tests exécutés et échecs détectés.
- À compléter : comment ils traitent les tests instables.

**Ce que je reprends**
- À compléter.

**Ce que je ferai différemment**
- À compléter.

**Questions à vérifier en lisant**
- [ ] Quelle est leur métrique principale et comment la reproduire ?
- [ ] Quelles features puis-je reconstruire avec des données publiques ?
- [ ] Quelles limites reconnaissent-ils ?

---

## Entrées quotidiennes

### 09/10/2026 : Étape 0, mise en place
- Fait : environnement vérifié (Java 21, Maven 3.9.10, Python 3.11, Git), dépôt GitHub créé, environnement virtuel `.venv` créé.
- Problèmes rencontrés : `python3` inconnu sous Windows (utiliser `py` ou `python`), authentification GitHub pour `git push`, mauvais dépôt Git détecté dans un dossier parent.
- À faire ensuite : finir les fiches de lecture, puis écrire `docs/cadrage.md`.

### JJ/MM/AAAA : titre
- Fait :
- Problèmes rencontrés :
- Chiffres relevés :
- À faire ensuite :
