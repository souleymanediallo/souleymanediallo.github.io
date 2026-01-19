# Les Modules et Packages
## Les modules
En Python, les modules sont des fichiers contenant des définitions de fonctions, de variables et d'autres types d'objets que l'on peut réutiliser dans d'autres programmes. Les modules permettent de structurer le code en le séparant en plusieurs fichiers, ce qui le rend plus facile à comprendre et à maintenir. Les modules Python sont créés en enregistrant des scriptes dans un fichier avec l'extension `.py`.

Il est possible d'utiliser les modules en utilisant l'instruction import. Par exemple, pour utiliser le module math, il suffit de taper import math en début de script. Il est également possible d'importer uniquement une partie des fonctions en utilisant l'instruction from suivi du nom du module, suivi de import suivi du nom des fonctions à importer.

Exemple : utilisation de la fonction `sqrt()` du module math pour calculer la racine carrée d'un nombre
``` 
# importation du module math
import math

nombre = 16
racine_carrée = math.sqrt(nombre)
print(racine_carrée) # affiche 4.0

# utilisation de la fonction pi du module math
print(math.pi) #affiche 3.141592653589793
```

Utilisation de la fonction sinus du module math
```
# importation du module math
import math

angle = math.radians(30)
sin_angle = math.sin(angle)
print(sin_angle)
```

Il est également possible de renommer le module lors de l'import pour éviter les conflits de noms 
```
import math as m
sin_angle = m.sin(m.radians(30))
print(sin_angle)
```


Les packages en Python sont un moyen de regrouper des modules en sous-dossiers pour une meilleure organisation de son code. Un package est simplement un répertoire qui contient un fichier `__init__.py` et peut contenir d'autres sous-dossiers qui contiennent des modules ou des sous-packages. Il est possible d'utiliser les packages en utilisant l'instruction import de manière hiérarchique.

Les modules tiers en python peuvent être installés en utilisant un gestionnaire de paquet comme pip. pip est un utilitaire qui permet d'installer des packages Python à partir du registre central Python ou à partir de dossiers locaux. Pour installer un module tiers, il suffit d'ouvrir une invite de commande ou un terminal, et de taper la commande `pip install <nom_module>`.

Voici un exemple d'installation d'un module tiers requests: