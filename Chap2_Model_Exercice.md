# 00_Exercice Configuration et creation de notre première base de données

Nous aurons besoin premièrement de **doctrine** qui est un **ORM (Object Relational Mapper)**.

> **Un ORM est un outil qui permet de faciliter l'interaction entre une application orientée objet et une base de données relationnelle**. Il résout le problème de la disparité entre le modèle de données orienté objet utilisé dans la programmation et le modèle de données relationnel utilisé dans les bases de données.  
**Un ORM nous permet de nous faire une représentation orienté objet d'une base de donnée relationnel au sein de notre programme**.

## Ajouter la dépendance [symfony/orm-pack](https://packagist.org/packages/symfony/orm-pack) et [symfony/maker-bundle](https://packagist.org/packages/symfony/maker-bundle)

```shell
composer require symfony/orm-pack
composer require symfony/maker-bundle
```  
Vous pouvez voir les dépendences déjà installé sur votre projet symfony dans le fichier **composer.json**.

## Configuration du ficher **.env**.

Afin de pouvoir créer notre base de données, nous devons d'abort indiquer à notre projet symfony où il peut déjà la trouver.

Dans votre fichier **.env**, trouver la ligne commenté `###> doctrine/doctrine-bundle ###`. En dessous il y a plusieur ligne commencant par `DATABASE_URL="`, vous reconnaitrez des url vers des bases de données; Commenté celles qui ne vous interesent pas et décommenté l'url qui correspond le mieux à votre base de données.  
Il faudra néanmoins modifier cette ligne d'instruction;
>DATABASE_URL="mysql://**mot_de_passe**:**nom_utilisateur**@127.0.0.1:3306/?serverVersion=**version_de_mysql**&charset=utf8mb4"

Pour trouver la version de votre application MySQL, vous pouvez vous y connécter et lancer la commande `status`; Parmis les information affiché vous trouverez la version de votre server.

## Création de la base de données de votre application

Vous pourriez utiliser la commande `CREATE DATABASES db_name;` pour créer directement votre base de données depuis celle-ci, mais pourquoi s'embêter à la créer manuellement alors que nous pouvons la créer automatiquement ?
Nous venons de configurer notre application afin qu'elle puisse communiquer avec MySQL.
Je vous invite à tapez la commande `php bin/console list doctrine:database` pour voir les commandes, maintenant disponible, concernant les bases de données :

```txt
Available commands for the "doctrine:database" namespace:
  doctrine:database:create  Creates the configured database
  doctrine:database:drop    Drops the configured database
```

Vous pouvez voir tout un pannel de nouvelles commandes disponiblent avec doctrine, en entrant la commande `php bin/console list doctrine`.

:rocket: On sait maintenant quelle commande nous pouvons taper pour créer notre base de données.
`php bin/console doctrine:database:create`

## Création de notre première table (ou plutôt de notre premier "entity class")

Lien vers la doc : [Creating an Entity Class](https://symfony.com/doc/current/doctrine.html#creating-an-entity-class)
Il ne faut pas hésiter à aller vers la [doc de symfony](https://symfony.com), qui est en générale à jour !

Et oui, on travaille avec un **ORM**, notre **table** dans notre base de données **est représenté par une classe dans notre application symfony**.

Avant de créer notre **table**, nous devons créer une **entity**, pour ça, il faut entrer dans notre terminale la commande suivante et nous laisser guider :

```shell
php bin/console make:entity
```
Une série de question nous sera posées, si vous ne savez pas y répondre, vous pouvez toujours entrer `?` pour voir les options disponiblent.

>Si vous avez oubliez une propriété, vous pouvez réappeler cette commande avec le nom de l'entité concernée.

Vous vous retrouvez maintenant avec un nouveau fichier php dans votre dossier **/src/entity/**, il s'agit de la représentation de notre future **table** (qui sera dans notre base de données).

Non, ça n'est toujours pas maintenant qu'on vas créer la base de données, avant ça, il faut générer le fichier de migration, un fichier PHP qui comporte les requêtes SQL qui nous servirons ...à créer notre **table ainsi que ses champs**.

Générer le fichier de migration :
```shell
php bin/console make:migration
```
Si vous avez bien suivi les étapes, un dossier **migrations** est apparu dans votre arborecsence. Il à était créer à l'ajout de la dépendence [**symfony/orm-pack**](https://packagist.org/packages/symfony/orm-pack). Et vous y trouverez le fichier de migration nouvellement créer.

> Maintenant, si vous le souhaitez, vous pouvez jeter un œuil à vos tables dans votre base de données avant et aprés la commande suivante.
Il faut faire un `USE nom_base_de_données` et puis `SHOW TABLES` pour afficher les tables.

Vous l'avez devinez, il est temps de créer notre **table**.

Créer la table dans notre base de donnée :
```shell
php bin/console doctrine:migrations:migrate
```

> [!WARNING]  
> Attention, si vous modifier votre entité, vous devrez refaire une migration !

## Ajouter des données d'exemples

Nous allons maintenant ajouter des données d'exemples dans notre table avec [symfony/orm-fixtures](https://symfony.com/bundles/DoctrineFixturesBundle/current/index.html).

```shell
composer require orm-fixtures --dev
```

Et pour générer des données fictives, on va installer [FakerPHP/Faker](https://fakerphp.github.io/) dans nos dépendences de développement.

```shell
composer require fakerphp/faker --dev
```

> [!TIP]
> Pour placer une dépendence dans les dépendence de développement, on utilise l'argument `--dev`.

À ce stade, nous avons un fichier **DataFixtures** dans lequel nous retrouvons un fichier **AppFixtures.php**.

```txt
dev-trainer/
└─ src/
    └─DataFixtures/
        └─AppFixtures.php
```

On vas pouvoir mettre notre première donnée en le configurant

```php
<?php

namespace App\DataFixtures;

use App\Entity\Trainers;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Persistence\ObjectManager;

class AppFixtures extends Fixture
{
    public function load(ObjectManager $manager): void
    {
        // $product = new Product();
        // $manager->persist($product);

        for($i = 0; $i < 10; $i++) { // Génère 10 fixtures
            $trainer = new Trainers(); // On instancie notre objet
            $trainer
                ->setName('Jessica')
                ->setEmail('jessica@example.com')
                ->setBio('Trainer chez DevTrainer depuis ...');
            
            // On fait persisté la donnée
            $manager->persist($trainer);
        }

        $manager->flush(); // Met à jour la base de donnée avec ces nouvelles donnée
    }
}
```

Maintenant il est temps de générer notre première fixture avec :

```shell
php bin/console doctrine:fixtures:load
```

Passons à FakerPHP, je vous invite à remplir votre base de données avec 10 trainers (vous allez devoir boucler quelque part).  
On part du code suivant : 

```php
use Faker\Factory;
use Faker\Generator;

class AppFixtures extends Fixture
{
    private Generator $faker;

    public function __construct()
    {
        // Créer un générateur que vous allez pouvoir réutiliser
        $this->faker = Factory::create('fr-FR');
    }
    public function load(ObjectManager $manager): void
    {
        // ...code

        $manager->flush();
    }
}
```
# 01_Exercice créer une entité foo

Avec ce que l'on a vue créer une entité foo dans lequel on retrouve les champs :
- title
- text
- creationDate

# 02_Exercice afficher les données
Avant de commencer l'exercice, je vous propose un petit guide pour configurer VSCode pour les fichier Twig, afin de gagner en confort dans le développement de notre application : [Twig + Tailwind: configuration  VSCode](https://www.notion.so/mathieu-constantin/Twig-Tailwind-configuration-VSCode-bf3e2aaa6f984515a4af0f8583990bfa?pvs=4).

Pour récupérer nos données, nous devons indiquer le namespace du repository avec le mot-clé `use`, utiliser le repository et lui appliquer la méthode `findAll()` pour obtenir une liste de nos données.

```php
<?php

namespace App\Controller;

// Namespace de TrainersRepository
use App\Repository\TrainersRepository;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotation\Route;

class TrainersController extends AbstractController
{
    #[Route('/trainers', name: 'app_trainers')]
    public function index(TrainersRepository $trainersRepository): Response
    {
        $trainers = $trainersRepository->findAll();
        dd($trainers);

        return $this->render('trainers/index.html.twig', [
            'controller_name' => 'TrainersController',
        ]);
    }
}
```

À partir de là, je vous laisse afficher la suite dans twig.

