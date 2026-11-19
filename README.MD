└── README.md (1000 tokens)


/README.md:
--------------------------------------------------------------------------------
 1 | # 🌍 Prévision des Exportations Marocaines (CI01)
 2 | 
 3 | ![ENCG Settat](https://img.shields.io/badge/ENCG-Settat-blue)
 4 | ![Filière](https://img.shields.io/badge/Fili%C3%A8re-BD%20%26%20DS%20(S7%20CI)-green)
 5 | ![Python](https://img.shields.io/badge/Python-3.13-yellow)
 6 | ![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.6.1-orange)
 7 | 
 8 | Ce dépôt contient le notebook réalisé dans le cadre du **Contrôle continu — Partie B · Commerce international (S7 CI)** à l'**ENCG Settat** (Année universitaire 2026–2027).
 9 | 
10 | * **Étudiant :** TAISA WARDA
11 | * **Code Apogée :** `25007836`
12 | * **Groupe :** CI
13 | * **Enseignant :** Pr. A. Larhlimi
14 | * **Sujet :** `CI01` — Prévision des exportations marocaines
15 | * **Date :** 19/11/2026
16 | 
17 | ---
18 | 
19 | ## 🎯 1. Problématique et Objectifs
20 | 
21 | ### Intérêt économique
22 | Le commerce extérieur joue un rôle moteur dans la croissance économique du Maroc, porté par des accords de libre-échange et des stratégies sectorielles dynamiques (automobile, agriculture, phosphates). Prédire avec précision la valeur des exportations marocaines permet d'anticiper les rentrées de devises et d'ajuster les politiques commerciales dans un contexte mondial volatil.
23 | 
24 | ### Problématique
25 | > *Comment pouvons-nous prédire la valeur des transactions (`primaryValue`) des exportations marocaines en fonction du pays partenaire, de la catégorie de produit (`cmdCode`), de l'année et du flux commercial ?*
26 | 
27 | * **Nature de la tâche :** Régression supervisée
28 | * **Objectif mesurable fixé :** Atteindre un coefficient de détermination $R^2 > 0.65$ sur l'ensemble de test et réduire l'erreur absolue moyenne (MAE) d'au moins **30 %** par rapport à une référence naïve.
29 | 
30 | ---
31 | 
32 | ## 📊 2. Jeu de données (Dataset)
33 | 
34 | * **Source officielle :** [UN Comtrade Database](https://comtradeplus.un.org/)
35 | * **Licence :** Licence publique UN Comtrade (extrait le 19/11/2026)
36 | * **Période couverte :** Données annuelles de **2016 à 2024**
37 | * **Périmètre :** Déclarant Maroc (`MAR`), partenaires mondiaux, flux Import/Export selon le Système Harmonisé (HS).
38 | * **Dimensions brutes :** `8 288` lignes et `47` colonnes (chaque ligne représente une transaction commerciale annuelle en USD).
39 | 
40 | ### Dictionnaire des variables retenues
41 | 
42 | | Variable | Description | Type / Unité | Rôle | Valeurs manquantes |
43 | | :--- | :--- | :--- | :--- | :---: |
44 | | `refYear` | Année de la transaction | Numérique (`int`) | Caractéristique | 0.0 % |
45 | | `flowDesc` | Sens du flux (Export / Import) | Catégoriel (`str`) | Caractéristique | 0.0 % |
46 | | `partnerDesc` | Pays partenaire commercial | Catégoriel (`str`) | Caractéristique | 0.0 % |
47 | | `cmdCode` | Code du produit (Classification SH) | Catégoriel (`int`) | Caractéristique | 0.0 % |
48 | | `primaryValue` | Valeur primaire de la transaction | Numérique (`$ USD`) | **Cible à prédire** | 0.0 % |
49 | 
50 | ---
51 | 
52 | ## 📈 3. Exploration des données (EDA)
53 | 
54 | L'analyse exploratoire s'articule autour de trois visualisations clés :
55 | 1. **Évolution temporelle des flux :** Analyse de la somme des valeurs commerciales par année (2016–2024) pour observer les tendances macroéconomiques.
56 | 2. **Top 10 des pays partenaires :** Identification des principaux partenaires stratégiques du Maroc en volume financier global.
57 | 3. **Distribution de la variable cible (échelle logarithmique) :** Étude de l'asymétrie de `primaryValue` (forte concentration de petites transactions et présence de valeurs extrêmes).
58 | 
59 | ---
60 | 
61 | ## 🧠 4. Modélisation & Algorithme principal
62 | 
63 | * **Algorithme retenu :** **Random Forest Regressor** (Forêt Aléatoire de Régression — Algorithme n°12).
64 | * **Justification :** Capacité à modéliser des relations non linéaires complexes et les interactions entre variables catégorielles (codes produits × pays partenaires) sans nécessiter de transformations paramétriques lourdes.
65 | 
66 | ### Formulation mathématique
67 | $$\hat{y} = \frac{1}{B} \sum_{b=1}^{B} T_b(x)$$
68 | * $\hat{y}$ : valeur prédite de la transaction (`primaryValue`)
69 | * $B$ : nombre d'arbres dans la forêt
70 | * $T_b(x)$ : prédiction de l'arbre individuel $b$ pour l'observation $x$
71 | 
72 | ### Hyperparamètres explorés
73 | * `n_estimators` : `[50, 100]` (nombre d'arbres)
74 | * `max_depth` : `[10, 15]` (profondeur maximale pour limiter le surapprentissage)
75 | 
76 | ---
77 | 
78 | ## ⚙️ 5. Installation et Reproductibilité
79 | 
80 | ### Prérequis techniques
81 | * Python `3.13.18`
82 | * `pandas` (`2.2.3`)
83 | * `scikit-learn` (`1.6.1`)
84 | * `numpy`, `matplotlib`, `seaborn`
85 | 
86 | ### Exécution locale ou sur Google Colab
87 | 1. Cloner le dépôt :
88 |    ```bash
89 |    git clone [https://github.com/wardataisa/25007836-Taisa-CI.git](https://github.com/wardataisa/25007836-Taisa-CI.git)
90 |    cd 25007836-Taisa-CI
91 | 


--------------------------------------------------------------------------------
