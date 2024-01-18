## Partie 1

**Réponses:**
1. b) intl, pdo_mysql, xsl, amqp, gd, openssl, sodium
2. b) `curl -sS https://get.symfony.com/cli/installer | bash`
3. b) `composer create-project symfony/skeleton my_project`
4. b) `symfony server:start`
5. b) Déclencher des actions en fonction des routes spécifiques.
6. b) index.php
7. a) `php bin/console make:controller MyController`
8. c) Twig
9. a) `{% include 'header.html.twig' %}`
10. a) `composer require symfonycasts/tailwind-bundle`


## Parie 2

Quel est le rôle d'un ORM dans un projet Symfony ?

Réponse correcte : b) Faciliter l'interaction entre une application orientée objet et une base de données relationnelle.
Quelle commande est utilisée pour installer les dépendances symfony/orm-pack et symfony/maker-bundle ?

Réponse correcte : a) composer require symfony/orm-pack
Quelle section du fichier .env doit être modifiée pour indiquer à Symfony la configuration de la base de données ?

Réponse correcte : b) ###> doctrine/doctrine-bundle ###
Quelle commande est utilisée pour créer la base de données configurée dans Symfony ?

Réponse correcte : b) php bin/console doctrine:database:create
Quelle commande est utilisée pour générer le fichier de migration après avoir créé une entité ?

Réponse correcte : a) php bin/console make:migration
Quelle commande est utilisée pour appliquer les migrations et créer effectivement la table dans la base de données ?

Réponse correcte : b) php bin/console doctrine:migrations:migrate
Quelle commande est utilisée pour générer des données fictives avec les DataFixtures ?

Réponse correcte : b) php bin/console doctrine:fixtures:load
Quelle bibliothèque est utilisée pour générer des données fictives dans les DataFixtures ?

Réponse correcte : a) FakerPHP/Faker