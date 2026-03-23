# Les 10 erreurs que font tous les débutants en Python

Apprendre Python, c'est rapide. Le langage est lisible, concis, et pardonne beaucoup. Mais cette apparente simplicité masque une série de pièges dans lesquels presque tout le monde tombe au début. Cet article passe en revue les dix erreurs les plus fréquentes, avec des exemples concrets et les bonnes pratiques pour les éviter définitivement.

## 1. Confondre les types mutables et immuables

En Python, chaque objet est soit **mutable** (modifiable après création), soit **immuable** (figé une fois créé). Cette distinction a des conséquences directes sur le comportement du code, notamment lorsqu'on passe des objets à des fonctions ou qu'on les assigne à plusieurs variables.

Les types immuables comprennent `int`, `float`, `str`, `tuple` et `frozenset`. Les types mutables sont `list`, `dict`, `set` et les instances de classes personnalisées.

Voici un exemple classique qui surprend beaucoup de débutants :

```python
# Avec un type immuable (str)
a = "bonjour"
b = a
b = "salut"
print(a)  # "bonjour" — a n'a pas changé

# Avec un type mutable (list)
a = [1, 2, 3]
b = a        # b pointe vers le MÊME objet
b.append(4)
print(a)     # [1, 2, 3, 4] — a a été modifié !
```

Quand vous écrivez `b = a` avec une liste, vous ne copiez pas la liste, vous créez simplement une nouvelle référence vers le même objet en mémoire. Modifier `b` modifie donc aussi `a`.

Pour éviter ce comportement, il faut créer explicitement une copie :

```python
a = [1, 2, 3]
b = a.copy()       # copie superficielle
b.append(4)
print(a)           # [1, 2, 3] — a est préservé
print(b)           # [1, 2, 3, 4]
```

Ce comportement s'applique partout où vous manipulez des objets mutables : dans les fonctions, les boucles, les structures imbriquées. En garder conscience dès le départ vous évitera des bugs difficiles à diagnostiquer.

## 2. Utiliser des arguments mutables par défaut dans les fonctions

C'est l'une des erreurs les plus connues en Python, et pourtant elle continue de piéger les débutants. Lorsqu'on définit une fonction avec un argument par défaut mutable — typiquement une liste ou un dictionnaire — cet objet est créé **une seule fois** au moment de la définition de la fonction, pas à chaque appel.

```python
# Mauvaise pratique
def ajouter_element(element, liste=[]):
    liste.append(element)
    return liste

print(ajouter_element(1))   # [1]
print(ajouter_element(2))   # [1, 2]  ← surprenant !
print(ajouter_element(3))   # [1, 2, 3]  ← la liste persiste entre les appels
```

La liste `[]` définie par défaut est partagée entre tous les appels successifs à la fonction. Ce n'est presque jamais le comportement voulu.

La bonne pratique consiste à utiliser `None` comme valeur par défaut, puis à initialiser l'objet mutable à l'intérieur de la fonction :

```python
# Bonne pratique
def ajouter_element(element, liste=None):
    if liste is None:
        liste = []
    liste.append(element)
    return liste

print(ajouter_element(1))   # [1]
print(ajouter_element(2))   # [2]  ← chaque appel repart d'une nouvelle liste
```

Cette règle s'applique aussi bien aux listes qu'aux dictionnaires, aux sets, ou à tout autre objet mutable utilisé comme valeur par défaut.

## 3. Mal comprendre la portée des variables (scope)

Python suit la règle **LEGB** pour résoudre les noms de variables : Local, Enclosing, Global, Built-in. Les débutants ont souvent du mal avec la portée globale et les closures.

Voici un cas typique :

```python
compteur = 0

def incrementer():
    compteur += 1  # UnboundLocalError !

incrementer()
```

Python voit l'assignation `compteur += 1` et considère que `compteur` est une variable locale à la fonction. Mais elle n'a pas été définie localement avant d'être utilisée, d'où l'erreur.

Pour modifier une variable globale depuis une fonction, il faut le déclarer explicitement :

```python
compteur = 0

def incrementer():
    global compteur
    compteur += 1

incrementer()
print(compteur)  # 1
```

Cela dit, utiliser `global` est souvent le signe d'une conception à revoir. Une meilleure approche est d'encapsuler l'état dans une classe ou de retourner la nouvelle valeur depuis la fonction :

```python
def incrementer(compteur):
    return compteur + 1

compteur = 0
compteur = incrementer(compteur)
print(compteur)  # 1
```

Dans le cas des fonctions imbriquées (closures), c'est le mot-clé `nonlocal` qui permet de modifier une variable de la fonction englobante :

```python
def creer_compteur():
    valeur = 0
    def incrementer():
        nonlocal valeur
        valeur += 1
        return valeur
    return incrementer

compteur = creer_compteur()
print(compteur())  # 1
print(compteur())  # 2
```

## 4. Comparer avec == là où il faut is

En Python, `==` compare la **valeur** de deux objets, tandis que `is` compare leur **identité** — c'est-à-dire s'ils sont le même objet en mémoire. Cette nuance est cruciale, surtout lorsqu'on travaille avec `None`, les booléens ou les petits entiers.

```python
# Mauvaise pratique
def traiter(valeur=None):
    if valeur == None:   # fonctionne, mais trompeur
        print("Aucune valeur fournie")

# Bonne pratique
def traiter(valeur=None):
    if valeur is None:   # idiomatique et sémantiquement correct
        print("Aucune valeur fournie")
```

Utiliser `==` avec `None` peut même produire des comportements inattendus si un objet personnalisé redéfinit `__eq__`. Avec `is None`, vous testez l'identité réelle, ce qui est toujours fiable.

La même logique s'applique aux booléens. Préférez toujours `is True` ou `is False` si vous avez vraiment besoin de distinguer `True` de toute valeur truthy, ou mieux encore, laissez Python évaluer directement la valeur :

```python
actif = True

# Inutilement verbeux
if actif == True:
    print("actif")

# Idiomatique
if actif:
    print("actif")
```

Un autre piège concerne l'interning des entiers. Python met en cache les petits entiers (généralement entre -5 et 256), ce qui peut donner l'illusion que `is` fonctionne comme `==` :

```python
a = 256
b = 256
print(a is b)   # True  ← par coïncidence (interning)

a = 1000
b = 1000
print(a is b)   # False ← deux objets distincts
```

Ne vous fiez donc jamais à `is` pour comparer des valeurs numériques ou des chaînes arbitraires. Réservez `is` exclusivement pour `None`, `True` et `False`.

## 5. Ignorer les exceptions ou les capturer trop largement

La gestion des erreurs est un sujet que beaucoup de débutants traitent trop vite. Deux erreurs symétriques sont fréquentes : ne pas gérer les exceptions du tout, ou les capturer de façon trop large avec un `except` générique.

```python
# Dangereux : capture TOUTES les exceptions, même les bugs
try:
    resultat = int(input("Entrez un nombre : "))
except:
    print("Erreur")
```

Ce code masque toutes les erreurs, y compris `KeyboardInterrupt`, `SystemExit`, et vos propres bugs. Vous ne saurez jamais ce qui s'est vraiment passé.

La bonne pratique est de toujours spécifier les exceptions attendues, de les traiter individuellement, et de n'attraper que ce que vous êtes capable de gérer :

```python
try:
    resultat = int(input("Entrez un nombre : "))
except ValueError:
    print("Ce n'est pas un entier valide.")
except KeyboardInterrupt:
    print("\nOpération annulée par l'utilisateur.")
else:
    print(f"Vous avez entré : {resultat}")
finally:
    print("Fin de la saisie.")
```

Le bloc `else` s'exécute uniquement si aucune exception n'a été levée. Le bloc `finally` s'exécute dans tous les cas — il est parfait pour libérer des ressources comme des fichiers ou des connexions.

Il est aussi possible de chaîner les exceptions pour conserver le contexte d'origine :

```python
try:
    avec_base_de_données()
except DatabaseError as e:
    raise RuntimeError("Impossible de charger les données") from e
```

Le mot-clé `from` préserve la trace de l'exception originale, ce qui facilite le débogage.

## 6. Construire des chaînes de caractères avec l'opérateur +

La concaténation de chaînes avec `+` dans une boucle est un classique des erreurs de performance. En Python, les chaînes sont immuables : chaque opération `+` crée un nouvel objet en mémoire, ce qui rend la construction itérative extrêmement coûteuse pour de grandes quantités de données.

```python
# Mauvaise pratique — O(n²) en termes de mémoire et de temps
mots = ["Python", "est", "un", "langage", "puissant"]
phrase = ""
for mot in mots:
    phrase += mot + " "
```

À chaque itération, une nouvelle chaîne est allouée et l'ancienne est abandonnée. Pour 10 mots, c'est anecdotique. Pour 100 000 éléments, c'est un goulot d'étranglement réel.

La solution idiomatique est `str.join()`, qui construit la chaîne finale en une seule passe :

```python
# Bonne pratique — O(n)
mots = ["Python", "est", "un", "langage", "puissant"]
phrase = " ".join(mots)
print(phrase)  # "Python est un langage puissant"
```

Pour les chaînes dynamiques avec des variables, préférez les **f-strings** introduites en Python 3.6. Elles sont lisibles, rapides, et supportent des expressions arbitraires :

```python
nom = "Alice"
age = 30

# Ancienne façon
message = "Bonjour, " + nom + ". Tu as " + str(age) + " ans."

# Avec format()
message = "Bonjour, {}. Tu as {} ans.".format(nom, age)

# Avec f-string (recommandé)
message = f"Bonjour, {nom}. Tu as {age} ans."
print(message)  # "Bonjour, Alice. Tu as 30 ans."
```

Les f-strings permettent également d'insérer des expressions directement :

```python
prix = 49.99
tva = 0.20
print(f"Prix TTC : {prix * (1 + tva):.2f} €")  # "Prix TTC : 59.99 €"
```

## 7. Modifier une liste pendant son itération

Modifier une liste (ou un dictionnaire) pendant qu'on l'itère est une erreur classique qui produit des comportements imprévisibles : des éléments sautés, des index décalés, ou des boucles qui ne se terminent pas comme prévu.

```python
# Comportement imprévisible
nombres = [1, 2, 3, 4, 5, 6]
for n in nombres:
    if n % 2 == 0:
        nombres.remove(n)

print(nombres)  # [1, 3, 5] ? Pas toujours...
```

Dans cet exemple, quand `2` est supprimé, les indices se décalent et `3` est sauté lors de l'itération suivante. Le résultat peut varier selon la version de Python et la structure exacte des données.

La solution la plus simple et la plus lisible est d'itérer sur une copie de la liste :

```python
nombres = [1, 2, 3, 4, 5, 6]
for n in nombres[:]:      # [:] crée une copie superficielle
    if n % 2 == 0:
        nombres.remove(n)

print(nombres)  # [1, 3, 5]
```

Encore mieux, utilisez une list comprehension pour construire une nouvelle liste filtrée plutôt que de modifier l'originale :

```python
nombres = [1, 2, 3, 4, 5, 6]
nombres = [n for n in nombres if n % 2 != 0]
print(nombres)  # [1, 3, 5]
```

Pour les dictionnaires, le problème est similaire. En Python 3, itérer sur un dictionnaire tout en le modifiant lève une `RuntimeError` explicite. La solution est la même : itérer sur une copie des clés :

```python
config = {"debug": True, "verbose": False, "timeout": 30}

for cle in list(config.keys()):
    if config[cle] is False:
        del config[cle]

print(config)  # {"debug": True, "timeout": 30}
```

## 8. Négliger les list comprehensions et les générateurs

Python met à disposition des outils très puissants pour transformer et filtrer des collections de façon concise et efficace. Les débutants ont souvent le réflexe d'écrire des boucles `for` explicites là où une comprehension serait plus claire et plus rapide.

Comparons les deux approches :

```python
# Style impératif
carres = []
for n in range(10):
    if n % 2 == 0:
        carres.append(n ** 2)

# List comprehension — une ligne, plus lisible
carres = [n ** 2 for n in range(10) if n % 2 == 0]

print(carres)  # [0, 4, 16, 36, 64]
```

Les comprehensions existent aussi pour les dictionnaires et les sets :

```python
# Dict comprehension
mots = ["chat", "chien", "lapin"]
longueurs = {mot: len(mot) for mot in mots}
# {"chat": 4, "chien": 5, "lapin": 5}

# Set comprehension (élimine les doublons automatiquement)
lettres = {lettre for lettre in "abracadabra"}
# {"a", "b", "c", "d", "r"}
```

Quand vous travaillez avec de très grandes collections et que vous n'avez pas besoin de stocker tous les résultats en mémoire simultanément, préférez les **expressions génératrices**. Contrairement aux list comprehensions, elles produisent les valeurs à la demande (lazy evaluation) :

```python
# List comprehension — alloue toute la liste en mémoire
somme = sum([n ** 2 for n in range(1_000_000)])

# Expression génératrice — n'alloue qu'un élément à la fois
somme = sum(n ** 2 for n in range(1_000_000))
```

La syntaxe est identique, à l'exception des crochets remplacés par de simples parenthèses (ou absents quand le générateur est le seul argument d'une fonction).

Pour des pipelines de transformation plus complexes, explorez aussi le module `itertools` de la bibliothèque standard, qui offre des générateurs optimisés pour des cas d'usage courants.

## 9. Confondre les copies superficielles et profondes

Nous avons abordé la copie dans la première erreur, mais le sujet mérite un traitement plus approfondi. Il existe en Python deux types de copies pour les objets mutables : la **copie superficielle** (shallow copy) et la **copie profonde** (deep copy), et les confondre peut conduire à des bugs très subtils.

Une copie superficielle crée un nouvel objet de premier niveau, mais les éléments imbriqués continuent de pointer vers les mêmes références :

```python
import copy

original = [[1, 2], [3, 4], [5, 6]]
superficielle = original.copy()   # ou list(original) ou original[:]

superficielle[0].append(99)

print(original)      # [[1, 2, 99], [3, 4], [5, 6]]  ← modifié !
print(superficielle) # [[1, 2, 99], [3, 4], [5, 6]]
```

Même si `superficielle` est un objet distinct d'`original`, les sous-listes qu'il contient sont partagées. Modifier `superficielle[0]` modifie donc aussi `original[0]`.

Pour éviter ce problème, utilisez `copy.deepcopy()`, qui copie récursivement tous les niveaux d'imbrication :

```python
import copy

original = [[1, 2], [3, 4], [5, 6]]
profonde = copy.deepcopy(original)

profonde[0].append(99)

print(original)  # [[1, 2], [3, 4], [5, 6]]  ← intact
print(profonde)  # [[1, 2, 99], [3, 4], [5, 6]]
```

Le choix entre les deux dépend du cas d'usage. La copie superficielle est plus rapide et suffisante pour les structures plates ou lorsque vous souhaitez délibérément partager les objets imbriqués. La copie profonde est nécessaire dès que vos structures contiennent des objets mutables imbriqués et que vous voulez une indépendance totale.

## 10. Écrire du code non idiomatique (non-Pythonic)

Python possède une philosophie interne résumée par le "Zen of Python" (accessible via `import this`). Écrire du code "Pythonic", c'est tirer parti des constructions propres au langage plutôt que de transposer mécaniquement des habitudes venues d'autres langages comme Java ou C.

Voici quelques exemples de transformations courantes vers un style plus idiomatique.

**Échanger deux variables sans variable temporaire :**

```python
# Style C/Java
temp = a
a = b
b = temp

# Style Python
a, b = b, a
```

**Itérer avec l'index et la valeur simultanément :**

```python
fruits = ["pomme", "banane", "cerise"]

# Non idiomatique
for i in range(len(fruits)):
    print(i, fruits[i])

# Idiomatique
for i, fruit in enumerate(fruits):
    print(i, fruit)
```

**Vérifier l'appartenance à une collection :**

```python
autorisés = ["admin", "moderateur", "editeur"]

# Non idiomatique
if role == "admin" or role == "moderateur" or role == "editeur":
    accorder_acces()

# Idiomatique
if role in autorisés:
    accorder_acces()
```

**Retourner des valeurs multiples depuis une fonction :**

```python
# Non idiomatique (simuler un objet de retour)
def min_max(nombres):
    return {"min": min(nombres), "max": max(nombres)}

resultat = min_max([3, 1, 4, 1, 5])
print(resultat["min"])

# Idiomatique (tuple unpacking)
def min_max(nombres):
    return min(nombres), max(nombres)

mini, maxi = min_max([3, 1, 4, 1, 5])
print(mini, maxi)
```

**Utiliser les gestionnaires de contexte pour les ressources :**

```python
# Non idiomatique — risque de ne jamais fermer le fichier si une exception survient
fichier = open("données.txt", "r")
contenu = fichier.read()
fichier.close()

# Idiomatique — le fichier est toujours fermé, même en cas d'erreur
with open("données.txt", "r") as fichier:
    contenu = fichier.read()
```

Le gestionnaire de contexte `with` est l'un des outils les plus puissants et sous-utilisés par les débutants. Il s'applique aux fichiers, aux connexions réseau, aux verrous de threading, et à toute classe qui implémente les méthodes `__enter__` et `__exit__`.

## En résumé

Ces dix erreurs ne sont pas le signe d'un manque de talent, mais simplement le résultat d'un apprentissage en cours. Python est un langage qui récompense ceux qui prennent le temps de comprendre ses mécanismes fondamentaux plutôt que de se contenter de faire "fonctionner" le code.

Garder ces points en tête au quotidien — la mutabilité, la portée, les exceptions, les copies, l'idiomatisme — vous permettra non seulement d'écrire du code plus correct, mais aussi du code plus lisible, plus maintenable, et plus performant.

La prochaine étape ? Lire le PEP 8 (guide de style officiel), explorer le module `collections` de la bibliothèque standard, et s'entraîner à écrire du code en pensant "comment Python résoudrait ce problème" plutôt que "comment je le ferais dans un autre langage".
