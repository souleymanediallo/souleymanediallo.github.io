# Les objets immuables et les objets mutables
En Python, il existe deux types d'objets : les objets immuables et les objets mutables. Les objets immuables sont des objets dont les valeurs ne peuvent pas être modifiées une fois créés, tandis que les objets mutables sont des objets dont les valeurs peuvent être modifiées après leur création.

Les objets immuables les plus courants sont les types de base tels que les nombres (int, float), les chaînes de caractères (str), les tuples, etc.

## objet immuable
Voici un exemple d'utilisation d'un objet immuable :
```
x = 3
y = x
y += 2
print(x) # affiche 3
```
Dans cet exemple, l'affectation de y = x crée une nouvelle référence à l'objet x, et l'instruction y += 2 crée un nouvel objet int avec la valeur 5. L'objet x n'est pas affecté par cette opération et reste inchangé.

## Les objets mutables
Les objets mutables les plus courants sont les listes, les dictionnaires, et les ensembles.

Voici un exemple d'utilisation d'un objet mutable :
```
my_list = [1, 2, 3]
my_list_2 = my_list
my_list_2.append(4)
print(my_list) # affiche [1, 2, 3, 4]
```

Dans cet exemple, l'affectation de `my_list_2 = my_list` crée une nouvelle référence à l'objet `my_list`, donc lorsque on utilise la méthode `append(4)` sur `my_list_2`, l'objet `my_list` est également modifié.

Il est important de noter que les objets immuables sont généralement plus simples à utiliser car ils sont plus sûrs et plus prévisibles car ils ne peuvent pas être modifiés accidentellement. Par contre, les objets mutables sont plus flexibles et peuvent être utilisés pour des tâches plus avancées, mais ils nécessitent une attention accrue pour éviter les erreurs potentielles.

