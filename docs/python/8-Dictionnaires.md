# Les dictionnaires

## Introduction

Un dictionnaire est l'une des structures de données les plus puissantes de Python. Contrairement à une liste qui stocke des éléments accessibles par leur position, un dictionnaire stocke des données sous forme de paires **clé-valeur**. Chaque valeur est associée à une clé unique, ce qui permet de retrouver une information rapidement sans avoir à connaître sa position.

On peut imaginer un dictionnaire Python comme un vrai dictionnaire de langue : on cherche un mot (la clé) et on obtient sa définition (la valeur). Ce modèle est extrêmement utile pour représenter des objets du monde réel, comme un utilisateur avec son nom, son âge et son adresse, ou encore un produit avec son prix et sa quantité en stock.

Depuis Python 3.7, les dictionnaires conservent l'ordre d'insertion des clés, ce qui les rend encore plus prévisibles à utiliser.


## 1. Créer un dictionnaire

Un dictionnaire se définit avec des accolades `{}`. Chaque paire clé-valeur est écrite sous la forme `clé: valeur`, et les paires sont séparées par des virgules. On peut aussi créer un dictionnaire vide, puis le remplir progressivement.

```python
# Un dictionnaire vide
mon_dict = {}

# Un dictionnaire représentant un étudiant
etudiant = {
    'nom': 'Ousmane',
    'age': 22,
    'ville': 'Paris',
    'moyenne': 14.5
}

# Un dictionnaire avec des types de valeurs variés
produit = {
    'nom': 'Ordinateur',
    'prix': 899.99,
    'disponible': True,
    'quantite': 12
}
```

Il est également possible de créer un dictionnaire avec la fonction intégrée `dict()`, en passant les paires clé-valeur comme arguments nommés.

```python
etudiant = dict(nom='Ousmane', age=22, ville='Paris')
print(etudiant)  # Affiche : {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}
```

Les clés d'un dictionnaire doivent être de type immuable, c'est-à-dire qu'elles ne peuvent pas changer après leur création. On utilise le plus souvent des chaînes de caractères ou des entiers comme clés. En revanche, les valeurs peuvent être de n'importe quel type : une chaîne, un nombre, une liste, un autre dictionnaire, etc.


## 2. Accéder aux valeurs

### Par la clé entre crochets

Pour accéder à la valeur associée à une clé, on utilise la syntaxe `dictionnaire[clé]`. Si la clé n'existe pas dans le dictionnaire, Python lève une erreur `KeyError`.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

print(etudiant['nom'])    # Affiche : Ousmane
print(etudiant['age'])    # Affiche : 22

print(etudiant['email'])  # Erreur : KeyError: 'email'
```

### Avec la méthode get()

La méthode `get()` est une alternative plus sûre. Si la clé n'existe pas, elle retourne `None` par défaut, ou une valeur de remplacement qu'on peut définir soi-même, sans lever d'erreur.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

print(etudiant.get('nom'))              # Affiche : Ousmane
print(etudiant.get('email'))            # Affiche : None
print(etudiant.get('email', 'inconnu')) # Affiche : inconnu
```

L'utilisation de `get()` est recommandée lorsqu'on n'est pas certain que la clé existe, ce qui est fréquent dans les programmes réels.


## 3. Modifier un dictionnaire

### Modifier une valeur existante

Pour modifier la valeur associée à une clé existante, on accède à la clé et on lui affecte une nouvelle valeur, comme on le ferait avec une variable.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

etudiant['age'] = 23
print(etudiant)  # Affiche : {'nom': 'Ousmane', 'age': 23, 'ville': 'Paris'}
```

### Ajouter une nouvelle paire clé-valeur

Si on affecte une valeur à une clé qui n'existe pas encore, Python l'ajoute automatiquement au dictionnaire.

```python
etudiant = {'nom': 'Ousmane', 'age': 22}

etudiant['email'] = 'ousmane@example.com'
print(etudiant)  # Affiche : {'nom': 'Ousmane', 'age': 22, 'email': 'ousmane@example.com'}
```

### La méthode update()

La méthode `update()` permet de mettre à jour plusieurs clés à la fois, ou de fusionner un autre dictionnaire dans le dictionnaire courant. Les clés existantes sont mises à jour, et les nouvelles clés sont ajoutées.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

etudiant.update({'age': 23, 'email': 'ousmane@example.com'})
print(etudiant)
# Affiche : {'nom': 'Ousmane', 'age': 23, 'ville': 'Paris', 'email': 'ousmane@example.com'}
```


## 4. Supprimer des éléments

### La méthode pop()

La méthode `pop()` supprime la clé spécifiée et retourne la valeur qui lui était associée. Si la clé n'existe pas et qu'aucune valeur par défaut n'est fournie, une erreur `KeyError` est levée.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

valeur = etudiant.pop('ville')
print(valeur)    # Affiche : Paris
print(etudiant)  # Affiche : {'nom': 'Ousmane', 'age': 22}

# Avec une valeur par défaut si la clé n'existe pas
valeur = etudiant.pop('email', 'non trouvé')
print(valeur)    # Affiche : non trouvé
```

### L'instruction del

L'instruction `del` supprime une paire clé-valeur directement, sans retourner la valeur.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

del etudiant['ville']
print(etudiant)  # Affiche : {'nom': 'Ousmane', 'age': 22}
```

### La méthode popitem()

La méthode `popitem()` supprime et retourne la dernière paire clé-valeur insérée dans le dictionnaire, sous forme de tuple `(clé, valeur)`.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

paire = etudiant.popitem()
print(paire)     # Affiche : ('ville', 'Paris')
print(etudiant)  # Affiche : {'nom': 'Ousmane', 'age': 22}
```

### La méthode clear()

La méthode `clear()` vide entièrement le dictionnaire. La variable existe toujours mais ne contient plus aucune paire clé-valeur.

```python
etudiant = {'nom': 'Ousmane', 'age': 22}

etudiant.clear()
print(etudiant)  # Affiche : {}
```


## 5. Parcourir un dictionnaire

### Parcourir les clés

Par défaut, lorsqu'on utilise une boucle `for` sur un dictionnaire, on itère sur ses clés. On peut aussi appeler explicitement la méthode `keys()` pour plus de clarté.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

for cle in etudiant:
    print(cle)
# Affiche : nom, age, ville

# Avec keys() explicitement
for cle in etudiant.keys():
    print(cle)
```

### Parcourir les valeurs

La méthode `values()` permet d'itérer directement sur les valeurs du dictionnaire.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

for valeur in etudiant.values():
    print(valeur)
# Affiche : Ousmane, 22, Paris
```

### Parcourir les paires clé-valeur

La méthode `items()` retourne chaque paire clé-valeur sous forme de tuple. C'est la façon la plus complète de parcourir un dictionnaire, et la plus utilisée en pratique.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

for cle, valeur in etudiant.items():
    print(f"{cle} : {valeur}")
# Affiche :
# nom : Ousmane
# age : 22
# ville : Paris
```


## 6. Les méthodes utiles sur les dictionnaires

### Connaître le nombre de paires : len()

La fonction `len()` retourne le nombre de paires clé-valeur dans un dictionnaire.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}
print(len(etudiant))  # Affiche : 3
```

### Vérifier la présence d'une clé : in

L'opérateur `in` vérifie si une clé est présente dans un dictionnaire. Il retourne `True` ou `False`. Cette vérification porte sur les clés uniquement, pas sur les valeurs.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

print('nom' in etudiant)    # Affiche : True
print('email' in etudiant)  # Affiche : False
```

### Obtenir toutes les clés, valeurs, paires

Les méthodes `keys()`, `values()` et `items()` retournent des vues dynamiques sur le dictionnaire. Ces vues reflètent automatiquement les modifications apportées au dictionnaire après leur création.

```python
etudiant = {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}

print(etudiant.keys())    # Affiche : dict_keys(['nom', 'age', 'ville'])
print(etudiant.values())  # Affiche : dict_values(['Alice', 22, 'Paris'])
print(etudiant.items())   # Affiche : dict_items([('nom', 'Ousmane'), ('age', 22), ('ville', 'Paris')])
```

### Copier un dictionnaire : copy()

La méthode `copy()` crée une copie superficielle du dictionnaire. Cela signifie qu'une modification de la copie n'affecte pas le dictionnaire original, à condition que les valeurs soient elles-mêmes immuables.

```python
original = {'nom': 'Ousmane', 'age': 22}
copie = original.copy()

copie['age'] = 30
print(original)  # Affiche : {'nom': 'Ousmane', 'age': 22}  (inchangé)
print(copie)     # Affiche : {'nom': 'Ousmane', 'age': 30}
```

Attention : si on fait simplement `copie = original`, les deux variables pointent vers le même dictionnaire en mémoire. Modifier l'une modifiera aussi l'autre.

### La méthode setdefault()

La méthode `setdefault()` retourne la valeur associée à une clé si elle existe. Si la clé n'existe pas, elle l'ajoute avec une valeur par défaut et retourne cette valeur.

```python
etudiant = {'nom': 'Ousmane', 'age': 22}

# La clé 'nom' existe déjà, setdefault retourne sa valeur sans la modifier
print(etudiant.setdefault('nom', 'Inconnu'))  # Affiche : Ousmane

# La clé 'ville' n'existe pas, elle est ajoutée avec la valeur par défaut
print(etudiant.setdefault('ville', 'Paris'))  # Affiche : Paris
print(etudiant)  # Affiche : {'nom': 'Ousmane', 'age': 22, 'ville': 'Paris'}
```


## 7. Les dictionnaires imbriqués

Un dictionnaire peut contenir d'autres dictionnaires comme valeurs. C'est une façon naturelle de représenter des structures de données hiérarchiques, comme des fiches d'étudiants, des catalogues de produits, ou des configurations complexes.

```python
etudiants = {
    'ousmane': {
        'age': 22,
        'ville': 'Paris',
        'notes': [14, 16, 12]
    },
    'issa': {
        'age': 24,
        'ville': 'Lyon',
        'notes': [11, 13, 15]
    }
}

# Accéder à une valeur imbriquée
print(etudiants['ousmane']['ville'])      # Affiche : Paris
print(etudiants['issa']['notes'][1])     # Affiche : 13

# Parcourir un dictionnaire imbriqué
for nom, infos in etudiants.items():
    print(f"{nom} habite à {infos['ville']} et a {infos['age']} ans")
# Affiche :
# ousmane habite à Paris et a 22 ans
# issa habite à Lyon et a 24 ans
```


## 8. La compréhension de dictionnaire

Tout comme les listes, les dictionnaires peuvent être construits de façon concise avec une syntaxe de compréhension. La forme générale est : `{clé: valeur for element in iterable if condition}`.

```python
# Créer un dictionnaire associant chaque nombre à son carré
carres = {x: x**2 for x in range(1, 6)}
print(carres)  # Affiche : {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Inverser les clés et les valeurs d'un dictionnaire
original = {'a': 1, 'b': 2, 'c': 3}
inverse = {valeur: cle for cle, valeur in original.items()}
print(inverse)  # Affiche : {1: 'a', 2: 'b', 3: 'c'}

# Filtrer un dictionnaire pour ne garder que certaines paires
notes = {'Ousmane': 14, 'Issa': 9, 'Marie': 17, 'Diana': 11}
admis = {nom: note for nom, note in notes.items() if note >= 12}
print(admis)  # Affiche : {'Ousmane': 14, 'Marie': 17}
```

La compréhension de dictionnaire est une syntaxe élégante qui remplace avantageusement une boucle `for` classique pour construire ou transformer des dictionnaires.


## 9. Fusionner des dictionnaires

### Avec update()

On a vu que `update()` permet d'ajouter ou de mettre à jour des clés. C'est aussi la méthode classique pour fusionner deux dictionnaires. En cas de clé commune, la valeur du second dictionnaire écrase celle du premier.

```python
dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 99, 'c': 3}

dict1.update(dict2)
print(dict1)  # Affiche : {'a': 1, 'b': 99, 'c': 3}
```

### Avec l'opérateur | (Python 3.9+)

Depuis Python 3.9, on peut utiliser l'opérateur `|` pour fusionner deux dictionnaires en créant un nouveau dictionnaire, sans modifier les originaux. L'opérateur `|=` permet de faire la fusion en place.

```python
dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 99, 'c': 3}

fusion = dict1 | dict2
print(fusion)  # Affiche : {'a': 1, 'b': 99, 'c': 3}
print(dict1)   # Affiche : {'a': 1, 'b': 2}  (inchangé)

dict1 |= dict2
print(dict1)   # Affiche : {'a': 1, 'b': 99, 'c': 3}  (modifié en place)
```


## 10. Cas d'utilisation courants

Les dictionnaires sont particulièrement adaptés à plusieurs situations fréquentes en programmation.

### Compter les occurrences

```python
texte = "python est un langage python facile et python puissant"
mots = texte.split()

compteur = {}
for mot in mots:
    compteur[mot] = compteur.get(mot, 0) + 1

print(compteur)
# Affiche : {'python': 3, 'est': 1, 'un': 1, 'langage': 1, 'facile': 1, 'et': 1, 'puissant': 1}
```

### Regrouper des données

```python
etudiants = [
    ('Ousmane', 'Informatique'),
    ('Issa', 'Mathématiques'),
    ('Marie', 'Informatique'),
    ('Diana', 'Mathématiques'),
    ('Eve', 'Informatique')
]

par_filiere = {}
for nom, filiere in etudiants:
    if filiere not in par_filiere:
        par_filiere[filiere] = []
    par_filiere[filiere].append(nom)

print(par_filiere)
# Affiche : {'Informatique': ['Ousmane', 'Marie', 'Eve'], 'Mathématiques': ['Issa', 'Diana']}
```

### Remplacer une longue suite de if/elif

```python
# Au lieu d'une longue chaîne de conditions
jour_numero = 3

jours = {
    1: 'Lundi',
    2: 'Mardi',
    3: 'Mercredi',
    4: 'Jeudi',
    5: 'Vendredi',
    6: 'Samedi',
    7: 'Dimanche'
}

print(jours.get(jour_numero, 'Jour inconnu'))  # Affiche : Mercredi
```


## Résumé

Les dictionnaires sont indispensables en Python pour stocker et manipuler des données structurées. Voici les points essentiels à retenir :

- Un dictionnaire stocke des paires clé-valeur, défini avec des accolades `{}`.
- On accède aux valeurs par leur clé, avec `dict[clé]` ou plus prudemment avec `dict.get(clé)`.
- On peut ajouter, modifier et supprimer des paires avec une syntaxe simple et des méthodes dédiées (`update`, `pop`, `del`, `clear`).
- Les méthodes `keys()`, `values()` et `items()` permettent de parcourir les différentes composantes du dictionnaire.
- Les dictionnaires peuvent être imbriqués pour représenter des structures hiérarchiques.
- La compréhension de dictionnaire offre une syntaxe concise pour construire ou transformer des dictionnaires.
- Les dictionnaires sont particulièrement utiles pour compter, regrouper des données, ou remplacer des structures conditionnelles complexes.

Avec les listes, les dictionnaires forment le duo de structures de données le plus utilisé en Python. Savoir choisir entre les deux, et savoir les combiner, est une compétence clé pour tout développeur Python.
