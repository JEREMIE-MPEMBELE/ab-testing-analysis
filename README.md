# 🧪 Analyse d'A/B Testing - Optimisation d'une Page d'Atterrissage E-Commerce

## 📌 Présentation du Projet

Ce projet réalise une **analyse d'A/B Testing** de bout en bout sur un jeu de données e-commerce (`ab_data.csv`) comprenant **294 478 sessions web**. L'objectif est d'évaluer si une nouvelle version de la page d'atterrissage (`new_page`) entraîne une augmentation statistiquement significative du taux de conversion par rapport à la version existante (`old_page`).

## 🛠️ Technologies & Bibliothèques

* **Langage :** Python 3.x
* **Environnement :** Jupyter Notebook / JupyterLab
* **Manipulation de données :** `pandas`, `numpy`
* **Analyse statistique :** `statsmodels`
* **Visualisation :** `matplotlib`, `seaborn`

## 🧹 Nettoyage & Audit d'Intégrité des Données

Une excellente intégrité des données est un prérequis strict pour toute inférence statistique valide. Avant le test d'hypothèse, les étapes de nettoyage suivantes ont été effectuées :

1. **Filtrage des erreurs de routage :** Identification et suppression de **3 893 enregistrements incohérents** où le groupe expérimental ne correspondait pas à la page affichée (ex. groupe `control` associé à la `new_page`).
2. **Dédoublonnage des utilisateurs :** Traitement de l'utilisateur présent en double (`user_id = 773192`) afin de garantir l'**indépendance des observations** entre les groupes.
3. **Taille du jeu de données nettoyé :** Obtention d'un échantillon final assaini de **290 584 utilisateurs uniques**.

## 📊 Analyse Descriptive & Métriques Clés

| Groupe | Page Assignée | Taille Échantillon ($n$) | Conversions | Taux de Conversion ($p$) |
| :--- | :--- | :--- | :--- | :--- |
| **Control** | `old_page` | 145 274 | 17 489 | **12,04 %** |
| **Treatment** | `new_page` | 145 310 | 17 264 | **11,88 %** |
| **Total** | \- | 290 584 | 34 753 | **11,96 %** |

* **Écart observé (**$\Delta_{obs}$**) :** $p_{new} - p_{old} = -0,16\%$

## 📐 Test d'Hypothèse (Z-test à Deux Proportions)

### Cadre Statistique

* **Hypothèse Nulle (**$H_0$**) :** $p_{new} - p_{old} = 0$ *(La nouvelle page n'apporte aucune amélioration supérieure au taux de conversion)*
* **Hypothèse Alternative (**$H_1$**) :** $p_{new} - p_{old} > 0$ *(La nouvelle page augmente le taux de conversion)*
* **Seuil de significativité (**$\alpha$**) :** $0,05$

### Résultats du Test

Exécution avec `statsmodels.api.stats.proportions_ztest` :

* **Z-score :** `-1.3109`
* **p-value :** `0.9051`

## 💡 Enseignements & Recommandations Métier

1. **Non-rejet de **$H_0$** :** Avec une **p-value de **$0,9051$ ($> \alpha = 0,05$), il n'y a aucune preuve statistique indiquant que la nouvelle page d'atterrissage surpasse l'ancienne.
2. **Décision Produit :** **Ne pas déployer la nouvelle page d'atterrissage.** Le déploiement de cette itération risque d'entraîner une légère baisse globale des conversions sans générer de valeur commerciale.
3. **Prochaines étapes :** Repenser les concepts UX/UI et formuler de nouvelles hypothèses avant de lancer un prochain test expérimental.

## 🚀 Guide d'Exécution

1. Cloner ce dépôt :
   ```bash
   git clone https://github.com/JEREMIE-MPEMBELE/ab-testing-analysis.git
   ```

2. Installer les packages requis :
   ```bash
   pip install pandas numpy statsmodels matplotlib seaborn
   ```

3. Ouvrir `A_B_Testing.ipynb` dans Jupyter Notebook et exécuter les cellules.
