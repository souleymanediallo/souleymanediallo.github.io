# Les Commentaires
En Python, les commentaires sont des lignes de code qui sont ignorées par l'interpréteur Python. Ils sont utilisés pour expliquer le code et le rendre plus facile à comprendre pour les autres personnes qui le lisent.

Il existe deux types de commentaires en Python :
* Les commentaires sur une seule ligne, qui commencent par le caractère "#" :

```
# Ceci est un commentaire sur une seule ligne
```

* Les commentaires sur plusieurs lignes, qui sont entourés par les caractères triple guillemet (""" ou ''') :
```
"""
Ceci est un commentaire
sur plusieurs lignes.
Il peut s'étendre sur
autant de lignes que nécessaire.
"""
```

Il est recommandé d'ajouter des commentaires dans votre code pour expliquer ce que vous faites et pourquoi vous le faites. Cela rend le code plus facile à comprendre et à maintenir pour vous-même et pour les autres personnes qui pourraient le lire.

Voici un exemple de code avec des commentaires :
```
# Cette fonction calcule la somme de deux nombres
def add(x, y):
    # On utilise l'opérateur "+" pour additionner x et y
    result = x + y
    # On retourne le résultat
    return result

# On appelle la fonction avec les valeurs 10 et 20
result = add(10, 20)
# On affiche le résultat
print(result)  # affiche 30
```

Il est également important de ne pas en abuser et de ne pas ajouter trop de commentaires inutiles. Un bon commentaire est concis, précis et utile. Il doit aider à comprendre le code, pas à le rendre plus compliqué.