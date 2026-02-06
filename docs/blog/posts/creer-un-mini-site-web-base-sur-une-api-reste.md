---
date:
  created: 2026-01-23

---
# Créer un mini-site web basé sur une API REST avec Flask
On va créer un mini-site web en Python qui interroge une API publique et affiche les résultats.
On utilisera le micro-framework Flask pour le serveur web et la librairie requests pour faire les requêtes HTTP.
On utilisera une API publique gratuite, sans clé API, et simple à utiliser (<a href="https://www.openbrewerydb.org/documentation#random-brewery" target="_blank">Open Brewery DB</a>)

<!-- more -->

## Objectif

Créer un petit site web en Python :

- interroge une API publique via des requêtes HTTP
- affiche une liste de résultats (recherche)
- affiche une page détail (un élément)
- gère les erreurs, la pagination, et une structure de projet propre
  
## Ce que tu vas apprendre
- Différence entre **client** (ton site) et **serveur** (API)
- Requêtes **GET** + paramètres de query string (`?by_city=...&page=...`)
- Lire du **JSON** en Python
- Créer un **front** simple avec Flask + bootstrap + templates Jinja
- Structurer un projet, gérer les erreurs, et faire une mini “couche service”

## API choisie : Open Brewery DB
Endpoints utiles (exemples) :

- `GET /breweries` (liste, filtres, pagination)
- `GET /breweries?by_city=paris`
- `GET /breweries?by_state=california`
- `GET /breweries/search?query=dog`
- `GET /breweries/{id}` (détail)

Pagination :

- `page` et `per_page` (ex: `?page=1&per_page=20`)
- Par défaut, 20 résultats par page

## Prérequis
- Python 3.10+
- Savoir lancer un terminal, créer un dossier, exécuter un script Python
- Notions : variable, fonction, dictionnaire, liste

## Étape 1 : Créer le dossier du projet et un environnement de travail

Avant de commencer, essayons de comprendre la différence entre **client** et **serveur**.

- Le **client** est ton mini-site web (Flask) qui va faire des requêtes HTTP vers l’API.
- Le **serveur** est l’API publique (Open Brewery DB) qui va répondre aux requêtes du client.
  
Créer le dossier projet
```bash
mkdir brewfinder
cd brewfinder
```

Créer un environnement virtuel + installer les librairies
```bash
python -m venv venv
source venv/bin/activate  # mac/linux
# venv\Scripts\activate   # windows

python -m pip install flask requests
python -m pip freeze > requirements.txt
```

Check : Vérifier que les paquets sont bien installés
```bash
pip show flask
pip show requests
```

## Étape 2 : Créer une application Flask minimale

Créer le fichier de base
```bash
touch app.py
```

Écrire le code minimal dans `app.py`
```python title="app.py"
from flask import Flask

app = Flask(__name__)

@app.get("/")
def home():
    return "Hello, Brewfinder!"

if __name__ == "__main__":
    app.run(debug=True)
```

Lance :
```bash
python app.py
```

Ouvre : `http://127.0.0.1:5000/`

Vérifier que tu vois "Hello, Brewfinder!"

Pourquoi commencer par ça ? Parce qu’avant de parler d’API, on veut vérifier que Flask tourne.

## Étape 3 : Faire une requête GET vers l’API

On va utiliser la librairie `requests` pour faire une requête GET vers l’API

Avant d’intégrer au site, on teste l’API dans un script simple.

Créer `test_api.py`
```python title="test_api.py"
import requests

url = "https://api.openbrewerydb.org/v1/breweries?per_page=3"
result = requests.get(url)
print(result.status_code)
print(result.json())
```

Lance :
```bash
python test_api.py
```

Check :

- 200 (souvent)
- et une liste de brasseries (JSON -> Python list) au nombre d’éléments demandé (3)

Explication :
On importe la librairie `requests`, on définit l’URL de l’endpoint, puis on fait une requête GET avec `requests.get()`.
La requête GET vers l’endpoint `/breweries` avec le paramètre `per_page=3` pour limiter à 3 résultats.
C'est l'équivalent du navigateur qui fait une requête HTTP GET vers une URL mais ici c’est notre script Python qui le fait.

L’API te répond avec une réponse HTTP que tu stockes dans `result`.
Le code de statut HTTP est dans `result.status_code` (200 = OK). 

Ça veut dire : la requête est valide, l’API a compris la demande, la réponse a été générée correctement et tout s’est bien passé.

Exemples d'autres codes de statuts :

- 400 : Bad Request (mauvaise requête)
- 401 : Unauthorized (non autorisé)
- 404 : Not Found (ressource non trouvée)
- 500 : Internal Server Error (erreur serveur)
- 503 : Service Unavailable (service indisponible)
  
```python
print(result.json())
```

Tu affiches le contenu de la réponse en format Python.

L’API renvoie du JSON, et `result.json()` le transforme en :

- list

- contenant des dict

Analyse la structure des données renvoyées.

```python
200
[
  { ... brasserie 1 ... },
  { ... brasserie 2 ... },
  { ... brasserie 3 ... }
]
```

Structure globale : une liste de brasseries (3 éléments)
```python
[
   {...},   # brasserie 1 (dict)
   {...},   # brasserie 2 (dict)
   {...}    # brasserie 3 (dict)
]
```

C’est une liste Python (list) et chaque élément est un dictionnaire (dict).

Donc en python, tu peux faire :
```python
type(result.json())  # list
type(result.json()[0])  # dict
```

Structure d'une brasserie (1 objet) :
```python
{
 'id': '5128df48-79fc-4f0f-8b52-d06be54d0cec',
 'name': '(405) Brewing Co',
 'brewery_type': 'micro',
 'city': 'Norman',
 'state': 'Oklahoma',
 'country': 'United States',
 'phone': '4058160490',
 'website_url': 'http://www.405brewing.com'
}
```

Faire un test :
```python
data = result.json()

print(type(data))         # type de la réponse
print(type(data[0]))      # type du 1er élément

print(data[0]["name"])    # nom de la 1ère brasserie
print(data[0]["city"])    # ville
print(data[0]["country"]) # pays
```

Tu verras que tu peux accéder aux champs de chaque brasserie via les clés du dictionnaire.

```python
<class 'list'>
<class 'dict'>
(405) Brewing Co
Norman
United States
```

Ce que tu dois retenir : L'API te renvoie des données structurées en JSON, que tu peux manipuler en Python comme des listes et des dictionnaires.

## Étape 4 : Créer la page d’accueil avec la liste des brasseries

On va maintenant intégrer la requête API dans notre application Flask pour afficher la liste des brasseries sur la page d’accueil.

On commence par vérifier que Flask sait rendre une page HTML depuis templates.

Mofifie `app.py` :
```python title="app.py"
from flask import Flask, render_template

app = Flask(__name__)

@app.get("/")
def index():
    return render_template("index.html")

if __name__ == "__main__":
    app.run(debug=True)
```

Check : lance l’application 
```bash
python app.py
```

Puis ouvre : `http://127.0.0.1:5000/`

Tu devrais avoir une erreur “TemplateNotFound: index.html” (normal), car il n’existe pas encore.

Créer templates/index.html (page simple)

```html title="templates/index.html"
<!doctype html>
<html lang="fr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Brewfinder</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB" crossorigin="anonymous">
  </head>
  <body>
  <section class="container text-center bg-light mt-3 p-5 rounded">
    <h1>Brewfinder</h1>
    <p>Ma première page avec Flask + templates.</p>
  </section>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js" integrity="sha384-FKyoEForCGlyvwx9Hj09JcYn3nv7wiPVlz7YYwJrWVcXK/BmnVDxM+D2scQbITxI" crossorigin="anonymous"></script>
  </body>
</html>
```

Check : recharge la page → tu vois le titre et le texte.

## Étape 5 — Ajouter un layout (base template) et intégrer Bootstrap

Le but d’un layout : ne pas répéter le même HTML (head, navbar, footer) sur toutes les pages.

Créer `templates/layout.html`   
```html title="templates/layout.html"
<!doctype html>
<html lang="fr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Brewfinder</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB" crossorigin="anonymous">
  </head>
  <body class="d-flex flex-column min-vh-100">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand" href="/">🍺 Brewfinder</a>
      </div>
    </nav>

    <main class="flex-grow-1">
      {% block content %}
      {% endblock %}
    </main>

    <footer class="bg-dark text-center py-4 mt-auto">
      <small class="text-light">Bootstrap + Flask + API</small>
    </footer>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js" integrity="sha384-FKyoEForCGlyvwx9Hj09JcYn3nv7wiPVlz7YYwJrWVlz7YYwJrWVcXK/BmnVDxM+D2scQbITxI" crossorigin="anonymous"></script>
  </body>
</html>
```

Modifie templates/index.html pour “hériter” du layout
```html title="templates/index.html"
{% extends "layout.html" %}

{% block content %}
<section>
    <div class="container mt-5">
        <div class="row">
            <div class="container mt-5 text-center">
                <h1 class="mb-4">Bienvenue sur Brewfinder</h1>
                <p>Recherchez des brasseries partout dans le monde !</p>
            </div>
        </div>
    </div>
</section>
{% endblock %}
```

## Étape 6 : Ajouter le formulaire sur la page index

A venir...



