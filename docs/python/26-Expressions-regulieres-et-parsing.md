# Les Expréssions régulières et parsing
Les expressions régulières (ou "regex" pour regular expressions en anglais) en Python sont un moyen puissant de rechercher, remplacer et manipuler des chaînes de caractères. Les expressions régulières utilisent des caractères spéciaux pour décrire des motifs dans les chaînes de caractères. Python inclut une bibliothèque intégrée appelée "re" pour travailler avec des expressions régulières.

Voici un exemple d'utilisation des expressions régulières pour rechercher un motif dans une chaîne de caractères :
```
import re

string = "Hello World!"

match = re.search("World", string)
if match:
    print("Found: ", match.group())
else:
    print("Not found")
```

Dans cet exemple, nous utilisons la fonction `search()` de la bibliothèque "re" pour rechercher le motif "World" dans la chaîne de caractères "string". La fonction renvoie un objet correspondant si elle trouve une correspondance, sinon elle renvoie None. Nous pouvons utiliser la méthode `group()` de l'objet correspondant pour obtenir la correspondance trouvée.

Il existe d'autres fonctions pour utiliser les expressions régulières comme `findall()` qui renvoie toutes les correspondances, `sub()` pour remplacer les correspondances ou `split()`

Les expressions régulières utilisent également des caractères spéciaux tels que ., *, +, ? pour décrire des motifs plus complexes. 

Par exemple : 
* le point `.` correspond à n'importe quel caractère, 
* l'étoile `*` correspond à zéro ou plusieurs occurrences d'un caractère, 
* le plus `+` correspond à une ou plusieurs occurrences d'un caractère, 
* le point d'interrogation `?` correspond à zéro ou une occurrence d'un caractère.

Il est important de noter que les expressions régulières peuvent être assez complexes à comprendre et à utiliser correctement, mais une fois maîtrisées, elles peuvent être d'une grande aide pour manipuler des données de texte de manière efficace et automatisée. Il est donc recommandé de consacrer du temps pour comprendre les concepts fondamentaux des expressions régulières et de s'entraîner à les utiliser avant de les utiliser dans des projets réels.