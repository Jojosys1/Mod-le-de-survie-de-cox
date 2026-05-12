# Modèle de survie de Cox

## 📊 Présentation du projet

Ce repository implémente un **modèle de survie de Cox** (modèle à risques proportionnels) pour l'analyse de données de survie en médecine, biostatistiques et études cliniques.

## 🎯 Objectifs

- Analyser le temps jusqu'à l'apparition d'un événement d'intérêt
- Évaluer l'impact de variables explicatives sur le risque
- Prédire les fonctions de survie pour différents profils de patients

## 📦 Fonctionnalités

- ✨ Estimation des coefficients par maximum de vraisemblance partielle
- 📈 Visualisation des courbes de survie (Kaplan-Meier)
- 🔍 Test de l'hypothèse des risques proportionnels
- 🎲 Sélection de variables (stepwise, LASSO)
- 📊 Calcul des rapports de risque (hazard ratios) avec IC 95%

## 🛠️ Installation

```bash
git clone https://github.com/votre-username/cox-survival-model.git
cd cox-survival-model
pip install -r requirements.txt
```

## 📚 Utilisation rapide

```python
from cox_model import SurvivalAnalysis
import pandas as pd

# Chargement des données
df = pd.read_csv('survival_data.csv')

# Initialisation du modèle
model = SurvivalAnalysis(time_col='time', 
                        event_col='status',
                        covariates=['age', 'treatment', 'stage'])

# Ajustement
model.fit(df)

# Prédiction de survie
survival_prob = model.predict_survival_function(df_new_patients)
```

## 📁 Structure du repository

```
├── data/               # Données d'exemple
├── src/                # Code source
│   ├── cox_model.py   # Implémentation principale
│   ├── utils.py       # Fonctions utilitaires
│   └── vis.py         # Visualisations
├── notebooks/          # Tutoriels Jupyter
├── tests/              # Tests unitaires
└── results/            # Résultats des analyses
```

## 📈 Exemples d'analyse

```python
# Résumé du modèle
model.summary()

# Visualisation des courbes de survie
model.plot_survival_curves()

# Test des risques proportionnels
model.test_proportional_hazards()
```

## 📖 Documentation détaillée

Voir le dossier [docs/](docs/) pour :
- Base théorique du modèle de Cox
- Guide d'interprétation des résultats
- Bonnes pratiques pour les données censurées

## 🤝 Contribution

Les contributions sont les bienvenues ! 
1. Fork le projet
2. Créez votre branche (`git checkout -b feature/AmazingFeature`)
3. Commit vos changements (`git commit -m 'Add AmazingFeature'`)
4. Push (`git push origin feature/AmazingFeature`)
5. Ouvrez une Pull Request

## 📝 Licence

Distribué sous licence MIT. Voir `LICENSE` pour plus d'informations.

## 📧 Contact

Votre Nom - [@votre_handle](https://twitter.com/votre_handle) - email@exemple.com

Lien du projet: [https://github.com/votre-username/cox-survival-model](https://github.com/votre-username/cox-survival-model)

## 🙏 Remerciements

- David Cox pour son travail fondateur
- La communauté des biostatisticiens
- Les contributeurs open-source

---
⭐️ N'oubliez pas de mettre une étoile si ce projet vous a été utile !
