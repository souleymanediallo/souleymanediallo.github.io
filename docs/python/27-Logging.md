# Logging
La journalisation (ou "logging" en anglais) en Python est un mécanisme qui permet de suivre les événements qui se produisent dans une application et de les enregistrer dans des fichiers de journal ou des consoles. Cela permet aux développeurs de suivre les erreurs, les avertissements et les informations de débogage, et de les utiliser pour résoudre les problèmes et améliorer les performances de l'application.

Python possède une bibliothèque intégrée pour la journalisation appelée "logging". Voici un exemple simple d'utilisation de cette bibliothèque pour enregistrer un message de journalisation :

```
import logging

logging.basicConfig(filename='example.log', level=logging.DEBUG)
logging.debug('This is a debug message')
logging.info('This is an info message')
logging.warning('This is a warning message')
logging.error('This is an error message')
```

Dans cet exemple, nous utilisons la fonction `basicConfig()` pour configurer la journalisation en spécifiant le nom de fichier de journal "example.log" et le niveau de journalisation à "DEBUG". Nous utilisons ensuite les fonctions `debug()`, `info()`, `warning()` et `error()` pour enregistrer des messages de journalisation de différents niveaux.

Il existe plusieurs niveaux de journalisation disponibles dans la bibliothèque "logging" : DEBUG, INFO, WARNING, ERROR, CRITICAL. Et il est possible de filtrer les messages en fonction de ces niveaux.

Il est possible de configurer la journalisation pour envoyer les messages de journalisation vers des destinations spécifiques telles que des fichiers, des consoles, des e-mails ou des services de journalisation en nuage. Il est également possible de formater les messages de journalisation pour les adapter à vos besoins.