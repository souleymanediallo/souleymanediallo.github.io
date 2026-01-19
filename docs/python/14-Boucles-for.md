# La Boucle for
La boucle for est utilisée pour itérer sur les éléments d'une séquence (liste, chaîne de caractères, tuple, etc.) ou sur un itérable (un objet qui peut être utilisé dans une boucle for). La syntaxe générale d'une boucle for est la suivante :
```
for variable in itérable:
    # code à exécuter pour chaque élément de l'itérable
```

Itération sur les éléments d'une liste
```
fruits = ["pomme", "banane", "orange"]
for fruit in fruits:
    print(fruit)
# affiche "pomme", "banane", "orange"
```

Itération sur les éléments d'une chaîne de caractères
```
mot = "Bonjour"
for letter in mot:
    print(letter)
# affiche "B", "o", "n", "j", "o", "u", "r"
```

Itération sur les range d'un nombre
```
for i in range(5):
    print(i)
#affiche 0 1 2 3 4
```

Il est possible d'utiliser la fonction enumerate() pour obtenir l'index et la valeur de chaque élément dans une boucle for.
```
fruits = ["pomme", "banane", "orange"]
for i, fruit in enumerate(fruits):
    print(i, fruit)
#affiche (0, 'pomme') (1, 'banane') (2, 'orange')
```

Il est également possible d'utiliser la boucle for pour itérer sur des dictionnaires en utilisant les méthodes items() ou keys().
```
person = {"nom": "Dupont", "age": 30, "ville": "Paris"}
for key in person:
    print(key, person[key])
#affiche 'nom' 'Dupont' ,'age' 30, 'ville' Paris
```

Il est possible d'utiliser les instruction break pour sortir d'une boucle for quand une certaine condition est remplie, ou continue pour passer à l'itération suivante.
```
for i in range(10):
    if i == 5:
        break
    print(i)
# affiche 0 1 2 3 4

for i in range(10):
    if i % 2 == 0:
        continue
    print(i)
# affiche 1 3 5 7 9
``` 


