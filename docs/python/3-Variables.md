# Les Variables

## Introduction

Une **variable** en Python est comme une boîte dans laquelle on stocke une valeur. Cette boîte possède un nom 
(l'identifiant de la variable) et contient une donnée (un nombre, du texte, etc.).

**Analogie** : Imaginez une variable comme un tiroir étiqueté. 
L'étiquette est le nom de la variable, et ce qu'il y a dans le tiroir est sa valeur.


## Créer une variable

Pour créer une variable, on utilise l'opérateur d'affectation `=` :

```python
# Syntaxe : nom_variable = valeur

# Exemple : créer une variable qui contient un nombre entier
x = 10

# Exemple : créer une variable qui contient du texte
y = "hello"

# Exemple : créer une variable qui contient un nombre décimal
z = 3.14
```

### Points importants

- **Pas besoin de déclaration** : En Python, on n'a pas besoin de déclarer le type de la variable avant de l'utiliser
- **Affectation dynamique** : Une variable peut changer de valeur et même de type au cours du programme

```python
# Une variable peut changer de valeur
age = 25
print(age)  # Affiche : 25

age = 26    # On change la valeur
print(age)  # Affiche : 26

# Une variable peut même changer de type !
valeur = 100        # valeur contient un nombre
valeur = "texte"    # maintenant valeur contient du texte
```

## Règles de nommage

Il existe des règles **obligatoires** et des conventions **recommandées** pour nommer vos variables.

### Règles obligatoires

| Règle | Correct | Incorrect | Explication |
|-------|---------|-----------|-------------|
| Ne pas commencer par un chiffre | `variable1`, `mon_age` | `1variable`, `9nom` | Doit commencer par une lettre ou `_` |
| Pas de caractères spéciaux | `mon_nom`, `prix_total` | `mon-nom`, `prix$`, `total!` | Seuls les lettres, chiffres et `_` sont autorisés |
| Pas de mots-clés Python | `ma_liste`, `mon_if` | `if`, `for`, `while`, `def` | Éviter les mots réservés de Python |

### Conventions recommandées (PEP 8)

- **Utiliser des minuscules** : `ma_variable` plutôt que `MaVariable`
- **Séparer les mots avec des underscores** : `prix_total` plutôt que `prixtotal`
- **Noms descriptifs** : `age_utilisateur` plutôt que `x`

```python
# Bonnes pratiques
prenom_utilisateur = "Alice"
age_en_annees = 30
prix_total_ttc = 99.99

# À éviter (mais techniquement valide)
x = "Issa"
a = 30
p = 99.99
```

### Exemples de noms

```python
# Noms valides et recommandés
compteur = 0
nom_complet = "Ousmane Sane"
prix_unitaire = 15.50
est_connecte = True
_variable_privee = "secret"

# Noms valides mais non recommandés
X = 10              # majuscule (convention pour les constantes)
monNom = "Marie"    # camelCase (utilisé en Java, pas en Python)
a = 5               # trop court, pas descriptif

# Noms invalides (causent des erreurs)
# 1nom = "test"     # commence par un chiffre
# mon-nom = "test"  # contient un tiret
# for = 10          # mot-clé Python
```

## Types de variables

Python est un langage à **typage dynamique** : le type est déterminé automatiquement selon la valeur assignée.

### Les types de base

| Type | Description | Exemple | Nom en anglais |
|------|-------------|---------|----------------|
| `int` | Nombre entier | `42`, `-10`, `0` | Integer |
| `float` | Nombre décimal | `3.14`, `-0.5`, `2.0` | Float |
| `str` | Chaîne de caractères (texte) | `"Bonjour"`, `'Python'` | String |
| `bool` | Booléen (Vrai/Faux) | `True`, `False` | Boolean |

### Vérifier le type : `type()`

La fonction `type()` permet de connaître le type d'une variable :

```python
# Créer différentes variables
x = 10
y = "hello"
z = 3.14
est_actif = True

# Vérifier leur type
print(type(x))         # Affiche : <class 'int'>
print(type(y))         # Affiche : <class 'str'>
print(type(z))         # Affiche : <class 'float'>
print(type(est_actif)) # Affiche : <class 'bool'>
```

### Exemple détaillé

```python
# Nombres entiers (int)
age = 25
temperature = -5
population = 1000000

print(f"age est de type : {type(age)}")  # <class 'int'>

# Nombres décimaux (float)
prix = 19.99
taille = 1.75
pi = 3.14159

print(f"prix est de type : {type(prix)}")  # <class 'float'>

# Chaînes de caractères (str)
nom = "Ousmane"
message = 'Bonjour le monde!'
phrase = """Ceci est un texte
sur plusieurs lignes"""

print(f"nom est de type : {type(nom)}")  # <class 'str'>

# Booléens (bool)
est_majeur = True
a_permis = False

print(f"est_majeur est de type : {type(est_majeur)}")  # <class 'bool'>
```

## Conversion de types

On peut transformer une variable d'un type à un autre avec les fonctions de conversion.

### Fonctions de conversion

| Fonction | Description | Exemple |
|----------|-------------|---------|
| `int()` | Convertit en nombre entier | `int("42")` → `42` |
| `float()` | Convertit en nombre décimal | `float("3.14")` → `3.14` |
| `str()` | Convertit en texte | `str(42)` → `"42"` |
| `bool()` | Convertit en booléen | `bool(1)` → `True` |

### Exemples pratiques

```python
# Conversion de chaîne vers nombre
age_texte = "25"
age_nombre = int(age_texte)
print(age_nombre + 5)  # Affiche : 30

# Conversion de nombre vers chaîne
nombre = 42
texte = str(nombre)
print("Le nombre est : " + texte)  # Affiche : Le nombre est : 42

# Conversion vers float
x = "3.14"
y = 10
resultat1 = float(x)    # "3.14" → 3.14
resultat2 = float(y)    # 10 → 10.0

print(resultat1)  # Affiche : 3.14
print(resultat2)  # Affiche : 10.0

# Conversion vers int (attention à la perte de décimales)
prix = 19.99
prix_entier = int(prix)
print(prix_entier)  # Affiche : 19 (la partie décimale est supprimée)
```

### Erreurs courantes

```python
# Conversion impossible
# age = int("vingt-cinq")  # ValueError: invalid literal for int()

# Perte de données
prix = 19.99
prix_entier = int(prix)  # 19 (on perd les centimes !)

# Solution : utiliser round() pour arrondir d'abord
prix = 19.99
prix_arrondi = int(round(prix))  # 20
```

### Exemple complet de conversion

```python
# Simuler une saisie utilisateur (en texte)
age_saisi = "28"
taille_saisie = "1.75"

# Convertir en nombres pour faire des calculs
age = int(age_saisi)
taille = float(taille_saisie)

# Faire des calculs
age_futur = age + 10
taille_cm = taille * 100

# Reconvertir en texte pour l'affichage
print("Dans 10 ans, j'aurai " + str(age_futur) + " ans")
print("Ma taille est de " + str(taille_cm) + " cm")
```

## Exercices pratiques

### Exercice 1 : Découverte des types

**Objectif** : Créer différentes variables et afficher leur type.

```python
# Créez trois variables
x = 5           # nombre entier
y = 3.14        # nombre décimal
z = "Bonjour"   # texte

# Affichez le type de chaque variable
print("Type de x :", type(x))  # <class 'int'>
print("Type de y :", type(y))  # <class 'float'>
print("Type de z :", type(z))  # <class 'str'>
```

**Résultat attendu :**
```
Type de x : <class 'int'>
Type de y : <class 'float'>
Type de z : <class 'str'>
```

### Exercice 2 : Présentation personnelle

**Objectif** : Créer des variables et les combiner dans un message.

```python
# Créez vos variables personnelles
name = "Karim"  # Remplacez par votre nom
age = 25        # Remplacez par votre âge

# Méthode 1 : Concaténation (assembler des textes)
message1 = "Bonjour, je m'appelle " + name + " et j'ai " + str(age) + " ans"
print(message1)

# Méthode 2 : f-string (plus moderne et lisible)
message2 = f"Bonjour, je m'appelle {name} et j'ai {age} ans"
print(message2)

# Méthode 3 : format()
message3 = "Bonjour, je m'appelle {} et j'ai {} ans".format(name, age)
print(message3)
```

**Résultat attendu :**
```
Bonjour, je m'appelle Karim et j'ai 25 ans
Bonjour, je m'appelle Karim et j'ai 25 ans
Bonjour, je m'appelle Karim et j'ai 25 ans
```

**Astuce** : Les f-strings (méthode 2) sont la façon la plus moderne et recommandée en Python.

### Exercice 3 : Calculs simples

**Objectif** : Effectuer des opérations mathématiques avec des variables.

```python
# Créez deux variables
a = 5
b = 10

# Créez une variable c qui contient la somme
c = a + b

# Affichez le résultat
print("La somme de", a, "et", b, "est :", c)

# Ou avec f-string
print(f"La somme de {a} et {b} est : {c}")
```

**Résultat attendu :**
```
La somme de 5 et 10 est : 15
```

**Bonus : Autres opérations**

```python
a = 5
b = 10

# Addition
somme = a + b
print(f"Addition : {a} + {b} = {somme}")

# Soustraction
difference = b - a
print(f"Soustraction : {b} - {a} = {difference}")

# Multiplication
produit = a * b
print(f"Multiplication : {a} × {b} = {produit}")

# Division
quotient = b / a
print(f"Division : {b} ÷ {a} = {quotient}")

# Division entière (sans décimales)
div_entiere = b // a
print(f"Division entière : {b} // {a} = {div_entiere}")

# Modulo (reste de la division)
reste = b % a
print(f"Modulo : {b} % {a} = {reste}")

# Puissance
puissance = a ** 2
print(f"Puissance : {a}² = {puissance}")
```

## Résumé des concepts clés

| Concept | Description | Exemple |
|---------|-------------|---------|
| **Création** | `nom = valeur` | `age = 25` |
| **Type** | Vérifié avec `type()` | `type(age)` → `<class 'int'>` |
| **Conversion** | `int()`, `float()`, `str()` | `int("10")` → `10` |
| **Nommage** | Minuscules + underscores | `mon_age`, `prix_total` |

## Documentation officielle Python sur les variables

Pour approfondir vos connaissances sur les variables, consultez la documentation officielle de Python :

Variables - Concepts de base

- [Introduction informelle à Python - Variables :octicons-link-external-16:](https://docs.python.org/fr/3/tutorial/introduction.html#first-steps-towards-programming){:target="_blank"}
- [Assignment statements (affectation) :octicons-link-external-16:](https://docs.python.org/fr/3/reference/simple_stmts.html#assignment-statements){:target="_blank"}
- [Naming and binding (nommage et liaison) :octicons-link-external-16:](https://docs.python.org/fr/3/reference/executionmodel.html#naming-and-binding){:target="_blank"}



