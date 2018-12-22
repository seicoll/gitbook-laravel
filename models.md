Models
Laravel inclou el seu propi sistema ORM anomenat Eloquent que ens proporciona una manera d'interactuar amb la base de dades.
Un ORM (Object-Relational mapping) és un tècnica de programació per convertir dades entre un llenguatge de programació orientat a objectes i una base de dades relacional.
Per cada taula de la base de dades hem de definir el seu corresponent model que s'utilitzarà per interactuar des de codi amb la taula.
En Laravel, els models es guarden a la carpeta app.
Per definir un model que utilitzi Eloquent només cal crear una classe que hereti de la classe Model.
<?php
namespace App;

use Illuminate\Database\Eloquent\Model;

class Article extends Model
{
    //...
}
Tot i així, és més fàcil i ràpid crear models utilitzant la comanda make:model de Artisan:
php artisan make:model Article
o bé

php artisan make:model Acticle -a
-a, --all Genera la migració, factory i controller per aquest model.
En la instal·lació inicial de Laravel ja tenim definit un Model anomenat User al fitxer app/User.php.