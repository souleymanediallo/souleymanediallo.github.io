# Les Booléens

## Introduction

En Python, le type booléen (`bool`) est l'un des types de données fondamentaux du langage. 
Il permet de représenter des valeurs logiques, c'est-à-dire des valeurs qui ne peuvent prendre que deux états :
**vrai** ou **faux**. Ce concept, emprunté à la logique mathématique développée par George Boole au XIXe siècle, 
est au cœur de tout mécanisme de prise de décision dans un programme informatique.

En Python, ces deux états sont représentés par les constantes littérales `True` (vrai) et `False` (faux), 
avec une majuscule obligatoire. Toute autre orthographe sera interprétée par l'interpréteur comme une variable 
ordinaire, et non comme une valeur booléenne.

## Déclaration et affectation d'une variable booléenne

La manière la plus directe d'utiliser un booléen consiste à affecter l'une des deux constantes à une variable. 
Cela permet de stocker un état logique et de s'y référer ultérieurement dans le programme.

```python
# Déclaration de variables booléennes
is_raining = True
is_sunny = False
```

Dans cet exemple, la variable `is_raining` stocke l'état "il pleut" (vrai), tandis que `is_sunny` stocke l'état 
"il fait beau" (faux). Les noms de variables commençant par `is_`, `has_`, `can_` ou `should_` sont une convention 
courante pour désigner des variables booléennes, car ils expriment naturellement une question à laquelle on répond 
par oui ou par non.

## Utilisation dans les structures conditionnelles

Les booléens trouvent leur première utilisation naturelle dans les instructions conditionnelles (`if`, `elif`, `else`). 
Une condition est évaluée comme vraie ou fausse, ce qui détermine quel bloc de code sera exécuté.

```python
is_raining = True
is_sunny = False

if is_raining:
    print("Il pleut.")
else:
    print("Il ne pleut pas.")
```

Ici, puisque `is_raining` vaut `True`, c'est le premier bloc qui sera exécuté. L'interpréteur Python évalue 
l'expression dans le `if`, constate qu'elle est vraie, et exécute l'instruction correspondante.

## Les opérateurs de comparaison

Python permet de comparer deux valeurs grâce aux opérateurs de comparaison. Le résultat de toute comparaison est 
toujours un booléen : soit `True`, soit `False`.

Voici les opérateurs de comparaison disponibles :

- `==` : égalité
- `!=` : différence
- `<` : inférieur strict
- `>` : supérieur strict
- `<=` : inférieur ou égal
- `>=` : supérieur ou égal

```python
x = 5

print(x == 5)   # True  → x est bien égal à 5
print(x > 3)    # True  → x est bien supérieur à 3
print(x != 10)  # True  → x est différent de 10
print(x < 2)    # False → x n'est pas inférieur à 2
```

Ces expressions peuvent être directement utilisées comme conditions dans un `if`, sans avoir besoin de stocker le 
résultat dans une variable intermédiaire.

## Les opérateurs logiques booléens

Python dispose de trois opérateurs logiques permettant de combiner plusieurs expressions booléennes entre elles : 
`and`, `or` et `not`. Ces opérateurs permettent d'exprimer des conditions plus complexes.

`and` retourne `True` uniquement si **les deux** opérandes sont `True`.

`or` retourne `True` si **au moins un** des opérandes est `True`.

`not` inverse la valeur booléenne : `not True` donne `False`, et `not False` donne `True`.

```python
is_raining = True
is_sunny = False

# and : les deux conditions doivent être vraies
if is_raining and not is_sunny:
    print("Il pleut et le ciel est couvert.")

# or : au moins une condition doit être vraie
elif is_raining or is_sunny:
    print("Il pleut ou il fait beau, mais pas les deux.")
```

Dans le premier bloc, `not is_sunny` vaut `True` (car `is_sunny` est `False`), et `is_raining` vaut `True`, donc 
la condition `is_raining and not is_sunny` est `True` : le premier message s'affiche.

## Relation entre les booléens et les entiers

Un aspect important à connaître en Python est que le type `bool` est une **sous-classe du type `int`** (entier). 
Cela signifie que `True` et `False` ont des équivalents numériques : `True` correspond à la valeur entière `1`, 
et `False` correspond à `0`.

```python
print(True + True)   # 2
print(True + False)  # 1
print(False + False) # 0
```

Ce comportement est rarement utilisé directement dans le code, mais il est utile à connaître pour comprendre certains 
résultats ou pour compter rapidement des occurrences de conditions vraies dans une liste.

## Conversion en booléen avec la fonction `bool()`

Python permet de convertir n'importe quelle valeur en booléen grâce à la fonction intégrée `bool()`. Cette conversion 
suit des règles précises : une valeur est considérée comme `False` (on dit qu'elle est "falsy") si elle représente 
l'absence, le vide ou la nullité. Dans tous les autres cas, elle est considérée comme `True` 
(on dit qu'elle est "truthy").

Sont considérés comme `False` :

- L'entier `0`
- Le flottant `0.0`
- La chaîne de caractères vide `""`
- La liste vide `[]`, le tuple vide `()`, le dictionnaire vide `{}`
- La valeur spéciale `None`

```python
# Entier non nul → True
x = 5
print(bool(x))    # True

# Entier nul → False
x = 0
print(bool(x))    # False

# Chaîne vide → False
x = ""
print(bool(x))    # False

# Chaîne non vide → True
x = "Bonjour"
print(bool(x))    # True
```

Cette conversion implicite est notamment utilisée dans les structures conditionnelles, où Python évalue automatiquement 
toute expression comme un booléen. Il est donc courant d'écrire `if ma_liste:` plutôt que `if len(ma_liste) > 0:`, 
les deux étant strictement équivalents.

## En résumé

Les booléens sont un outil fondamental en Python. Ils permettent de prendre des décisions, de contrôler le flux 
d'exécution d'un programme, et de formuler des conditions complexes grâce aux opérateurs logiques. Comprendre leur 
fonctionnement, leur relation avec les entiers, et les règles de conversion implicite permet d'écrire un code 
plus clair, plus concis et plus idiomatique.
