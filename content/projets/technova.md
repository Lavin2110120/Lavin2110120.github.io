---
title: "TechNova — Système de Prédiction d'Attrition Employés"
date: 2026-05-20
description: "Industrialisation et déploiement d'un pipeline de Machine Learning (FastAPI, Docker, CI/CD) avec traçabilité complète sur base PostgreSQL."
tags: ["Machine Learning", "FastAPI", "Docker", "PostgreSQL", "CI/CD", "DevOps"]
showToc: true
---

**Ce projet est le rendu de mon 5ème projet de mon parcours de MBA data Scientist chez OpenClassrooms. C'est une simulation de mise en situation pour le compte de l'entreprise "TechNova", une entreprise fictive.**

### 📈 Contexte & Objectif Métier

L'objectif de ce projet est d'anticiper le risque de départ des collaborateurs (attrition RH) afin de permettre aux équipes de ressources humaines d'agir préventivement. 

La contrainte technique majeure résidait dans l'obligation de concevoir un système **auditable et résilient** : chaque prédiction doit être tracée en base de données, sans jamais bloquer l'expérience utilisateur en cas de panne de l'infrastructure de stockage.

---

### 🛠️ Architecture du Système & Approche DevOps
Ce projet démontre une maîtrise complète du cycle de vie d'un modèle (MLOps), de son empaquetage à sa mise en production :

* **API REST (FastAPI)** : Développement d'une API haute performance pour exposer les prédictions du modèle.
* **Pipeline ML de Production** : Utilisation d'un `PolarsPreprocessor` personnalisé intégré de bout en bout dans un pipeline Scikit-Learn pour un nettoyage de données rapide et reproductible.
* **Conteneurisation (Docker)** : Création d'une image Docker isolée, garantissant un déploiement agnostique de l'application sur n'importe quel serveur ou service Cloud.
* **CI/CD Automatisée** : Configuration de **GitHub Actions** pour exécuter automatiquement les suites de tests à chaque modification du code. En cas de succès, l'image Docker est déployée de manière transparente sur **Hugging Face Spaces**.

---

### 🗄️ Modèle de Données & Persistance Fail-Safe
Pour répondre au besoin de monitoring et d'audit des décisions de l'IA, une base de données **PostgreSQL** (gérée via SQLAlchemy) enregistre l'historique complet :

`id` (Integer) : Clé primaire (auto-incrément)
`employee_id` (Integer) : ID unique du collaborateur testé
`prediction_text` (String) : Résultat (`High` pour Risque, `Low` pour Stable)
`probability` (Float) : Score de confiance du modèle (0 à 1)
`created_at` (DateTime) : Horodatage automatique (UTC)

**Mécanisme de Résilience (Fail-Safe)** : L'application intègre une logique de gestion des pannes. Si la base PostgreSQL devient temporairement indisponible, l'incident est consigné dans les logs, mais l'API délivre tout de même la prédiction à l'utilisateur pour assurer la continuité du service RH.

---

### 🧪 Qualité du Code & Tests
Le projet respecte les standards exigeants de l'ingénierie logicielle :
* **Tests Unitaires & E2E** (`pytest`) : Validation de la cohérence des prédictions et de la persistance.
* **Couverture de code** : **88%** du code est couvert par la suite de tests, garantissant une forte maintenabilité.

---

### 🔗 Liens du Projet
* **Déploiement API (Hugging Face Spaces)** : https://huggingface.co/spaces/Lavin2110/projet5_OC/tree/main
* **Code Source** : https://github.com/Lavin2110120/Projet5_OC