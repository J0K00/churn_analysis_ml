# Prédiction du Churn - Analyse Machine Learning

## 🎓 Contexte Académique et Professionnel
Ce projet a été réalisé dans le cadre du stage académique de Licence 3 en Mathématiques, Statistique et Informatique de l'**Université de Kinshasa**, effectué au mois de **juillet 2026** chez **Vodacom Congo SA** au sein du département Technology, services de Big Data.

- **Stagiaires :** Monsieur Joseph Kowa et Monsieur Hoben Kayudi
- **Encadreurs :** Monsieur Fally Katako et Monsieur Gradi Kamingu

---

## 📌 Description du Projet
Ce projet de Machine Learning a pour objectif de prédire l'attrition (churn) des clients dans le secteur des télécommunications. En analysant les comportements d'utilisation passés des abonnés (jours d'activité, consommation de données, appels, etc.) et les informations sur leurs équipements, le modèle permet d'identifier de manière proactive les clients susceptibles de cesser d'utiliser les services.

## 📊 Structure des Données
Le jeu de données principal (`Dataset_churn.csv`) contient de nombreuses caractéristiques décrivant le profil et le comportement des utilisateurs sur plusieurs mois :
- **Informations sur l'équipement :** `gadget_type`, `device_category`, `smart_phone_flag`, `manufacturer`.
- **Engagement et Activité :** Nombre de jours actifs sur les mois précédents (`active_days_count_mth2`, `mth3`, `mth4`).
- **Consommation :** Utilisation moyenne de la voix et des données, appels intra-réseau (on-net) et inter-réseaux (off-net).
- **Valeur client :** Segmentation de la valeur (`value_segment`) et historiques de recharge (`avg_recharge_tot_amount`).

## 🛠 Étapes du Pipeline

### 1. Nettoyage et Imputation des Données
- Traitement des valeurs aberrantes (ex: chaînes de caractères `unknown`) transformées en valeurs manquantes.
- Conversion et nettoyage des valeurs au format scientifique.
- **Imputation :** Remplacement des valeurs manquantes par le **mode** (valeur la plus fréquente) pour les variables catégorielles et par la **médiane** pour les variables numériques.

### 2. Prétraitement et Feature Engineering
- **Création de la variable cible :** Un client est considéré comme en churn (1) s'il a 0 jour d'activité au cours du mois le plus récent (mois 2). Autrement, il est actif (0).
- **Encodage :** Utilisation du **Target Encoding** sur les variables catégorielles (avec lissage croisé) pour capturer leur relation avec la variable cible sans introduire de fuite de données.
- **Mise à l'échelle :** Application d'un **RobustScaler** pour standardiser les variables numériques en minimisant l'impact potentiel des valeurs extrêmes (outliers).
- **Rééquilibrage des classes :** Le taux de churn initial étant faible (~6.46%), la technique **SMOTE** (Synthetic Minority Over-sampling Technique) a été appliquée sur le jeu d'entraînement pour équilibrer les classes et améliorer la détection.

### 3. Modélisation et Évaluation
Trois modèles de classification ont été entraînés et comparés :
1. **Régression Logistique** (Modèle de base linéaire)
2. **Random Forest** (Modèle ensembliste bagging)
3. **XGBoost** (Modèle ensembliste boosting)

## 🏆 Résultats
L'évaluation des modèles a été réalisée avec des métriques de classification robustes : Exactitude (Accuracy), Précision, Rappel (Recall), F1-Score, et ROC-AUC. 

Le modèle **XGBoost** présente les meilleures performances globales avec :
- **F1-Score :** ~96.4%
- **ROC-AUC :** ~99.9%
- **Taux de détection (Recall) :** Plus de 99% des clients en attrition ont été correctement identifiés.

## 🚀 Utilisation
Pour reproduire les résultats, il suffit d'exécuter les notebooks Jupyter présents dans ce dépôt. Les scripts incluent le chargement automatique des données depuis `Dataset_churn.csv`, l'application complète de la chaîne de traitement (nettoyage, prétraitement, équilibrage) et l'affichage comparatif final des performances des modèles, incluant les rapports de classification et les matrices de confusion.