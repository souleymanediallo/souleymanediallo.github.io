# La Boucle While
La boucle `while` permet d'exécuter une suite d'instructions tant qu'une condition est vraie. La syntaxe générale d'une boucle while est la suivante :
```
while condition:
    # code à exécuter tant que la condition est vraie
```

Utilisation de la boucle while pour compter les nombres impairs jusqu'à 10
```
i = 0
while i < 10:
    i += 1
    if i % 2 == 0:
        continue
    print(i)
#affiche 1 3 5 7 9
```

Utilisation de while pour demander à l'utilisateur de saisir un mot jusqu'à ce qu'il saisisse 'stop'
```
word = ""
while word != "stop":
    word = input("Entrez un mot (entrez 'stop' pour quitter): ")
    print("Le mot saisi est : ", word)
```

Il est important de noter que si la condition est fausse dès le départ la boucle ne sera jamais exécutée, il est donc important d'initialiser les variables qui servent pour la condition, pour s'assurer qu'elle sera vraie au moins une fois.

Il est également possible d'utiliser les instruction `break` pour sortir d'une boucle `while` quand une certaine condition est remplie, ou `continue` pour passer à l'itération suivante. Il est important d'utiliser ces instructions avec précaution pour éviter les boucles infinies qui bloque le programme. Il est recommandé de mettre des conditions pour sortir de la boucle ou utiliser des compteurs pour limiter les tours de boucles.