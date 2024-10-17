# TP Automatisation

## Binôme:
- Baudson Dylan
- Pedretti Zack

## PARTIE 1 : Tests

```
L'objectif principal de cette action est d'automatiser le processus de tests en utilisant PHPUnit, un framework de tests pour PHP. Voici les étapes détaillées de cette partie :

Trigger des actions :

L'action est déclenchée à chaque push ou pull request (ligne on).
Cela garantit que les tests sont exécutés automatiquement à chaque modification du code.
Environnement d'exécution :

Le job utilise l'environnement ubuntu-latest (ligne runs-on), qui est une version récente d'Ubuntu préconfigurée par GitHub pour l'exécution des workflows.
Étape de checkout :

L'étape Checkout code utilise actions/checkout@v3 pour cloner le code source du dépôt Git dans l'environnement virtuel afin de l'exécuter.
Installation des dépendances :

composer install --no-progress --no-suggest installe les bibliothèques PHP nécessaires sans afficher d'informations superflues. Composer gère les dépendances du projet.
Lancement de PHPUnit :

php-actions/phpunit@v3 est une action qui exécute les tests unitaires via PHPUnit, avec les extensions PHP nécessaires pour les tests (gd, sqlite3, xdebug, etc.).
La version 9.6.11 de PHPUnit est spécifiée, avec la configuration provenant de phpunit.xml, qui définit les règles et les spécificités des tests.

Difficulté rencontré :

Sur cette étape, nous n'avons pas eu tant de difficulté. La difficulté principale a été d'installer les extensions nécessaires pour permettre aux tests de pouvoir être correct. La deuxième difficulté a été de trouver la version correcte des extension compatible avec notre version de PHP.
```

## PARTIE 2 : Coverage

```

