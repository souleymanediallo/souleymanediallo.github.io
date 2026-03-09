# Les listes

## Introduction

En Python, une liste est l'une des structures de données les plus utilisées. Elle permet de regrouper plusieurs valeurs dans une seule variable, dans un ordre précis. Contrairement à certains autres langages de programmation, Python offre une grande flexibilité avec les listes : elles peuvent changer de taille, contenir des types de données variés, et sont manipulables grâce à de nombreuses méthodes intégrées.

Comprendre les listes est une étape fondamentale pour tout programmeur Python, car elles interviennent dans presque tous les types de programmes : traitement de données, gestion d'entrées utilisateur, algorithmes de tri, et bien plus encore.


## 1. Créer une liste

Une liste se définit avec des crochets `[]`, et ses éléments sont séparés par des virgules. On peut créer une liste vide, une liste de nombres, une liste de chaînes de caractères, ou même une liste qui mélange différents types.

```python
# Une liste vide
ma_liste = []

# Une liste de nombres entiers
notes = [12, 15, 9, 18, 11]

# Une liste de chaînes de caractères
fruits = ['pomme', 'banane', 'orange', 'mangue']

# Une liste mixte
divers = [42, 'bonjour', 3.14, True]
```

Il est important de noter que l'ordre des éléments dans une liste est préservé. Cela signifie que `['pomme', 'banane']` et `['banane', 'pomme']` sont deux listes différentes en Python.


## 2. Accéder aux éléments d'une liste

### L'indexation positive

Python numérote les éléments d'une liste à partir de zéro. On appelle ce principe l'indexation base zéro. Ainsi, le premier élément se trouve à l'index 0, le deuxième à l'index 1, et ainsi de suite.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue']

print(fruits[0])  # Affiche : pomme
print(fruits[1])  # Affiche : banane
print(fruits[3])  # Affiche : mangue
```

Si l'on tente d'accéder à un index qui n'existe pas, Python lèvera une erreur de type `IndexError`. Par exemple, avec une liste de 4 éléments, l'index 4 est invalide car le dernier index valide est 3.

```python
print(fruits[4])  # Erreur : IndexError: list index out of range
```

### L'indexation négative

Python permet également d'accéder aux éléments depuis la fin de la liste grâce aux index négatifs. L'index -1 désigne le dernier élément, -2 l'avant-dernier, et ainsi de suite. C'est particulièrement utile lorsqu'on ne connaît pas la taille exacte d'une liste.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue']

print(fruits[-1])  # Affiche : mangue
print(fruits[-2])  # Affiche : orange
print(fruits[-4])  # Affiche : pomme
```


## 3. Le slicing : accéder à une portion de liste

Le slicing (ou découpage) permet d'extraire une sous-liste à partir d'une liste existante. La syntaxe est la suivante : `liste[debut:fin]`. Python retourne alors les éléments depuis l'index `debut` jusqu'à l'index `fin` exclu.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue', 'kiwi']

print(fruits[1:3])   # Affiche : ['banane', 'orange']
print(fruits[0:2])   # Affiche : ['pomme', 'banane']
print(fruits[2:])    # Affiche : ['orange', 'mangue', 'kiwi']  (du 3ème jusqu'à la fin)
print(fruits[:3])    # Affiche : ['pomme', 'banane', 'orange'] (du début jusqu'au 3ème)
print(fruits[:])     # Affiche toute la liste (copie)
```

Il est également possible de définir un pas dans le slicing avec la syntaxe `liste[debut:fin:pas]`. Un pas de 2 permet par exemple de sélectionner un élément sur deux.

```python
nombres = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(nombres[::2])   # Affiche : [0, 2, 4, 6, 8]  (un élément sur deux)
print(nombres[1::2])  # Affiche : [1, 3, 5, 7, 9]
print(nombres[::-1])  # Affiche : [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]  (liste inversée)
```


## 4. Modifier une liste

### Modifier un élément existant

On peut remplacer la valeur d'un élément en accédant à son index et en lui affectant une nouvelle valeur.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue']

fruits[1] = 'fraise'
print(fruits)  # Affiche : ['pomme', 'fraise', 'orange', 'mangue']
```

### Modifier plusieurs éléments avec le slicing

Il est également possible de modifier plusieurs éléments d'un coup en combinant le slicing et l'affectation.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue']

fruits[1:3] = ['kiwi', 'citron']
print(fruits)  # Affiche : ['pomme', 'kiwi', 'citron', 'mangue']
```


## 5. Ajouter des éléments à une liste

### La méthode append()

La méthode `append()` ajoute un seul élément à la fin de la liste. C'est la façon la plus courante d'enrichir une liste au fil de l'exécution d'un programme.

```python
fruits = ['pomme', 'banane']

fruits.append('orange')
print(fruits)  # Affiche : ['pomme', 'banane', 'orange']
```

### La méthode insert()

La méthode `insert()` permet d'insérer un élément à une position précise. Elle prend deux arguments : l'index auquel insérer l'élément, et l'élément lui-même.

```python
fruits = ['pomme', 'banane', 'orange']

fruits.insert(1, 'kiwi')
print(fruits)  # Affiche : ['pomme', 'kiwi', 'banane', 'orange']
```

### La méthode extend()

La méthode `extend()` permet d'ajouter plusieurs éléments d'un coup en fusionnant une autre liste (ou tout autre itérable) avec la liste existante.

```python
fruits = ['pomme', 'banane']
nouveaux_fruits = ['mangue', 'fraise', 'cerise']

fruits.extend(nouveaux_fruits)
print(fruits)  # Affiche : ['pomme', 'banane', 'mangue', 'fraise', 'cerise']
```

On peut également utiliser l'opérateur `+` pour concaténer deux listes et obtenir une nouvelle liste.

```python
liste1 = [1, 2, 3]
liste2 = [4, 5, 6]

liste3 = liste1 + liste2
print(liste3)  # Affiche : [1, 2, 3, 4, 5, 6]
```


## 6. Supprimer des éléments d'une liste

### La méthode remove()

La méthode `remove()` supprime la première occurrence d'un élément dont on spécifie la valeur. Si l'élément n'existe pas, Python lève une erreur `ValueError`.

```python
fruits = ['pomme', 'banane', 'orange', 'banane']

fruits.remove('banane')
print(fruits)  # Affiche : ['pomme', 'orange', 'banane']  (seule la première occurrence est supprimée)
```

### La méthode pop()

La méthode `pop()` supprime et retourne l'élément situé à un index donné. Sans argument, elle supprime le dernier élément de la liste.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue']

element = fruits.pop()
print(element)  # Affiche : mangue
print(fruits)   # Affiche : ['pomme', 'banane', 'orange']

element = fruits.pop(1)
print(element)  # Affiche : banane
print(fruits)   # Affiche : ['pomme', 'orange']
```

### L'instruction del

L'instruction `del` permet de supprimer un élément par son index, ou même de supprimer une portion de liste grâce au slicing.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue', 'kiwi']

del fruits[2]
print(fruits)  # Affiche : ['pomme', 'banane', 'mangue', 'kiwi']

del fruits[1:3]
print(fruits)  # Affiche : ['pomme', 'kiwi']
```

### La méthode clear()

La méthode `clear()` vide entièrement une liste, sans la supprimer. La variable existe toujours mais ne contient plus aucun élément.

```python
fruits = ['pomme', 'banane', 'orange']

fruits.clear()
print(fruits)  # Affiche : []
```


## 7. Parcourir une liste

### Avec une boucle for

La façon la plus simple de parcourir tous les éléments d'une liste est d'utiliser une boucle `for`. À chaque itération, la variable de boucle prend la valeur de l'élément courant.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue']

for fruit in fruits:
    print(fruit)
# Affiche :
# pomme
# banane
# orange
# mangue
```

### Avec enumerate() pour avoir l'index

Lorsqu'on a besoin à la fois de l'index et de la valeur, la fonction `enumerate()` est très utile. Elle retourne des paires (index, valeur) à chaque itération.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue']

for index, fruit in enumerate(fruits):
    print(f"Index {index} : {fruit}")
# Affiche :
# Index 0 : pomme
# Index 1 : banane
# Index 2 : orange
# Index 3 : mangue
```

### Avec une boucle while

Il est également possible de parcourir une liste avec une boucle `while`, en utilisant un compteur d'index. Cette approche est moins courante mais peut s'avérer utile dans certains cas.

```python
fruits = ['pomme', 'banane', 'orange']
i = 0

while i < len(fruits):
    print(fruits[i])
    i += 1
```


## 8. Les méthodes utiles sur les listes

Python fournit un ensemble de méthodes intégrées pour manipuler les listes de façon efficace.

### Connaître la taille d'une liste : len()

La fonction `len()` retourne le nombre d'éléments dans une liste.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue']
print(len(fruits))  # Affiche : 4
```

### Trier une liste : sort() et sorted()

La méthode `sort()` trie la liste en place, c'est-à-dire qu'elle modifie directement la liste originale. La fonction `sorted()`, quant à elle, retourne une nouvelle liste triée sans modifier l'originale.

```python
nombres = [5, 2, 8, 1, 9, 3]

nombres.sort()
print(nombres)  # Affiche : [1, 2, 3, 5, 8, 9]

# Tri en ordre décroissant
nombres.sort(reverse=True)
print(nombres)  # Affiche : [9, 8, 5, 3, 2, 1]

# sorted() ne modifie pas la liste originale
original = [5, 2, 8, 1]
trie = sorted(original)
print(original)  # Affiche : [5, 2, 8, 1]  (inchangée)
print(trie)      # Affiche : [1, 2, 5, 8]
```

### Inverser une liste : reverse()

La méthode `reverse()` inverse l'ordre des éléments de la liste en place.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue']
fruits.reverse()
print(fruits)  # Affiche : ['mangue', 'orange', 'banane', 'pomme']
```

### Compter les occurrences : count()

La méthode `count()` retourne le nombre de fois qu'une valeur apparaît dans la liste.

```python
notes = [12, 15, 12, 9, 15, 12, 18]
print(notes.count(12))  # Affiche : 3
print(notes.count(15))  # Affiche : 2
```

### Trouver l'index d'un élément : index()

La méthode `index()` retourne l'index de la première occurrence d'une valeur donnée. Si la valeur n'est pas présente, une erreur `ValueError` est levée.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue']
print(fruits.index('orange'))  # Affiche : 2
```

### Vérifier la présence d'un élément : in

L'opérateur `in` permet de vérifier si un élément est présent dans une liste. Il retourne `True` ou `False`.

```python
fruits = ['pomme', 'banane', 'orange', 'mangue']

print('banane' in fruits)   # Affiche : True
print('cerise' in fruits)   # Affiche : False
```


## 9. Les listes imbriquées

Une liste peut elle-même contenir d'autres listes. On parle alors de listes imbriquées ou de listes de listes. C'est une façon courante de représenter des tableaux ou des matrices en Python.

```python
matrice = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Accéder à l'élément de la 2ème ligne, 3ème colonne
print(matrice[1][2])  # Affiche : 6

# Parcourir une matrice
for ligne in matrice:
    for element in ligne:
        print(element, end=' ')
    print()
# Affiche :
# 1 2 3
# 4 5 6
# 7 8 9
```


## 10. La compréhension de liste

La compréhension de liste est une syntaxe concise et très pythonique pour créer une nouvelle liste à partir d'une liste existante (ou de tout itérable). Elle combine en une seule ligne ce qu'on ferait normalement avec une boucle `for` et éventuellement une condition `if`.

La syntaxe générale est : `[expression for element in iterable if condition]`

```python
# Créer une liste des carrés de 0 à 9
carres = [x**2 for x in range(10)]
print(carres)  # Affiche : [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# Filtrer les nombres pairs
nombres = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
pairs = [n for n in nombres if n % 2 == 0]
print(pairs)  # Affiche : [2, 4, 6, 8, 10]

# Mettre en majuscule les fruits dont le nom contient la lettre 'a'
fruits = ['pomme', 'banane', 'orange', 'mangue', 'kiwi']
resultat = [fruit.upper() for fruit in fruits if 'a' in fruit]
print(resultat)  # Affiche : ['BANANE', 'ORANGE', 'MANGUE']
```

La compréhension de liste est généralement plus rapide et plus lisible qu'une boucle `for` classique pour construire des listes, et elle est très appréciée dans la communauté Python.


## Résumé

Les listes sont au cœur de la programmation Python. Voici les points essentiels à retenir :

- Une liste est une collection ordonnée et modifiable, définie avec des crochets `[]`.
- Les éléments sont accessibles par leur index (positif ou négatif).
- Le slicing permet d'extraire des sous-listes.
- Python propose de nombreuses méthodes pour ajouter (`append`, `insert`, `extend`), supprimer (`remove`, `pop`, `del`, `clear`) et manipuler (`sort`, `reverse`, `count`, `index`) les éléments.
- Les listes peuvent être imbriquées pour représenter des structures à plusieurs dimensions.
- La compréhension de liste offre une syntaxe élégante pour construire des listes à partir d'autres collections.

Maîtriser les listes est indispensable pour écrire des programmes Python efficaces et lisibles.
