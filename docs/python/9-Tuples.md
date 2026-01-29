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
