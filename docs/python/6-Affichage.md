# L'Affichage
En Python, vous pouvez utiliser la fonction `print()` pour afficher du texte ou des valeurs sur la sortie standard (généralement la console).

Voici quelques exemples d'utilisation de la fonction print() :
```
>>> print("Bonjour !")  # affiche "Bonjour !"
>>> print(42)  # affiche 42
>>> print(3.14)  # affiche 3.14
>>> print("La réponse est", 42)  # affiche "La réponse est 42"
>>> print("Pi vaut environ", 3.14)  # affiche "Pi vaut environ 3.14"
```

La fonction `print()` accepte un ou plusieurs arguments, qui peuvent être des chaînes de caractères, des nombres ou d'autres types de données. Elle les convertit en chaînes de caractères et les affiche séparées par des espaces.

Vous pouvez également utiliser la fonction `print()` pour afficher des résultats de calculs mathématiques :
```
>>> x = 10
>>> y = 3
>>> z = x / y
>>> print("Le résultat de", x, "/", y, "est", z)  # affiche "Le résultat de 10 / 3 est 3.3333333333333335"
```

## function format
Il est également possible de formatter l'affichage en utilisant la fonction `format()` de Python ou la syntaxe de formatage de chaîne (f-string) introduite en Python 3.6. Voici quelques exemples :
```
>>> x = 10
>>> y = 3
>>> z = x / y
>>> print("Le résultat de {} / {} est {}".format(x, y, z))  # affiche "Le résultat de 10 / 3 est 3.3333333333333335"
```

## formatage de chaîne
La syntaxe de formatage de chaîne `(f-string)` est une syntaxe concise et pratique pour formatter l'affichage en Python. Elle permet de remplacer des placeholders dans une chaîne de caractères par des valeurs en utilisant la syntaxe {nom_de_variable} ou `{nom_de_variable:format}`.
```
>>> x = 10
>>> y = 3.14
>>> z = "hello"
>>> a = True
>>> b = [1, 2, 3]

>>> print(x, y, z)  # affiche "10 3.14 hello"
>>> print(f"{x} {y} {z}")  # affiche "10 3.14 hello"
>>> print(f"{x=} {y=} {z=}")  # affiche "x=10 y=3.14 z='hello'"
>>> print(f"{a=} {b=}")  # affiche "a=True b=[1, 2, 3]"
```
