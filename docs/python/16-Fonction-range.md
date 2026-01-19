# Le Fonction range
La fonction `range()` permet de créer un objet itérable contenant une séquence de nombres. Elle prend un, deux ou trois arguments :
* `range(stop)`: génère une séquence de nombres allant de 0 (inclus) à `stop` (exclu).
* `range(start, stop)`: génère une séquence de nombres allant de `start` (inclus) à `stop` (exclu).
* `range(start, stop, step)`: génère une séquence de nombres allant de `start` (inclus) à stop (exclu), en sautant de `step` en `step`.

Générer une séquence de nombres de 0 à 4
```
for i in range(5):
    print(i) #affiche 0 1 2 3 4
```

Générer une séquence de nombres de 2 à 7
```
for i in range(2, 8):
    print(i) #affiche 2 3 4 5 6 7
```

Générer une séquence de nombres de 1 à 10 en sautant de 2 en 2
```
for i in range(1, 11, 2):
    print(i) #affiche 1 3 5 7 9
```

Il est important de noter que la fonction `range()` ne génère pas tous les éléments de la séquence en mémoire mais elle génère les éléments au fur et à mesure de l'itération, cela permet de générer des séquences de nombres très grandes sans manger toute la mémoire. Il est donc possible de l'utiliser en combinaison avec la boucle for pour itérer sur des séquences de nombres.
