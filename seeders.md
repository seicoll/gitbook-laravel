# Seeders (Llavors)

## Introducció

Laravel també facilita la inserció de **dades inicials o dades _llavor_** a la base de dades. Aquesta opció és molt útil per tenir dades de prova.

Els fitxers de **_llavors (seeders)_** es troben a la carpeta `database/seeds`. 

## Crear fitxers Seeder

Per generar un Seeder, executeu la comanda Artisan `make:seeder`. 

  `php artisan make:seeder UsersTableSeeder`

Per defecte Laravel inclou el fitxer `DatabaseSeeder` amb el següent contingut:

```php
<?php

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;

class DatabaseSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
       //...
    }
}
```


Una **classe Seeder** només conté un mètode per defecte: `run`. 

Aquest mètode es crida quan s'executa la comanda Artisan `db:seed`. 

Dins del mètode, podeu inserir dades a la vostra base de dades de vàries formes:
*  Utilitzar el constructor de consultes (**query builder**) per inserir dades manualment.
*  Utilitzar **Eloquent model factories**.

Com a exemple s'inserció de dades utilitzant **query builder**, modifiquem la classe predeterminada  `DatabaseSeeder` i afegim una instrucció d'inserció de la base de dades al mètode `run`:

```php
<?php

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;

class DatabaseSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        DB::table('users')->insert([
            'name' => str_random(10),
            'email' => str_random(10).'@gmail.com',
            'password' => bcrypt('secret'),
        ]);
    }
}
```


### Utilitzant Model Factories

Especificar manualment el valor de cada atribut per a cada seeder és laboriós.

Podeu utilitzar els **_model factories_** per generar grans quantitats de registres a la base de dades. 

Per a una millor organització, creem un fitxer de **factory** per a cada model fins la carpeta `database/factories`. 

**PostFactory.php**
```php
<?php
    use Faker\Generator as Faker;
    
    $factory->define(App\Post::class, function(Faker $faker) {

        $title = $faker->sentence;
        
        return[
            'title'=> $title,
            'slug' => str_slyg($title),
            'excerpt' => $faker->text(300),
            'body' => $faker->text(800)
        ];
    });
?>
```


El  Closure anterior rebrà una instància de la biblioteca **_Faker_** de PHP, que us permetrà generar diversos tipus de dades aleatòries per a la prova.

Una vegada que hàgiu definit el vostre factory **generem el seeder** amb la comanda:

  `php artisan make:seeder PostsTableSeeder`

I en el seeder podeu utilitzar la funció `factory()` per inserir registres a la vostra base de dades.

Per **exemple**, creem 300 posts:

```php
<?php

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;

class DatabaseSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        factory(App\Post::class, 300)->create();
    }
}
```

### Executant altres Seeders

A partir de la classe DatabaseSeeder, podem utilitzar el mètode `run` per executar altres classes seed (llavors), i així podrem controlar l'ordre del seeding (sembrat).

```php
<?php
/**
 * Run the database seeds.
 *
 * @return void
 */
public function run()
{
    $this->call([
        UsersTableSeeder::class,
        PostsTableSeeder::class,
        CommentsTableSeeder::class,
    ]);
}
?>
```

## Executar la inicialització de dades (seeders)

Una vegada hem fet els seeders, podem executar la següent comanda Artisan per a reconstruir completament la base de dades **executant totes les nostres migracions i seeders**.

  `php artisan migrate:refresh --seed`

## Referències

* **Documentació de Laravel:** [Seeding](https://laravel.com/docs/5.7/seeding)
