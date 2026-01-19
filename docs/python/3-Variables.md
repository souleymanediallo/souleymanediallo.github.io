# Les Variables
Une variable en Python est un nom qui réfère à une valeur stockée en mémoire. Vous pouvez créer une variable en lui donnant un nom et en lui affectant une valeur en utilisant l'opérateur d'affectation "=". Par exemple :

```
>>> x = 10
>>> y = "hello"
>>> z = 3.14
```

Dans cet exemple, nous avons créé trois variables : x, y et z. x contient la valeur entière 10, y contient la chaîne de caractères "hello" et z contient le nombre flottant 3.14.

Il y a quelques règles à respecter lors de la définition des noms de variables en Python :

* Les noms de variables ne peuvent pas commencer par un chiffre.
* Les noms de variables ne peuvent pas contenir de caractères spéciaux, tels que "!" ou "$".
* Les noms de variables ne peuvent pas être des mots-clés Python, tels que "for" ou "while".
* Les noms de variables doivent être courts, précis et représentatifs de leur contenu.

Il est recommandé de suivre les conventions de nommage standard en Python, qui consistent à utiliser des minuscules et des underscores (par exemple, my_variable) pour les noms de variables. Cela rend le code plus facile à lire et à maintenir.

## Type de variable
Vous pouvez également utiliser la fonction type() de Python pour vérifier le type de données d'une variable. Par exemple :

```
>>> x = 10
>>> y = "hello"
>>> z = 3.14
>>> print(type(x))  # affiche "<class 'int'>"
>>> print(type(y))  # affiche "<class 'str'>"
>>> print(type(z))  # affiche "<class 'float'>"
```

Vous pouvez également changer le type de données d'une variable en utilisant des fonctions de conversion de type, comme int(), float() et str(). Par exemple :

```
>>> x = 10
>>> y = "15"
>>> z = 3.14
>>> a = int(y)  # a est maintenant une variable entière avec la valeur 15
>>> b = float(y)  # b est maintenant une variable flottante avec la valeur 15.0
>>> c = str(x)  # c est maintenant une variable chaîne de caractères avec la valeur "10"
```

## Exercices

Exercice 1 : Créez une variable x contenant la valeur entière 5, une variable y contenant la valeur flottante 3.14 et une variable z contenant la chaîne de caractères "Bonjour". Affichez le type de chaque variable.

Exercice 2 : Créez une variable name contenant votre nom et une variable age contenant votre âge. Affichez une chaîne de caractères de la forme "Bonjour, je m'appelle `[nom]` et j'ai `[âge]` ans".

Exercice 3 : Créez une variable a contenant la valeur entière 5 et une variable b contenant la valeur entière 10. Créez une variable c qui contient la somme de a et b. Affichez la valeur de c.