### QCM Symfony

## 1. Partie introduction

1. **Quelles extensions PHP sont requises pour utiliser Symfony 7 ?**
   - a) json, xml, mbstring
   - b) intl, pdo_mysql, xsl, amqp, gd, openssl, sodium
   - c) zip, curl, gd, xml

2. **Comment installer la CLI de Symfony sur un système Mac de manière globale ?**
   - a) `composer require symfony/cli`
   - b) `curl -sS https://get.symfony.com/cli/installer | bash`
   - c) `scoop install symfony-cli`

3. **Quelle(s) commande(s) permet de créer un nouveau projet Symfony ?**
   - a) `symfony init my_project`
   - b) `composer create-project symfony/skeleton my_project`
   - c) `symfony new my_project`

4. **Quelle(s) est/sont la/les commande(s) pour lancer le serveur de test Symfony ?**
   - a) `php -S localhost:8000 -t public`
   - b) `symfony server:start`
   - c) `php bin/console server:start`

5. **Quel est le rôle du Kernel dans Symfony ?**
   - a) Gérer les dépendances du projet.
   - b) Déclencher des actions en fonction des routes spécifiques.
   - c) Gérer la configuration de l'application.

6. **Quel est le point d'entrée (FrontController) du framework Symfony ?**
   - a) importmap.php
   - b) public/index.php
   - c) Kernel.php

7. **Quelle commande est utilisée pour créer un contrôleur automatiquement (maker) dans Symfony ?**
   - a) `php bin/console make:controller MyController`
   - b) `symfony generate:controller MyController`
   - c) `make:controller MyController`

8. **Quel moteur de template est généralement utilisé dans Symfony pour la gestion des vues ?**
   - a) Blade
   - b) Smarty
   - c) Twig

9. **Comment inclure un fichier dans un template Twig ?**
   - a) `{% include 'header.html.twig' %}`
   - b) `{{ include('header.html.twig') }}`
   - c) `{% import 'header.html.twig' as header %}`

10. **Quelle(s) commande(s) est/sont utilisée(s) pour installer Tailwind CSS dans un projet Symfony ?**
    - a) `composer require symfonycasts/tailwind-bundle`
    - b) `npm install tailwindcss`
    - c) `php bin/console tailwind:init`

## 2. Partie Model 

11. **Quel est le rôle d'un ORM dans un projet Symfony ?**
    - a) Gérer les dépendances du projet.
    - b) Faciliter l'interaction entre une application orientée objet et une base de données relationnelle.
    - c) Gérer la configuration de l'application.

12. **Quelle commande est utilisée pour installer les dépendances symfony/orm-pack et symfony/maker-bundle ?**
    - a) symfony new symfony/orm-pack 
      symfony new symfony/maker-bundle  
    - b) composer require symfony/orm-pack  
      composer require symfony/maker-bundle  
    - c) php bin/console symfony/orm-pack

13. **Quelle section du fichier .env doit être modifiée pour indiquer à Symfony la configuration de la base de données ?**

    - a) ###> symfony/database ###
    - b) ###> doctrine/doctrine-bundle ###
    - c) ###> symfony/orm ###

14. **Quelle commande est utilisée pour créer la base de données configurée dans Symfony ?**

    - a) php bin/console doctrine:create-database
    - b) php bin/console doctrine:database:create
    - c) php bin/console create-database

15. **Quelle commande est utilisée pour générer le fichier de migration après avoir créé une entité ?**

    - a) php bin/console make:migration
    - b) php bin/console generate:migration
    - c) php bin/console doctrine:generate:migration

16. **Quelle commande est utilisée pour appliquer les migrations et créer effectivement la table dans la base de données ?**

    - a) php bin/console doctrine:migration:execute
    - b) php bin/console doctrine:migrations:migrate
    - c) php bin/console apply:migrations

17. **Quelle commande est utilisée pour générer des données fictives avec les DataFixtures ?**

    - a) php bin/console doctrine:generate:fixtures
    - b) php bin/console doctrine:fixtures:load
    - c) php bin/console load:fixtures

18. **Quelle bibliothèque est utilisée pour générer des données fictives dans les DataFixtures ?**

    - a) FakerPHP/Faker
    - b) Symfony/Fixtures
    - c) Doctrine/Faker