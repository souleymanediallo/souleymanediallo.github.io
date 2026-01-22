# Erreurs et Exceptions en Python

En Python, les **erreurs** (ou **exceptions**) sont des événements qui se produisent pendant l'exécution d'un programme et qui interrompent son flux normal. Apprendre à les gérer est essentiel pour créer des programmes robustes.

### Pourquoi gérer les erreurs ?
- Éviter que le programme plante complètement
- Informer l'utilisateur de manière claire
- Déboguer plus facilement
- Créer des applications professionnelles

---

## Les types d'erreurs

### 1. Erreurs de syntaxe (Syntax Errors)

Ces erreurs surviennent **avant** l'exécution du programme. Python ne peut même pas démarrer votre code.

```python
# ❌ ERREUR : oubli des deux points
if x > 5
    print("Grand")

# ❌ ERREUR : parenthèse non fermée
print("Bonjour"

# ✅ CORRECT
if x > 5:
    print("Grand")
```

### 2. Erreurs d'exécution (Runtime Errors / Exceptions)

Ces erreurs surviennent **pendant** l'exécution du programme.

```python
# Cette ligne s'exécute sans problème
print("Début du programme")

# ❌ Ici, le programme plante (division par zéro)
resultat = 10 / 0

# Cette ligne ne sera jamais exécutée
print("Fin du programme")
```

**Sortie :**
```
Début du programme
Traceback (most recent call last):
  File "script.py", line 5, in <module>
    resultat = 10 / 0
ZeroDivisionError: division by zero
```

---

## Gestion des exceptions avec try-except

### La structure de base

La structure `try-except` permet d'intercepter les erreurs et de gérer proprement leur traitement.

```python
# Structure de base
try:
    # Code qui pourrait causer une erreur
    nombre = int(input("Entrez un nombre : "))
    resultat = 100 / nombre
    print(f"Résultat : {resultat}")
except:
    # Code exécuté si une erreur survient
    print("⚠️ Une erreur s'est produite !")
```

**Explication :**
- Le bloc `try` contient le code à surveiller
- Si une erreur survient, Python saute directement au bloc `except`
- Le programme continue après le bloc `except` au lieu de planter

### Capturer des exceptions spécifiques

Il est préférable de capturer des erreurs spécifiques plutôt que toutes les erreurs.

```python
try:
    age = int(input("Votre âge : "))
    print(f"Vous avez {age} ans")
except ValueError:
    # Cette erreur survient si l'utilisateur entre du texte au lieu d'un nombre
    print("❌ Veuillez entrer un nombre valide !")
```

**Exemple d'exécution :**
```
Votre âge : vingt
❌ Veuillez entrer un nombre valide !
```

### Plusieurs blocs except

Vous pouvez gérer différents types d'erreurs différemment.

```python
def diviser(a, b):
    try:
        resultat = a / b
        return resultat
    except ZeroDivisionError:
        # Gestion spécifique de la division par zéro
        print("❌ Erreur : Division par zéro impossible !")
        return None
    except TypeError:
        # Gestion des types incompatibles
        print("❌ Erreur : Les valeurs doivent être des nombres !")
        return None

# Tests
print(diviser(10, 2))      # ✅ 5.0
print(diviser(10, 0))      # ❌ Division par zéro
print(diviser(10, "abc"))  # ❌ TypeError
```

### Else et Finally

```python
def lire_fichier(nom_fichier):
    try:
        fichier = open(nom_fichier, 'r')
        contenu = fichier.read()
    except FileNotFoundError:
        print(f"❌ Le fichier '{nom_fichier}' n'existe pas")
    except PermissionError:
        print(f"❌ Pas de permission pour lire '{nom_fichier}'")
    else:
        # Exécuté SEULEMENT si aucune erreur ne survient
        print(f"✅ Fichier lu avec succès")
        print(f"Contenu : {contenu}")
    finally:
        # Exécuté TOUJOURS, qu'il y ait erreur ou non
        try:
            fichier.close()
            print("🔒 Fichier fermé")
        except:
            pass

# Test
lire_fichier("document.txt")
```

**Explication des blocs :**
- `try` : Code à surveiller
- `except` : Gestion des erreurs
- `else` : Exécuté si **aucune** erreur
- `finally` : Exécuté **toujours** (utile pour libérer des ressources)

---

## Les exceptions courantes

### 1. ValueError

Survient quand une fonction reçoit un argument du bon type mais avec une valeur inappropriée.

```python
# Exemple 1 : Conversion impossible
try:
    nombre = int("abc")  # "abc" n'est pas un nombre
except ValueError as e:
    print(f"Erreur : {e}")
    # Sortie : invalid literal for int() with base 10: 'abc'

# Exemple 2 : Utilisation pratique
def obtenir_age():
    while True:
        try:
            age = int(input("Votre âge : "))
            if age < 0 or age > 150:
                print("⚠️ L'âge doit être entre 0 et 150")
                continue
            return age
        except ValueError:
            print("❌ Veuillez entrer un nombre valide")

age_utilisateur = obtenir_age()
print(f"Votre âge : {age_utilisateur} ans")
```

### 2. TypeError

Survient lors d'opérations sur des types incompatibles.

```python
# Exemple 1 : Addition impossible
try:
    resultat = "5" + 3  # On ne peut pas additionner str et int
except TypeError as e:
    print(f"Erreur : {e}")
    # Solution : convertir en même type
    resultat = int("5") + 3  # ✅ Fonctionne
    print(f"Résultat : {resultat}")

# Exemple 2 : Fonction avec mauvais type d'argument
def calculer_carre(nombre):
    try:
        return nombre ** 2
    except TypeError:
        print("❌ L'argument doit être un nombre")
        return None

print(calculer_carre(5))      # ✅ 25
print(calculer_carre("abc"))  # ❌ TypeError géré
```

### 3. IndexError

Survient quand on accède à un index qui n'existe pas dans une liste.

```python
fruits = ["pomme", "banane", "orange"]

try:
    print(fruits[0])  # ✅ "pomme"
    print(fruits[5])  # ❌ IndexError
except IndexError:
    print("❌ Cet index n'existe pas dans la liste")

# Méthode sécurisée pour accéder aux éléments
def obtenir_element(liste, index):
    try:
        return liste[index]
    except IndexError:
        print(f"⚠️ Index {index} hors limites (liste de taille {len(liste)})")
        return None

print(obtenir_element(fruits, 1))  # ✅ "banane"
print(obtenir_element(fruits, 10)) # ⚠️ Message d'erreur
```

### 4. KeyError

Survient lors de l'accès à une clé inexistante dans un dictionnaire.

```python
utilisateur = {
    "nom": "Alice",
    "age": 25,
    "ville": "Paris"
}

# ❌ Accès direct (risqué)
try:
    print(utilisateur["email"])  # Cette clé n'existe pas
except KeyError:
    print("❌ La clé 'email' n'existe pas")

# ✅ Méthodes sécurisées
# Méthode 1 : get() avec valeur par défaut
email = utilisateur.get("email", "Non renseigné")
print(f"Email : {email}")

# Méthode 2 : Vérifier l'existence de la clé
if "email" in utilisateur:
    print(utilisateur["email"])
else:
    print("Email non disponible")
```

### 5. ZeroDivisionError

Survient lors d'une division par zéro.

```python
def calculer_moyenne(total, nombre):
    try:
        return total / nombre
    except ZeroDivisionError:
        print("❌ Impossible de diviser par zéro")
        return 0

# Tests
print(calculer_moyenne(100, 4))  # ✅ 25.0
print(calculer_moyenne(100, 0))  # ❌ Gestion de l'erreur
```

### 6. FileNotFoundError

Survient quand on essaie d'ouvrir un fichier qui n'existe pas.

```python
def lire_configuration(fichier):
    try:
        with open(fichier, 'r') as f:
            contenu = f.read()
            return contenu
    except FileNotFoundError:
        print(f"❌ Le fichier '{fichier}' est introuvable")
        # Créer un fichier par défaut
        print("📝 Création d'un fichier de configuration par défaut...")
        with open(fichier, 'w') as f:
            f.write("# Configuration par défaut\n")
        return "# Configuration par défaut\n"

config = lire_configuration("config.txt")
```

### 7. AttributeError

Survient quand on accède à un attribut ou une méthode inexistant.

```python
class Personne:
    def __init__(self, nom):
        self.nom = nom
    
    def dire_bonjour(self):
        return f"Bonjour, je suis {self.nom}"

personne = Personne("Bob")

try:
    print(personne.nom)           # ✅ Fonctionne
    print(personne.dire_bonjour()) # ✅ Fonctionne
    print(personne.age)            # ❌ AttributeError
except AttributeError as e:
    print(f"❌ Erreur : {e}")
```

## Bonnes pratiques de gestion des exceptions

- Toujours capturer des exceptions spécifiques (`ValueError`, `TypeError`, etc.)
- Ne jamais masquer une erreur sans message
- Ne pas utiliser les exceptions pour la logique normale du programme
- Toujours libérer les ressources (fichiers, connexions)
- Afficher des messages clairs pour l’utilisateur