# La Boucle `for`

## Introduction

La boucle `for` est l'une des structures de contrôle fondamentales du langage Python. Elle permet d'itérer de manière 
séquentielle sur les éléments d'une séquence ou de tout objet dit « itérable », c'est-à-dire un objet capable de 
retourner ses éléments un par un. Les types itérables les plus courants en Python sont les listes, les tuples, 
les chaînes de caractères, les dictionnaires, les ensembles (`set`) ainsi que les objets générés par des 
fonctions telles que `range()`.

Contrairement à la boucle `while`, qui s'exécute tant qu'une condition booléenne est vraie, 
la boucle `for` parcourt un nombre déterminé d'éléments, ce qui la rend particulièrement adaptée lorsque l'on connaît 
à l'avance la collection à traiter.

Sa syntaxe générale est la suivante :

```python
for variable in itérable:
    # Code à exécuter pour chaque élément de l'itérable
```

À chaque itération, la variable prend la valeur de l'élément courant de l'itérable, et le bloc de code indenté 
est exécuté. Une fois tous les éléments parcourus, la boucle se termine naturellement.

## Itération sur une liste

L'usage le plus courant de la boucle `for` consiste à parcourir les éléments d'une liste. À chaque tour de boucle, 
la variable de contrôle prend successivement la valeur de chaque élément, du premier au dernier.

```python
fruits = ["pomme", "banane", "orange"]
for fruit in fruits:
    print(fruit)
# Affiche :
# pomme
# banane
# orange
```

Cet exemple illustre la lisibilité caractéristique de Python : le code se lit presque comme une phrase en langage 
naturel — « pour chaque fruit dans fruits, afficher le fruit ».

## Itération sur une chaîne de caractères

En Python, une chaîne de caractères est elle-même un objet itérable. Il est donc possible de la parcourir caractère 
par caractère à l'aide d'une boucle `for`, sans avoir besoin de recourir à un index.

```python
mot = "Bonjour"
for lettre in mot:
    print(lettre)
# Affiche :
# B
# o
# n
# j
# o
# u
# r
```

Cette technique est particulièrement utile pour effectuer des traitements sur chaque caractère d'une chaîne, 
comme compter les occurrences d'une lettre ou construire une nouvelle chaîne transformée.

## Itération sur une plage de nombres avec `range()`

Lorsqu'il est nécessaire de répéter une action un nombre précis de fois, ou d'itérer sur une suite de nombres entiers, 
la fonction intégrée `range()` est la solution appropriée. Elle génère une séquence d'entiers à la demande, 
sans les stocker tous en mémoire, ce qui la rend efficace même pour de grandes plages.

La fonction `range()` accepte jusqu'à trois arguments : `range(début, fin, pas)`. Par défaut, 
le début est `0` et le pas est `1`.

```python
# Itération simple de 0 à 4
for i in range(5):
    print(i)
# Affiche : 0, 1, 2, 3, 4

# Itération de 2 à 10 avec un pas de 2
for i in range(2, 11, 2):
    print(i)
# Affiche : 2, 4, 6, 8, 10
```

Il est important de noter que la valeur de fin spécifiée dans `range()` est exclue de la séquence générée.

## Utilisation de `enumerate()`

Dans certaines situations, il est nécessaire de connaître non seulement la valeur de chaque élément, 
mais aussi sa position (son index) dans la séquence. La fonction intégrée `enumerate()` répond précisément à ce besoin :
elle retourne, à chaque itération, un tuple composé de l'index courant et de la valeur correspondante.

```python
fruits = ["pomme", "banane", "orange"]
for i, fruit in enumerate(fruits):
    print(i, fruit)
# Affiche :
# 0 pomme
# 1 banane
# 2 orange
```

Il est également possible de spécifier la valeur de départ de l'index en passant un second argument à `enumerate()` :

```python
for i, fruit in enumerate(fruits, start=1):
    print(i, fruit)
# Affiche :
# 1 pomme
# 2 banane
# 3 orange
```

Cette approche est préférable à l'utilisation manuelle d'un compteur, car elle rend le code plus lisible et 
moins sujet aux erreurs.

## Itération sur un dictionnaire

Les dictionnaires sont des structures de données associant des clés à des valeurs. 
La boucle `for` permet de les parcourir de plusieurs façons selon le besoin.

Par défaut, itérer sur un dictionnaire revient à itérer sur ses clés :

```python
personne = {"nom": "Diallo", "age": 30, "ville": "Paris"}
for cle in personne:
    print(cle, personne[cle])
# Affiche :
# nom Diallo
# age 30
# ville Paris
```

Pour accéder simultanément aux clés et aux valeurs, il est conseillé d'utiliser la méthode `items()`, 
qui retourne des paires `(clé, valeur)` :

```python
for cle, valeur in personne.items():
    print(f"{cle} : {valeur}")
# Affiche :
# nom : Diallo
# age : 30
# ville : Paris
```

Il est également possible de n'itérer que sur les valeurs grâce à la méthode `values()`, ou 
uniquement sur les clés avec `keys()`.

## Instructions `break` et `continue`

Python fournit deux instructions permettant de modifier le comportement d'une boucle `for` en cours d'exécution :
`break` et `continue`.

### L'instruction `break`

L'instruction `break` permet d'interrompre immédiatement l'exécution de la boucle, quelle que soit l'étape 
d'itération en cours. Elle est généralement utilisée lorsqu'une condition particulière est remplie et qu'il n'est 
plus utile de poursuivre le parcours.

```python
for i in range(10):
    if i == 5:
        break
    print(i)
# Affiche : 0, 1, 2, 3, 4
# La boucle s'arrête dès que i vaut 5
```

### L'instruction `continue`

L'instruction `continue` permet, quant à elle, de passer directement à l'itération suivante sans exécuter le reste du 
bloc de code de l'itération courante. Elle est utile pour ignorer certains éléments selon une condition, sans 
interrompre la boucle entièrement.

```python
for i in range(10):
    if i % 2 == 0:
        continue
    print(i)
# Affiche : 1, 3, 5, 7, 9
# Les nombres pairs sont ignorés
```

## Résumé

La boucle `for` est un outil puissant et polyvalent en Python. Combinée aux fonctions intégrées 
comme `range()`, `enumerate()` ou aux méthodes propres aux dictionnaires, elle couvre la grande majorité des besoins 
d'itération rencontrés en programmation quotidienne. Maîtriser ses différentes formes et savoir choisir la plus adaptée 
à chaque situation est essentiel pour écrire un code clair, efficace et pythonique.
