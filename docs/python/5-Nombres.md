# Les Nombres

Python propose deux grands types de nombres pour représenter des valeurs numériques : les nombres entiers et les nombres décimaux. Comprendre la différence entre ces deux types est essentiel, car Python ne les traite pas exactement de la même manière.

## Les nombres entiers

Un nombre entier est un nombre sans virgule, qu'il soit positif, négatif ou égal à zéro. En Python, ce type de donnée s'appelle `int` (abréviation de *integer*, qui signifie « entier » en anglais).

Voici quelques exemples de déclarations de variables entières :

```python
>>> x = 10  # x est une variable entière avec la valeur 10
>>> y = -5  # y est une variable entière avec la valeur -5
>>> z = 0   # z est une variable entière avec la valeur 0
```

Pour vérifier le type d'une variable, on peut utiliser la fonction `type()` :

```python
>>> type(x)
<class 'int'>
```

## Les nombres décimaux

Un nombre décimal est un nombre qui comporte une virgule (représentée par un point en Python). En Python, ce type s'appelle `float` (abréviation de *floating point number*, qui signifie « nombre à virgule flottante »).

Voici quelques exemples de déclarations de variables décimales :

```python
>>> x = 3.14  # x est une variable flottante avec la valeur 3.14
>>> y = -2.5  # y est une variable flottante avec la valeur -2.5
>>> z = 0.0   # z est une variable flottante avec la valeur 0.0
```

A noter : même si la valeur est `0.0`, Python considère cette variable comme un `float` et non comme un `int`. La simple présence du point fait toute la différence.

## Opérations mathématiques

Python permet d'effectuer les opérations mathématiques courantes directement sur les nombres. Voici les quatre opérations de base :

| Opération      | Symbole | Exemple     | Résultat |
|----------------|---------|-------------|----------|
| Addition       | `+`     | `10 + 3.14` | `13.14`  |
| Soustraction   | `-`     | `10 - 3.14` | `6.86`   |
| Multiplication | `*`     | `10 * 3.14` | `31.4`   |
| Division       | `/`     | `10 / 3.14` | `3.1847…`|

Voici ces opérations en pratique :

```python
>>> x = 10
>>> y = 3.14
>>> z = x + y  # addition : z vaut 13.14
>>> a = x - y  # soustraction : a vaut 6.86
>>> b = x * y  # multiplication : b vaut 31.4
>>> c = x / y  # division : c vaut 3.1847133757961783
```

Un point important à retenir : lorsqu'une opération mélange un `int` et un `float`, le résultat est toujours un `float`. Python convertit automatiquement le nombre entier en décimal avant de faire le calcul.

## Convertir une variable

Il arrive fréquemment de devoir passer d'un type numérique à un autre. Python met à disposition deux fonctions de conversion :

- `int()` transforme un nombre décimal en entier en supprimant la partie après la virgule (sans arrondir).
- `float()` transforme un nombre entier en décimal en ajoutant `.0` à la fin.

```python
>>> x = 10
>>> y = 3.14
>>> z = int(y)    # z vaut 3 (la partie décimale est simplement supprimée)
>>> a = float(x)  # a vaut 10.0
```

Attention : la conversion avec `int()` ne fait pas un arrondi. Elle tronque simplement la partie décimale. Par exemple, `int(3.99)` donne `3` et non `4`.

Pour aller plus loin, la documentation officielle de Python détaille le fonctionnement des types numériques :

- [Types numériques — int, float, complex :octicons-link-external-16:](https://docs.python.org/fr/3/library/stdtypes.html#numeric-types-int-float-complex){:target="_blank"}
