# Les Nombres en Python

## 1. Deux grandes familles de nombres

Python distingue deux types de nombres fondamentaux :

| Type | Nom Python | Description | Exemples |
|------|-----------|-------------|---------|
| Entier | `int` | Nombre sans virgule | `-5`, `0`, `42`, `1000` |
| Décimal | `float` | Nombre avec virgule | `-2.5`, `0.0`, `3.14`, `1.0` |

> **Pourquoi cette distinction ?** Entiers et décimaux sont stockés différemment en mémoire. Un `int` est exact, tandis qu'un `float` est une approximation (c'est la nature du calcul en virgule flottante).

## 2. Les entiers — `int`

Un entier est un nombre **sans partie décimale** : positif, négatif ou nul.

```python
age = 25          # entier positif
temperature = -3  # entier négatif
score = 0         # zéro
population = 8_100_000_000  # les _ améliorent la lisibilité (Python 3.6+)
```

Pour vérifier le type d'une variable, on utilise `type()` :

```python
>>> type(age)
<class 'int'>
```

### À retenir

- Un `int` peut être aussi grand que la mémoire le permet (pas de limite fixe en Python).
- Écrire `25` sans point → c'est un `int`.


## 3. Les décimaux — `float`

Un décimal est un nombre **avec un point** (Python utilise le point `.`, pas la virgule `,`).

```python
prix = 9.99       # float positif
poids = -0.5      # float négatif
pi = 3.14159      # float positif
vide = 0.0        # aussi un float, malgré la valeur zéro !
```

```python
>>> type(prix)
<class 'float'>
>>> type(0.0)
<class 'float'>   # ← même 0.0 est un float, pas un int !
```

### Piège classique

```python
>>> type(0)
<class 'int'>

>>> type(0.0)
<class 'float'>   # Le simple point change tout !
```

> La présence du `.` dans le code source est ce qui détermine le type, pas la valeur.

## 4. Opérations mathématiques

Python supporte toutes les opérations classiques :

| Opération | Symbole | Exemple | Résultat |
|-----------|---------|---------|---------|
| Addition | `+` | `10 + 3` | `13` |
| Soustraction | `-` | `10 - 3` | `7` |
| Multiplication | `*` | `10 * 3` | `30` |
| Division | `/` | `10 / 3` | `3.3333...` |
| Division entière | `//` | `10 // 3` | `3` |
| Modulo (reste) | `%` | `10 % 3` | `1` |
| Puissance | `**` | `2 ** 8` | `256` |

```python
x = 10
y = 3

print(x + y)   # 13   → int
print(x - y)   # 7    → int
print(x * y)   # 30   → int
print(x / y)   # 3.3333333333333335  → TOUJOURS un float !
print(x // y)  # 3    → int (division sans reste)
print(x % y)   # 1    → int (reste de la division)
print(x ** y)  # 1000 → int (10 à la puissance 3)
```

### Règle de la contamination par le `float`

Dès qu'une opération mélange un `int` et un `float`, le résultat est **toujours** un `float` :

```python
>>> 10 + 3.0
13.0        # int + float → float

>>> 10 * 1.0
10.0        # int * float → float

>>> 10 / 2
5.0         # La division / donne TOUJOURS un float, même si le résultat est entier !
```

## 5. Convertir entre les types

Python fournit deux fonctions de conversion :

### `int()` — Convertir en entier

```python
>>> int(3.99)   # Tronque (ne arrondit PAS)
3

>>> int(3.14)
3

>>> int(-2.9)   # Attention, tronque vers zéro !
-2

>>> int("42")   # Peut aussi convertir une chaîne de caractères
42
```

> **`int()` tronque, il n'arrondit pas !**
> `int(3.99)` donne `3`, pas `4`.
> Pour arrondir, utilisez `round()`.

### `float()` — Convertir en décimal

```python
>>> float(10)
10.0

>>> float(-5)
-5.0

>>> float("3.14")   # Peut aussi convertir une chaîne
3.14
```

### `round()` — Arrondir correctement

```python
>>> round(3.14159, 2)   # Arrondi à 2 décimales
3.14

>>> round(2.5)          # Arrondi au plus proche
2                       # (Python utilise l'arrondi bancaire : vers le pair)

>>> round(3.5)
4
```

## 6. Résumé visuel

```
       TYPES DE NOMBRES EN PYTHON
       ───────────────────────────

   int                     float
  ──────                  ──────
  0, 1, -5, 100      0.0, 3.14, -2.5

  ↕ conversion            ↕ conversion
  int(3.14) → 3        float(10) → 10.0
  (tronque !)          (ajoute .0)

       OPÉRATIONS MIXTES
       ─────────────────
  int OP int → int  (sauf / qui donne float)
  int OP float → float  (toujours)
  float OP float → float  (toujours)
```

## 7. Bonnes pratiques

- Utilisez `int` pour les comptages, indices, identifiants — tout ce qui est naturellement entier.
- Utilisez `float` pour les mesures, prix, coordonnées — tout ce qui peut avoir une partie décimale.
- Préférez `//` à `/` quand vous voulez un résultat entier (ex. : partage d'un gâteau en parts égales).
- N'utilisez jamais `int()` pour arrondir : utilisez `round()`.


## 8. Pour aller plus loin

- [Documentation officielle — Types numériques](https://docs.python.org/fr/3/library/stdtypes.html#numeric-types-int-float-complex)
- Python propose aussi les **complexes** (`complex`) : `2 + 3j`, mais ils sont rarement utilisés en dehors des mathématiques avancées.
- Le module [`decimal`](https://docs.python.org/fr/3/library/decimal.html) permet des calculs décimaux **exactement précis** (utile en finance).
- Le module [`fractions`](https://docs.python.org/fr/3/library/fractions.html) permet de manipuler des fractions comme `1/3` sans perte de précision.
