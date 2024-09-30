# TP Automatisation

## Binôme:
- Baudson Dylan
- Pedretti Zack

## 1. Les tests

```
Les actions GitHub permettent de déclencher des tests à partir de l'événement de notre choix (push, pull request, etc.). Ce système offre donc la possibilité de tester notre code à tout moment, et s'avère très utile pour continuer à maintenir et mettre à jour notre code.

Les différentes actions :
actions/checkout@v3 :
Cette action permet de cloner le dépôt Git dans l'environnement d'exécution. C'est une étape essentielle car elle rend le code source disponible pour les actions suivantes.

php-actions/composer@v6 :
Cette action exécute Composer, un gestionnaire de dépendances pour PHP. Elle installe les bibliothèques nécessaires définies dans le fichier composer.json du projet. Cela permet de s'assurer que toutes les dépendances sont installées avant de passer à l'étape suivante.

php-actions/phpunit@v3 :
Cette action exécute PHPUnit, un framework de test pour PHP. Elle permet de lancer les tests automatisés définis dans le projet afin de vérifier que le code fonctionne correctement et n'introduit pas de régressions. Voici les principales configurations utilisées pour cette étape :

    - php_extensions : Installe les extensions PHP nécessaires, telles que gd, mbstring, sqlite3, simplexml et xdebug (pour la couverture de code).
    - configuration : Utilise le fichier phpunit.xml pour configurer PHPUnit, définissant les tests à exécuter et les options spécifiques.
    - bootstrap : Spécifie le fichier Bootstrap.php situé dans le répertoire tst, exécuté avant les tests pour configurer l'environnement ou initialiser certaines ressources.
    - version : Définit la version de PHPUnit utilisée, ici la version 9.
    - php_version : Utilise PHP 8.1 pour exécuter les tests, garantissant que le projet est testé sur une version moderne de PHP.
```

## 2. Code coverage

```

