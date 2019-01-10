# Controladors

En Laravel, els **controladors** es guarden a la carpeta `app/Http/Controllers`. I aquí es poden organitzar en subcarpetes.

Codi d'un controlador bàsic:

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

## Generar controladors automàticament amb Artisan

Crear controladors és una tasca repetitiva en Laravel, per això existeix una comanda
artisan per crear-los automàticament.

`php artisan make:controller CategoriasController`

## Referències

* **Llibre Lavarel 5 (Antonio Javier Gallego):** [Controladores](https://ajgallego.gitbooks.io/laravel-5/content/capitulo_2_controladores.html)