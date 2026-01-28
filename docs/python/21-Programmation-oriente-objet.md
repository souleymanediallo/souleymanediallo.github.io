# Programmation Orientée Objet en Python

## Introduction

La **programmation orientée objet (POO)** est un paradigme de programmation qui structure le code autour du concept 
d'**objets**. Ces objets combinent des données (appelées **attributs**) et des fonctionnalités (appelées **méthodes**) au sein d'unités cohérentes et réutilisables.

### Avantages de la POO

- **Réutilisabilité** : Le code peut être réutilisé via l'héritage et la composition
- **Maintenabilité** : Le code est mieux organisé et plus facile à modifier
- **Modularité** : Les programmes sont divisés en composants indépendants
- **Abstraction** : Permet de masquer la complexité et de se concentrer sur l'essentiel
- **Extensibilité** : Facilite l'ajout de nouvelles fonctionnalités

### Les quatre piliers de la POO

1. **Encapsulation** : Regroupement des données et des méthodes qui les manipulent
2. **Abstraction** : Masquer les détails d'implémentation complexes
3. **Héritage** : Création de nouvelles classes basées sur des classes existantes
4. **Polymorphisme** : Capacité d'utiliser une interface commune pour différents types

## Concepts fondamentaux

### Qu'est-ce qu'une classe ?

Une **classe** est un modèle (ou blueprint) qui définit la structure et le comportement d'un type d'objet. Elle spécifie :

- Les **attributs** : les données que l'objet contient
- Les **méthodes** : les actions que l'objet peut effectuer

### Qu'est-ce qu'un objet ?

Un **objet** est une instance concrète d'une classe. C'est une entité qui possède :

- Un **état** : les valeurs de ses attributs à un moment donné
- Un **comportement** : les méthodes qu'il peut exécuter
- Une **identité** : un identifiant unique en mémoire

**Analogie** : Si une classe est un plan architectural d'une maison, un objet est une maison réelle construite à partir de ce plan.


## Classes et objets

### Définir une classe

En Python, une classe se définit avec le mot-clé `class`, suivi du nom de la classe (par convention en PascalCase) 
et de deux-points.

```python
class Personne:
    """Classe représentant une personne."""
    pass
```

### Le constructeur `__init__`

La méthode `__init__` est le **constructeur** de la classe. Elle est automatiquement appelée lors de la création d'un 
objet et permet d'initialiser ses attributs.

```python
class Personne:
    """Classe représentant une personne avec un nom et un âge."""
    
    def __init__(self, nom, age):
        """
        Initialise une nouvelle personne.
        
        Args:
            nom (str): Le nom de la personne
            age (int): L'âge de la personne
        """
        self.nom = nom
        self.age = age
```

**Le paramètre `self`** : C'est une référence à l'instance courante de la classe. Il doit être le premier paramètre de 
toutes les méthodes d'instance (par convention nommé `self`).

### Créer des objets (instances)

Pour créer un objet, on appelle la classe comme une fonction, en passant les arguments nécessaires au constructeur.

```python
# Création d'instances de la classe Personne
personne1 = Personne("Ousmane", 30)
personne2 = Personne("Ismael", 25)

# Accès aux attributs
print(personne1.nom)  # Affiche: Ousmane
print(personne1.age)  # Affiche: 30
print(personne2.nom)  # Affiche: Ismael
```

### Exemple complet

```python
class Voiture:
    """Classe représentant une voiture."""
    
    def __init__(self, marque, modele, annee):
        """Initialise une nouvelle voiture."""
        self.marque = marque
        self.modele = modele
        self.annee = annee
        self.kilometrage = 0  # Attribut avec valeur par défaut
    
    def afficher_info(self):
        """Affiche les informations de la voiture."""
        print(f"{self.marque} {self.modele} ({self.annee}) - {self.kilometrage} km")
    
    def rouler(self, distance):
        """Ajoute des kilomètres au compteur."""
        self.kilometrage += distance
        print(f"La voiture a parcouru {distance} km.")

# Utilisation
ma_voiture = Voiture("Toyota", "Corolla", 2020)
ma_voiture.afficher_info()  # Toyota Corolla (2020) - 0 km
ma_voiture.rouler(150)       # La voiture a parcouru 150 km.
ma_voiture.afficher_info()  # Toyota Corolla (2020) - 150 km
```

## Attributs et méthodes

### Types d'attributs

#### 1. Attributs d'instance

Les attributs d'instance sont propres à chaque objet. Ils sont généralement définis dans `__init__`.

```python
class Compteur:
    def __init__(self, valeur_initiale=0):
        self.valeur = valeur_initiale  # Attribut d'instance

c1 = Compteur(10)
c2 = Compteur(20)
print(c1.valeur)  # 10
print(c2.valeur)  # 20
```

#### 2. Attributs de classe

Les attributs de classe sont partagés par toutes les instances de la classe.

```python
class Employe:
    # Attribut de classe
    nombre_employes = 0
    
    def __init__(self, nom):
        self.nom = nom  # Attribut d'instance
        Employe.nombre_employes += 1
    
    @classmethod
    def obtenir_nombre_employes(cls):
        """Retourne le nombre total d'employés."""
        return cls.nombre_employes

# Utilisation
e1 = Employe("Alice")
e2 = Employe("Bob")
print(Employe.nombre_employes)  # 2
print(Employe.obtenir_nombre_employes())  # 2
```

### Types de méthodes

#### 1. Méthodes d'instance

Les méthodes d'instance opèrent sur une instance spécifique de la classe. Elles ont accès à `self`.

```python
class Rectangle:
    def __init__(self, largeur, hauteur):
        self.largeur = largeur
        self.hauteur = hauteur
    
    def calculer_aire(self):
        """Méthode d'instance calculant l'aire."""
        return self.largeur * self.hauteur
    
    def calculer_perimetre(self):
        """Méthode d'instance calculant le périmètre."""
        return 2 * (self.largeur + self.hauteur)

rect = Rectangle(5, 3)
print(rect.calculer_aire())       # 15
print(rect.calculer_perimetre())  # 16
```

#### 2. Méthodes de classe

Les méthodes de classe opèrent sur la classe elle-même, pas sur une instance. 
Elles utilisent le décorateur `@classmethod` et prennent `cls` comme premier paramètre.

```python
class Date:
    def __init__(self, jour, mois, annee):
        self.jour = jour
        self.mois = mois
        self.annee = annee
    
    @classmethod
    def depuis_chaine(cls, date_str):
        """Crée une Date à partir d'une chaîne 'JJ-MM-AAAA'."""
        jour, mois, annee = map(int, date_str.split('-'))
        return cls(jour, mois, annee)
    
    def afficher(self):
        print(f"{self.jour:02d}/{self.mois:02d}/{self.annee}")

# Utilisation
date1 = Date(15, 3, 2024)
date1.afficher()  # 15/03/2024

date2 = Date.depuis_chaine("25-12-2024")
date2.afficher()  # 25/12/2024
```

#### 3. Méthodes statiques

Les méthodes statiques n'ont accès ni à `self` ni à `cls`. Elles sont définies avec le décorateur `@staticmethod`.

```python
class Calculatrice:
    @staticmethod
    def additionner(a, b):
        """Additionne deux nombres."""
        return a + b
    
    @staticmethod
    def multiplier(a, b):
        """Multiplie deux nombres."""
        return a * b

# Utilisation (pas besoin d'instance)
print(Calculatrice.additionner(5, 3))   # 8
print(Calculatrice.multiplier(4, 7))    # 28
```

## Encapsulation

L'**encapsulation** consiste à restreindre l'accès direct aux attributs et méthodes d'un objet, en les rendant privés 
ou protégés.

### Conventions de nommage

- **Public** : `attribut` - Accessible de partout
- **Protégé** : `_attribut` - Convention indiquant usage interne (mais toujours accessible)
- **Privé** : `__attribut` - Name mangling appliqué (renommé en `_Classe__attribut`)

```python
class CompteBancaire:
    def __init__(self, titulaire, solde_initial):
        self.titulaire = titulaire           # Public
        self._historique = []                # Protégé
        self.__solde = solde_initial         # Privé
    
    def deposer(self, montant):
        """Dépose de l'argent sur le compte."""
        if montant > 0:
            self.__solde += montant
            self._historique.append(f"Dépôt: +{montant}€")
            return True
        return False
    
    def retirer(self, montant):
        """Retire de l'argent du compte."""
        if 0 < montant <= self.__solde:
            self.__solde -= montant
            self._historique.append(f"Retrait: -{montant}€")
            return True
        return False
    
    def obtenir_solde(self):
        """Retourne le solde actuel (getter)."""
        return self.__solde
    
    def afficher_historique(self):
        """Affiche l'historique des transactions."""
        for transaction in self._historique:
            print(transaction)

# Utilisation
compte = CompteBancaire("Jules", 1000)
compte.deposer(500)
compte.retirer(200)
print(f"Solde: {compte.obtenir_solde()}€")  # Solde: 1300€
compte.afficher_historique()
```

### Properties (propriétés)

Les **properties** permettent de contrôler l'accès aux attributs via des getters et setters, tout en conservant 
une syntaxe d'attribut.

```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius
    
    @property
    def celsius(self):
        """Getter pour la température en Celsius."""
        return self._celsius
    
    @celsius.setter
    def celsius(self, valeur):
        """Setter pour la température en Celsius."""
        if valeur < -273.15:
            raise ValueError("La température ne peut pas être inférieure au zéro absolu")
        self._celsius = valeur
    
    @property
    def fahrenheit(self):
        """Getter pour la température en Fahrenheit."""
        return self._celsius * 9/5 + 32
    
    @fahrenheit.setter
    def fahrenheit(self, valeur):
        """Setter pour la température en Fahrenheit."""
        self.celsius = (valeur - 32) * 5/9

# Utilisation
temp = Temperature(25)
print(f"{temp.celsius}°C")       # 25°C
print(f"{temp.fahrenheit}°F")    # 77.0°F

temp.fahrenheit = 86
print(f"{temp.celsius}°C")       # 30.0°C
```

## Héritage

L'**héritage** permet de créer une nouvelle classe (classe dérivée ou sous-classe) basée sur une classe existante 
(classe de base ou superclasse). La sous-classe hérite des attributs et méthodes de la superclasse.

### Héritage simple

```python
class Animal:
    """Classe de base représentant un animal."""
    
    def __init__(self, nom, age):
        self.nom = nom
        self.age = age
    
    def manger(self):
        print(f"{self.nom} mange.")
    
    def dormir(self):
        print(f"{self.nom} dort.")

class Chien(Animal):
    """Classe dérivée représentant un chien."""
    
    def __init__(self, nom, age, race):
        super().__init__(nom, age)  # Appel du constructeur parent
        self.race = race
    
    def aboyer(self):
        print(f"{self.nom} aboie: Wouf!")
    
    def manger(self):
        """Surcharge de la méthode manger."""
        print(f"{self.nom} mange des croquettes.")

class Chat(Animal):
    """Classe dérivée représentant un chat."""
    
    def __init__(self, nom, age, couleur):
        super().__init__(nom, age)
        self.couleur = couleur
    
    def miauler(self):
        print(f"{self.nom} miaule: Miaou!")

# Utilisation
chien = Chien("Rex", 5, "Labrador")
chat = Chat("Felix", 3, "Noir")

chien.manger()   # Rex mange des croquettes.
chien.aboyer()   # Rex aboie: Wouf!
chat.manger()    # Felix mange.
chat.miauler()   # Felix miaule: Miaou!
```

### La fonction `super()`

La fonction `super()` permet d'accéder aux méthodes de la classe parente.

```python
class Vehicule:
    def __init__(self, marque, vitesse_max):
        self.marque = marque
        self.vitesse_max = vitesse_max
    
    def afficher_info(self):
        print(f"Véhicule {self.marque}, vitesse max: {self.vitesse_max} km/h")

class VoitureElectrique(Vehicule):
    def __init__(self, marque, vitesse_max, autonomie):
        super().__init__(marque, vitesse_max)
        self.autonomie = autonomie
    
    def afficher_info(self):
        super().afficher_info()  # Appel de la méthode parente
        print(f"Autonomie: {self.autonomie} km")

# Utilisation
tesla = VoitureElectrique("Tesla Model 3", 225, 500)
tesla.afficher_info()
# Véhicule Tesla Model 3, vitesse max: 225 km/h
# Autonomie: 500 km
```

### Héritage multiple

Python supporte l'héritage multiple (une classe peut hériter de plusieurs classes parentes).

```python
class Terrestre:
    def se_deplacer_terre(self):
        print("Se déplace sur terre")

class Aquatique:
    def se_deplacer_eau(self):
        print("Se déplace dans l'eau")

class Amphibien(Terrestre, Aquatique):
    """Hérite de Terrestre et Aquatique."""
    def __init__(self, nom):
        self.nom = nom

# Utilisation
grenouille = Amphibien("Grenouille")
grenouille.se_deplacer_terre()  # Se déplace sur terre
grenouille.se_deplacer_eau()    # Se déplace dans l'eau
```

### Vérification d'héritage

```python
# isinstance() : vérifie si un objet est une instance d'une classe
print(isinstance(chien, Chien))    # True
print(isinstance(chien, Animal))   # True
print(isinstance(chien, Chat))     # False

# issubclass() : vérifie si une classe hérite d'une autre
print(issubclass(Chien, Animal))   # True
print(issubclass(Chat, Animal))    # True
print(issubclass(Chien, Chat))     # False
```

## Polymorphisme

Le **polymorphisme** permet à des objets de différentes classes d'être traités de manière uniforme à travers une 
interface commune. Il existe principalement sous deux formes en Python.

### Polymorphisme par héritage

Des classes dérivées peuvent redéfinir (surcharger) des méthodes de leur classe parente.

```python
class Forme:
    """Classe de base pour les formes géométriques."""
    
    def __init__(self, nom):
        self.nom = nom
    
    def calculer_aire(self):
        """Méthode à surcharger dans les sous-classes."""
        raise NotImplementedError("Cette méthode doit être implémentée")
    
    def afficher(self):
        print(f"{self.nom} - Aire: {self.calculer_aire()}")

class Cercle(Forme):
    def __init__(self, rayon):
        super().__init__("Cercle")
        self.rayon = rayon
    
    def calculer_aire(self):
        return 3.14159 * self.rayon ** 2

class Rectangle(Forme):
    def __init__(self, largeur, hauteur):
        super().__init__("Rectangle")
        self.largeur = largeur
        self.hauteur = hauteur
    
    def calculer_aire(self):
        return self.largeur * self.hauteur

class Triangle(Forme):
    def __init__(self, base, hauteur):
        super().__init__("Triangle")
        self.base = base
        self.hauteur = hauteur
    
    def calculer_aire(self):
        return (self.base * self.hauteur) / 2

# Polymorphisme en action
formes = [
    Cercle(5),
    Rectangle(4, 6),
    Triangle(3, 8)
]

for forme in formes:
    forme.afficher()
# Cercle - Aire: 78.53975
# Rectangle - Aire: 24
# Triangle - Aire: 12.0
```

### Duck Typing

En Python, le polymorphisme ne nécessite pas nécessairement d'héritage. Le "duck typing" signifie : 
"Si ça marche comme un canard et ça fait coin-coin comme un canard, alors c'est un canard."

```python
class Chien:
    def __init__(self, nom):
        self.nom = nom
    
    def parler(self):
        return f"{self.nom} dit: Wouf!"

class Chat:
    def __init__(self, nom):
        self.nom = nom
    
    def parler(self):
        return f"{self.nom} dit: Miaou!"

class Robot:
    def __init__(self, nom):
        self.nom = nom
    
    def parler(self):
        return f"{self.nom} dit: Bip bip!"

def faire_parler(entite):
    """Fonction polymorphe qui fonctionne avec tout objet ayant une méthode parler()."""
    print(entite.parler())

# Utilisation
animaux = [
    Chien("Rex"),
    Chat("Minou"),
    Robot("R2D2")
]

for animal in animaux:
    faire_parler(animal)
# Rex dit: Wouf!
# Minou dit: Miaou!
# R2D2 dit: Bip bip!
```

### Classes abstraites

Les classes abstraites définissent une interface que les sous-classes doivent implémenter. 
Elles ne peuvent pas être instanciées directement.

```python
from abc import ABC, abstractmethod

class Paiement(ABC):
    """Classe abstraite définissant l'interface pour les paiements."""
    
    @abstractmethod
    def effectuer_paiement(self, montant):
        """Méthode abstraite à implémenter dans les sous-classes."""
        pass
    
    @abstractmethod
    def obtenir_historique(self):
        """Méthode abstraite à implémenter dans les sous-classes."""
        pass

class PaiementCarte(Paiement):
    def __init__(self, numero_carte):
        self.numero_carte = numero_carte
        self.historique = []
    
    def effectuer_paiement(self, montant):
        self.historique.append(f"Paiement carte: {montant}€")
        print(f"Paiement de {montant}€ effectué par carte {self.numero_carte}")
    
    def obtenir_historique(self):
        return self.historique

class PaiementPayPal(Paiement):
    def __init__(self, email):
        self.email = email
        self.historique = []
    
    def effectuer_paiement(self, montant):
        self.historique.append(f"Paiement PayPal: {montant}€")
        print(f"Paiement de {montant}€ effectué via PayPal ({self.email})")
    
    def obtenir_historique(self):
        return self.historique

# Utilisation
def traiter_paiement(methode_paiement, montant):
    """Traite un paiement de manière polymorphe."""
    methode_paiement.effectuer_paiement(montant)

carte = PaiementCarte("1234-5678")
paypal = PaiementPayPal("user@example.com")

traiter_paiement(carte, 50)   # Paiement de 50€ effectué par carte 1234-5678
traiter_paiement(paypal, 100) # Paiement de 100€ effectué via PayPal (user@example.com)
```

## Méthodes spéciales

Les **méthodes spéciales** (ou méthodes magiques) sont entourées de double underscores `__`. 
Elles permettent de personnaliser le comportement des objets.

### Méthodes communes

```python
class Livre:
    def __init__(self, titre, auteur, pages):
        """Constructeur."""
        self.titre = titre
        self.auteur = auteur
        self.pages = pages
    
    def __str__(self):
        """Représentation lisible (pour print)."""
        return f"'{self.titre}' par {self.auteur}"
    
    def __repr__(self):
        """Représentation technique (pour débogage)."""
        return f"Livre(titre='{self.titre}', auteur='{self.auteur}', pages={self.pages})"
    
    def __len__(self):
        """Retourne la longueur (nombre de pages)."""
        return self.pages
    
    def __eq__(self, other):
        """Vérifie l'égalité entre deux livres."""
        if not isinstance(other, Livre):
            return False
        return self.titre == other.titre and self.auteur == other.auteur
    
    def __lt__(self, other):
        """Compare deux livres (par nombre de pages)."""
        return self.pages < other.pages
    
    def __add__(self, other):
        """Additionne deux livres (combine les pages)."""
        if isinstance(other, Livre):
            return self.pages + other.pages
        return NotImplemented

# Utilisation
livre1 = Livre("1984", "George Orwell", 328)
livre2 = Livre("Le Meilleur des mondes", "Aldous Huxley", 288)

print(livre1)              # '1984' par George Orwell
print(repr(livre1))        # Livre(titre='1984', auteur='George Orwell', pages=328)
print(len(livre1))         # 328
print(livre1 == livre2)    # False
print(livre1 > livre2)     # True
print(livre1 + livre2)     # 616
```

### Méthodes pour conteneurs

```python
class Bibliotheque:
    def __init__(self):
        self.livres = []
    
    def ajouter_livre(self, livre):
        self.livres.append(livre)
    
    def __len__(self):
        """Retourne le nombre de livres."""
        return len(self.livres)
    
    def __getitem__(self, index):
        """Permet l'accès par index."""
        return self.livres[index]
    
    def __contains__(self, livre):
        """Permet l'utilisation de 'in'."""
        return livre in self.livres
    
    def __iter__(self):
        """Permet l'itération."""
        return iter(self.livres)

# Utilisation
biblio = Bibliotheque()
biblio.ajouter_livre(livre1)
biblio.ajouter_livre(livre2)

print(len(biblio))           # 2
print(biblio[0])             # '1984' par George Orwell
print(livre1 in biblio)      # True

for livre in biblio:
    print(livre)
```

### Context Manager (Gestionnaire de contexte)
Les context managers permettent de gérer des ressources (fichiers, connexions réseau, etc.) de manière sûre et efficace, 
en s'assurant qu'elles sont correctement libérées après utilisation.

```python
class FichierTexte:
    def __init__(self, nom_fichier, mode):
        self.nom_fichier = nom_fichier
        self.mode = mode
        self.fichier = None
    
    def __enter__(self):
        """Appelé au début du bloc 'with'."""
        self.fichier = open(self.nom_fichier, self.mode)
        return self.fichier
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        """Appelé à la fin du bloc 'with'."""
        if self.fichier:
            self.fichier.close()
        return False

# Utilisation
with FichierTexte("test.txt", "w") as f:
    f.write("Bonjour le monde!")
# Le fichier est automatiquement fermé
```

## Bonnes pratiques

### 1. Principe de responsabilité unique (SRP)

Chaque classe doit avoir une seule responsabilité.

```python
# Mauvais exemple
class Utilisateur:
    def __init__(self, nom, email):
        self.nom = nom
        self.email = email
    
    def sauvegarder_en_base(self):
        # Logique de base de données
        pass
    
    def envoyer_email(self):
        # Logique d'envoi d'email
        pass

# Bon exemple
class Utilisateur:
    def __init__(self, nom, email):
        self.nom = nom
        self.email = email

class UtilisateurRepository:
    def sauvegarder(self, utilisateur):
        # Logique de base de données
        pass

class ServiceEmail:
    def envoyer(self, destinataire, message):
        # Logique d'envoi d'email
        pass
```

### 2. Favoriser la composition à l'héritage

```python
# Composition (préférable)
class Moteur:
    def demarrer(self):
        print("Moteur démarré")

class Voiture:
    def __init__(self):
        self.moteur = Moteur()  # Composition
    
    def demarrer(self):
        self.moteur.demarrer()
```

### 3. Utiliser des noms descriptifs

```python
# Bon
class GestionnaireUtilisateurs:
    def creer_utilisateur(self, nom, email):
        pass

# Éviter
class GU:
    def cu(self, n, e):
        pass
```

### 4. Documenter le code

```python
class Calculatrice:
    """
    Classe fournissant des opérations mathématiques de base.
    
    Cette classe implémente les opérations fondamentales
    d'arithmétique pour des nombres réels.
    """
    
    def additionner(self, a, b):
        """
        Additionne deux nombres.
        
        Args:
            a (float): Premier nombre
            b (float): Deuxième nombre
        
        Returns:
            float: La somme de a et b
        
        Examples:
            >>> calc = Calculatrice()
            >>> calc.additionner(2, 3)
            5
        """
        return a + b
```

### 5. Utiliser les dataclasses (Python 3.7+)

Pour les classes simples qui stockent principalement des données :

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: float
    y: float
    
    def distance_origine(self):
        return (self.x**2 + self.y**2)**0.5

# Utilisation
p = Point(3, 4)
print(p)                      # Point(x=3, y=4)
print(p.distance_origine())   # 5.0
```

## Exercices pratiques

### Exercice 1 : Système de gestion de bibliothèque

Créez un système avec les classes suivantes :

- `Livre` : titre, auteur, ISBN, disponible
- `Membre` : nom, numéro de membre, livres empruntés
- `Bibliotheque` : liste de livres, liste de membres, méthodes pour emprunter/retourner

### Exercice 2 : Hiérarchie de formes géométriques

Implémentez :

- Une classe abstraite `Forme` avec des méthodes `calculer_aire()` et `calculer_perimetre()`
- Des classes dérivées : `Cercle`, `Rectangle`, `Triangle`
- Une fonction qui affiche les informations de n'importe quelle forme

### Exercice 3 : Système bancaire

Créez :

- Une classe `CompteBancaire` avec solde, titulaire, numéro de compte
- Des classes dérivées : `CompteEpargne` (avec taux d'intérêt), `CompteCourant` (avec découvert autorisé)
- Des méthodes pour déposer, retirer, transférer de l'argent

### Exercice 4 : Jeu de cartes

Implémentez :

- Une classe `Carte` (valeur, couleur)
- Une classe `Paquet` (liste de cartes, mélanger, distribuer)
- Une classe `Joueur` (main de cartes, ajouter/retirer des cartes)
- Une classe `Jeu` qui orchestre le tout

## Conclusion

La programmation orientée objet en Python est un outil puissant pour structurer et organiser votre code. 
Les concepts clés à retenir sont :

- **Classes et objets** : Modèles et instances
- **Encapsulation** : Protection des données
- **Héritage** : Réutilisation et extension du code
- **Polymorphisme** : Flexibilité et interfaces communes
- **Méthodes spéciales** : Personnalisation du comportement des objets

La maîtrise de la POO nécessite de la pratique. N'hésitez pas à expérimenter, à créer vos propres classes et à résoudre des problèmes réels avec ces concepts.

### Ressources supplémentaires

-  [Documentation officielle Python :octicons-link-external-16:](https://docs.python.org/fr/3/tutorial/classes.html){:target="_blank"}
-  [PEP 8 (Style Guide) :octicons-link-external-16:](https://peps.python.org/pep-0008/){:target="_blank"}
