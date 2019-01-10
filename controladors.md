# Controladors

## Introducció

> Recordem, que els **controladors** són els que han de contenir tota la lògica associada al processament d'una petició, encarregant-se de realitzar les consultes necessàries a la base de dades, de preparar les dades i de cridar a la vista corresponent amb aquestes dades.

En general, la forma recomanable de treballar serà **associar les rutes a un mètode d'un controlador**. 

Això ens permetrà separar millor el codi i crear classes (controladors) que agrupen tota la funcionalitat d'un determinat recurs. 

* Per exemple, podem crear un controlador per gestionar tota la lògica associada al control d'usuaris o qualsevol altre tipus de recurs.

## Controlador bàsic

En Laravel, els **controladors** es guarden en fitxers PHP a la carpeta `app/Http/Controllers`. I aquí es poden organitzar en subcarpetes.

Normalment se'ls afegeix el **sufix _Controller_**, per exemple `UserController.php`o `MoviesController.php`.

Codi d'un **controlador bàsic**:

```php
<?php
    namespace App\Http\Controllers;
    
    use App\Http\Controllers\Controller;
    
    class ArticulosController extends Controller
    //El controlador extén la classe base Controller de Laravel
    {
        public function ver($id)
        {
            return view('articulos.ver', ['id' => $id]);
        }
    }
?>
```

## Cridar un controlador des del sistema de routing

Els controladors els cridarem, normalment, des del sistema de routing.

Indicarem el nom del controlador i l'acció (mètode) que s'ha d'executar.

```php
<?php
    Route::get('articulos/{id}','ArticulosController@ver');
?>
```

* En aquest exemple, la ruta té un paràmetre que serà passat al mètode `ver()` del `ArticulosController`.

## Crear nous controladors automàticament

Crear controladors és una tasca repetitiva en Laravel, per això existeix una comanda Artisan per **crear-los automàticament**.

`php artisan make:controller ArticulosController`

Aquesta comanda crearà el controlador `ArticulosController` dins de la carpeta `app/Http/Controllers` i el completarà amb el codi bàsic que hem vist abans.

## Referències

* **Llibre Lavarel 5 (Antonio Javier Gallego):** [Controladores](https://ajgallego.gitbooks.io/laravel-5/content/capitulo_2_controladores.html)