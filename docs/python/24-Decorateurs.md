# Les Décorateurs
Les décorateurs en Python sont des fonctions ou des classes qui permettent de modifier ou d'étendre le comportement d'autres fonctions ou classes. Ils permettent de rajouter de la logique supplémentaire à une fonction existante sans avoir à la modifier directement.

Les décorateurs sont utilisés en ajoutant le symbole "@" suivi du nom du décorateur avant la déclaration de la fonction ou de la classe à décorer.

Il existe deux types de décorateurs: les décorateurs de fonctions et les décorateurs de classes. Les décorateurs de fonctions s'appliquent à des fonctions, et les décorateurs de classes s'appliquent à des classes.

Les décorateurs sont utilisés pour une variété de tâches, comme :
* La validation des entrées d'une fonction
* La mise en cache des résultats d'une fonction
* La journalisation des appels à une fonction
* L'ajout de fonctionnalités supplémentaires à une classe, comme les propriétés de lecture-seule.

## Décorateur de fonction
```
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before calling the function")
        result = func(*args, **kwargs)
        print("After calling the function")
        return result
    return wrapper

@my_decorator
def add(a, b):
    return a + b

print(add(1, 2))
```

Dans cet exemple, la fonction `my_decorator` est un décorateur qui prend une fonction `func` en entrée, et renvoie une fonction `wrapper` qui exécute des instructions supplémentaires avant et après l'appel à la fonction `func`. La fonction add est décorée avec `my_decorator` en utilisant le symbole "@". Lorsque `add(1, 2)` est appelé, la fonction `wrapper` est exécutée, ce qui affiche "Before calling the function", appelle `add(1, 2)` puis affiche "After calling the function".

## Décorateur de classe
```
class MyDecorator:
    def __init__(self, func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print("Before calling the function")
        result = self.func(*args, **kwargs)
        print("After calling the function")
        return result

@MyDecorator
def add(a, b):
    return a + b

print(add(1, 2))
```

Dans cet exemple, la classe `MyDecorator` est utilisée comme décorateur en surchargeant la méthode `__call__` . Lorsque `add(1, 2)` est appelé, l'objet `MyDecorator(add)` est créé avec la fonction add en entrée, puis `__call__` est appelé avec les paramètres de `add(1,2)` et exécute les instructions supplémentaires avant et après l'appel à la fonction `add`.

Il est important de noter que dans les deux exemples ci-dessus, la fonction `add` n'a pas besoin d'être modifiée pour ajouter la logique supplémentaire fournie par le décorateur.

En résumé, les décorateurs sont un mécanisme en python permettant d'ajouter de la logique autour d'une fonction ou d'une classe sans altérer son code source, ceci permet de rendre le code plus lisible et de faciliter l'entretien.