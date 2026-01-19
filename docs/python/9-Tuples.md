# Les Tuples
Un tuple est un type de séquence immuable en Python. Cela signifie qu'une fois que vous avez créé un tuple, vous ne pouvez pas modifier son contenu. Les tuples sont créés en mettant une séquence d'éléments séparés par des virgules entre parenthèses (`()`).

Voici un exemple de tuple en Python :

```
coordinates = (4, 5)
```

Vous pouvez accéder aux éléments d'un tuple à l'aide d'un index, comme avec une liste. Python utilise une indexation de base zéro, de sorte que le premier élément du tuple a un index de 0, le deuxième élément a un index de 1, et ainsi de suite.
```
print(coordinates[0])  # Output: 4
print(coordinates[1])  # Output: 5
```

Vous pouvez également utiliser des index négatifs pour accéder aux éléments à partir de la fin du tuple. Par exemple, `coordinates[-1]`fait référence au dernier élément du tuple, `coordinates[-2]` fait référence à l'avant-dernier élément, etc.
```
print(coordinates[-1])  # Output: 5
print(coordinates[-2])  # Output: 4
```

Les tuples peuvent contenir des éléments de différents types, tout comme les listes.
```
mixed = (1, 'hello', 3.14, True)
```

Une différence entre les tuples et les listes est que les tuples sont immuables, ce qui signifie que vous ne pouvez pas modifier le contenu d'un tuple. Par exemple, vous ne pouvez pas affecter une nouvelle valeur à un index ou ajouter un élément à un tuple.
```
# This will raise a TypeError
coordinates[0] = 10

# This will also raise a TypeError
coordinates.append(6)
```

Les tuples sont souvent utilisés pour stocker des données qui ne doivent pas être modifiées, telles que des enregistrements de base de données ou des configurations fixes. Ils sont également plus rapides que les listes, car ils nécessitent moins de mémoire et sont plus efficaces pour y accéder.
