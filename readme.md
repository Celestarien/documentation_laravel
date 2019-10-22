# Documentation Laravel

![Logo Laravel](https://miro.medium.com/max/1024/1*IQ9laxKlEm6CodFOZIbgLQ.png)

## 1 - Installation


* Requis :
    * Minimum [PHP](https://www.php.net/downloads.php) => 7.2.0
    * BCMath PHP Extension
    * Ctype PHP Extension
    * JSON PHP Extension
    * Mbstring PHP Extension
    * OpenSSL PHP Extension
    * PDO PHP Extension
    * Tokenizer PHP Extension
    * XML PHP Extension
    * [Composer](https://getcomposer.org/)

* Laravel installer :
    * Ouvrir un terminal et exécuter : `composer global require laravel/installer`
    * Vérifier si dans $PATH la variable d'environnement Laravel existe sinon ajoutez la

## 2 - Lancement d'un nouveau projet

* Créer un dossier de travail qui portera le nom que vous souhaitez
    * #### ⚠️ Attention : Le dossier doit être placé là où vous avez des droits (exemple: Bureau)

* Ouvrir un terminal et exécutez les commandes suivantes :
    * Pour créer un nouveau projet : `laravel new NOM_DU_PROJET`
    * Lancer le serveur de developpement PHP avec : `php artisan serve`
        * Le serveur tourne sur : http://localhost:8000

## 3 - Les droits

* Fichier de configuration :
    * Tous les fichiers de configuration du framework Laravel sont stockés dans le répertoire `config`.
    * Il est possible que vous devrez peut-être configurer certaines autorisations. Les répertoires de `storage` doivent être accessibles en écriture par votre serveur Web, sinon Laravel ne fonctionnera pas.
    * Dans le cas de `Homestead` (une machine virtuelle), ces dernières sont déjà définies.

* Votre application contient une clé, pour la générer utilisez la commande : `php artisan key:generate`
    * Cette clé sera stocké dans le fichier d'environnement `.env`

* Désormais on peut créer, modifier ou encore supprimer des pages web dans le dossier `laravel\resources\views` 

## 4 - Homestead

* Installer Homestead avec la commande : `composer require laravel/homestead --dev`

* Installer [Vagrant](https://www.vagrantup.com/downloads.html)

* Exécuter la commande : `vagrant box add laravel/homestead`

* Utiliser "provider" avec la commande : `provider: virtualbox`
    * Si vous utilisez un autre hyperviseur que virtualbox modifier la commande :
        * `provider: vmware_fusion`
        * `provider: vmware_workstation`
        * `provider: parallels`
        * `provider: hyperv`

* Afin de générer le fichier `Vagrantfile` à la racine de votre projet, utiliser la commande make :
    * Sous Windows :
        * `vendor\\bin\\homestead make`
    * Sous Linux & Mac :
        * `php vendor/bin/homestead make`

* Puis exécuter `vagrant up`


## 5 - Les routes avec Laravel

### **Qu'est-ce qu'une route ?**

Ce sont des instances de la classe et contiennent les en-têtes appropriés nécessaires pour rediriger l'utilisateur vers une autre URL.

```h
Route::get('dashboard', function () {
    return redirect('home/dashboard');
});
```
Vous pouvez tout à fait rediriger un utilisateur vers son emplacement précédent, par exemple lorsqu'un formulaire soumis est invalide :

```h
Route::post('user/profile', function () {
    // Code

    return back()->withInput();
});
```

Vous pouvez aussi rediriger un utilisateur vers un itinéraire nommé parce que la commande `redirect` vous permet d'appeler n'importe quelle méthode de l' instance, exemple :

```h
return redirect()->route('login');
```

Si vous le souhaitez vous pouvez aussi faire une redirection avec action :
```h
return redirect()->action('HomeController@index');
```

### **Existe-t-il des routes "privés" ?**

Grâce à la méthode `middleware` nous pouvons effectivement créer spécifique à un groupe de personne :

```h
Route::middleware(['first', 'second'])->group(function () {
    Route::get('/', function () {
        // Uses first & second Middleware
    });

    Route::get('user/profile', function () {
        // Uses first & second Middleware
    });
});
```

Nous pouvons aussi utiliser une autre méthode dont le nom est `namespace` :

```h
Route::namespace('Admin')->group(function () {
    // Controllers Within The "App\Http\Controllers\Admin" Namespace
});
```

### 🔆Bonus

Il est possible de changer la page 404 avec la méthode `fallback` :

```
Route::fallback(function () {

});
```