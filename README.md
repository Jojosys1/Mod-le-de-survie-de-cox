# Modèle de Cox — application numérique à une étude de récidive

## 1. Présentation

Ce projet propose une mise en pratique complète du **modèle de survie de Cox** à partir d'une cohorte entièrement simulée.

Le scénario retenu est volontairement concret : des patients sont suivis après un traitement et l'on cherche à étudier le **temps jusqu'à une récidive**. Une partie des patients ne présente pas de récidive pendant la période de suivi ; leurs observations sont donc censurées.

Le projet reprend les éléments développés dans le document de référence *Modèle de survie de Cox* : fonction de survie, risque instantané, modèle à risques proportionnels, gestion de la censure, vraisemblance partielle, interprétation des coefficients par hazard ratio et vérification de l'hypothèse de risques proportionnels.

> Les données utilisées dans le notebook sont simulées. Les résultats ont donc une valeur pédagogique et méthodologique, et ne constituent pas une conclusion médicale.

## 2. Problématique

La question étudiée est :

**Quels facteurs sont associés à une augmentation ou à une diminution du risque instantané de récidive au cours du suivi ?**

Le modèle de Cox est adapté à cette situation parce que l'on observe simultanément :

- un temps de suivi ;
- un indicateur précisant si la récidive a été observée ;
- des observations censurées ;
- plusieurs variables explicatives.

Le modèle considéré est

$$
h(t|X)=h_0(t)\exp(\beta^T X),
$$

où $h_0(t)$ est le risque de base et $\beta$ le vecteur des coefficients associés aux covariables.

## 3. Données simulées

La cohorte contient 500 individus.

Les variables sont :

| Variable | Description |
|---|---|
| `time` | temps de suivi observé |
| `event` | 1 si récidive observée, 0 si censuré |
| `age` | âge en années |
| `age10` | âge centré autour de 60 ans et exprimé par tranche de 10 ans |
| `treatment` | 1 pour le traitement renforcé, 0 sinon |
| `biomarker` | biomarqueur standardisé |

Les paramètres utilisés pour générer les temps sont connus dans la simulation :

- âge : $\beta=0.22$ ;
- traitement renforcé : $\beta=-0.55$ ;
- biomarqueur : $\beta=0.45$.

Ils servent uniquement de référence pour évaluer la capacité du modèle à retrouver les effets présents dans les données simulées.

## 4. Contenu du notebook

Le fichier `modele_cox_cas_pratique.ipynb` suit une progression complète :

1. formulation de la problématique ;
2. génération d'une cohorte simulée ;
3. exploration des temps et des censures ;
4. estimation de Kaplan-Meier ;
5. implémentation de la log-vraisemblance partielle du modèle de Cox ;
6. estimation numérique des coefficients ;
7. calcul des hazard ratios ;
8. construction d'intervalles de confiance approximatifs ;
9. estimation du risque cumulé de base par Breslow ;
10. prédiction de courbes de survie pour deux profils ;
11. diagnostic pédagogique à partir des résidus de Schoenfeld ;
12. étude de stabilité selon la taille de l'échantillon ;
13. discussion des résultats et des limites.

## 5. Résultats attendus

Le mécanisme de simulation impose les effets suivants :

- une augmentation de l'âge doit être associée à un risque de récidive plus élevé ;
- le traitement renforcé doit être associé à un risque plus faible ;
- une augmentation du biomarqueur doit être associée à un risque plus élevé.

Le notebook compare les coefficients estimés aux coefficients réellement utilisés lors de la simulation. Cette comparaison permet de distinguer clairement :

**paramètres du phénomène simulé → données observées → estimation numérique → incertitude → interprétation.**

Deux profils sont ensuite comparés à partir des courbes de survie prédites.

## 6. Choix numériques

L'estimation des coefficients est réalisée par optimisation numérique de la négative log-vraisemblance partielle.

Une formulation stable du calcul du dénominateur utilise une transformation de type **log-sum-exp**, afin de limiter les problèmes numériques lorsque les prédicteurs exponentiels deviennent grands.

Les intervalles de confiance reposent sur une approximation quadratique de la fonction objectif et sur l'inversion de la Hessienne numérique. Cette étape est explicitement présentée comme une approximation.

L'estimation du risque cumulé de base utilise ensuite l'idée de Breslow afin de construire des courbes de survie conditionnelles aux profils étudiés.

## 7. Pourquoi simuler avant de travailler sur des données réelles ?

La simulation permet de connaître le mécanisme générateur des données. On peut donc vérifier si la méthode retrouve les effets que l'on a volontairement introduits.

Cette étape est utile avant une application réelle car elle permet de tester :

- la cohérence du code ;
- l'interprétation des coefficients ;
- l'effet de la censure ;
- la stabilité des estimations ;
- les conséquences d'une diminution du nombre d'observations.

Une fois cette étape maîtrisée, le même cadre peut être adapté à une base publique de survie.

## 8. Limites

Cette étude ne doit pas être interprétée comme une analyse clinique.

Les principales limites sont :

- données entièrement simulées ;
- mécanisme de génération relativement simple ;
- covariables simulées sans structure complexe de dépendance ;
- hypothèse de risques proportionnels imposée lors de la simulation ;
- diagnostic des résidus de Schoenfeld présenté sous une forme pédagogique ;
- intervalles de confiance fondés sur une approximation numérique de la Hessienne.

Dans une étude réelle, il faudrait également examiner la qualité des données, les valeurs manquantes, les relations non linéaires, les interactions, la proportionnalité des risques et la pertinence clinique des covariables.

## 9. Structure du projet

```text
projet_cox/
│
├── modele_cox_cas_pratique.ipynb
└── README.md
```

## 10. Exécution

Installer les dépendances principales :

```bash
pip install numpy pandas matplotlib scipy jupyter
```

Puis lancer :

```bash
jupyter notebook modele_cox_cas_pratique.ipynb
```

ou :

```bash
jupyter lab
```

Le notebook est autonome et ne nécessite pas de téléchargement de données externes.

## 11. Références

- Cox, D. R. (1975). *Partial likelihood*. Biometrika, 62(2), 269–276.
- Schoenfeld, D. (1982). *Partial Residuals for the Proportional Hazards Regression Model*. Biometrika, 69(1), 239–241.
- GLODJO, Jolémon (2026). *Modèle de survie de Cox*. Document de cours fourni avec le projet.

