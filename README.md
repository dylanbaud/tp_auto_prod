# tp_auto_prod

## Binôme:
- Baudson Dylan
- Pedretti Zack

Les actions GITHUB permettent de lancer des tests lors de l'action de notre choix (push, pull requests etc...).
Ce système permet donc de tester notre code à tout moment et il est très utile pour continuer à mettre note code à jour.

uses: actions/checkout@v3 :
Cette action permet de cloner le dépôt Git dans l'environnement d'exécution. C'est une étape essentielle car elle met le code source à disposition pour les actions suivantes.

uses: php-actions/composer@v6 :
Cette action exécute Composer, un gestionnaire de dépendances pour PHP. Elle installe les bibliothèques nécessaires définies dans le fichier composer.json du projet. C'est utile pour s'assurer que toutes les dépendances du projet sont installées avant de passer à l'étape suivante.

uses: php-actions/phpunit@v3 :
Cette action exécute PHPUnit, un framework de test pour PHP. Elle permet de lancer les tests automatisés définis dans le projet afin de vérifier que le code fonctionne correctement et ne casse pas les fonctionnalités existantes.
