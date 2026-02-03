# Découvrir le terminal

## Introduction

Le terminal (aussi appelé console, ligne de commande, ou shell) est une interface textuelle qui permet d'interagir 
avec votre ordinateur en tapant des commandes. Pour un développeur Python, maîtriser le terminal est essentiel.

### Pourquoi utiliser le terminal ?

- **Efficacité** : Certaines tâches sont plus rapides en ligne de commande
- **Automatisation** : Possibilité de créer des scripts pour automatiser des tâches
- **Développement** : Gérer des projets, installer des packages, exécuter des programmes
- **Serveurs** : Les serveurs n'ont souvent pas d'interface graphique

## 1. Accéder au Terminal

### Windows
- **PowerShell** : Rechercher "PowerShell" dans le menu Démarrer
- **Invite de commandes** : Rechercher "cmd" 
- **Git Bash** : Si Git est installé (recommandé pour une expérience Unix-like)
- **Windows Terminal** : Application moderne qui combine plusieurs shells

### macOS
- **Terminal** : Applications → Utilitaires → Terminal
- Ou : `Cmd + Espace` puis taper "Terminal"

### Linux
- **Raccourci clavier** : Généralement `Ctrl + Alt + T`
- Ou : Chercher "Terminal" dans les applications


## 2. Comprendre l'Interface du Terminal

Quand vous ouvrez le terminal, vous voyez quelque chose comme :

```bash
utilisateur@ordinateur:~$
```

Cette ligne s'appelle le **prompt** et contient :

- **utilisateur** : votre nom d'utilisateur
- **ordinateur** : le nom de votre machine
- **~** : le répertoire actuel (~ signifie le répertoire personnel)
- **$** : indique que vous êtes un utilisateur normal (# pour root/admin)

## 3. Commandes de Base pour la Navigation

### pwd (Print Working Directory)
Affiche le chemin du répertoire actuel

```bash
pwd
# Résultat : /home/utilisateur
```

### ls (List)
Liste les fichiers et dossiers du répertoire actuel

```bash
# Liste simple
ls

# Liste détaillée avec permissions, taille, date
ls -l

# Afficher les fichiers cachés
ls -a

# Combinaison (détaillé + cachés)
ls -la

# Trier par date de modification
ls -lt
```

**Windows (cmd/PowerShell)** : utiliser `dir` au lieu de `ls`

### cd (Change Directory)
Change de répertoire

```bash
# Aller dans un dossier
cd Documents

# Remonter d'un niveau
cd ..

# Aller au répertoire personnel
cd ~
# ou simplement
cd

# Aller à la racine du système
cd /

# Revenir au répertoire précédent
cd -

# Chemin absolu (depuis la racine)
cd /home/utilisateur/Documents

# Chemin relatif (depuis la position actuelle)
cd ../Images
```

## 4. Manipulation de Fichiers et Dossiers

### mkdir (Make Directory)
Créer un nouveau dossier

```bash
# Créer un dossier
mkdir mon_projet

# Créer plusieurs dossiers
mkdir dossier1 dossier2 dossier3

# Créer une arborescence de dossiers
mkdir -p projets/python/mon_app
```

### touch
Créer un fichier vide (Unix/Mac/Git Bash)

```bash
touch fichier.txt
touch script.py
```

**Windows (PowerShell)** :
```powershell
New-Item fichier.txt -ItemType File
```

### cp (Copy)
Copier des fichiers ou dossiers

```bash
# Copier un fichier
cp source.txt destination.txt

# Copier dans un autre dossier
cp fichier.txt /chemin/vers/dossier/

# Copier un dossier entier (récursif)
cp -r dossier_source/ dossier_destination/
```

**Windows (cmd)** : utiliser `copy` pour les fichiers, `xcopy` pour les dossiers

### mv (Move)
Déplacer ou renommer des fichiers

```bash
# Renommer un fichier
mv ancien_nom.txt nouveau_nom.txt

# Déplacer un fichier
mv fichier.txt /chemin/vers/destination/

# Déplacer et renommer
mv fichier.txt /autre/dossier/nouveau_nom.txt
```

**Windows (cmd)** : utiliser `move` ou `ren` pour renommer

### rm (Remove)
Supprimer des fichiers ou dossiers

```bash
# Supprimer un fichier
rm fichier.txt

# Supprimer plusieurs fichiers
rm fichier1.txt fichier2.txt

# Supprimer un dossier vide
rmdir dossier_vide

# Supprimer un dossier et son contenu (ATTENTION !)
rm -r dossier/

# Forcer la suppression sans confirmation
rm -rf dossier/
```

**ATTENTION** : `rm -rf` est dangereux ! Il supprime sans confirmation et sans possibilité de récupération.

**Windows (cmd)** : utiliser `del` pour les fichiers, `rmdir` ou `rd /s` pour les dossiers

## 5. Visualiser le Contenu des Fichiers

### cat (Concatenate)
Afficher le contenu d'un fichier

```bash
cat fichier.txt

# Afficher plusieurs fichiers
cat fichier1.txt fichier2.txt

# Afficher avec numéros de ligne
cat -n fichier.txt
```

**Windows (cmd)** : utiliser `type`

### less / more
Visualiser un fichier page par page

```bash
less fichier.txt
# Navigation : espace (page suivante), b (page précédente), q (quitter)

more fichier.txt
```

**Windows (PowerShell)** : utiliser `more`

### head / tail
Afficher le début ou la fin d'un fichier

```bash
# 10 premières lignes
head fichier.txt

# 5 premières lignes
head -n 5 fichier.txt

# 10 dernières lignes
tail fichier.txt

# Suivre un fichier en temps réel (utile pour les logs)
tail -f application.log
```

## 6. Commandes Spécifiques à Python

### python / python3
Exécuter l'interpréteur Python

```bash
# Lancer Python interactif
python
# ou
python3

# Exécuter un script
python script.py
python3 mon_programme.py

# Exécuter du code directement
python -c "print('Hello World')"

# Afficher la version de Python
python --version
```

### pip
Gestionnaire de packages Python

```bash
# Installer un package
pip install numpy
pip install requests pandas matplotlib

# Installer une version spécifique
pip install django==6.0.0

# Installer depuis requirements.txt
pip install -r requirements.txt

# Lister les packages installés
pip list

# Afficher les infos d'un package
pip show numpy

# Mettre à jour un package
pip install --upgrade numpy

# Désinstaller un package
pip uninstall numpy

# Créer un fichier requirements.txt
pip freeze > requirements.txt
```

### Environnements Virtuels

```bash
# Créer un environnement virtuel
python -m venv mon_env

# Activer l'environnement (Linux/Mac)
source mon_env/bin/activate

# Activer l'environnement (Windows)
mon_env\Scripts\activate

# Désactiver l'environnement
deactivate
```

## 7. Recherche et Filtrage

### grep (Global Regular Expression Print)
Rechercher du texte dans des fichiers

```bash
# Rechercher "erreur" dans un fichier
grep "erreur" log.txt

# Recherche insensible à la casse
grep -i "erreur" log.txt

# Rechercher dans tous les fichiers .py
grep "def " *.py

# Rechercher récursivement dans tous les sous-dossiers
grep -r "TODO" .

# Afficher le numéro de ligne
grep -n "import" script.py
```

**Windows (PowerShell)** : utiliser `Select-String`

### find
Rechercher des fichiers

```bash
# Trouver tous les fichiers .py
find . -name "*.py"

# Trouver tous les fichiers modifiés dans les 7 derniers jours
find . -mtime -7

# Trouver les fichiers de plus de 100MB
find . -size +100M
```

**Windows** : utiliser `dir /s` ou PowerShell `Get-ChildItem -Recurse`

## 8. Redirection et Pipes

### Redirection de sortie

```bash
# Écrire la sortie dans un fichier (écrase le contenu)
ls > liste_fichiers.txt
python script.py > resultat.txt

# Ajouter à la fin d'un fichier (sans écraser)
echo "Nouvelle ligne" >> fichier.txt
python script.py >> log.txt

# Rediriger les erreurs
python script.py 2> erreurs.txt

# Rediriger sortie standard ET erreurs
python script.py > output.txt 2>&1
```

### Pipes (|)
Enchaîner des commandes

```bash
# Compter le nombre de fichiers .py
ls *.py | wc -l

# Afficher les lignes contenant "def" dans tous les .py
cat *.py | grep "def"

# Trier et afficher les 10 premiers
ls -l | sort | head -n 10
```

## 9. Raccourcis Clavier Utiles

### Navigation
- `Ctrl + A` : Aller au début de la ligne
- `Ctrl + E` : Aller à la fin de la ligne
- `Ctrl + U` : Effacer du curseur au début de la ligne
- `Ctrl + K` : Effacer du curseur à la fin de la ligne
- `Ctrl + W` : Effacer le mot précédent
- `Alt + B` : Reculer d'un mot
- `Alt + F` : Avancer d'un mot

### Historique
- `↑` / `↓` : Naviguer dans l'historique des commandes
- `Ctrl + R` : Rechercher dans l'historique (très utile !)
- `history` : Afficher l'historique des commandes
- `!!` : Répéter la dernière commande
- `!n` : Exécuter la commande numéro n de l'historique

### Contrôle
- `Ctrl + C` : Arrêter/Interrompre le processus en cours
- `Ctrl + D` : Fermer le terminal (EOF)
- `Ctrl + Z` : Mettre en pause le processus
- `Ctrl + L` : Effacer l'écran (équivalent de `clear`)
- `Tab` : Auto-complétion (TRÈS UTILE !)

## 10. Gestion des Processus

### ps (Process Status)
Afficher les processus en cours

```bash
# Processus de l'utilisateur actuel
ps

# Tous les processus
ps aux

# Filtrer les processus Python
ps aux | grep python
```

**Windows** : utiliser le Gestionnaire des tâches ou `tasklist` en cmd

### kill
Arrêter un processus

```bash
# Arrêter proprement un processus
kill PID

# Forcer l'arrêt
kill -9 PID

# Arrêter tous les processus Python
pkill python
```

**Windows (cmd)** : utiliser `taskkill /PID numero` ou `taskkill /IM nom_processus.exe`

### top / htop
Moniteur de processus en temps réel

```bash
top
# ou (plus convivial si installé)
htop
```

**Windows** : Gestionnaire des tâches ou `Get-Process` en PowerShell

## 11. Permissions (Linux/Mac)

### chmod (Change Mode)
Modifier les permissions d'un fichier

```bash
# Rendre un script exécutable
chmod +x script.py

# Permissions complètes pour le propriétaire
chmod 755 fichier.txt

# Lecture seule pour tous
chmod 444 fichier.txt
```

Les chiffres représentent :

- **7** = lecture + écriture + exécution (rwx)
- **6** = lecture + écriture (rw-)
- **5** = lecture + exécution (r-x)
- **4** = lecture seule (r--)

### chown (Change Owner)
Changer le propriétaire d'un fichier

```bash
# Changer le propriétaire
sudo chown utilisateur fichier.txt

# Changer le propriétaire et le groupe
sudo chown utilisateur:groupe fichier.txt
```

## 12. Variables d'Environnement

### Afficher les variables

```bash
# Afficher toutes les variables d'environnement
env
# ou
printenv

# Afficher une variable spécifique
echo $PATH
echo $HOME
echo $USER
```

**Windows (cmd)** : utiliser `set` ou `echo %PATH%`

### Définir des variables

```bash
# Temporaire (session actuelle uniquement)
export MA_VARIABLE="valeur"

# Vérifier
echo $MA_VARIABLE

# Ajouter au PATH
export PATH=$PATH:/nouveau/chemin
```

Pour rendre permanentes les modifications, ajouter ces lignes à :
- Linux/Mac : `~/.bashrc` ou `~/.zshrc`
- Windows : Variables d'environnement système

## 13. Commandes Réseau Utiles

### ping
Tester la connectivité réseau

```bash
ping google.com
ping 8.8.8.8

# Limiter à 4 paquets
ping -c 4 google.com
```

### curl
Télécharger ou interroger des URLs

```bash
# Télécharger un fichier
curl -O https://example.com/fichier.zip

# Afficher le contenu d'une page
curl https://api.github.com/users/python

# Envoyer une requête POST
curl -X POST -d "param=value" https://example.com/api
```

### wget
Télécharger des fichiers

```bash
wget https://example.com/fichier.zip

# Télécharger en arrière-plan
wget -b https://example.com/gros_fichier.zip
```

## 14. Archivage et Compression

### tar
Créer et extraire des archives

```bash
# Créer une archive
tar -cvf archive.tar dossier/

# Créer une archive compressée (gzip)
tar -czvf archive.tar.gz dossier/

# Extraire une archive
tar -xvf archive.tar

# Extraire une archive gzip
tar -xzvf archive.tar.gz

# Lister le contenu sans extraire
tar -tvf archive.tar.gz
```

Options :
- **c** : create (créer)
- **x** : extract (extraire)
- **v** : verbose (détaillé)
- **f** : file (fichier)
- **z** : gzip compression

### zip / unzip

```bash
# Créer un zip
zip -r archive.zip dossier/

# Extraire un zip
unzip archive.zip

# Lister le contenu
unzip -l archive.zip
```

## 15. Astuces pour Développeurs Python

### Créer la structure d'un projet rapidement

```bash
mkdir mon_projet
cd mon_projet
mkdir src tests docs
touch README.md requirements.txt .gitignore
touch src/__init__.py src/main.py
touch tests/__init__.py tests/test_main.py
```

### Script d'initialisation de projet

Créer un fichier `init_projet.sh` :

```bash
#!/bin/bash
# Script d'initialisation de projet Python

PROJECT_NAME=$1

if [ -z "$PROJECT_NAME" ]; then
    echo "Usage: ./init_projet.sh nom_du_projet"
    exit 1
fi

mkdir $PROJECT_NAME
cd $PROJECT_NAME

# Structure de dossiers
mkdir src tests docs

# Fichiers de base
touch README.md
touch requirements.txt
touch .gitignore
touch src/__init__.py
touch src/main.py
touch tests/__init__.py

# Environnement virtuel
python -m venv venv

echo "Projet $PROJECT_NAME initialisé avec succès !"
echo "Pour activer l'environnement : source venv/bin/activate"
```

Rendre le script exécutable : `chmod +x init_projet.sh`

Utiliser : `./init_projet.sh mon_super_projet`

### Alias utiles

Ajouter dans `~/.bashrc` ou `~/.zshrc` :

```bash
# Raccourcis Python
alias py='python3'
alias pip='pip3'
alias venv='python3 -m venv'
alias activate='source venv/bin/activate'

# Raccourcis généraux
alias ll='ls -lah'
alias ..='cd ..'
alias ...='cd ../..'
alias cls='clear'
```

Puis recharger : `source ~/.bashrc`

## 16. Commandes Avancées

### xargs
Construire et exécuter des commandes depuis l'entrée standard

```bash
# Supprimer tous les fichiers .pyc
find . -name "*.pyc" | xargs rm

# Compter les lignes de tous les fichiers .py
find . -name "*.py" | xargs wc -l
```

### awk
Traitement de texte et extraction de colonnes

```bash
# Extraire la 2ème colonne
ls -l | awk '{print $2}'

# Calculer l'espace disque total utilisé
ls -l | awk '{sum += $5} END {print sum}'
```

### sed
Édition de flux (stream editor)

```bash
# Remplacer du texte
sed 's/ancien/nouveau/g' fichier.txt

# Supprimer les lignes vides
sed '/^$/d' fichier.txt

# Modifier en place
sed -i 's/ancien/nouveau/g' fichier.txt
```

## 17. Exercices Pratiques

### Exercice 1 : Navigation
1. Affichez votre répertoire actuel
2. Listez tous les fichiers (y compris cachés)
3. Créez un dossier `exercices_python`
4. Allez dans ce dossier
5. Revenez au répertoire parent

### Exercice 2 : Création de projet
1. Créez un projet avec la structure suivante :
```
mon_app/
├── src/
│   ├── __init__.py
│   └── app.py
├── tests/
│   └── test_app.py
├── README.md
└── requirements.txt
```

### Exercice 3 : Manipulation de fichiers
1. Créez un fichier `notes.txt`
2. Ajoutez-y du texte avec `echo "Ma première note" > notes.txt`
3. Ajoutez une autre ligne avec `echo "Ma deuxième note" >> notes.txt`
4. Affichez le contenu
5. Copiez le fichier en `notes_backup.txt`

### Exercice 4 : Python et pip
1. Vérifiez votre version de Python
2. Créez un environnement virtuel
3. Activez-le
4. Installez `requests` et `beautifulsoup4`
5. Créez un fichier `requirements.txt`
6. Désactivez l'environnement

### Exercice 5 : Recherche
1. Créez plusieurs fichiers `.py` avec différents contenus
2. Utilisez `grep` pour trouver tous les fichiers contenant `import`
3. Utilisez `find` pour lister tous les fichiers `.py`

## 18. Ressources Supplémentaires

### Sites Web
- **SS64.com** : Référence complète des commandes (Windows, Linux, Mac)
- **ExplainShell.com** : Explique les commandes complexes
- **TLDR Pages** : Exemples simplifiés de commandes

### Commandes d'aide

```bash
# Manuel d'une commande (Linux/Mac)
man ls
man grep

# Aide intégrée
ls --help
python --help

# Commande "which" pour trouver l'emplacement
which python
which pip
```

### Cheat Sheets
- Imprimez et gardez à portée de main un cheat sheet des commandes
- Créez vos propres notes avec vos commandes fréquentes

## 19. Conseils Finaux

### Bonnes Pratiques
1. **Utilisez Tab** pour l'auto-complétion : gain de temps énorme
2. **Utilisez Ctrl+R** pour rechercher dans l'historique
3. **Lisez les messages d'erreur** : ils sont souvent explicites
4. **Testez d'abord** avec `ls` ou `echo` avant des commandes destructrices
5. **Faites des sauvegardes** avant d'utiliser `rm -rf`
6. **Utilisez `--help`** quand vous découvrez une nouvelle commande
7. **Créez des alias** pour vos commandes fréquentes
8. **Documentez vos scripts** avec des commentaires

### Pour Aller Plus Loin
- Apprenez **vim** ou **nano** pour éditer des fichiers dans le terminal
- Maîtrisez **tmux** ou **screen** pour gérer plusieurs sessions
- Explorez **bash scripting** pour automatiser vos tâches
- Découvrez **zsh** et **oh-my-zsh** pour un terminal amélioré
- Utilisez **Docker** pour containeriser vos applications Python

## En résumé

Le terminal peut sembler intimidant au début, mais c'est un outil puissant qui deviendra vite indispensable. 
Commencez par maîtriser les commandes de base (navigation, création de fichiers), puis progressez vers des usages plus avancés.

**La pratique est la clé** : utilisez le terminal quotidiennement pour vos projets Python, et vous deviendrez rapidement à l'aise.
