# Les Expressions Lambda
Les expressions lambda en Python sont un moyen de créer des fonctions anonymes, c'est-à-dire des fonctions sans nom. Ces fonctions peuvent être utilisées pour des tâches simples et courtes, telles que des calculs simples ou des filtrages de listes.

Voici un exemple d'utilisation d'une expression lambda pour créer une fonction qui prend un nombre en entrée et le multiplie par 2 :
```
double = lambda x: x*2
print(double(5)) # 10
```

Dans cet exemple, nous utilisons la syntaxe lambda pour créer une fonction anonyme qui prend un argument x et retourne x multiplié par 2. Nous assignons ensuite cette fonction à la variable "double" et utilisons ensuite cette variable pour appeler la fonction.

Les expressions lambda peuvent également être utilisées avec des fonctions telles que `map()` et `filter()` pour effectuer des opérations sur des listes.

Voici un exemple d'utilisation d'une expression lambda avec la fonction `map()` pour doubler tous les éléments d'une liste:
``` 
numbers = [1, 2, 3, 4, 5]
doubled_numbers = list(map(lambda x: x*2, numbers))
print(doubled_numbers) # [2, 4, 6, 8, 10]
```

Il est important de noter que les expressions lambda sont limitées à une seule instruction et doivent être utilisées pour des tâches simples et courtes. Pour des tâches plus complexes, il est préférable d'utiliser des fonctions normales définies avec la syntaxe `def`. Les fonctions définies avec def ont un nom et peuvent contenir plusieurs instructions, ce qui les rend plus faciles à lire, à comprendre et à maintenir. Les fonctions définies avec def peuvent également être réutilisées dans d'autres parties de votre code, ce qui n'est pas le cas pour les fonctions lambda qui sont généralement utilisées pour des tâches spécifiques et ponctuelles.