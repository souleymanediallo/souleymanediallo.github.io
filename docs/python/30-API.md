# Les API

## Définition 2

Une API, ou Interface de Programmation Applicative (Application Programming Interface en anglais), est un ensemble de règles et de protocoles qui permettent à des logiciels de communiquer entre eux. Elle définit les méthodes et les formats de données à utiliser pour l'échange d'informations.


En Python, il existe de nombreuses bibliothèques et frameworks qui fournissent des API pour faciliter l'intégration de fonctionnalités spécifiques dans vos applications. Voici quelques exemples d'API couramment utilisées en Python :

### API de requêtes HTTP avec la bibliothèque `requests` :

``` 
import requests

response = requests.get('https://api.example.com/data')
data = response.json()
``` 

### API de manipulation de fichiers JSON avec la bibliothèque standard json 2 :

```
import json

data = {'name': 'John', 'age': 30}
json_data = json.dumps(data)

# Utilisation de l'API pour enregistrer les données dans un fichier
with open('data.json', 'w') as file:
    file.write(json_data)

# Utilisation de l'API pour lire les données depuis un fichier
with open('data.json', 'r') as file:
    json_data = file.read()
    data = json.loads(json_data)

```

### API de manipulation de bases de données relationnelles avec la bibliothèque sqlite3 (intégrée à Python) :

```
import sqlite3

# Connexion à une base de données SQLite
conn = sqlite3.connect('example.db')

# Création d'une table
conn.execute('CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT, age INTEGER)')

# Insertion de données
conn.execute("INSERT INTO users (name, age) VALUES ('John', 30)")
conn.execute("INSERT INTO users (name, age) VALUES ('Alice', 25)")

# Récupération des données
cursor = conn.execute('SELECT * FROM users')
for row in cursor:
    print(row)

# Fermeture de la connexion à la base de données
conn.close()

```

Ces exemples illustrent différents types d'API utilisées en Python pour des tâches telles que les requêtes HTTP, la manipulation de données JSON et l'interaction avec une base de données SQLite. Il existe de nombreuses autres API pour une variété de domaines, tels que les réseaux sociaux, les services de cloud, les services de messagerie, etc.