# DeepFake Detect Project

Guide d'installation et de configuration de l'environnement de développement local sous Windows (PowerShell).

---

## 1. Prérequis : Version de Python

Pour garantir la compatibilité avec toutes les dépendances (notamment **TensorFlow** et **Keras**) :

- **Version recommandée :** Python **3.11** (ex: `3.11.x`)
- **Version également compatible :** Python **3.12** (ex: `3.12.x`)
- **Non supporté :** Python **3.13+** (TensorFlow n'est pas encore compatible avec les versions plus récentes).

### Vérifier la version de Python installée
Ouvrez un terminal PowerShell et exécutez :

```powershell
python --version
```

Si vous avez plusieurs versions de Python installées avec le lanceur `py` :

```powershell
py --list
```

---

## 2. Configuration de l'environnement virtuel

Il est fortement recommandé d'utiliser un environnement virtuel dédié pour isoler les paquets du projet.

### Étape 1 : Créer l'environnement virtuel
À la racine du projet, lancez :

```powershell
# Avec la commande python standard
python -m venv .venv

# OU en ciblant explicitement Python 3.11 avec le lanceur py :
py -3.11 -m venv .venv
```

### Étape 2 : Activer l'environnement virtuel sous PowerShell

```powershell
.\.venv\Scripts\Activate.ps1
```

> *(Une fois activé, le préfixe `(.venv)` s'affiche au début de votre ligne de commande).*

---

## 3. Installation des dépendances

### Étape 1 : Mettre à jour `pip`

```powershell
python -m pip install --upgrade pip
```

### Étape 2 : Installer les packages du projet

```powershell
pip install -r requirements.txt
```

---

## 4. Vérification de l'installation

Pour vous assurer que les principales bibliothèques de Machine Learning et de traitement d'images sont prêtes à l'emploi :

```powershell
python -c "import tensorflow as tf; import keras; import cv2; print('TensorFlow:', tf.__version__); print('Keras:', keras.__version__); print('OpenCV:', cv2.__version__)"
```

**Résultat attendu :** Les versions installées de TensorFlow, Keras et OpenCV doivent s'afficher sans aucune erreur d'importation.

---

## 5. Dépannage (Troubleshooting)

### Erreur lors de l'activation du venv : `L'exécution de scripts est désactivée`
Si PowerShell bloque l'exécution du script `Activate.ps1`, autorisez l'exécution des scripts locaux :

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```
Puis relancez la commande d'activation `.\.venv\Scripts\Activate.ps1`.

### Erreur `ERROR: Could not find a version that satisfies the requirement tensorflow`
Cette erreur se produit généralement lorsque vous utilisez une version de Python non prise en charge (ex. **Python 3.13**).
- **Solution :** Installez Python 3.11 ou 3.12 (64-bit), puis recréez votre environnement virtuel avec la version compatible.

### Erreur liée aux DLL manquantes (TensorFlow / OpenCV)
Sous Windows, TensorFlow et OpenCV nécessitent les bibliothèques C++ de Microsoft.
- **Solution :** Téléchargez et installez les [Visual C++ Redistributable pour Visual Studio 2015-2022](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist) (version x64).

### Problème de cache lors de l'installation
Si un téléchargement de paquet échoue ou s'interrompt :

```powershell
pip install --no-cache-dir -r requirements.txt
```
