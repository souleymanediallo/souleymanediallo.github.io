# Les conditions

## Introduction

En Python, les structures conditionnelles permettent d'exécuter un bloc de code uniquement lorsqu'une condition 
spécifique est satisfaite. Elles constituent l'un des mécanismes fondamentaux de tout programme, car elles permettent 
de contrôler le flux d'exécution en fonction de l'état des données.

## La structure de base : l'instruction `if`

L'instruction `if` est la forme la plus simple d'une condition. Sa syntaxe est la suivante :

```python
if condition:
    # Bloc de code exécuté si la condition est vraie
```

La `condition` est une expression qui s'évalue à `True` (vrai) ou `False` (faux). Si elle est vraie, 
le bloc de code indenté en dessous est exécuté. Dans le cas contraire, il est ignoré et l'exécution du programme se 
poursuit normalement.

Exemple :

```python
x = 10

if x > 5:
    print("x est supérieur à 5")  # Affiche : x est supérieur à 5
```

Ici, comme `x` vaut 10 et que 10 est bien supérieur à 5, la condition est vraie et le message s'affiche.

## Ajouter une alternative : la clause `else`

La clause `else` permet de définir un bloc de code à exécuter lorsque la condition du `if` est fausse. 
Elle couvre donc le cas complémentaire.

```python
if condition:
    # Bloc exécuté si la condition est vraie
else:
    # Bloc exécuté si la condition est fausse
```

Exemple :

```python
x = 3

if x > 5:
    print("x est supérieur à 5")
else:
    print("x n'est pas supérieur à 5")  # Affiche : x n'est pas supérieur à 5
```

Comme `x` vaut 3 et que 3 n'est pas supérieur à 5, c'est le bloc `else` qui est exécuté.

## Tester plusieurs conditions : la clause `elif`

Lorsque plusieurs cas distincts doivent être traités, la clause `elif` (contraction de *else if*) permet d'enchaîner 
des conditions supplémentaires entre le `if` initial et le `else` final.

```python
if condition_1:
    # Bloc exécuté si condition_1 est vraie
elif condition_2:
    # Bloc exécuté si condition_1 est fausse et condition_2 est vraie
else:
    # Bloc exécuté si aucune condition précédente n'est vraie
```

Exemple :

```python
x = 3

if x > 5:
    print("x est supérieur à 5")
elif x < 5:
    print("x est inférieur à 5")  # Affiche : x est inférieur à 5
else:
    print("x est égal à 5")
```

Les conditions sont évaluées dans l'ordre. Dès qu'une condition est vraie, le bloc correspondant est exécuté et 
les suivantes sont ignorées.

## Les opérateurs logiques

Il est possible de combiner plusieurs conditions au sein d'une même instruction grâce aux opérateurs logiques :

- `and` : la condition globale est vraie uniquement si toutes les sous-conditions sont vraies.
- `or` : la condition globale est vraie dès qu'au moins une sous-condition est vraie.
- `not` : inverse la valeur booléenne d'une condition.

Exemple :

```python
x = 7

if x > 5 and x < 10:
    print("x est compris entre 5 et 10")  # Affiche : x est compris entre 5 et 10
```

## Remarque sur les valeurs booléennes

Toute expression utilisée dans une condition doit pouvoir être évaluée comme un booléen, c'est-à-dire `True` ou `False`. 
En Python, certaines valeurs sont considérées comme fausses par convention, notamment `0`, `None`, une chaîne vide `""` 
ou une liste vide `[]`. Toutes les autres valeurs sont considérées comme vraies.

## En résumé
Les structures conditionnelles en Python permettent de contrôler le flux d'exécution du programme en fonction de 
conditions spécifiques. Voici un résumé des principales structures conditionnelles et de leurs rôles :

| Structure | Rôle |
|---|---|
| `if` | Exécute un bloc si la condition est vraie |
| `else` | Exécute un bloc si aucune condition précédente n'est vraie |
| `elif` | Teste une condition supplémentaire entre `if` et `else` |
| `and` | Combine deux conditions (toutes deux doivent être vraies) |
| `or` | Combine deux conditions (au moins une doit être vraie) |
| `not` | Inverse une condition |

