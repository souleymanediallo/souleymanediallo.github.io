# Contenus textuels

L'une des meilleures aides en accessibilité qu'un utilisateur de lecteur d'écran peut avoir est une bonne structure des titres, paragraphes, listes, etc. 

Commençons par créer une page html

```
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Accessibilité</title>
</head>
<body>
   
</body>
</html>
```

Les informations suivantes sont importantes :

- L'attribut `lang` doit être renseigner exemple `fr` pour le Français.
- Le meta ```name="viewport"``` pour une page responsive (ordinateur, tablette, portable).
- Le title pour indiquer le titre de la page web.

Créer le contenu de la page web
```
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Accessibilité</title>
</head>
<body>
    <h1>Mon titre</h1>

    <p>Ceci est la premère section de mon document.</p>

    <p>Je vais ajouter ici un autre paragraphe.</p>

    <ol>
    <li>Voici</li>
    <li>une liste</li>
    <li>en HTML</li>
    </ol>

    <h2>Mon sous-titre</h2>

    <p>Ceci est la première sous-section de mon document. J'aurais aimé que les gens puissent trouver ce contenu!</p>

    <h2>Mon second sous-titre</h2>

    <p>Ceci est la seconde sous-section de mon document. Je pense qu'elle est plus intéressante que la dernière.</p>
</body>
</html>
```

- Un lecteur d'écran peut lire à voix haute chaque élément au fur et à mesure que vous progressez dans le contenu, vous notifiant ce qui est un paragraphe, ce qui est un titre, etc.
- Le lecteur d'écran s'arrête après chaque élément, vous laissant aller à n'importe quel endroit vous convenant.
- Vous pouvez sauter au précédent ou au prochain titre avec de nombreux lecteurs d'écran.
- Vous pouvez aussi dresser une liste de tous les titres avec de nombreux lecteurs d'écrans, vous permettant de les utiliser comme une table des matières pratique pour trouver un contenu spécifique.

## Utiliser un langage clair
Le langage que vous employez peut aussi affecter l'accessiblité. En général vous ne devriez pas utiliser un langage trop complexe, ni utiliser un jargon ou de l'argot inutiles. Eviter d'utiliser un langage et des caractères qui ne sont pas lus clairement à voix haute par le lecteur d'écran. 

Par exemple :

- N'utilisez pas des tirets si vous le pouvez. Au lieu d'écrire 5–7, écrivez 5 à 7.
- Explicitez les abréviations — au lieu d'écrire Jan, écrivez Janvier.
- Explicitez les acronymes, au moins une ou deux fois. Au lieu d'écrire "HTML" en premier lieu, écrivez Hypertext Markup Language.