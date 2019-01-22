# Migracions

> Les **migracions** permeten treballar sobre una base de dades creant taules, afegint i modificant camps, mantenint un històric dels canvis realitzats i de l'estat actual de la base de dades.

## Taula de migracions

Per poder començar a treballar amb les migracions és necessari en primer lloc **crear la taula de migracions**. 

Per això hem d'executar la següent comanda de Artisan:

`php artisan migrate:install`

Si ens dóna algun error haurem de revisar la configuració que hem posat de la base de dades i si hem creat la base de dades amb el nom, usuari i contrasenya indicat.

Si tot funciona correctament podem anar al navegador i accedir de nou a la nostra base de dades amb PHPMyAdmin, podrem veure que se'ns haurà creat la taula **_migrations_**. 

## Crear una nova migració

Per a crear una nova migració s'utilitza la comanda de Artisan `make:migration`, al qual li passarem el nom del fitxer a crear i el nom de la taula:

`php artisan make:migration create_categories_table --create=categories` 

`--create=categories` indica el nom de la taula a la base de dades.

Això ens crearà un fitxer de migració a la carpeta `database/migrations` amb el nom `<TIMESTAMP>_create_categories_table.php`. 

Al afegir un _**timestamp**_ a les migracions, el sistema sap l'ordre en el què ha d'executar-les (o desfer-les).


## Estructura d'una migració

El fitxer o classe PHP generada per una migració sempre té una estructura similar a la següent:

```php
<?php

use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateUsersTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        //
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        //
    }
}
```

En el mètode `up`és on tindrem crear o modificar la taula, i en el mètode `down` haurem de desfer els canvis que es facin al `up` (eliminar la taula o eliminar el camp que s'hagi afegit). Això ens permetrà poder anar afegint i eliminant canvis sobre la base de dades i tenir un control o històric d'aquests canvis.


## Crear i esborrar una taula

Un cop creada una migració hem de completar els seus mètodes `up`i `down`per a indicar la taula que volem crear o el camp que volem modificar.

En el mètode `down`sempre haurem d'afegir l'operació inversa, eliminar la taula que s'ha creat en el mètode `up`o eliminar la columna que s'ha afegit. Això ens permetrà desfer migracions deixant la base de dades en el mateix estat en què es trobaven abans que s'afegissin.


Per especificar la taula a crear o modificar, així com les columnes i tipus de dades de les mateixes, s'utilitza la classe _Schema_.

Per afegir una nova taula a la base de dades:

```php
Schema::create('users', function (Blueprint $table) {
    $table->increments('id');
});
```

A la secció `down`de la migració haurem d'eliminar la taula que hem creat, per això farem servir algun dels següents mètodes:

```php
Schema::drop('users');

Schema::dropIfExists('users');
```

## Afegir columnes a un taula

El constructor `Schema::create` rep com a segon paràmetre una funció que ens permet especificar les columnes que ha de tenir la taula. En aquesta funció podem anar afegint tots els camps que vulguem, indicant per a cadascun d'ells el seu tipus i nom:

```php
Schema::create('users', function($table)
{
    $table->increments('id');
    $table->string('username');
    $table->smallInteger('vots');
    $table->boolean('confirmat')->default(false);
    $table->timestamps();
});
```

### Tipus de camps disponibles

**Més informació:** [https://laravel.com/docs/5.7/migrations#creating-columns](https://laravel.com/docs/5.7/migrations#creating-columns)
  
### Modificadors de columnes

A més dels tipus de columnes, hi ha diversos **_modificadors_** de columna que podeu utilitzar quan s'afegeix una columna a la taula de la base de dades. 

Per exemple, per fer que la columna "nul·la", podeu utilitzar el mètode `nullable`:

```php
Schema::table('users', function (Blueprint $table) {
    $table->string('email')->nullable();
});
```

**Més informació:** [https://laravel.com/docs/5.7/migrations#column-modifiers](https://laravel.com/docs/5.7/migrations#column-modifiers)

## Afegir índexs
https://ajgallego.gitbooks.io/laravel-5/content/base_de_datos_schema_builder.html

## Afegir claus foranies
https://ajgallego.gitbooks.io/laravel-5/content/base_de_datos_schema_builder.html

## Executar migracions

Després de crear una migració i de definir els camps de la taula hem de **llançar la migració** amb la següent comanda:

  `php artisan migrate`

Aquesta comanda s'aplicarà la migració sobre la base de dades. Si hi hagués més d'una migració pendent, s'executaran totes. Per a cada migració es cridarà al seu mètode `up` perquè creï o modifiqui la base de dades. 

Posteriorment en cas que vulguem **desfer els canvis** podrem executar:

  `php artisan migrate:rollback`

 O si volem **desfer totes les migracions**:
 
  `php artisan migrate:reset`

Una comanda interessant quan estem desenvolupant un nou lloc web és `migrate:refresh`, que **desfarà tots els canvis i tornar a aplicar les migracions**:

  `php artisan migrate:refresh`

A més si volem **comprovar l'estat de les migracions**, per veure les que ja estan realitzades i les que queden pendents, podem executar:

  `php artisan migrate:status`


## Referències

* **Llibre Lavarel 5 (Antonio Javier Gallego):** 
[Migraciones](https://ajgallego.gitbooks.io/laravel-5/content/base_de_datos_migraciones.html)