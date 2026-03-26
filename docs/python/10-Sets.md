# Les Sets

## Qu'est-ce qu'un set ?

Un **set** (ou ensemble) est une structure de données Python qui stocke une collection d'éléments avec deux caractéristiques fondamentales :

- Les éléments sont **uniques** : il ne peut pas y avoir de doublons.
- Les éléments sont **non ordonnés** : il n'existe pas de notion de premier, deuxième ou troisième élément.

Ces deux propriétés font du set un outil très différent des listes ou des tuples, et particulièrement adapté à certains cas d'usage comme la suppression de doublons ou la comparaison de collections.


## Créer un set

On crée un set en plaçant des éléments séparés par des virgules entre accolades `{}`.

```python
fruits = {'apple', 'banana', 'orange', 'mango'}
print(fruits)
# Résultat possible : {'mango', 'apple', 'orange', 'banana'}
```

Remarquez que l'ordre d'affichage peut différer de l'ordre de saisie. C'est tout à fait normal : un set ne conserve pas l'ordre d'insertion.

On peut également créer un set à partir d'une liste existante avec la fonction `set()`. C'est utile pour éliminer automatiquement les doublons :

```python
nombres = [1, 2, 2, 3, 3, 3, 4]
ensemble = set(nombres)
print(ensemble)
# Résultat : {1, 2, 3, 4}
```

Pour créer un set vide, il faut obligatoirement utiliser `set()` et non `{}`, car `{}` crée un dictionnaire vide en Python.

```python
ensemble_vide = set()
```


## Accéder aux éléments

Comme un set n'est pas ordonné, il est impossible d'accéder à un élément via un index comme on le ferait avec une liste (`fruits[0]` ne fonctionnerait pas).

En revanche, on peut vérifier la présence d'un élément dans un set grâce à l'opérateur `in` :

```python
print('apple' in fruits)   # True
print('kiwi' in fruits)    # False
```

On peut aussi parcourir tous les éléments d'un set avec une boucle `for`, même si l'ordre de parcours n'est pas garanti :

```python
for fruit in fruits:
    print(fruit)
```


## Ajouter et supprimer des éléments

### Ajouter un élément

La méthode `add()` permet d'ajouter un élément au set. Si l'élément est déjà présent, le set reste inchangé.

```python
fruits.add('strawberry')
print(fruits)
# Résultat : {'apple', 'banana', 'orange', 'mango', 'strawberry'}
```

### Supprimer un élément

Deux méthodes permettent de supprimer un élément :

La méthode `remove()` supprime l'élément spécifié. Si l'élément est absent, elle lève une erreur `KeyError`.

```python
fruits.remove('apple')
print(fruits)
# Résultat : {'banana', 'orange', 'mango', 'strawberry'}
```

La méthode `discard()` supprime l'élément spécifié s'il est présent, mais ne lève aucune erreur s'il est absent. Elle est donc plus sûre quand on n'est pas certain que l'élément existe.

```python
fruits.discard('kiwi')   # Aucune erreur, même si 'kiwi' n'est pas dans le set
```

La méthode `pop()` supprime et retourne un élément arbitraire du set. Comme le set n'est pas ordonné, on ne peut pas prédire quel élément sera retiré.

```python
element = fruits.pop()
print(element)   # Un fruit quelconque
```

La méthode `clear()` vide entièrement le set.

```python
fruits.clear()
print(fruits)   # set()
```


## Les opérations ensemblistes

C'est l'une des grandes forces des sets : ils permettent d'effectuer des opérations mathématiques sur des ensembles, directement en Python.

Prenons deux sets pour illustrer :

```python
fruits = {'banana', 'mango', 'strawberry', 'orange'}
vegetables = {'carrot', 'tomato', 'cabbage', 'potato'}
```

### Union

L'union retourne un nouveau set contenant tous les éléments présents dans l'un ou l'autre des sets (ou les deux). On utilise l'opérateur `|` ou la méthode `union()`.

```python
print(fruits | vegetables)
# Résultat : {'banana', 'orange', 'mango', 'strawberry', 'carrot', 'tomato', 'cabbage', 'potato'}
```

### Intersection

L'intersection retourne un nouveau set contenant uniquement les éléments présents dans les deux sets à la fois. On utilise l'opérateur `&` ou la méthode `intersection()`.

```python
print(fruits & vegetables)
# Résultat : set()   (aucun élément en commun ici)
```

### Différence

La différence retourne un nouveau set contenant les éléments présents dans le premier set mais absents du second. On utilise l'opérateur `-` ou la méthode `difference()`.

```python
print(fruits - vegetables)
# Résultat : {'banana', 'orange', 'mango', 'strawberry'}
```

### Différence symétrique

La différence symétrique retourne un nouveau set contenant les éléments présents dans l'un ou l'autre des sets, mais pas dans les deux. On utilise l'opérateur `^` ou la méthode `symmetric_difference()`.

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
print(a ^ b)
# Résultat : {1, 2, 5, 6}
```


## Comparer des sets

Python offre plusieurs méthodes pour comparer deux sets entre eux.

`issubset()` retourne `True` si tous les éléments du set sont présents dans l'autre set (le set est un sous-ensemble).

```python
a = {1, 2}
b = {1, 2, 3, 4}
print(a.issubset(b))    # True
print(b.issubset(a))    # False
```

`issuperset()` retourne `True` si le set contient tous les éléments de l'autre set (le set est un sur-ensemble).

```python
print(b.issuperset(a))  # True
```

`isdisjoint()` retourne `True` si les deux sets n'ont aucun élément en commun.

```python
c = {10, 20}
print(a.isdisjoint(c))  # True
```


## Modifier un set en place

Certaines méthodes ne retournent pas un nouveau set mais modifient directement le set existant.

`difference_update(other_set)` supprime du set tous les éléments qui se trouvent dans `other_set`.

```python
a = {1, 2, 3, 4}
a.difference_update({3, 4, 5})
print(a)   # {1, 2}
```

`intersection_update(other_set)` ne conserve dans le set que les éléments communs avec `other_set`.

```python
a = {1, 2, 3, 4}
a.intersection_update({3, 4, 5})
print(a)   # {3, 4}
```


## Copier un set

La méthode `copy()` retourne une copie indépendante du set. Modifier la copie ne modifie pas le set original.

```python
original = {1, 2, 3}
copie = original.copy()
copie.add(4)
print(original)   # {1, 2, 3}
print(copie)      # {1, 2, 3, 4}
```


## Récapitulatif des méthodes

| Méthode | Description |
|---|---|
| `add(x)` | Ajoute l'élément `x` au set |
| `remove(x)` | Supprime `x`, lève `KeyError` si absent |
| `discard(x)` | Supprime `x` sans erreur si absent |
| `pop()` | Supprime et retourne un élément arbitraire |
| `clear()` | Vide le set |
| `copy()` | Retourne une copie indépendante |
| `union(other)` | Retourne l'union des deux sets |
| `intersection(other)` | Retourne l'intersection des deux sets |
| `difference(other)` | Retourne la différence (éléments du set absents de `other`) |
| `symmetric_difference(other)` | Retourne les éléments présents dans un seul des deux sets |
| `difference_update(other)` | Modifie le set en supprimant les éléments de `other` |
| `intersection_update(other)` | Modifie le set en ne conservant que les éléments communs |
| `issubset(other)` | `True` si le set est un sous-ensemble de `other` |
| `issuperset(other)` | `True` si le set est un sur-ensemble de `other` |
| `isdisjoint(other)` | `True` si les deux sets n'ont aucun élément commun |


## Quand utiliser un set ?

Un set est le bon choix dans les situations suivantes :

- Vous avez besoin d'éliminer des doublons dans une collection.
- Vous devez vérifier fréquemment si un élément est présent (cette opération est plus rapide sur un set que sur une liste).
- Vous souhaitez effectuer des opérations mathématiques entre des collections (union, intersection, différence).

En revanche, si l'ordre des éléments est important ou si vous avez besoin d'accéder aux éléments par leur position, préférez une liste ou un tuple.
