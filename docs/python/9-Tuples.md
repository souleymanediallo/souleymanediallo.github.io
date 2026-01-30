# Les Tuples

## 1. Définition et Concepts Fondamentaux

### 1.1 Qu'est-ce qu'un Tuple ?

Un **tuple** est une structure de données séquentielle **immuable** en Python. L'immuabilité signifie qu'une fois créé, 
un tuple ne peut être ni modifié, ni étendu, ni réduit. Cette caractéristique le distingue fondamentalement des listes, 
qui sont mutables.

**Syntaxe de base :**
```python
# Création d'un tuple avec des parenthèses
mon_tuple = (1, 2, 3, 4, 5)

# Création d'un tuple sans parenthèses (par juxtaposition)
mon_tuple_alt = 1, 2, 3, 4, 5

# Tuple vide
tuple_vide = ()

# Tuple à un seul élément (la virgule est obligatoire)
tuple_simple = (42,)  # Correct
pas_un_tuple = (42)   # Incorrect - c'est juste un entier entre parenthèses
```

### 1.2 Pourquoi Utiliser les Tuples ?

Les tuples offrent plusieurs avantages :

- **Intégrité des données** : Protection contre les modifications accidentelles
- **Performance** : Plus rapides et moins gourmands en mémoire que les listes
- **Hashabilité** : Peuvent servir de clés dans les dictionnaires (contrairement aux listes)
- **Sémantique** : Indiquent clairement l'intention de garder des données constantes
- **Unpacking** : Facilitent l'assignation multiple de variables

## 2. Création et Initialisation des Tuples

### 2.1 Différentes Méthodes de Création

```python
# Méthode 1 : Avec parenthèses
coordinates = (4, 5)

# Méthode 2 : Sans parenthèses (packing de tuple)
dimensions = 1920, 1080

# Méthode 3 : Avec le constructeur tuple()
liste_nombres = [1, 2, 3, 4]
tuple_nombres = tuple(liste_nombres)
print(tuple_nombres)  # Output: (1, 2, 3, 4)

# Méthode 4 : À partir d'une chaîne
tuple_lettres = tuple("Python")
print(tuple_lettres)  # Output: ('P', 'y', 't', 'h', 'o', 'n')

# Méthode 5 : Tuple imbriqué
tuple_complexe = (1, (2, 3), (4, (5, 6)))
```

### 2.2 Tuples Hétérogènes

Les tuples peuvent contenir des éléments de types différents, ce qui les rend très flexibles :

```python
# Tuple mixte avec différents types de données
personne = ("Mariam", 30, 1.65, True, ["Python", "Java"])
#          (str,    int, float, bool, list)

# Exemple pratique : informations d'un employé
employe = (
    "E12345",                    # ID
    "Souleymane Diallo",         # Nom
    "Développeur",               # Poste
    55000,                       # Salaire
    (2020, 3, 15)                # Date d'embauche (tuple imbriqué)
)
```

---

## 3. Accès aux Éléments

### 3.1 Indexation Positive

Python utilise une **indexation base zéro**, où le premier élément a l'index 0 :

```python
coordinates = (10, 20, 30, 40, 50)

# Accès par index
print(coordinates[0])   # Output: 10 (premier élément)
print(coordinates[1])   # Output: 20 (deuxième élément)
print(coordinates[4])   # Output: 50 (cinquième/dernier élément)

# Utilisation dans des calculs
x, y = (4, 5)
distance = (x**2 + y**2) ** 0.5
print(f"Distance: {distance}")  # Output: Distance: 6.4031242374328485
```

### 3.2 Indexation Négative

Les indices négatifs permettent d'accéder aux éléments depuis la fin du tuple :

```python
coordinates = (10, 20, 30, 40, 50)

print(coordinates[-1])   # Output: 50 (dernier élément)
print(coordinates[-2])   # Output: 40 (avant-dernier élément)
print(coordinates[-5])   # Output: 10 (premier élément, équivalent à [0])

# Exemple pratique : récupération du dernier élément
historique_prix = (100, 105, 103, 108, 110)
prix_actuel = historique_prix[-1]
prix_precedent = historique_prix[-2]
variation = prix_actuel - prix_precedent
print(f"Variation: {variation}€")  # Output: Variation: 2€
```

### 3.3 Slicing (Découpage)

Le slicing permet d'extraire des sous-tuples :

```python
nombres = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)

# Syntaxe : tuple[start:stop:step]
print(nombres[2:5])      # Output: (2, 3, 4) - éléments d'index 2 à 4
print(nombres[:3])       # Output: (0, 1, 2) - du début jusqu'à l'index 2
print(nombres[7:])       # Output: (7, 8, 9) - de l'index 7 jusqu'à la fin
print(nombres[::2])      # Output: (0, 2, 4, 6, 8) - un élément sur deux
print(nombres[::-1])     # Output: (9, 8, 7, 6, 5, 4, 3, 2, 1, 0) - inversion

# Exemple pratique : extraction de données
jours_semaine = ("Lundi", "Mardi", "Mercredi", "Jeudi", "Vendredi", "Samedi", "Dimanche")
jours_travail = jours_semaine[:5]
weekend = jours_semaine[-2:]
print(jours_travail)  # Output: ('Lundi', 'Mardi', 'Mercredi', 'Jeudi', 'Vendredi')
print(weekend)        # Output: ('Samedi', 'Dimanche')
```

## 4. Immuabilité : Concept Clé

### 4.1 Qu'est-ce que l'Immuabilité ?

L'immuabilité signifie qu'un objet ne peut pas être modifié après sa création. Pour les tuples, cela implique :

- Impossibilité de changer la valeur d'un élément
- Impossibilité d'ajouter ou de supprimer des éléments
- Impossibilité de modifier la structure du tuple

```python
coordinates = (4, 5)

# Tentatives de modification (toutes génèrent des erreurs)
try:
    coordinates[0] = 10
except TypeError as e:
    print(f"Erreur: {e}")
    # Output: Erreur: 'tuple' object does not support item assignment

try:
    coordinates.append(6)
except AttributeError as e:
    print(f"Erreur: {e}")
    # Output: Erreur: 'tuple' object has no attribute 'append'

try:
    del coordinates[0]
except TypeError as e:
    print(f"Erreur: {e}")
    # Output: Erreur: 'tuple' object doesn't support item deletion
```

### 4.2 Immuabilité Superficielle

**Important** : L'immuabilité des tuples est superficielle. Si un tuple contient des objets mutables (comme des listes), 
ces objets peuvent être modifiés :

```python
# Tuple contenant une liste
tuple_avec_liste = (1, 2, [3, 4, 5])

# Le tuple lui-même ne peut pas être modifié
# Mais la liste à l'intérieur peut l'être
tuple_avec_liste[2].append(6)
print(tuple_avec_liste)  # Output: (1, 2, [3, 4, 5, 6])

# Exemple pratique : configuration avec paramètres modifiables
configuration = (
    "MonApp",                    # Nom (immuable)
    "1.0.0",                     # Version (immuable)
    {"debug": True, "port": 8080}  # Options (dictionnaire modifiable)
)

# Modification des options
configuration[2]["port"] = 9000
print(configuration)
# Output: ('MonApp', '1.0.0', {'debug': True, 'port': 9000})
```

### 4.3 Création d'un Nouveau Tuple (Workaround)

Si vous devez "modifier" un tuple, vous devez en créer un nouveau :

```python
original = (1, 2, 3, 4)

# Méthode 1 : Concaténation
nouveau = original + (5, 6)
print(nouveau)  # Output: (1, 2, 3, 4, 5, 6)

# Méthode 2 : Conversion en liste, modification, reconversion
liste_temp = list(original)
liste_temp[0] = 10
modifie = tuple(liste_temp)
print(modifie)  # Output: (10, 2, 3, 4)

# Méthode 3 : Slicing et concaténation
remplace = original[:1] + (99,) + original[2:]
print(remplace)  # Output: (1, 99, 3, 4)
```

## 5. Opérations sur les Tuples

### 5.1 Opérations de Base

```python
tuple1 = (1, 2, 3)
tuple2 = (4, 5, 6)

# Concaténation
resultat = tuple1 + tuple2
print(resultat)  # Output: (1, 2, 3, 4, 5, 6)

# Répétition
repete = tuple1 * 3
print(repete)  # Output: (1, 2, 3, 1, 2, 3, 1, 2, 3)

# Appartenance (membership)
print(2 in tuple1)      # Output: True
print(10 not in tuple1) # Output: True

# Longueur
print(len(tuple1))  # Output: 3

# Minimum et maximum (pour les tuples homogènes)
nombres = (5, 2, 8, 1, 9)
print(min(nombres))  # Output: 1
print(max(nombres))  # Output: 9
print(sum(nombres))  # Output: 25
```

### 5.2 Méthodes des Tuples

Les tuples ont seulement deux méthodes intégrées :

```python
valeurs = (1, 2, 3, 2, 4, 2, 5)

# count() : compte le nombre d'occurrences d'un élément
nombre_de_2 = valeurs.count(2)
print(nombre_de_2)  # Output: 3

# index() : retourne l'index de la première occurrence
position = valeurs.index(4)
print(position)  # Output: 4

# index() avec plage de recherche
# Syntaxe : tuple.index(valeur, debut, fin)
position_2 = valeurs.index(2, 2, 6)  # Cherche 2 entre les index 2 et 6
print(position_2)  # Output: 3

# Gestion d'erreur si l'élément n'existe pas
try:
    valeurs.index(10)
except ValueError as e:
    print(f"Erreur: {e}")
    # Output: Erreur: tuple.index(x): x not in tuple
```

## 6. Unpacking (Déballage) de Tuples

### 6.1 Unpacking Simple

```python
# Assignation multiple
coordinates = (10, 20)
x, y = coordinates
print(f"x={x}, y={y}")  # Output: x=10, y=20

# Unpacking direct
nom, age, ville = ("Karim", 25, "Paris")
print(f"{nom} a {age} ans et habite à {ville}")
# Output: Karim a 25 ans et habite à Paris

# Échange de valeurs (swap)
a, b = 5, 10
a, b = b, a  # Élégant et pythonique
print(f"a={a}, b={b}")  # Output: a=10, b=5
```

### 6.2 Unpacking avec l'Opérateur *

L'opérateur `*` permet de capturer plusieurs éléments :

```python
# Capturer le reste des éléments
nombres = (1, 2, 3, 4, 5, 6)
premier, *milieu, dernier = nombres
print(f"Premier: {premier}")    # Output: Premier: 1
print(f"Milieu: {milieu}")      # Output: Milieu: [2, 3, 4, 5]
print(f"Dernier: {dernier}")    # Output: Dernier: 6

# Ignorer des éléments avec _
personne = ("Ousmane", 30, "Ingénieur", "Lyon", "France")
nom, _, profession, *_ = personne
print(f"{nom} est {profession}")  # Output: Ousmane est Ingénieur

# Exemple pratique : traitement de données
resultat_match = ("Paris SG", "Lyon", 3, 1, "Parc des Princes")
equipe1, equipe2, *scores, lieu = resultat_match
print(f"{equipe1} {scores[0]} - {scores[1]} {equipe2} au {lieu}")
# Output: Paris SG 3 - 1 Lyon au Parc des Princes
```

### 6.3 Unpacking dans les Boucles

```python
# Iteration sur une liste de tuples
employes = [
    ("Karim", "Dev", 55000),
    ("Ousmane", "Designer", 50000),
    ("Antoine", "Manager", 65000)
]

for nom, poste, salaire in employes:
    print(f"{nom} - {poste}: {salaire}€")

# Output:
# Karim - Dev: 55000€
# Ousmane - Designer: 50000€
# Antoine - Manager: 65000€

# Avec enumerate()
fruits = ("pomme", "banane", "orange")
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# Output:
# 0: pomme
# 1: banane
# 2: orange
```

## 7. Cas d'Usage Pratiques

### 7.1 Retour de Plusieurs Valeurs

```python
def calculer_statistiques(nombres):
    """Retourne min, max, moyenne sous forme de tuple"""
    minimum = min(nombres)
    maximum = max(nombres)
    moyenne = sum(nombres) / len(nombres)
    return minimum, maximum, moyenne  # Retourne un tuple

# Utilisation
valeurs = [23, 45, 12, 67, 89, 34]
min_val, max_val, moy_val = calculer_statistiques(valeurs)
print(f"Min: {min_val}, Max: {max_val}, Moyenne: {moy_val:.2f}")
# Output: Min: 12, Max: 89, Moyenne: 45.00
```

### 7.2 Tuples comme Clés de Dictionnaire

```python
# Matrice d'adjacence avec des coordonnées comme clés
distances_villes = {
    ("Paris", "Lyon"): 465,
    ("Paris", "Marseille"): 775,
    ("Lyon", "Marseille"): 315,
    ("Lyon", "Bordeaux"): 540
}

# Accès aux valeurs
print(distances_villes[("Paris", "Lyon")])  # Output: 465

# Exemple : système de coordonnées
grille = {
    (0, 0): "Départ",
    (1, 0): "Mur",
    (2, 0): "Vide",
    (2, 1): "Trésor",
    (3, 3): "Sortie"
}

position_joueur = (2, 1)
print(f"Le joueur est sur: {grille[position_joueur]}")
# Output: Le joueur est sur: Trésor
```

### 7.3 Données Constantes et Configuration

```python
# Constantes mathématiques
POINT_ORIGINE = (0, 0)
COULEURS_PRIMAIRES = ("Rouge", "Vert", "Bleu")
JOURS_MOIS = (31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31)

# Configuration d'application
CONFIG_SERVEUR = (
    "localhost",      # host
    8080,            # port
    False,           # debug
    60               # timeout
)

def demarrer_serveur(config):
    host, port, debug, timeout = config
    print(f"Serveur démarré sur {host}:{port}")
    print(f"Mode debug: {debug}, Timeout: {timeout}s")

demarrer_serveur(CONFIG_SERVEUR)
```

### 7.4 Tuples Nommés (namedtuple)

Pour plus de lisibilité, Python offre `namedtuple` :

```python
from collections import namedtuple

# Définition d'un tuple nommé
Point = namedtuple('Point', ['x', 'y'])
Personne = namedtuple('Personne', ['nom', 'age', 'ville'])

# Création d'instances
p1 = Point(10, 20)
p2 = Point(x=30, y=40)

# Accès par nom (plus lisible)
print(f"Coordonnées: x={p1.x}, y={p1.y}")  # Output: Coordonnées: x=10, y=20

# Toujours accessible par index
print(p1[0], p1[1])  # Output: 10 20

# Exemple pratique
alice = Personne("Alice", 28, "Paris")
print(f"{alice.nom} a {alice.age} ans")  # Output: Alice a 28 ans

# Conversion en dictionnaire
print(alice._asdict())
# Output: {'nom': 'Alice', 'age': 28, 'ville': 'Paris'}
```

## 8. Comparaison Tuples vs Listes

| Caractéristique | Tuple | Liste |
|-----------------|-------|-------|
| **Mutabilité** | Immuable | Mutable |
| **Syntaxe** | `()` | `[]` |
| **Performance** | Plus rapide | Plus lente |
| **Mémoire** | Moins gourmande | Plus gourmande |
| **Méthodes** | 2 (count, index) | Nombreuses (append, remove, etc.) |
| **Usage** | Données constantes | Données modifiables |
| **Hashable** | Oui (si contenu hashable) | Non |
| **Clé dict** | Oui | Non |

```python
import sys

# Comparaison mémoire
tuple_data = (1, 2, 3, 4, 5)
list_data = [1, 2, 3, 4, 5]

print(f"Taille tuple: {sys.getsizeof(tuple_data)} octets")
print(f"Taille liste: {sys.getsizeof(list_data)} octets")
# Output typique:
# Taille tuple: 64 octets
# Taille liste: 88 octets

# Comparaison performance
import timeit

temps_tuple = timeit.timeit('x = (1, 2, 3, 4, 5)', number=1000000)
temps_liste = timeit.timeit('x = [1, 2, 3, 4, 5]', number=1000000)

print(f"Création tuple: {temps_tuple:.4f}s")
print(f"Création liste: {temps_liste:.4f}s")
```

## 9. Bonnes Pratiques

### 9.1 Quand Utiliser les Tuples

**Utilisez les tuples pour :**

- Données qui ne doivent jamais changer (coordonnées, dates, configurations)
- Retourner plusieurs valeurs d'une fonction
- Clés de dictionnaires
- Garantir l'intégrité des données
- Optimiser les performances

**Évitez les tuples pour :**

- Collections devant être modifiées fréquemment
- Données devant croître ou diminuer dynamiquement

### 9.2 Conventions de Nommage

```python
# Bon : noms explicites
coordonnees_gps = (48.8566, 2.3522)
rgb_couleur = (255, 128, 0)

# Moins bon : noms vagues
data = (48.8566, 2.3522)
values = (255, 128, 0)

# Constantes globales : majuscules
CONFIGURATION_DEFAUT = ("localhost", 8080, False)
DIMENSIONS_ECRAN = (1920, 1080)
```

### 9.3 Documentation

```python
def obtenir_informations_utilisateur(user_id: int) -> tuple[str, int, str]:
    """
    Récupère les informations d'un utilisateur.
    
    Args:
        user_id: L'identifiant unique de l'utilisateur
        
    Returns:
        Un tuple contenant (nom, age, email) de l'utilisateur
        
    Example:
        >>> obtenir_informations_utilisateur(123)
        ('Alice Dupont', 30, 'alice@example.com')
    """
    # Simulation de récupération de données
    return ("Alice Dupont", 30, "alice@example.com")
```

## 10. Exercices Pratiques

### Exercice 1 : Manipulation de Base

```python
# Créez un tuple contenant les 7 jours de la semaine
jours = ("Lundi", "Mardi", "Mercredi", "Jeudi", "Vendredi", "Samedi", "Dimanche")

# Affichez le troisième jour
print(jours[2])  # Mercredi

# Affichez les jours du weekend
print(jours[-2:])  # ('Samedi', 'Dimanche')

# Comptez combien de fois "Lundi" apparaît
print(jours.count("Lundi"))  # 1
```

### Exercice 2 : Fonctions avec Tuples

```python
def analyser_notes(notes):
    """
    Analyse un tuple de notes et retourne (moyenne, min, max)
    """
    moyenne = sum(notes) / len(notes)
    minimum = min(notes)
    maximum = max(notes)
    return moyenne, minimum, maximum

# Test
notes_eleve = (15, 12, 18, 14, 16)
moy, mini, maxi = analyser_notes(notes_eleve)
print(f"Moyenne: {moy}, Min: {mini}, Max: {maxi}")
```

### Exercice 3 : Tuples comme Clés

```python
# Créez un dictionnaire de température par coordonnées GPS
temperatures = {
    (48.8566, 2.3522): 15,   # Paris
    (43.2965, 5.3698): 22,   # Marseille
    (45.7640, 4.8357): 18    # Lyon
}

# Récupérez la température de Paris
paris_coords = (48.8566, 2.3522)
print(f"Température à Paris: {temperatures[paris_coords]}°C")
```

## 11. Pièges Courants et Solutions

### 11.1 Oublier la Virgule pour un Tuple à un Élément

```python
# INCORRECT
pas_tuple = (42)
print(type(pas_tuple))  # <class 'int'>

# CORRECT
vrai_tuple = (42,)
print(type(vrai_tuple))  # <class 'tuple'>
```

### 11.2 Confusion entre Immuabilité du Tuple et de son Contenu

```python
# Le tuple est immuable mais pas nécessairement son contenu
tuple_liste = ([1, 2], [3, 4])

# ERREUR : ne peut pas réassigner
# tuple_liste[0] = [5, 6]  # TypeError

# CORRECT : peut modifier le contenu mutable
tuple_liste[0].append(3)
print(tuple_liste)  # ([1, 2, 3], [3, 4])
```

### 11.3 Unpacking avec Mauvais Nombre de Variables

```python
coordonnees = (10, 20, 30)

# ERREUR : trop peu de variables
# x, y = coordonnees  # ValueError

# SOLUTIONS
x, y, z = coordonnees  # Correct
x, *reste = coordonnees  # x=10, reste=[20, 30]
```

## 12. Ressources Supplémentaires

### 12.1 Documentation Officielle

- [Python Tuples Documentation :octicons-link-external-16:](https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences){:target="_blank"}
- [Built-in Types - Tuple :octicons-link-external-16:](https://docs.python.org/3/library/stdtypes.html#tuple){:target="_blank"}
- [Collections - namedtuple :octicons-link-external-16:](https://docs.python.org/3/library/collections.html#collections.namedtuple){:target="_blank"}

### 12.2 Concepts Avancés

```python
# Tuples et compréhension (nécessite tuple())
carres = tuple(x**2 for x in range(5))
print(carres)  # (0, 1, 4, 9, 16)

# Tuples et fonctions d'ordre supérieur
nombres = (1, 2, 3, 4, 5)
pairs = tuple(filter(lambda x: x % 2 == 0, nombres))
print(pairs)  # (2, 4)

# Tuples et unpacking dans les paramètres
def afficher_coordonnees(x, y, z):
    print(f"x={x}, y={y}, z={z}")

coords = (10, 20, 30)
afficher_coordonnees(*coords)  # Unpacking avec *
```

## 13. Conclusion

Les tuples sont une structure de données fondamentale en Python qui offre immuabilité, performance et sécurité. 
Leur compréhension est essentielle pour écrire du code Python idiomatique et efficace. Utilisez-les judicieusement pour protéger vos données contre les modifications accidentelles et optimiser vos programmes.

### Points clés à retenir :

1. **Immuabilité** : Les tuples ne peuvent pas être modifiés après création
2. **Performance** : Plus rapides et moins gourmands en mémoire que les listes
3. **Hashabilité** : Peuvent servir de clés dans les dictionnaires
4. **Unpacking** : Facilitent l'assignation multiple et les échanges de valeurs
5. **Sémantique** : Indiquent clairement l'intention de conserver des données constantes

### Quand utiliser les tuples :

-  Données immuables (coordonnées, configurations, constantes)
-  Retour de multiples valeurs depuis une fonction
-  Clés de dictionnaires
-  Protection de l'intégrité des données
-  Optimisation des performances

### Quand préférer les listes :

-  Collections devant être modifiées fréquemment
-  Données avec taille variable
-  Besoin de méthodes de modification (append, remove, etc.)


