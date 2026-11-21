# OTTO – Multi-Objective Recommender System

Système de recommandation pour la compétition Kaggle
[OTTO – Multi-Objective Recommender System](https://www.kaggle.com/c/otto-recommender-system).

## Objectif

À partir des événements d'une session e-commerce (clicks, carts, orders),
prédire jusqu'à 20 produits pour chaque type d'événement futur.
Métrique : Recall@20 pondéré (clicks 10 %, carts 30 %, orders 60 %).

## Données

- Environ 216 millions d'événements en entraînement et 6,9 millions en test (1,67 million de sessions).
- Version optimisée en parquet : *Otto Full Optimized Memory Footprint* (Radek Osmulski, Kaggle).
- Les données ne sont pas incluses dans ce dépôt.

## Approche

1. Construction d'une matrice de co-visitation : produits apparus dans une même session à moins de 24 h d'intervalle.
2. Score de chaque produit candidat selon la récence de l'événement et le type d'événement (clicks, carts, orders), avec normalisation des poids des voisins.
3. Complétion avec les produits les plus cliqués lorsque moins de 20 candidats sont disponibles.
4. Génération du fichier `submission.csv` (3 lignes par session : clicks, carts, orders).

## Résultats

| Version | Description | Score privé | Score public |
|---|---|---|---|
| V1 | Co-visitation, 300 000 sessions | 0.51956 | 0.51882 |
| V3 | Co-visitation, 1 M sessions + sessions de test + poids par type d'événement | 0.53460 | 0.53533 |

## Structure

- `otto_covisitation.ipynb` : notebook complet (chargement, co-visitation, prédictions, soumission)

## Exécution

Le notebook s'exécute sur Kaggle avec deux entrées : la compétition OTTO
et le dataset *Otto Full Optimized Memory Footprint*.

## Pistes d'amélioration

- Validation locale avec Recall@20
- Word2Vec pour les produits similaires
- Re-ranking avec LightGBM

## Auteure

Chaymae Hanida – Master MLAIM, USMBA Fès
