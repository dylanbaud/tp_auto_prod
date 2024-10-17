# TP Automatisation

## Binôme:
- Baudson Dylan
- Pedretti Zack

## PARTIE 1 : Tests

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

## PARTIE 2 : Coverage

Cette partie du pipeline concerne la génération d'un rapport de couverture de code, essentiel pour visualiser quelles parties du code sont couvertes par les tests.

Xdebug pour la couverture :

L'environnement est configuré avec XDEBUG_MODE: coverage, ce qui permet à l'extension Xdebug de générer des rapports de couverture lorsque PHPUnit est exécuté.
Xdebug, en mode couverture, analyse les lignes de code exécutées lors des tests pour calculer la couverture.

Création du rapport de couverture :

irongut/CodeCoverageSummary@v1.3.0 est utilisé pour générer un rapport de couverture de code.
Le rapport est extrait du fichier log/cobertura.xml, un format compatible avec des outils d'analyse de couverture comme SonarQube.
L'action génère un badge pour indiquer le pourcentage de couverture, avec une sortie en format Markdown, utile pour afficher le résultat dans les commentaires ou dans les pages de documentation.

Exportation du rapport :

cat code-coverage-results.md >> $GITHUB_STEP_SUMMARY concatène le rapport de couverture généré dans un fichier Markdown et l'ajoute au résumé du workflow GitHub. Cela permet de visualiser facilement les résultats de la couverture de code dans l'interface GitHub.

Difficulté rencontré :

Cette étape a été l'étape ou l'on a eu le plus de difficulté :
- Le fichier cobertura.xml ne voulait pas être trouvé par l'action car il n'était pas defini dans le phpunit.xml
- L'utilisation de irongut/CodeCoverageSummary@v1.3.0 a été assez complexe à comprendre
- On avait oublié d'ajouter le mode coverage dans XDEBUG_MODE

## PARTIE 3 : Linting

La partie linting consiste à analyser statiquement le code pour détecter les erreurs de style, les violations des bonnes pratiques de programmation ou les problèmes potentiels avant même l'exécution des tests. Voici comment cette étape est intégrée dans le pipeline d'intégration continue en utilisant trois outils de linting populaires pour PHP : PHPStan, PHP Mess Detector (PHPMD) et PHP Code Sniffer (PHPCS).

### A. PHPStan - Analyse statique de code :

Objectif : PHPStan est un outil d'analyse statique qui vérifie le code PHP pour détecter les erreurs possibles sans l'exécuter. Il signale les types d'erreurs comme les fautes de syntaxe ou les appels de méthodes sur des objets incorrects.

```
- name: PHP Stan
  uses: php-actions/phpstan@v3
  with:
    path: ./
```

Fonctionnement : Cette étape exécute PHPStan sur l'ensemble du code (path: ./), assurant que le code respecte les règles définies pour éviter les erreurs de typage et autres problèmes.

### B. PHP Mess Detector (PHPMD) - Détection de code mal structuré :

Objectif : PHPMD analyse le code à la recherche de mauvaises pratiques et de failles dans la qualité du code, comme les classes trop complexes, les méthodes inutilisées ou les conventions de nommage non respectées.

- name: PHP Mess Detector
  uses: php-actions/phpmd@v1
  with:
    path: ./

Fonctionnement : Cette étape lance PHPMD sur l'ensemble du projet pour détecter les problèmes de conception et de structure.

### C. PHP Code Sniffer (PHPCS) - Respect des standards de codage :

Objectif : PHPCS vérifie que le code respecte des standards de codage spécifiques, tels que PSR-12 (PHP Standards Recommendations). Il assure la cohérence du style de codage dans tout le projet.

- name: PHP Code Sniffer
  uses: php-actions/phpcs@v1
  with:
    path: ./

Fonctionnement : PHPCS vérifie tout le code source et signale les violations des conventions de codage. Cela aide à maintenir un style de code uniforme.

### D. Conclusion

Ces trois outils assurent que le code est propre, bien structuré et conforme aux standards de l'industrie avant même d'exécuter les tests unitaires.
Nous n'avons pas eu de problème particulier sur cette partie car toutes ces actions étaient assez bien documenté.

## PARTIE 4 : Déploiement continu


