# HTML et Accessibilité
Le HTML5 est utilisé pour définir les différentes zones de votre page web comme l'en‑tête, le menu de navigation, le contenu principal, etc. 

Exemple : ```<header>, <nav>, <main>, <aside>, <footer>```

C'est un langage de balise, composé d'une série d'élément avec lesquels vous pouvez encadrer, envelopper ou baliser différentes parties du contenu pour les faire apparaître ou agir d'une certaine manière. 

Une grande partie des contenus web peut être rendue accessible simplement en s'assurant d'utiliser les éléments HTML appropriés telle que **WAI-ARIA**.

Commençons par se familiariser avec **WAI-ARIA** et savoir comment l'utiliser pour fournir une sémantique supplémentaire utile afin d'améliorer l'accessibilité.

##  Qu'est-ce que WAI-ARIA ?
WAI-ARIA est une spécification écrite par le W3C et définissant un ensemble d'attributs HTML supplémentaires pouvant être appliqués aux éléments pour fournir une sémantique supplémentaire et améliorer l'accessibilité en cas de manque.

### Trois caractéristiques principales sont définies dans la spécification :

- **Les rôles** : décrivent différentes structures de pages, telles que l'en‑tête, le menu de navigation, le contenu principal, etc.

Exemple : Recommandation RGAA pour les attributs ```role```:
```
    <header role="banner">
    <nav role="navigation">
    <main role ="main">
    <footer role="contentinfo"> 
```
Les attributs ```role``` doivent être unique sur une page web sauf le rôle ```navigation``` qui peut être utiliser pour les menus secondaires.

Exemple : Autres attributs ```role``` non nécessaire pour le RGAA
```
    <aside role="complementary">
    <section role="region">
    <article role ="article">
```
Les attributs rôles très important : ```role=search, role=form, role=tab```.

Il est conseillé d'utiliser les balises sémantiques et les attributs ```role``` pour améliorer l'accessibilité numérique.

- **Les propriétés** : peuvent être utilisés pour donner une signification supplémentaire ou une sémantique. 

Par exemple, spécifie qu'une entrée de formulaire doit être renseignée pour être valide

```aria-required="true"```

Autre exemple, mettre un ID sur un élément, puis de le référencer en tant qu'étiquette

```aria-labelledby="label"``` 

- **Les états** : définissent les conditions actuelles des éléments.

Exemple : signaler à un lecteur d'écran que l'entrée de formulaire est actuellement désactivée

```aria-disabled="true"```

## Le Texte
