# 🌍 Prévision des Exportations Marocaines (CI01)

![ENCG Settat](https://img.shields.io/badge/ENCG-Settat-blue)
![Filière](https://img.shields.io/badge/Fili%C3%A8re-BD%20%26%20DS%20(S7%20CI)-green)
![Python](https://img.shields.io/badge/Python-3.13-yellow)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.6.1-orange)

Ce dépôt contient le notebook réalisé dans le cadre du **Contrôle continu — Partie B · Commerce international (S7 CI)** à l'**ENCG Settat** (Année universitaire 2026–2027).

* **Étudiant :** TAISA WARDA
* **Code Apogée :** `25007836`
* **Groupe :** CI
* **Enseignant :** Pr. A. Larhlimi
* **Sujet :** `CI01` — Prévision des exportations marocaines
* **Date :** 19/11/2026

---

## 🎯 1. Problématique et Objectifs

### Intérêt économique
Le commerce extérieur joue un rôle moteur dans la croissance économique du Maroc, porté par des accords de libre-échange et des stratégies sectorielles dynamiques (automobile, agriculture, phosphates). Prédire avec précision la valeur des exportations marocaines permet d'anticiper les rentrées de devises et d'ajuster les politiques commerciales dans un contexte mondial volatil.

### Problématique
> *Comment pouvons-nous prédire la valeur des transactions (`primaryValue`) des exportations marocaines en fonction du pays partenaire, de la catégorie de produit (`cmdCode`), de l'année et du flux commercial ?*

* **Nature de la tâche :** Régression supervisée
* **Objectif mesurable fixé :** Atteindre un coefficient de détermination $R^2 > 0.65$ sur l'ensemble de test et réduire l'erreur absolue moyenne (MAE) d'au moins **30 %** par rapport à une référence naïve.

---

## 📊 2. Jeu de données (Dataset)

* **Source officielle :** [UN Comtrade Database](https://comtradeplus.un.org/)
* **Licence :** Licence publique UN Comtrade (extrait le 19/11/2026)
* **Période couverte :** Données annuelles de **2016 à 2024**
* **Périmètre :** Déclarant Maroc (`MAR`), partenaires mondiaux, flux Import/Export selon le Système Harmonisé (HS).
* **Dimensions brutes :** `8 288` lignes et `47` colonnes (chaque ligne représente une transaction commerciale annuelle en USD).

### Dictionnaire des variables retenues

| Variable | Description | Type / Unité | Rôle | Valeurs manquantes |
| :--- | :--- | :--- | :--- | :---: |
| `refYear` | Année de la transaction | Numérique (`int`) | Caractéristique | 0.0 % |
| `flowDesc` | Sens du flux (Export / Import) | Catégoriel (`str`) | Caractéristique | 0.0 % |
| `partnerDesc` | Pays partenaire commercial | Catégoriel (`str`) | Caractéristique | 0.0 % |
| `cmdCode` | Code du produit (Classification SH) | Catégoriel (`int`) | Caractéristique | 0.0 % |
| `primaryValue` | Valeur primaire de la transaction | Numérique (`$ USD`) | **Cible à prédire** | 0.0 % |

---

## 📈 3. Exploration des données (EDA)

L'analyse exploratoire s'articule autour de trois visualisations clés :
1. **Évolution temporelle des flux :** Analyse de la somme des valeurs commerciales par année (2016–2024) pour observer les tendances macroéconomiques.
2. **Top 10 des pays partenaires :** Identification des principaux partenaires stratégiques du Maroc en volume financier global.
3. **Distribution de la variable cible (échelle logarithmique) :** Étude de l'asymétrie de `primaryValue` (forte concentration de petites transactions et présence de valeurs extrêmes).

---

## 🧠 4. Modélisation & Algorithme principal

* **Algorithme retenu :** **Random Forest Regressor** (Forêt Aléatoire de Régression — Algorithme n°12).
* **Justification :** Capacité à modéliser des relations non linéaires complexes et les interactions entre variables catégorielles (codes produits × pays partenaires) sans nécessiter de transformations paramétriques lourdes.

### Formulation mathématique
$$\hat{y} = \frac{1}{B} \sum_{b=1}^{B} T_b(x)$$
* $\hat{y}$ : valeur prédite de la transaction (`primaryValue`)
* $B$ : nombre d'arbres dans la forêt
* $T_b(x)$ : prédiction de l'arbre individuel $b$ pour l'observation $x$

### Hyperparamètres explorés
* `n_estimators` : `[50, 100]` (nombre d'arbres)
* `max_depth` : `[10, 15]` (profondeur maximale pour limiter le surapprentissage)

---

## ⚙️ 5. Installation et Reproductibilité

### Prérequis techniques
* Python `3.13.18`
* `pandas` (`2.2.3`)
* `scikit-learn` (`1.6.1`)
* `numpy`, `matplotlib`, `seaborn`

### Exécution locale ou sur Google Colab
1. Cloner le dépôt :
   ```bash
   git clone [https://github.com/wardataisa/25007836-Taisa-CI.git](https://github.com/wardataisa/25007836-Taisa-CI.git)
   cd 25007836-Taisa-CI
