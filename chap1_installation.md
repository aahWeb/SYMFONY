# Installation

Pour utiliser Symfony il faut :

-  PHP 8.1 intl, pdo_mysql, xsl, amqp, gd, openssl, sodium ou plus & les extensions suivantes :
 curl et zip.

 *Dans votre configuration MAMP ou WAMP, cela devrait être le cas.*

Ouvrez un terminal et tapez la ligne de commande suivante pour voir les extensions de votre PHP :

```bash
php -m
```

- De manière optionelle vous pouvez installer la CLI de Symfony :

*Remarques : une CLI ou Command Line Interface, est une suite de programmes exécutables en ligne de commandes, écrit en PHP et permettant de créer des controller, model, view. Elle permet également le testing et le déploiement de l'application.*

- Pour Mac

```bash
curl -sS https://get.symfony.com/cli/installer | bash
```
Une fois la CLI de Symfony installée vous pouvez y accéder de manière gloable :

```bash
mv /Users/votre_nom_de_machine/.symfony/bin/symfony /usr/local/bin/symfony
```

*Voir sur cette page les autres options selon votre OS.*

[Dowload Symfony](https://symfony.com/download)

- Pour Windows utilisez scoop

```bash
scoop install symfony-cli
```

- Il faut également le gestionnaire de package PHP **composer**, voir l'installation directement sur le site de composer (rien de compliqué).

Composer doit-être installé et à jour.

- Mise à jour de composer

```bash
# mise à jour de composer
composer self-update
```

- Installation du projet 

Vous pouvez soit installer Symfony soit en microservice, soit en full.

Microservice est très adapté par exemple pour la création d'API (Application programming Interface).

Full correspond à une installation pour les Web App "traditionnelle".

Pour **découvrir Symfony**, nous allons faire les deux installations : **microservice** et **full**.

Vérifiez avant de continuer que votre système est correctement configuré avec la CLI de SF :

```bash
symfony check:requirements
```

## Installation 

Sur votre bureau dans un dossier **web-trainer** tapez dans la console la ligne de commande suivante :

```bash
symfony new web-trainer
```

Avec composer uniquement, vous pourvez taper la ligne de commande suivante ( dans le dossier web-trainer) :

```bash
composer create-project symfony/skeleton web-trainer
```

Vérifiez la configuration, placez-vous dans le dossier **web-trainer** et tapez la ligne de commande suivante (commandes SF) :

```bash
php bin/console about
```

Nous allons également voir toutes les commandes de la console disponibles pour une application.

**Remarque** : une commande de la console permet par exemple de créer (makers) un "controller" **automatiquement** dans l'application (création et import des classes directement dans le fichier). L'intérêt de créer un contrôleur, à l'aide d'une commande de la console est que Symfony **définit lui-même**  les dépendances SF du controller de SF :

```bash
php bin/console
```

Nous reviendrons sur l'utilisation de ces commandes ci-dessous.

Nous allons lancer le serveur de test Symfony, dans le dossier de notre application, tapez la ligne de code suivante, vous pouvez avant de la lancer obtenir sa documentation, voyez la première ci-dessous.

```bash
symfony help server:start
```

Pour lancer le serveur lui-même :

```bash
symfony server:start
```

Ouvrez également un autre terminal à côté pour que l'on puisse exécuter des commmandes de la console Symfony.

1. Le framework utilise comme point d'entrée (FrontController) : l'index.php dans le dossier public

1. Le Kernel, en fonction d'une route spécifique, déclenchera une autre action spécifique appelle d'une méthode ou action dans une classe le controller, qui orchestrera la réponse.

*Le router gère les actions/contrôleurs métiers, c'est lui qui fait ce mapping.*

1. Une réponse est retournée au client HTTP ( le navigateur par exemple).

## Présentation de la structure d'une App Symfony

- config/
*Vous permet de configurer l'application ... Par exemples : définition des routes, services ou packages installés.*

- src/
*Cet ici que vous écrivez le code de l'application que vous développerez.*

- templates/
*Toutes les vues HTML/JS seront développées dans ce dossier, avec twig par exemple.*

- bin/
*Tous les exécutables PHP seront placés dans ce dossier. Vous trouverez nottament la fameuse console de Symfony.*
- var/
*Les fichiers qui se trouvent dans ce dossier sont créés automatiquement, vous trouverez par exemple les fichiers de cache de l'application ainsi que ses logs.*

- vendor/
Ce dossier contient toutes les dépendances de votre application comme Symfony par exemple.

- public/
*Dans ce dossier est placé tous les fichiers accessibles publiquement assets, js et le point d'entrée de votra application l'index.php*

## Le projet fil rouge pour la semaine Web tainer

### Installation

Déjà vu plus haut.

### Création du contrôleur HomeController

Dans un Framework on utilise la ligne de commande (CLI) pour créer les classes métiers qui dépendantes du Framework. Voici les commandes utiles pour créer un contrôleur avec Symfony.

Comme nous utilisons l'option **microservice** pour découvrir Symfony (installation not full), vous n'avez pas de commande maker, pour l'instant, permettant de créer automatiquement un contrôleur.

- Installez dans SF à l'aide de la CLI et en ligne de commande ce maker, il s'ajoutera aux commandes de la CLI SF

```bash
symfony composer req maker --dev
```

Listez dans la console maintenant ces dépendances.

```bash
symfony console list make
```

### Installation de Twig moteur de template

Installez maintenant **le moteur de template Twig**, il permet de gérer les vues HTML de manière dynamique ( méta-langage Twig ou moteur de template).

```bash
composer require twig
```

**Remarque** : vous pouvez également désinstaller un composant. Par exemple si vous souhaitez désinstaller Twig vous taperez :

```bash
composer remove twig
```

Un dernier point pour Twig, vous pouvez vérifier la configuration de Twig pour votre application à l'aide de la commande suivante :

```bash
 php bin/console debug:config twig
 ```

 Pour la gestion moderne des JS, CSS et autres assets on installera **AssetMapper**, un dossier assets sera créé à la racine du projet.

 ```bash
 composer require symfony/asset-mapper symfony/asset symfony/twig-pack
 ```

 Dans vos page HTML vous utiliserez alors la syntaxe suivante pour liées vos images, JS ou CSS ( nous allons mettre cela en place plus loin dans le projet fil rouge).

 ```html
{% block javascripts %}
    {{ importmap('app') }}
{% endblock %}
```

Remarques sur AssetMapper, quelques commandes :

1. pour la production, il faudra penser à **builder** vos assets (pas maintenant) :

```bash
php bin/console asset-map:compile
```

1. Pour voir le mapping de vos dépendances avec vos assets

```bash
php bin/console debug:asset-map
```

1. Si vous changez d'ordinateur pensez à ré-installer vos dépendances (assets)

```bash
php bin/console importmap:install
```

### Création du controller HomeController

Deux syntaxes, si vous appelez Home votre controller SF vous nommera automatiquement la classe **HomeController**, voyez également, si twig est installé, le dossier **home** sera également automatiquement créer dans le dossier **templates**.

Vous deux commandes pour créer un controller :

```bash
symfony console make:controller Home
# php bin/console make:controller Home 
 ```

 Symfony crée un contrôleur, en utilisant les routes de type **attribut** ( du pur PHP ). Ouvrez le dossier **src/Controller** dans le projet. Vous trouverez le contrôleur **HomeController**. 

 Notez que la route est ici **/home** (voir les attributs de la classe), elle est crée en fonction du nom du controller.

```php
<?php
namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotation\Route;

class HomeController extends AbstractController
{
    #[Route('/home', name: 'app_home')]
    public function index(): Response
    {
        // SF utilise le templace index.html.twig pour construire la vue
        return $this->render('home/index.html.twig', [
            'title' => 'HomeController', // tableau associatif pour passer des valeurs à la vue
        ]);
    }
}
```

Si votre serveur de test est lancé (**symfony server:start**), testez la route suivante /home, vous devriez voir la page Twig que nous venons de créer (vérifiez le port, il correspondre à votre serveur de tests).

```txt
http://127.0.0.1:8000/home
```

Les templates se trouvent dans les dossiers suivants :

```txt
templates/
    home/
        index.html.twig
    base.html.twig
```

Le layout (modèle) **base.html.twig** est un template que les vues composites, comme **index.html.twig**, hériteront. Cela permet de "factoriser" du code qui se répète dans toutes les pages.

## 01 Exercice duck

Mettez un petit canard dans la page d'accueil.

1. Vérifiez que AssetMapper est installé.
1. Vous avez un dossier assets
1. Créez le dossier images
1. Placez l'image dans ce dossier
1. Dans le code du HTML écrivez ce qui suit pour télécharger l'image dans la vue

```html
<!-- si le nom de votre image est duck.png -->
<img src="{{ asset('images/duck.png') }}">
```

## 02 Exercice Tailwindcss

1. Installation de Tailwindcss (framework CSS), dans le projet Web trainer

```bash
composer require symfonycasts/tailwind-bundle
php bin/console tailwind:init

# build and watch tailwind
php bin/console tailwind:build --watch
```

1. Configuration de Tailwind pour l'avoir au démarrage dans votre serveur de test ( CLI server start)

Créez le fichier .symfony.local.yaml à la racine du projet et mettez le code suivant, redémarrez SF, vous avez maintenant le watch de Tailwind en place dans le projet.

```yaml
# .symfony.local.yaml
workers:
    tailwind:
        cmd: ['symfony', 'console', 'tailwind:build', '--watch']
```

## 03 Exercice Wireframe page d'accueil

Vous allez réaliser une page sur deux colonnes en utilisant **Tailwindcss** ou vos propres framework css, voyez le Wireframe ci-dessous.

1. Dans le cas où vous voulez changer de Framework CSS voyez la documentation en ligne : [assetmapper](https://symfony.com/doc/current/frontend/asset_mapper.html)

1. Si vous utilisez Tailwindcss utilisez la documentation suivante : [tailwindcss](https://tailwindcss.com/docs/installation)

### Wireframe Home page 