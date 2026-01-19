# Les Opérateurs
En Python, il existe différents types d'opérateurs qui permettent d'effectuer des opérations arithmétiques, de comparaison, d'affectation, logiques, d'appartenance, d'identité etc.

## Opérateurs arithmétiques :
* Addition : `+`
* Soustraction : `-`
* Multiplication : `*`
* Division avec un nombre décimal : `/`
* Modulo : `%`
* Exponentiation : `**`
* division avec un nombre positif : `//`

```
x = 5
y = 3
print(x + y)  # 8
print(x - y)  # 2
print(x * y)  # 15
print(x / y)  # 1.6666666666666667
print(x % y)  # 2
print(x ** y) # 125
print(x // y) # 1
```

## Opérateurs de comparaison :
* Egal : ==
* Différent : !=
* Inférieur : <
* Inférieur ou égal : <=
* Supérieur : >
* Supérieur ou égal : >=

```
x = 5
y = 3
print(x == y)  # False
print(x != y)  # True
print(x < y)   # False
print(x <= y)  # False
print(x > y)   # True
print(x >= y)  # True
```

## Opérateurs logiques :
* And : and
* Or : or
* Not : not

```
x = True
y = False
print(x and y) # False
print(x or y)  # True
print(not x)   # False
```

## Opérateurs d'affectation :
* Affectation : =
* Addition et affectation : +=
* Soustraction et affectation : -=
* Multiplication et affectation : *=
* Division et affectation : /=
* Modulo et affectation : %=
* Exponentiation et affectation : **=
* division positive et affectation : //=
```
x = 5
x += 3 # x = x + 3
print(x) # 8
x *= 2 # x = x * 2
print(x) # 16
```

## Operateurs spécifique en python
il existe des opérateurs spécifiques en Python qui permettent de réaliser des opérations spécifiques. Voici quelques exemples :

### Opérateur d'appartenance : `in` et `not in`
* `in` permet de vérifier si un élément appartient à une séquence (liste, chaîne de caractères, tuple, etc.). Il retourne True si l'élément est présent dans la séquence et False sinon.
* `not in` permet de vérifier si un élément n'appartient pas à une séquence. Il retourne True si l'élément n'est pas présent dans la séquence et False s'il y est.
```
x = [1, 2, 3, 4, 5]
print(3 in x)  # True
print(6 in x)  # False
print(3 not in x)  # False
print(6 not in x)  # True
```

### Opérateurs d'identité : `is` et `is not`
* `is` permet de vérifier si deux références de variables pointent vers le même objet. Il retourne `True` si les deux références pointent vers le même objet et `False` sinon.
* `is not` permet de vérifier si deux références de variables ne pointent pas vers le même objet. Il retourne `True` si les deux références ne pointent pas vers le même objet et `False` sinon.
```
x = [1, 2, 3]
y = x
z = [1, 2, 3]
print(x is y)  # True
print(x is z)  # False
print(x is not y) # False
print(x is not z) # True
```
Il est important de noter que l'opérateur == comparant les valeurs des objets alors que is comparant les objets eux-même.

### Opérateur ternaire : `x if c else y`

* Il permet de choisir entre x et y en fonction de la valeur booléene c.
```
age = 25
is_adult = True if age >= 18 else False
print(is_adult) # True
```

### Opérateur de déballage d'emballage `*`

* Il permet de déballer les éléments d'une liste ou d'un tuple et de les passer en paramètre d'une fonction.
```
def add(x, y, z):
    return x + y + z
x = [1, 2, 3]
print(add(*x))  # 6
```

Ces opérateurs et fonctionnalités sont très utiles pour écrire des codes plus concis et plus lisible, ils permettent de simplifier les structures de contrôle de flux, les comparaisons et les affectations. Il est important de comprendre comment ils fonctionnent pour pouvoir les utiliser efficacement dans vos programmes.

Il est également important de mentionner qu'il existe d'autres opérateurs spécifique en python tels que les operateurs de bit (shift, AND, OR, NOT, XOR), operateur `lambda` pour créer des fonction anonymes, operateur `with` pour la gestion des contextes, `yield` pour la création des générateurs, et bien d'autres.