# MLOps TP1 – Au-delà du Notebook

Projet réalisé dans le cadre du module **Déploiement d'applications intelligentes** (5IASD, EMSI Rabat).

Ce dépôt pose les bases d'un projet MLOps propre :
- un **environnement Conda reproductible** décrit dans `environment.yml` ;
- un **script d'entraînement** (`train.py`) exécutable en une commande, à la place d'un notebook ;
- un **`.gitignore`** qui garde les environnements, les données et les modèles hors du dépôt.

## Structure du projet

```
tp1-git-env/
├── .gitignore         # Fichiers et dossiers exclus du suivi Git
├── environment.yml    # Définition de l'environnement Conda
├── train.py           # Pipeline d'entraînement (Iris + Random Forest)
└── models/            # Créé à l'exécution, ignoré par Git
```

## Prérequis

- [Anaconda](https://www.anaconda.com/download) ou Miniconda
- [Git](https://git-scm.com/downloads)
- Visual Studio Code (recommandé)

## Installation

1. **Cloner le dépôt**
   ```bash
   git clone https://github.com/yassir-drissi/mlops-tp1-tutorial.git
   cd mlops-tp1-tutorial
   ```

2. **Créer l'environnement Conda**
   ```bash
   conda env create -f environment.yml
   ```

3. **Activer l'environnement**
   ```bash
   conda activate mlops_base_env
   ```

4. **(Optionnel) Sélectionner l'interpréteur dans VS Code**
   `Ctrl + Shift + P` → *Python: Select Interpreter* → `mlops_base_env`

## Utilisation

Lancer le pipeline d'entraînement :

```bash
python train.py
```

Résultat attendu :

```
[MLOps Pipeline] Starting pipeline execution...
[MLOps Pipeline] Target model successfully cached! Score: 1.0000
```

Le modèle entraîné est sauvegardé dans `models/iris_model.pkl`.

## Ce que fait `train.py`

1. Charge le jeu de données **Iris** depuis scikit-learn.
2. Sépare les données en jeu d'entraînement (80 %) et jeu de test (20 %), avec `random_state=42`.
3. Entraîne un **RandomForestClassifier** (100 arbres).
4. Sauvegarde le modèle dans `models/iris_model.pkl`.
5. Affiche l'exactitude sur le jeu de test.

## Pourquoi `models/` n'est pas dans le dépôt

Le `.gitignore` contient les règles `models/` et `*.pkl`. Les modèles entraînés sont des fichiers binaires, lourds et régénérables : ils n'ont pas leur place dans Git. Pour les versionner, on utilisera un outil dédié comme **DVC** ou **MLflow** dans les prochains TPs.

Pour le vérifier :

```bash
python train.py
git status   # models/ n'apparaît pas dans les fichiers non suivis
```

## Dépannage

| Problème | Solution |
|---|---|
| `'conda' n'est pas reconnu` | Lancer `conda init cmd.exe powershell`, puis rouvrir le terminal |
| `EnvironmentFileNotFound` | Vérifier que le fichier s'appelle bien `environment.yml` et qu'on est dans le bon dossier |
| Erreur `Invoke-Expression` avec `conda activate` sous PowerShell | Vérifier avec `conda env list` que l'environnement existe, sinon utiliser le terminal *Command Prompt* |
| `Terms of Service have not been accepted` | `conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main` (idem pour `pkgs/r` et `pkgs/msys2`) |

## Auteur

**Yassir Drissi** – 5IASD, EMSI Rabat (2026-2027)
