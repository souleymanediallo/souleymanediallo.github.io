# Les Fichiers
Les fichiers en Python sont des ressources externes qui contiennent des données telles que des textes, des images ou des vidéos. Pour accéder à ces données, vous devez ouvrir un fichier en utilisant des fonctions de la bibliothèque standard de Python. Il existe deux modes d'ouverture de fichiers en Python : le mode lecture et le mode écriture.

##  Lire un fichier en utilisant le mode lecture :
```
with open('example.txt', 'r') as f:
    print(f.read())
```

Dans cet exemple, nous utilisons la fonction open() pour ouvrir un fichier appelé "example.txt" en mode lecture ('r'). La fonction read() est ensuite utilisée pour lire le contenu du fichier et l'afficher à l'écran.

## Ecrire dans un fichier en utilisant le mode écriture :
```
with open('example.txt', 'w') as f:
    f.write("Hello World!")
```

Dans cet exemple, nous utilisons la fonction `open()` pour ouvrir un fichier appelé "example.txt" en mode écriture ('w'). La fonction `write()` est ensuite utilisée pour écrire le texte "Hello World!" dans le fichier. Si le fichier n'existe pas, il sera créé. Si le fichier existe déjà, son contenu précédent sera écrasé.

Il est important de noter que lorsque vous utilisez `open()` on utilise généralement "with" pour gérer la fermeture automatique du fichier. Cela permet de s'assurer que le fichier est fermé correctement même en cas d'exception.


