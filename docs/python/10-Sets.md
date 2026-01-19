# Les Sets

Un ensemble est une collection d'éléments non ordonnés et uniques en Python. Il est similaire à une liste, mais les éléments d'un ensemble ne sont pas ordonnés et ne peuvent pas être dupliqués.

Les ensembles sont créés en plaçant une séquence d'éléments séparés par des virgules entre accolades `({})`.

Voici un exemple d'ensemble en Python :

```
fruits = {'apple', 'banana', 'orange', 'mango'}
```

Comme les ensembles ne sont pas ordonnés, vous ne pouvez pas accéder à leurs éléments à l'aide d'un index. Au lieu de cela, vous pouvez utiliser l' inopérateur pour vérifier si un élément se trouve dans un ensemble :

```
print('apple' in fruits)  # Output: True
print('kiwi' in fruits)   # Output: False
```

Vous pouvez ajouter des éléments à un ensemble en utilisant la méthode `add()` :

```
fruits.add('strawberry')
print(fruits)  # Output: {'apple', 'banana', 'orange', 'mango', 'strawberry'}
```

Vous pouvez supprimer des éléments d'un ensemble à l'aide de la méthode `remove()` :

```
fruits.remove('apple')
print(fruits)  # Output: {'banana', 'orange', 'mango', 'strawberry'}
```

Vous pouvez également effectuer des opérations d'ensemble telles que l'union, l'intersection et la différence à l'aide des méthodes ou opérateurs correspondants :

```
vegetables = {'carrot', 'tomato', 'cabbage', 'potato'}

# Union
print(fruits | vegetables)  # Output: {'banana', 'orange', 'mango', 'cabbage', 'potato', 'strawberry', 'carrot', 'tomato'}

# Intersection
print(fruits & vegetables)  # Output: set()

# Difference
print(fruits - vegetables)  # Output: {'banana', 'orange', 'mango', 'strawberry'}
```

Les ensembles sont utiles pour stocker et manipuler des collections de données où l'ordre des éléments n'est pas important et les doublons doivent être évités.

Voici une liste de certaines méthodes et opérations courantes que vous pouvez utiliser avec les ensembles en Python :

- add(x): Ajoute un élément xà l'ensemble.
- clear(): Supprime tous les éléments de l'ensemble.
- copy(): renvoie une copie superficielle de l'ensemble.
- difference(other_set): Renvoie un nouvel ensemble qui contient les éléments qui sont dans l'ensemble mais pas dans other_set.
- difference_update(other_set): Supprime les éléments qui se trouvent dans other_setl'ensemble.
- discard(x): Supprime l'élément xde l'ensemble, s'il est présent.
- intersection(other_set): Renvoie un nouvel ensemble qui contient les éléments communs à l'ensemble et other_set.
- intersection_update(other_set): Supprime les éléments qui ne sont pas communs à l'ensemble et other_set.
- isdisjoint(other_set): Renvoie Truesi l'ensemble n'a aucun élément en commun avec other_set, Falsesinon.
- issubset(other_set): Retourne Truesi l'ensemble est un sous-ensemble de other_set, Falsesinon.
- issuperset(other_set): Retourne Truesi l'ensemble est un sur-ensemble de other_set, Falsesinon.
- pop(): Supprime et renvoie un élément arbitraire de l'ensemble.
- remove(x): Supprime l'élément xde l'ensemble. S'il xn'est pas présent, il lève un KeyError.
- symmetric_difference(other_set): Renvoie un nouvel ensemble qui contient les éléments
