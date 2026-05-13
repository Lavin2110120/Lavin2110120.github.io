---
title: "Portfolio & CI/CD"
date: 2026-05-13
description: "Mise en place d'un portfolio automatisé avec Hugo et GitHub Actions."
tags: ["DevOps", "GitHub Actions", "Hugo", "Git"]
showToc: true
---

### 🚀 Objectif du projet
L'idée était de concevoir un support professionnel pour présenter mes travaux en **Data Science**, tout en démontrant mes compétences techniques en **DevOps**  et en automatisation.

### 🛠️ Architecture Technique
Ce portfolio repose sur une chaîne de déploiement moderne, illustrant une maîtrise de l'intégralité d'une chaîne de production:

* **Générateur :** [Hugo](https://gohugo.io/) (Framework ultra-rapide).
* **Thème :** PaperMod (Optimisé pour la performance).
* **Versionnage :** Git (Gestion des branches et des submodules pour le thème).
* **Hébergement :** GitHub Pages[cite: 82].

### ⚙️ Automatisation CI/CD
Le point fort de ce projet est l'utilisation de **GitHub Actions**. Chaque fois que je pousse une modification sur mon dépôt GitHub, un workflow s'exécute automatiquement :

1.  **Build :** Installation de la version *extended* de Hugo sur une machine virtuelle Ubuntu (environnement Linux).
2.  **Génération :** Compilation du site Markdown en HTML/CSS optimisé.
3.  **Déploiement :** Mise à jour automatique du site en ligne sur `https://Lavin2110120.github.io/`.

> Cela garantit que mon portfolio est toujours à jour sans aucune intervention manuelle.

### 📈 Compétences Validées
* Maîtrise du workflow **Git** (Versioning & CI/CD).
* Configuration de pipelines via **YAML**.
* Rédaction technique et structuration de l'information.