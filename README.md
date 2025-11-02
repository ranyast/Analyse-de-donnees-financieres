# Analyse de données financières et socio-économiques

## Projet Data Science – ING 4 DATA & IA – Application interactive

---

### I. Présentation du projet

Ce projet a été réalisé dans le cadre de notre module **Data Science** durant notre premier semestre d'ING4.  
L’objectif principal de ce projet est de **mettre en pratique les compétences en data science que nous avons acquises au cours de cette formation**.
Nous devons donc créer une application avec des solutions utiles pour un investisseur immobilier en fonction des besoins de notre persona.

Voici notre persona: 
Stéphane, 45 ans, est chirurgien plasticien. Il souhaite aujourd'hui développer son patrimoine et préparer sa retraite à travers un point d'investissement réfléchi. Ouvert
sur les opportunités, il ne privilégie pas de région en particulier, mais s'intéresse surtout aux villes étudiantes dynamiques comme Rennes, Toulouse, Lyon, Bordeaux, Lille, Grenoble,
Marseille, Montpellier et Paris. Son objectif : investir intelligemment pour assurer l'avenir tout en diversifiant ses placements. 

Notre application permet de croiser plusieurs thématiques :
- L'évolution et la tendance du marché immobilier
- Le calcul du rendement en fonction du budget, de la surface donnés
- Les effectifs étudiants dans ses villes
- Les incivilités qui y sont recensées
- L’évolution de la population par ville
 

---

### II. Sources et jeux de données

#### 1. Marché immobilier (2020–2024)
**Fichier :** `statistiques_grandes_villes_2020_2024_toutes_colonnes.csv`

**Source :** [Données de valeurs foncières](https://files.data.gouv.fr/geo-dvf/latest/csv/) – Données de valeurs foncières (DVF)  

**Contenu :**
- Prix moyen au m² et nombre de transactions par ville et par année.  
**Colonnes principales :**
- `ville`, `annee`, `prix_m2_moyen`, `nb_transactions`.

#### 2. Population municipale (2016–2024)
**Fichiers :**
- `population_municipale_departement_france.csv`
- `population_municipale_communes_france.csv`

**Source :** [Population par départements](https://www.data.gouv.fr/datasets/population-municipale-des-departements-france-entiere/) – Population par département | [Population par communes](https://www.data.gouv.fr/datasets/population-municipale-des-communes-france-entiere/) – Population par communes

**Contenu :**
- Nombre d’habitants par département et commune selon les années.  
**Colonnes principales :**
- `dep`, `nom_dep`, `p16_pop`, `p17_pop`, …, `p24_pop`.


#### 3. Effectifs étudiants (2001–2023)
**Fichier :** `fr-esr-atlas_regional-effectifs-d-etudiants-inscrits.csv`

**Source :** Ministère de l’Enseignement Supérieur et de la Recherche (ESR).  

**Contenu :**
- Effectifs d’étudiants inscrits par commune, niveau géographique et année universitaire. 

**Colonnes principales :**
- `geo_nom`, `niveau_geographique`, `annee_universitaire`, `effectif`, `regroupement`.

#### 4. Incivilités et sécurité publique (2016–2024)
**Fichier :** `incivilites_departement_france.csv`  

**Source :** [data.gouv.fr](https://www.data.gouv.fr) – Indicateurs de sécurité et de délinquance (SSMSI).  

**Contenu :**
- Nombre d’incivilités recensées par département et par année.  
**Colonnes principales :**
- `Zone_geographique`, `annee`, `Valeurs`, `Champ`.

#### 5. Loyers relevés par commune et calcul du rendement (2023-2024)
**Fichier :** `loyers_rendement.csv`  

**Source :** [data.gouv.fr](https://www.data.gouv.fr) – Résultats nationaux des observatoires locaux des loyers.  

**Contenu :**
- Loyers observés selon le type de logement, l'époque de construction, le nombre de pièces ou l'ancienneté d'occupation.  
**Colonnes principales :**
- `annee`, `agglomeration`, `Type d'habitat`, `loyer_median`, `loyer_mensuel`, `surface_moyenne`

---

### III. Objectifs analytiques

| Domaine d’étude        | Objectif                                                                     | Période   |
|------------------------|------------------------------------------------------------------------------|-----------|
| Marché immobilier      | Étudier l’évolution des prix moyens au m² et du volume des transactions      | 2020–2024 |
| Enseignement supérieur | Observer la dynamique des effectifs étudiants par grande ville universitaire | 2001–2024 |
| Population             | Analyser la croissance ou le déclin démographique par département            | 2016–2021 |
| Incivilités            | Mettre en relation le nombre d’incivilités avec la population départementale | 2016–2024 |
| Loyers                 | Comparer les différents loyers dans les communes                             | 2023–2024 |
| Rendement              | Savoir combien un investissement a rapporté par rapport au capital investi   | 2016–2024 |
---

### IV. Technologies utilisées

- **Langage :** Python 3.9 ou 3.10 
- **Bibliothèques :**
  - `pandas` : manipulation et transformation de données
  - `numpy` : calculs statistiques
  - `matplotlib` : visualisations statiques
  - `plotly.express`, `plotly.graph_objects` : visualisations interactives
  - `ipywidgets` : interface utilisateur dynamique
  - `IPython.display` : affichage et gestion des sorties interactives

---

### V. Méthodologie et traitements

#### 1. Population
Les fichiers INSEE ont été transformés afin de convertir les colonnes `p16_pop`, `p17_pop`, …, `p24_pop` en un format long (`année`, `population`).  
Des taux d’évolution ont été calculés sur la période 2016–2024 pour chaque département.

#### 2. Marché immobilier
Les données issues des valeurs foncières ont permis de produire :
- Un graphique d’évolution du **prix moyen au m²** (2020–2024),
- Un calcul du **taux d’évolution du prix** sur la période,
- Un suivi de l’évolution du **nombre de transactions**.

Ces graphiques sont mis à jour automatiquement à l’aide de cases à cocher interactives, permettant la sélection de plusieurs villes simultanément.

#### 3. Effectifs étudiants
Analyse effectuée à partir du fichier du ministère de l’Enseignement Supérieur :
- Sélection des communes uniquement (`niveau_geographique == "Commune"`),
- Agrégation des arrondissements sous un même nom de ville (Paris, Lyon, Marseille),
- Regroupement du nombre d’étudiants par **ville** et **année universitaire**,
- Calcul du **delta et du taux d’évolution** entre 2001–02 et 2023–24.


#### 4. Incivilités

Le nombre d’incivilités est rapporté à la population départementale afin d’obtenir un **ratio par habitant**.  
Des visualisations temporelles et comparatives permettent de mettre en évidence les écarts entre départements.

---

#### 5. Loyer et Rendement 

à compléter 

---

### VI. Interface interactive

L’application repose sur un ensemble de widgets interactifs (`ipywidgets`), notamment :

- Des **cases à cocher** permettant de sélectionner les villes à analyser.  
- Différents graphes permettant d'afficher nos solutions répondant au besoin de notre persona. 

Chaque graphique se met automatiquement à jour selon les villes sélectionnées.

---

### VII. Équipe projet

Dans ce projet, nous avons tous participer à l'analyse de données, leur nettoyage et par la suite leur visualisation. 

Cependant, nous avons tous travaillé sur des widgets différents que vous allez trouver ci-dessous : 

| Nom               | Rôle                                                                                 |
|-------------------|--------------------------------------------------------------------------------------|
| STITOU Ranya      | Widget `Incivilités dans les villes étudiantes`, `README.md`                         |
| LALLEMENT Antoine | Widget `cases à cocher`, `Evolution du marché immobilier`, `Evolution des étudiants` |
| AYRIVIE Pia       | Widget `choix des paramètres`, `classement du meilleur résultat`                     |
| BOUZOUBAA Salma   | Widget `choix des paramètres`, `classement du meilleur résultat`                                                                               |

---

### IX. Conclusion

FAIRE UNE CONCLUSION ! 

---

*(Projet académique – ING 4 DATA & IA – 2025)*


