# Les Itérateurs et Générateurs

## Les Itérateurs
Les itérateurs en Python sont des objets qui permettent de parcourir des collections d'éléments, comme des listes, des tuples, des dictionnaires, etc. Ils sont utilisés pour parcourir ces collections de manière efficace et sûre. Les itérateurs sont utilisés en conjonction avec les boucles for et les fonctions next`()` pour accéder aux éléments d'une collection un par un.

Il existe deux types d'itérateurs en Python: les itérateurs internes et les itérateurs externes. Les itérateurs internes sont intégrés aux objets de collection, tels que les listes et les tuples, et peuvent être utilisés avec les boucles `for`. Les itérateurs externes sont des objets distincts qui peuvent être créés à partir d'objets de collection, et doivent être utilisés avec les fonctions `next()` pour accéder aux éléments d'une collection un par un.

Voici un exemple d'utilisation d'un itérateur interne avec une boucle for pour parcourir une liste :
```
my_list = [1, 2, 3, 4, 5]
for element in my_list:
    print(element)
```

Ce qui donne comme sortie :
``` 
1
2
3
4
5
```

Voici un exemple d'utilisation d'un itérateur externe avec la fonction next() pour parcourir un tuple :
```
my_tuple = (1, 2, 3, 4, 5)
iterator = iter(my_tuple)
print(next(iterator)) # 1
print(next(iterator)) # 2
print(next(iterator)) # 3
print(next(iterator)) # 4
print(next(iterator)) # 5
```

Il est important de noter que lorsque on parcours les element avec la fonction `next()` lorsque on arrive a la fin de l'objet ( en l'occurence le tuple ) une exception "StopIteration" sera levée.
Il est possible de gérer cette exception en utilisant un constructeur try except.

En résumé, les itérateurs en Python sont des objets qui permettent de parcourir des collections d'éléments de manière efficace et sûre. Ils peuvent être utilisés avec les boucles for pour les itérateurs internes ou les fonctions `next()` pour les itérateurs externes. Les itérateurs peuvent aider à économiser de la mémoire et à améliorer les performances en parcourant les collections un élément à la fois plutôt que de charger toute la collection en mémoire.

## Les générateurs
Les générateurs en Python sont des objets qui permettent de créer des itérateurs pour des séquences de données qui ne sont pas nécessairement entièrement chargées en mémoire. Ils permettent de produire des éléments un par un au fur et à mesure qu'ils sont demandés, plutôt que de charger toute la séquence de données en mémoire avant de commencer à l'itérer. Les générateurs sont particulièrement utiles pour traiter des séquences de données volumineuses ou infinies.

Les générateurs peuvent être créés en utilisant des fonctions génératrices, qui sont des fonctions qui utilisent le mot clé yield pour renvoyer des valeurs à chaque itération. Les fonctions génératrices ne s'exécutent pas tout de suite, mais produisent un générateur qui peut être utilisé pour produire les valeurs de la séquence de données au fur et à mesure qu'elles sont demandées.

Voici un exemple de fonction génératrice qui produit les nombres de 0 à 9 :
```
def my_generator():
    for i in range(10):
        yield i

gen = my_generator()
print(next(gen)) # 0
print(next(gen)) # 1
print(next(gen)) # 2
```

Ici, la fonction `my_generator` est une fonction génératrice qui produit les nombres de 0 à 9 en utilisant une boucle for et le mot-clé yield. Lorsque la fonction est appelée, elle ne s'exécute pas immédiatement mais renvoie un générateur, qui peut être stocké dans la variable gen. Pour récupérer les valeurs produites par le générateur, on utilise la fonction `next()` qui va retourner le prochaine élément dans la séquence.

On peut aussi utiliser les générateurs avec les boucles for, qui vont automatiquement appeler next() pour chaque tour de boucle.
``` 
gen = my_generator()
for number in gen:
    print(number)
```

Ce qui donne la même sortie qu'avant mais plus lisible.

Il est important de noter que les générateurs n'ont qu'une seule direction, on ne peut pas remonter en arrière pour récupérer des valeurs précédentes après les avoir "passées".

En résumé, les générateurs en Python sont des objets qui permettent de créer des itérateurs pour des séquences de données qui ne sont pas entièrement chargées en mémoire. Ils sont créés en utilisant des fonctions génératrices qui utilisent le mot-clé yield pour renvoyer des valeurs à chaque itération. Les générateurs permettent de produire des éléments un par un au fur et à mesure qu'ils sont demandés, plutôt que de charger toute la séquence de données en mémoire avant de commencer à l'itérer. Ils sont particulièrement utiles pour traiter des séquences de données volumineuses ou infinies, car ils aident à économiser de la mémoire et à améliorer les performances en ne chargeant qu'une partie de la séquence de données à la fois.