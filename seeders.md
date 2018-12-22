Seeders (Llavors)

Introducció
Laravel també facilita la inserció de dades inicials o dades llavor a la base de dades. Aquesta opció és molt útil per tenir dades de prova.
Els fitxers de llavors (seeders) es troben a la carpeta database/seeds.
Crear fitxers Seeder
Per generar un Seeder, executeu la comanda Artisan make:seeder.
php artisan make:seeder UsersTableSeeder
Per defecte Laravel inclou el fitxer DatabaseSeeder amb el següent contingut:
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
Una classe Seeder només conté un mètode per defecte: run.
Aquest mètode es crida quan s'executa la comanda Artisan db:seed.
Dins del mètode, podeu inserir dades a la vostra base de dades de vàries formes:
Utilitzar el constructor de consultes (query builder) per inserir dades manualment.
Utilitzar Eloquent model factories.
Com a exemple s'inserció de dades utilitzant query builder, modifiquem la classe predeterminada DatabaseSeeder i afegim una instrucció d'inserció de la base de dades al mètode run:
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
Utilitzant Model Factories
PostFactory.php
<?php
use Faker\Generator as Faker;

$factory->define(App\Post::class, function(Faker $faker){
    $title = $faker->sentence;
    return[
        'title'=> $title,
        'slug' => str_slyg($title),
        'excerpt' => $faker->text(300),
        'body' => $faker->text(800)
    ];
}
?>
php artisan make:seeder PostsTableSeeder
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
Executant altres Seeders
A partir de la classe DatabaseSeeder, podem utilitzar el mètode run per executar altres classes seed (llavors), i així podrem controlar l'ordre del seeding (sembrat).
```php <?php /**
Run the database seeds. *
@return void */ public function run() { $this->call([
 UsersTableSeeder::class,
 PostsTableSeeder::class,
 CommentsTableSeeder::class,
]); } ?> ```php
Executar la inicialització de dades
Generem els 300 posts a la base de dades: php artisan migrate:refresh --seed
Referències
https://laravel.com/docs/5.7/seeding