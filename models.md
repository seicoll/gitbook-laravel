<!-- notoc -->

# Models

Laravel inclou el seu propi sistema **ORM** anomenat **_Eloquent_** que ens proporciona una manera d'interactuar amb la base de dades.

> Un **ORM (Object-Relational mapping)** és un tècnica de programació per convertir dades entre un llenguatge de programació orientat a objectes i una base de dades relacional.

Amb **_Eloquent_** podrem accedir als registres de la base de dades com si fossin **objectes** de PHP sense haver d'executar sentències SQL per obtenir les dades.

**Per cada taula de la base de dades hem de definir el seu corresponent model** que s'utilitzarà per interactuar des de codi amb la taula.

En Laravel, els **models** es guarden a la carpeta `app`.

Per definir un model que utilitzi **_Eloquent_** només cal crear una classe que hereti de la classe `Model`.

```php
<?php
namespace App;

use Illuminate\Database\Eloquent\Model;

class Article extends Model
{
    //...
}
```

Tot i així, és més fàcil i ràpid crear models utilitzant la comanda de Artisan `make:model`:

`php artisan make:model Article`

o bé

`php artisan make:model Acticle -a`

* `-a, --all` Genera la migració, factory i controller per aquest model.

En la instal·lació inicial de Laravel ja tenim definit un Model anomenat `User` al fitxer `app/User.php`.

## Referències

* **Llibre Lavarel 5 (Antonio Javier Gallego):** 
[Eloquent ORM](https://ajgallego.gitbooks.io/laravel-5/content/base_de_datos_eloquent_orm.html)
