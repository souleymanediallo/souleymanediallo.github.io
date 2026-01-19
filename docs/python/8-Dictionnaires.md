# Dictionnaires Python

Un dictionnaire est une collection de paires clé-valeur en Python. Il s'agit d'un type de données non ordonné et modifiable qui vous permet de stocker et d'accéder à des données à l'aide de clés plutôt que d'index.

Les dictionnaires sont créés en plaçant une liste de paires clé-valeur séparées par des virgules entre accolades (`{}`). Les clés et les valeurs sont séparées par deux-points (`:`).

Voici un exemple de dictionnaire en Python :
```
person = {'name': 'John', 'age': 30, 'country': 'USA'}
```

Vous pouvez accéder aux valeurs d'un dictionnaire à l'aide des touches.
```
print(person['name'])  # Output: 'John'
print(person['age'])   # Output: 30
```

Vous pouvez également utiliser la get()méthode pour accéder aux valeurs, qui renvoie une valeur par défaut si la clé n'est pas trouvée dans le dictionnaire.
```
print(person.get('name'))  # Output: 'John'
print(person.get('income', 0))  # Output: 0
```

Vous pouvez modifier les valeurs d'un dictionnaire en affectant une nouvelle valeur à une clé.
```
person['age'] = 35
print(person)  # Output: {'name': 'John', 'age': 35, 'country': 'USA'}
```

Vous pouvez ajouter de nouvelles paires clé-valeur à un dictionnaire à l'aide de l'opérateur d'affectation.
```
person['income'] = 50000
print(person)  # Output: {'name': 'John', 'age': 35, 'country': 'USA', 'income': 50000}
```

Vous pouvez supprimer des paires clé-valeur d'un dictionnaire à l'aide de l'instruction `del` ou de la méthode `pop()`.
```
del person['income']
print(person)  # Output: {'name': '
```

Vous pouvez parcourir les clés, les valeurs ou les éléments d'un dictionnaire à l'aide de la forboucle en Python.

Pour parcourir les clés d'un dictionnaire, vous pouvez utiliser la méthode `keys()` :

```
person = {
  'name': 'John Smith',
  'age': 30,
  'city': 'New York'
}

for key in person.keys():
  print(key)  # Output: 'name', 'age', 'city'
```

Pour parcourir les valeurs d'un dictionnaire, vous pouvez utiliser la méthode `values()` :
```
for value in person.values():
  print(value)  # Output: 'John Smith', 30, 'New York'
```

Pour parcourir les paires clé-valeur d'un dictionnaire, vous pouvez utiliser la méthode `items()` :
```
for key, value in person.items():
  print(key, value)  # Output: ('name', 'John Smith'), ('age', 30), ('city', 'New York')
```

Vous pouvez également utiliser la boucle `for` pour parcourir un dictionnaire en parcourant le dictionnaire lui-même :
```
for key in person:
  print(key, person[key])  # Output: ('name', 'John Smith'), ('age', 30), ('city', 'New York')
``` 