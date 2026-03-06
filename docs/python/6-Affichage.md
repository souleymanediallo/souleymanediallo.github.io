# L'Affichage

En Python, la fonction `print()` permet d'afficher du texte ou des valeurs dans la console. C'est l'un des premiers outils que l'on utilise pour interagir avec un programme.

## La fonction `print()`

`print()` accepte un ou plusieurs arguments séparés par des virgules. Elle les convertit automatiquement en texte et les affiche côte à côte, séparés par un espace.

```python
>>> print("Bonjour !")          # affiche : Bonjour !
>>> print(42)                   # affiche : 42
>>> print(3.14)                 # affiche : 3.14
>>> print("La réponse est", 42) # affiche : La réponse est 42
```

On peut également afficher le résultat d'un calcul :

```python
>>> x = 10
>>> y = 3
>>> z = x / y
>>> print("Le résultat de", x, "/", y, "est", z)
Le résultat de 10 / 3 est 3.3333333333333335
```

## La méthode `format()`

La méthode `format()` permet d'insérer des valeurs dans une chaîne de caractères à l'aide de marqueurs `{}`. Chaque marqueur est remplacé, dans l'ordre, par les arguments passés à `format()`.

```python
>>> x = 10
>>> y = 3
>>> z = x / y
>>> print("Le résultat de {} / {} est {}".format(x, y, z))
Le résultat de 10 / 3 est 3.3333333333333335
```

Cette approche est lisible mais devient vite encombrante quand le nombre de variables augmente.

## Les f-strings

Introduites en Python 3.6, les f-strings (chaînes formatées) sont la façon la plus moderne et la plus concise de construire un affichage. Il suffit de préfixer la chaîne avec `f` et d'écrire les variables directement entre accolades `{}`.

```python
>>> x = 10
>>> y = 3.14
>>> z = "hello"
>>> a = True
>>> b = [1, 2, 3]

>>> print(f"{x} {y} {z}")      # affiche : 10 3.14 hello
>>> print(f"{x=} {y=} {z=}")   # affiche : x=10 y=3.14 z='hello'
>>> print(f"{a=} {b=}")        # affiche : a=True b=[1, 2, 3]
```

La syntaxe `{variable=}` est particulièrement utile pour le débogage : elle affiche à la fois le nom de la variable et sa valeur.

## Comparaison des trois approches

Pour afficher `"x vaut 10 et y vaut 3.14"` :

```python
x = 10
y = 3.14

# Avec print() simple
print("x vaut", x, "et y vaut", y)

# Avec format()
print("x vaut {} et y vaut {}".format(x, y))

# Avec f-string
print(f"x vaut {x} et y vaut {y}")
```

Les trois affichent le même résultat. En pratique, les f-strings sont aujourd'hui la méthode recommandée : elles sont plus lisibles et moins sujettes aux erreurs.

## Pour aller plus loin

Les f-strings permettent aussi d'appliquer des formats directement sur les valeurs, comme limiter le nombre de décimales affichées :

```python
>>> z = 10 / 3
>>> print(f"Résultat : {z:.2f}")   # affiche : Résultat : 3.33
>>> print(f"Résultat : {z:.4f}")   # affiche : Résultat : 3.3333
```

La syntaxe `{variable:.2f}` signifie : afficher la variable comme un nombre décimal avec 2 chiffres après la virgule.

- [Documentation officielle — print()](https://docs.python.org/fr/3/library/functions.html#print)
- [Documentation officielle — f-strings](https://docs.python.org/fr/3/reference/lexical_analysis.html#f-strings)
