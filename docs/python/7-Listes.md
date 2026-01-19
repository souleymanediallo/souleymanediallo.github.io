# C'est quoi une liste en python ?

Une liste est une collection d'éléments ordonnés et modifiables. En Python, une liste est créée en plaçant une séquence d'éléments séparés par des virgules entre crochets (`[]`).

Voici un exemple de liste en Python :
```
fruits = ['apple', 'banana', 'orange', 'mango']
```

Vous pouvez accéder aux éléments d'une liste à l'aide d'un index. Python utilise l'indexation de base zéro, de sorte que le premier élément de la liste a un index de 0, le deuxième élément a un index de 1, et ainsi de suite.
```
print(fruits[0])  # Output: 'apple'
print(fruits[2])  # Output: 'orange'
```

Vous pouvez également utiliser des index négatifs pour accéder aux éléments à partir de la fin de la liste. Par exemple, `fruits[-1]` fait référence au dernier élément de la liste, `fruits[-2]`fait référence à l'avant-dernier élément, etc.
```
print(fruits[-1])  # Output: 'mango'
print(fruits[-3])  # Output: 'banana'
```

Vous pouvez modifier les éléments d'une liste en affectant une nouvelle valeur à un index :
```
fruits[0] = 'kiwi'
print(fruits)  # Output: ['kiwi', 'banana', 'orange', 'mango']
```

Vous pouvez également ajouter de nouveaux éléments à une liste en utilisant la méthode `append()` :
```
fruits.append('strawberry')
print(fruits)  # Output: ['kiwi', 'banana', 'orange', 'mango', 'strawberry']
``` 

Les listes en Python sont dynamiques et peuvent contenir des éléments de différents types. Vous pouvez mélanger et assortir différents types dans une seule liste.
```
mixed = [1, 'hello', 3.14, True]
```
