# Les fonctions
En Python, les fonctions sont des blocs de code réutilisables qui peuvent être appelés à plusieurs endroits dans un programme. Les fonctions permettent de rendre le code plus lisible, maintenable et réutilisable.

La syntaxe générale pour déclarer une fonction est la suivante :
```
def nom_de_fonction(paramètres):
    # bloc d'instructions
```

Déclaration d'une fonction qui prend deux nombres en entrée et renvoie leur somme
```
def somme(a, b):
    return a + b

# Appel de la fonction
resultat = somme(3, 4)
print(resultat) # affiche 7
```

Déclaration d'une fonction sans paramètre
```
def bonjour():
    return "Bonjour"

resultat = bonjour()
print(resultat) #affiche Bonjour
```

Il est possible de définir des valeurs par défaut pour les paramètres d'une fonction :
```
def somme(a, b=0):
    return a + b

# Appel de la fonction
resultat = somme(3) # si on ne donne pas de valeur pour b il prend 0 comme valeur par défaut
print(resultat) # affiche 3
```

Il est possible également de utiliser *args et **kwargs pour passer un nombre variable de paramètre à une fonction.
```
def test_args_kwargs(*args, **kwargs):
    print(args)
    print(kwargs)

test_args_kwargs(1, 2, 3, a=1, b=2)
# affiche (1, 2, 3) {'a': 1, 'b': 2}
```

Les fonctions en python ont un scope local qui est indépendant des variables définies dans d'autres parties du programme. Cela signifie que les variables déclarées dans une fonction ne sont accessibles qu'à l'intérieur de cette fonction et ne peuvent pas être utilisées à l'extérieur de cette fonction.

Cependant, il est possible d'accéder aux variables déclarées à l'extérieur d'une fonction en les déclarant comme `global` à l'intérieur de la fonction. Il est aussi possible de retourner une ou plusieurs valeurs en utilisant l'instruction `return`.

```
# déclaration de variable globale
x = 10

def my_function():
    # déclaration de variable locale
    y = 5
    # utilisation de variable locale
    print(y)

# appel de la fonction
my_function() # affiche 5

# utilisation de variable globale
print(x) # affiche 10

# utilisation de variable locale à l'extérieur de la fonction
print(y) # provoque une erreur car y est une variable locale de la fonction my_function et n'est pas définie à l'extérieur de cette fonction
```