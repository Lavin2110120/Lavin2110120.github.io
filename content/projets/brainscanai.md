---
title: "BrainScanAI : Classification d'IRM cérébrales par apprentissage semi-supervisé"
date: 2026-09-28
draft: false
tags: ["Deep Learning", "PyTorch", "Semi-Supervised", "UMAP", "Computer Vision", "MLOps"]
categories: ["Data Science", "Santé"]
summary: "Exploitation de 93 % de données IRM non étiquetées grâce à l'extraction de caractéristiques via ResNet-50, UMAP et aux algorithmes de Label Propagation."
cover:
  image: "/images/projects/brainscanai-irm-pictures.png"
  alt: "Projection UMAP 2D des caractéristiques ResNet-50"
github: "https://github.com/Lavin2110120/Lavin2110120.github.io"
---

## Contexte & Enjeu Clinique

En imagerie médicale, l'annotation de données exige un temps expert considérable de la part des radiologues. Ce projet répond à une contrainte forte de sobriété d'annotation :

* **Données disponibles** : 1 506 IRM au total.
* **Jeu étiqueté** : 100 images seulement (50 cas sains, 50 cas tumoraux).
* **Données non étiquetées** : 1 406 images (soit **93,4 % du jeu global**).

L'objectif principal est de maximiser le **rappel (Recall)** pour éradiquer les faux négatifs (non-détection de tumeurs) tout en propageant automatiquement les étiquettes aux données brutes.

---

## Pipeline Technique & Architecture

Le projet est structuré sous forme de package Python propriétaire (`brainscanai`) installable en mode éditable (`pip install -e .`).


[IRM Brutes] > [Filtre Médian 3x3] > [ResNet-50 PyTorch] > [Embeddings (2048d)]

[Matrice de Confusion] < [Label Propagation / Spreading] < [Projection UMAP]

## Prétraitement de l'imageFiltrage spatial 

Filtrage spatial : application d'un filtre médian 3x3 via OpenCV pour supprimer le bruit de numérisation tout en préservant le contraste des bordures tumorales.
Normalisation : redimensionnement en 224x224 et alignement sur les statistiques ImageNet.

## Feature Extraction (PyTorch)

Extraction des repères visuels denses via le backbone d'un réseau ResNet-50 pré-entraîné (suppression de la couche de classification finale pour obtenir des vecteurs de dimension 2048).

## Clustering & Réduction de dimension

Analyse comparative de la séparabilité spatiale des embeddings via UMAP, PCA et t-SNE.

![Projection UMAP 2D des caractéristiques ResNet-50](/images/projects/brainscanai-umap.png)

Score ARI (Adjusted Rand Index) : Ajoute la valeur brute (ARI max de 0,514) pour quantifier scientifiquement la qualité de la séparation des structures tumorales sans supervision, avant même d'appliquer la propagation d'étiquettes.

## Apprentissage Semi-Supervisé

Implémentation des algorithmes Label Propagation et Label Spreading (scikit-learn) pour classifier les 1 406 images non annotées à partir des 100 ancres initiales.

![Distribution du Recall et du F1-Score sur 25 folds](/images/projects/brainscanai-cv-boxplot.png)

Résultats & Métriques
Modèle / Approche               Rappel (Recall)    F1-Score        Données annotées requises 
BrainScanAI (Label Spreading)     98,2 %             0,96                  6,6 %

Validation croisée (25-folds) : Précise que les résultats ne reposent pas sur un split unique mais sur une CV 25-folds. Mentionne que Self-Training garantit un rappel stable au-dessus du seuil clinique de la Definition of Done (85 %), alors que LabelSpreading montre une plus forte variance malgré son score pointe.

## Déploiement, ROI & Active Learning

![Évaluation, métriques et recommandation budgétaire](/images/projects/brainscanai-active-learning.png)

Passe à l'échelle & Coût GPU : Mentionne que le coût d'inférence GPU pour 4 millions d'images est inférieur à 15 €.Stratégie d'Active Learning : Explique la réallocation du budget restant (~985€) vers de l'Active Learning : les cas ambigus dont la probabilité de prédiction se situe entre 0,40 et 0,60 sont automatiquement routés vers un contrôle humain (radiologues) pour affiner le modèle.

## Stack Technique

Langage & Environnement : Python 3.11, pyproject.toml

Deep Learning & Vision : PyTorch, torchvision, OpenCV (opencv-python)

Machine Learning & Reduction : scikit-learn, UMAP-learn, NumPy, Pandas

Data Viz : Matplotlib, Seaborn