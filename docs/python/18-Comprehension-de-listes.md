# Les compréhension de listes
Les compréhensions de listes en Python sont un moyen concis de créer des listes en utilisant une syntaxe simple. Il s'agit d'une technique de compréhension de liste qui permet de créer une nouvelle liste en itérant sur une autre liste (ou tout autre itérable), en appliquant une fonction à chaque élément de celle-ci et en sélectionnant les éléments qui satisfont une condition.

Voici un exemple de compréhension de liste qui crée une nouvelle liste contenant les carrés des entiers de 0 à 9:

```
squares = [x**2 for x in range(10)]
print(squares)
```

La sortie sera :
```
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

On peut également ajouter une condition pour filtrer les éléments de la liste d'origine en utilisant le mot-clé "if" :
```
squares = [x**2 for x in range(10) if x % 2 == 0]
print(squares)
```

La sortie sera :
```
[0, 4, 16, 36, 64]
```

Il est possible d'utiliser des compréhensions de listes pour créer des listes à partir de plusieurs itérables en utilisant des expressions de compréhension de listes imbriquées.

Voici un exemple de compréhension de listes imbriquées en Python :
```
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flat_list = [x for row in matrix for x in row]
print(flat_list)
```

La sortie sera :
```
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Dans cet exemple, nous avons une matrice (liste de listes) et nous voulons créer une nouvelle liste qui contient tous les éléments de la matrice dans un ordre plat. Pour ce faire, nous utilisons une compréhension de liste imbriquée. La première compréhension de liste (for row in matrix) itère sur chaque ligne de la matrice, tandis que la seconde compréhension de liste (for x in row) itère sur chaque élément de chaque ligne.

Il est important de noter que l'ordre des boucles dans une compréhension de listes imbriquées est important. Dans l'exemple ci-dessus, nous avons d'abord itéré sur les lignes de la matrice, puis sur les éléments de chaque ligne. Si nous avions inversé l'ordre des boucles, nous aurions obtenu une liste qui contient d'abord tous les éléments de la première colonne, puis tous les éléments de la seconde colonne, etc.
