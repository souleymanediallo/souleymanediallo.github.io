---
date:
  created: 2026-03-21

---

# Docstrings : écrire du code qui se comprend tout seul

Vous avez déjà ouvert un fichier Python que vous aviez écrit six mois plus tôt et vous êtes retrouvé à vous demander ce que vous aviez bien pu vouloir faire ? Ou pire, vous avez hérité du code de quelqu'un d'autre, sans la moindre explication ? C'est exactement pour ça que les docstrings existent.

<!-- more -->

## C'est quoi une docstring, au juste ?

Une docstring (contraction de "documentation string") est une chaîne de caractères placée juste après la définition d'une fonction, d'une classe ou d'un module. Elle sert de notice d'utilisation intégrée directement dans le code.

Voici la forme la plus simple :

```python
def additionner(a, b):
    """Retourne la somme de deux nombres."""
    return a + b
```

Ce texte entre triple guillemets n'est pas un commentaire ordinaire. Python le stocke dans un attribut spécial appelé `__doc__`, ce qui lui donne un statut bien particulier.

La grande différence avec un commentaire classique (celui qui commence par `#`) ? Le commentaire est ignoré par Python une fois le fichier lu. La docstring, elle, reste vivante dans le programme. Elle peut être lue, affichée, exploitée par des outils.


## À quoi ça sert vraiment ?

La docstring remplit trois rôles distincts.

D'abord, elle sert à vous, au développeur. En la rédigeant, vous vous forcez à articuler clairement ce que fait votre fonction. C'est souvent révélateur : si vous peinez à l'expliquer en une phrase, c'est peut-être que la fonction essaie d'en faire trop.

Ensuite, elle sert aux autres développeurs qui liront votre code, qu'il s'agisse de collègues ou de vous-même dans quelques mois. Une bonne docstring leur évite de devoir lire chaque ligne pour comprendre l'intention.

Enfin, elle sert aux outils. Les environnements de développement (VS Code, PyCharm...) l'affichent quand vous survolez une fonction. Des générateurs de documentation comme Sphinx peuvent construire un site web de référence automatiquement à partir de vos docstrings. Les frameworks de test peuvent même les utiliser pour exécuter des exemples de code.


## Comment accéder à une docstring ?

Plusieurs chemins mènent à la docstring d'une fonction ou d'une classe.

La méthode la plus directe est l'attribut `__doc__` :

```python
print(additionner.__doc__)
# Retourne la somme de deux nombres.
```

La fonction native `help()` affiche quelque chose de plus lisible, surtout pour les docstrings longues :

```python
help(additionner)
```

Dans un notebook Jupyter ou IPython, vous pouvez aussi utiliser le point d'interrogation :

```python
additionner?
```

Ces trois approches vous donnent accès à la même information, juste sous des formes différentes selon le contexte.


## Les grands styles de docstrings

Il n'existe pas qu'une seule façon d'écrire une docstring. La communauté Python a développé plusieurs conventions, chacune avec ses propres forces.


### Le style Google

C'est probablement le plus lisible à l'œil nu. Il utilise des sections avec indentation :

```python
def diviser(a, b):
    """Divise a par b et retourne le résultat.

    Args:
        a (float): Le numérateur.
        b (float): Le dénominateur, ne doit pas être zéro.

    Returns:
        float: Le résultat de la division.

    Raises:
        ValueError: Si b est égal à zéro.
    """
    if b == 0:
        raise ValueError("Division par zéro impossible.")
    return a / b
```

Sa lisibilité directe en fait un excellent choix pour des équipes qui lisent beaucoup de code dans un éditeur de texte.


### Le style NumPy

Inspiré des projets scientifiques comme NumPy et SciPy, il utilise des tirets pour souligner les titres de sections. Plus verbeux, il convient bien aux fonctions avec de nombreux paramètres ou à la documentation scientifique :

```python
def diviser(a, b):
    """
    Divise a par b et retourne le résultat.

    Parameters
    ----------
    a : float
        Le numérateur.
    b : float
        Le dénominateur, ne doit pas être zéro.

    Returns
    -------
    float
        Le résultat de la division.

    Raises
    ------
    ValueError
        Si b est égal à zéro.
    """
    if b == 0:
        raise ValueError("Division par zéro impossible.")
    return a / b
```


### Le style reStructuredText (reST)

C'est le format historique de Python, celui utilisé par défaut dans Sphinx. Il est plus compact mais moins agréable à lire directement :

```python
def diviser(a, b):
    """Divise a par b et retourne le résultat.

    :param a: Le numérateur.
    :type a: float
    :param b: Le dénominateur, ne doit pas être zéro.
    :type b: float
    :returns: Le résultat de la division.
    :rtype: float
    :raises ValueError: Si b est égal à zéro.
    """
    if b == 0:
        raise ValueError("Division par zéro impossible.")
    return a / b
```

Ce style reste pertinent si vous générez de la documentation avec Sphinx sans plugin supplémentaire.


## Quelle structure choisir selon le contexte ?

Tout dépend de la complexité de ce que vous documentez.

Pour une petite fonction évidente, une seule ligne suffit parfaitement :

```python
def est_pair(n):
    """Retourne True si n est pair, False sinon."""
    return n % 2 == 0
```

Pas besoin de s'étendre davantage. La règle d'or : la docstring doit être proportionnelle à la complexité de la fonction.

Pour une fonction plus élaborée, avec plusieurs paramètres, des valeurs de retour et des cas d'erreur possibles, adoptez une docstring structurée. Elle comprend alors un résumé sur la première ligne, une ligne vide, puis les sections détaillées.

Pour une classe, documentez l'objet dans la docstring de la classe elle-même et chaque méthode dans sa propre docstring. Inutile de dupliquer dans `__init__` ce que vous avez déjà dit au niveau de la classe.

Pour un module (un fichier Python entier), placez la docstring tout en haut, avant les imports. Elle explique à quoi sert ce module et ce qu'il contient.

En équipe, le plus important est la cohérence. Choisissez un style ensemble et tenez-vous-y. Un projet qui mélange Google, NumPy et reST est plus difficile à lire qu'un projet qui utilise un seul style, même imparfaitement.


## Les erreurs qui reviennent le plus souvent

Certaines mauvaises habitudes sont très répandues. Les voici, avec leur remède.

La docstring qui répète juste le nom de la fonction n'apporte rien. Écrire `"""Calcule le prix."""` pour une fonction nommée `calculer_prix` est inutile. Dites plutôt ce que la fonction fait vraiment, avec ses nuances.

La docstring qui ne se met pas à jour quand le code change est parfois pire qu'une absence de documentation, car elle induit en erreur. Traitez la docstring comme faisant partie du code : quand vous modifiez une fonction, mettez sa documentation à jour.

Documenter le "comment" au lieu du "quoi" est une erreur classique. La docstring doit expliquer ce que fait la fonction et pourquoi, pas détailler son implémentation interne. Pour ça, les commentaires dans le corps de la fonction sont plus appropriés.

Ignorer les cas limites et les exceptions est regrettable. Si votre fonction plante dans certaines conditions, dites-le. C'est une information précieuse pour quiconque l'utilisera.

Enfin, ne pas documenter les modules et les classes est fréquent. On pense souvent à documenter les fonctions mais on oublie d'expliquer à quoi sert un module entier ou une classe. Ces docstrings de haut niveau sont pourtant souvent les premières que quelqu'un lira.


## En résumé

Une bonne docstring se reconnaît à ceci : elle répond aux questions que se poserait un développeur compétent mais qui ne connaît pas votre code. Qu'est-ce que cette fonction fait ? Qu'est-ce qu'elle attend comme entrée ? Qu'est-ce qu'elle retourne ? Dans quels cas peut-elle échouer ?

Vous n'avez pas besoin de rédiger un roman. Quelques lignes bien choisies valent mieux qu'un pavé confus. L'objectif est simple : que votre code puisse se lire et se comprendre sans que son auteur soit dans la pièce.

Et si vous doutez encore de l'utilité de cet effort, imaginez simplement votre futur vous, à trois heures du matin, à deux jours d'une deadline, qui tombe sur une fonction bien documentée. Il vous remerciera.
