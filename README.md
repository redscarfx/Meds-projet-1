# Évaluation expérimentale de modèles de Question Answering tabulaire : TAPEX et TAPAS

Ce dépôt contient l’ensemble du code, des analyses et des expérimentations menées dans le cadre d’un projet consacré à l’évaluation comparative des modèles **TAPEX** (Liu et al., 2022) et **TAPAS** (Herzig et al., 2020) sur des tâches de *Question Answering* (QA) appliquées à des données tabulaires.  
L’étude repose principalement sur le dataset de référence **WikiTableQuestions**, dont les particularités structurelles et sémantiques permettent de mesurer finement la capacité de généralisation des modèles vers des tables et des entités inédites.

---

## 📌 Objectifs du projet

- Analyser les performances de TAPEX et TAPAS sur des questions portant sur des tables semi-structurées.
- Étudier la sensibilité des modèles aux variations thématiques, structurelles et lexicales.
- Examiner les comportements selon différents types d’opérations tabulaires : extraction, superlatifs, comparatifs, agrégations, opérations arithmétiques, etc.
- Évaluer la robustesse sur des données vues et non vues.
- Mesurer les temps d’inférence pour déterminer l’adéquation à des usages pratiques.

---

## 📂 Contenu du dépôt

- `src/` : scripts d’inférence, de prétraitement des tables, normalisation des prédictions.
- `analysis/` : notebooks d’analyse exploratoire, clustering sémantique, visualisations (UMAP, wordclouds, distributions).
- `models/` : chargement et configuration des modèles TAPAS et TAPEX via HuggingFace.
- `results/` : résultats expérimentaux, matrices de performances, tableaux comparatifs.
- `rapport/` : rapport final au format PDF (rédigé en LaTeX).

---

## 🗃️ Dataset : WikiTableQuestions

Le corpus comporte plus de 22 000 paires question–réponse, réparties sur plus de 2 000 tables extraites de Wikipédia.  
Les jeux de données incluent notamment :
- un ensemble d'entraînement,
- un ensemble *pristine-unseen* (tables non vues lors de l’entraînement),
- un ensemble *pristine-seen*.

Le dataset couvre une grande variété d’opérations logiques et arithmétiques, rendant l’analyse particulièrement riche.

---

## 🧪 Méthodologie expérimentale

### Prétraitements
- normalisation textuelle,
- uniformisation des formats numériques et pourcentages,
- linearisation contrôlée des tables pour les modèles.

### Évaluation
- **Exact Match Accuracy (EMA)** pour les réponses singulières,
- gestion expérimentale des réponses multiples,
- analyses par :
  - cluster sémantique,
  - type d’opération,
  - cardinalité de la réponse.

### Clustering sémantique
Les embeddings (SentenceTransformer, *all-MiniLM-L6-v2*) ont été réduits via UMAP puis organisés par DBSCAN.  
Cette approche permet :
- d’identifier les thématiques dominantes (sport, cinéma, politique, statistiques, etc.),
- d’étudier la stabilité des modèles par groupe de questions.

---

## 🧾 Résultats principaux

- **TAPEX** surpasse nettement **TAPAS** sur l’ensemble des tâches, notamment sur les opérations nécessitant du raisonnement computationnel (agrégations, calculs arithmétiques).
- TAPAS demeure compétitif lorsqu’il s’agit d’extraction directe ou de superlatifs simples.
- Les performances chutent sur les clusters impliquant une forte variabilité lexicale (noms propres, entités rares).
- Les opérations complexes révèlent des limites structurelles de TAPAS.
- Temps d’inférence moyens :
  - TAPEX : **≈ 0.13 s** / question  
  - TAPAS : **≈ 0.156 s** / question  

---

## 🔭 Perspectives

- Étude de la robustesse sous perturbations contrôlées (reformulations, permutations de lignes/colonnes).
- Intégration de mécanismes de raisonnement multi-étapes ou symbolique.
- Usage de RLHF ou de supervision plus fine pour les questions à réponses multiples.
- Exploration de modèles plus récents (TAPAS-v2, tableaux hybrides texte–graphe, models de type TUTA).

---

## 👤 Auteurs

- *Yacine Chettab*  
- *Titouan Guérin*  
Encadrement : **Olivier Schwander**

---

## 📄 Licence

Projet académique — reproduction autorisée à des fins non commerciales.
