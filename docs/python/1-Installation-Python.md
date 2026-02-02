# Installation Python

## 1 — Qu'est-ce que Python ?

Python est un **langage de programmation** créé en 1991 par **Guido van Rossum**. 
Il est aujourd'hui l'un des langages les plus populaires du monde pour plusieurs raisons :

-  Sa syntaxe est **simple et lisible** (proche du français/anglais)
-  Il est utilisé en **web, data science, IA, automatisation, jeux**…
-  Il est **gratuit et open source**
-  Sa communauté est **immense** → beaucoup de ressources disponibles

>  **Conseil pédagogique** : Avant d'installer quoi que ce soit, lisez d'abord ce guide dans sa totalité. 
> Une bonne préparation évite 90% des problèmes !


## 2 — Avant de commencer — Vérifions si Python est déjà installé

Sur beaucoup de systèmes, Python est **déjà présent** par défaut. Vérifions !

### Sur Windows
Ouvrez le **Terminal** (cmd) :
```
Touche Windows → tapez "cmd" → Entrée
```
Puis tapez :
```bash
python --version
```

### Sur macOS / Linux
Ouvrez le **Terminal** et tapez :
```bash
python3 --version
```

### Que devrait-on voir ?
Si Python est installé, vous verrez quelque chose comme :
```
Python 3.12.3
```

>  Si vous voyez un **message d'erreur** comme *"command not found"*, alors Python n'est pas installé. 
> Continuez avec le guide ci-dessous selon votre système.


## 3 — Installation sur Windows

### Étape 1 : Télécharger Python
1. Rendez-vous sur le site officiel : [https://www.python.org/downloads/ :octicons-link-external-16:](https://www.python.org/downloads/) {:target="_blank"}
2. Cliquez sur le bouton jaune **"Download Python 3.X.X"** (la dernière version stable)

>  Le site détecte automatiquement votre système d'exploitation et vous propose le bon fichier.

### Étape 2 : Lancer l'installateur
1. Ouvrez le fichier téléchargé (exemple : `python-3.12.3-amd64.exe`)
2. Une fenêtre d'installation apparaît

### Étape 3 : Configuration importante (ne pas négliger !)
Avant de cliquer "Install now", **activez cette case** :

```
☑ Add python.exe to PATH
```

> **C'est crucial !** Cette option permet à votre ordinateur de trouver Python depuis n'importe où. 
> Sans ça, vous aurez des problèmes plus tard.

### Étape 4 : Installer
1. Cliquez **"Install now"**
2. Attendez la fin de l'installation (quelques secondes)
3. Cliquez **"Close"**

Python est installé sur Windows !


## 4 — Installation sur macOS

### Option A : Via le site officiel (recommandée pour les débutants)
1. Allez sur [https://www.python.org/downloads/ :octicons-link-external-16:](https://www.python.org/downloads/){:target="_blank"}
2. Téléchargez le dernier **installer macOS**
3. Ouvrez le fichier `.pkg` téléchargé
4. Suivez les instructions sur l'écran
5. Entrez votre mot de passe si demandé

### Option B : Via Homebrew (pour les plus avancés)
Si vous avez déjà **Homebrew** installé, ouvrez un Terminal et tapez :
```bash
brew install python
```

> **Qu'est-ce que Homebrew ?** C'est un "gestionnaire de paquets" pour macOS. 
> Il permet d'installer des logiciels facilement depuis le Terminal. 
> Vous pouvez le télécharger sur [https://brew.sh/ :octicons-link-external-16:](https://brew.sh/){:target="_blank"}

Python est installé sur macOS !


## 5 — Installation sur Linux

Linux est un peu plus divers car il existe beaucoup de "distributions" (Ubuntu, Fedora, Arch…). 
Voici les commandes pour les plus courantes.

### Ubuntu / Debian
```bash
sudo apt update
sudo apt install python3
```

### Fedora
```bash
sudo dnf install python3
```

### Arch Linux
```bash
sudo pacman -S python
```

> **Explication des commandes** :
> - `sudo` = exécuter en tant qu'administrateur
> - `apt install` / `dnf install` / `pacman -S` = installer un logiciel
> - `update` = mettre à jour la liste des logiciels disponibles

Python est installé sur Linux !


## 6 — Vérifier l'installation

Après l'installation, vérifions que tout fonctionne.

### Étape 1 : Vérifier la version
Ouvrez un Terminal et tapez :
```bash
python --version       # Windows
python3 --version      # macOS / Linux
```
Vous devriez voir : `Python 3.12.X` (ou une version récente)

### Étape 2 : Lancer Python en mode interactif
Tapez :
```bash
python        # Windows
python3       # macOS / Linux
```
Vous verrez apparaître un prompt comme celui-ci :
```
Python 3.12.3 (...)
>>> 
```
Les trois chevrons `>>>` signifient que Python est prêt à recevoir des commandes !

### Étape 3 : Un petit test
Tapez cette ligne et appuyez sur Entrée :
```python
>>> print("Bonjour, Python !")
```
Si vous voyez :
```
Bonjour, Python !
```
Félicitations ! Python fonctionne parfaitement !

Pour quitter l'environnement interactif, tapez :
```python
>>> exit()
```

## 7 — Configurer un environnement virtuel

### Pourquoi un environnement virtuel ?

Imaginons que vous travaillez sur **deux projets** en même temps :

- Le projet A nécessite la version **1.0** d'une bibliothèque
- Le projet B nécessite la version **2.0** de la même bibliothèque

Sans environnement virtuel, ces deux versions **entrent en conflit**. 
L'environnement virtuel résout ce problème en créant un **espace isolé** pour chaque projet.

> C'est comme avoir plusieurs "bureaux" propres, chacun avec ses propres outils.

### Créer un environnement virtuel

```bash
# 1. Créer un dossier pour votre projet
mkdir mon_projet
cd mon_projet

# 2. Créer l'environnement virtuel
python -m venv mon_environnement       # Windows
python3 -m venv mon_environnement      # macOS / Linux
```

### Activer l'environnement virtuel

```bash
# Windows (cmd)
mon_environnement\Scripts\activate

# Windows (PowerShell)
mon_environnement\Scripts\Activate.ps1

# macOS / Linux
source mon_environnement/bin/activate
```

Vous remarquerez que le nom de votre environnement apparaît **entre parenthèses** avant votre prompt :
```
(mon_environnement) C:\Users\vous\mon_projet>
```
Cela confirme que l'environnement est bien **activé** !

### Désactiver l'environnement virtuel
Quand vous avez fini de travailler :
```bash
deactivate
```

## 8 — Installer un éditeur de code (IDE)

Pour écrire du code Python, vous avez besoin d'un bon éditeur. Voici les meilleurs choix :

### Option 1 : Visual Studio Code (VS Code) — Recommandé
- **Gratuit** et très populaire
- Très léger et rapide
- Téléchargez ici : [https://code.visualstudio.com/ :octicons-link-external-16:](https://code.visualstudio.com/){:target="_blank"}

Après installation, ajoutez l'extension **Python** :
1. Ouvrez VS Code
2. Cliquez sur l'icône des extensions (à gauche)
3. Tapez **"Python"**
4. Installez l'extension officielle de Microsoft

### Option 2 : PyCharm
- Fait **spécifiquement** pour Python
- La version **Community** est gratuite
- Téléchargez ici : [https://www.jetbrains.com/pycharm/ :octicons-link-external-16:](https://www.jetbrains.com/pycharm/){:target="_blank"}

### Option 3 : Jupyter Notebook
- Parfait pour la **data science** et l'apprentissage
- Vous pouvez exécuter du code **ligne par ligne**
- Installez via : `pip install jupyter`

| Éditeur | Coût | Niveau | Meilleur pour |
|---|---|---|---|
| VS Code | Gratuit | Débutant → Avancé | Tout projet |
| PyCharm | Gratuit (Community) | Intermédiaire → Avancé | Projets Python dédiés |
| Jupyter | Gratuit | Débutant | Data science, apprentissage |


## 9 — Votre premier script Python

Créons ensemble votre **tout premier fichier Python** !

### Étape 1 : Créer un fichier
1. Ouvrez VS Code
2. Créez un nouveau fichier : `Ctrl + N` (ou `Cmd + N` sur Mac)
3. Sauvegardez-le avec le nom : **`bonjour.py`**

>  Les fichiers Python se terminent toujours par `.py`

### Étape 2 : Écrire du code
Copiez-collez (ou tapez) ce code :
```python
# Ceci est un commentaire (une ligne qui n'est pas exécutée)

# Afficher un message
print("Bienvenue dans Python !")

# Demander le prénom à l'utilisateur
prenom = input("Comment vous appelez-vous ? ")

# Afficher un message personnalisé
print(f"Bonjour, {prenom} ! Vous êtes désormais un programmeur Python !")
```

### Étape 3 : Exécuter le script
Dans VS Code, appuyez sur :
```
Bouton Run  (en haut à droite)
```
Ou depuis un Terminal :
```bash
python bonjour.py        # Windows
python3 bonjour.py       # macOS / Linux
```

### Ce que vous devriez voir :
```
Bienvenue dans Python !
Comment vous appelez-vous ? Marie
Bonjour, Marie ! Vous êtes désormais un programmeur Python !
```

Vous avez écrit et exécuté votre premier programme Python !


## 10 — Problèmes courants et solutions

| Problème | Cause probable | Solution |
|---|---|---|
| `'python' is not recognized` | Python n'est pas dans le PATH | Réinstaller avec l'option "Add to PATH" activée |
| `Permission denied` | Droits insuffisants | Utiliser `sudo` (Linux/Mac) ou exécuter en admin (Windows) |
| `ModuleNotFoundError` | Bibliothèque non installée | Installer avec `pip install nom_bibliothèque` |
| Deux versions de Python | Plusieurs versions installées | Utiliser `python3` ou spécifier le chemin exact |
| `SyntaxError` | Erreur dans le code | Vérifier les guillemets, les deux-points `:`, l'indentation |


## 11 — Glossaire

| Terme | Définition |
|---|---|
| **Python** | Langage de programmation interprété créé en 1991 |
| **Terminal / CMD** | Fenêtre noire où on tape des commandes texte |
| **PATH** | Liste des dossiers où l'ordinateur cherche les programmes |
| **pip** | Gestionnaire de paquets Python (pour installer des bibliothèques) |
| **Environnement virtuel** | Espace isolé pour un projet, évite les conflits |
| **IDE** | Éditeur de code spécialisé pour la programmation |
| **.py** | Extension des fichiers Python |
| **print()** | Fonction Python qui affiche du texte |
| **input()** | Fonction Python qui demande une donnée à l'utilisateur |
| **Bibliothèque** | Ensemble de fonctions pré-écrites pour vous aider |


## Et maintenant ?

Vous avez installé Python avec succès ! Voici les prochaines étapes suggérées :

1.  Explorez la [documentation officielle :octicons-link-external-16:](https://docs.python.org/3/){:target="_blank"}
2.  Construisez des **petits projets** pour vous familiariser

>  **Rappel** : La programmation s'apprend avant tout en **pratiquant**. 
> N'ayez pas peur de faire des erreurs — c'est le meilleur moyen d'apprendre !