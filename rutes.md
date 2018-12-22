# Rutes

> Les **rutes** són les urls disponibles en la nostra aplicació.

Es defineixen al fitxer l'arxiu de rutes situat a `routes/web.php`.

Per exemple:
* Si nosaltres demanem la ruta `/productes` volem que ens llisti tots els productes.
* Si volem veure el producte 1, tindrem una ruta com per exemple `/producte/1`.

> Qualsevol ruta no definida en aquest fitxer no serà vàlida, generat una excepció (el que retornarà un error 404).

## Rutes bàsiques

Vegem l'arxiu de rutes situat a `routes/web.php`:

```php
<?php

/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
| Here is where you can register web routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| contains the "web" middleware group. Now create something great!
|
*/

Route::get('/', function () {
    return view('welcome');
});
?>
```


* Aquest codi s'executerà quan es realitzi una petició tipus GET a la ruta arrel de la nostra aplicació.

* Veiem que només hi ha una **ruta (url)** definida, que:
  * Defineix la URL de la petició que és l'arrel '/'
  * Retorna una vista anomenada _welcome_.


* També indiquen el **mètode** amb el qual s'ha de fer aquesta petició, en aquest cas GET.
Els dos mètodes més utilitzats són les peticions tipus GET i tipus POST.
  * És important indicar que si es realitza una petició tipus POST o d'un altre tipus que no sigui GET a aquesta direcció es retornaria un error ja que aquesta ruta no està definida.


* Totes les vistes són al directori `resources/views`.
  * Si anem al directori views veiem que hi ha un arxiu anomenat `welcome.blade.php`.
  * Quan cridem a la vista amb el mètode `view('welcome')` no cal posar-li l'extensió.
  * Aquesta vista conté el Blade de la pàgina que veiem quan anem a l'arrel del**


## Veure rutes definides

Podem **veure totes les rutes** que tenim definides utilitzant la comanda Artisan:

`php artisan route:list`

Ens mostrarà una taula amb el mètode, la direcció, l'acció i els filtres definits per a totes les rutes:

![](/assets/laravel-route-list.png)

## Rutes amb paràmetres

Si volem afegir paràmetres a una ruta simplement els hem d'indicar entre claus {} a continuació de la ruta:

```php
<?php
   Route::get('inici/{nom}', function ($nom) {
       return "Benvingut $nom";
   });
?>
```

* En el cas anterior el paràmetre és obligatori per tant si no s'especifica cap `nom` es produiria un error.

També es poden enviar varis paràmetres:

```php
<?php
   Route::get('agenda/{mes}/{any}', function($mes, $any) {
       return "Mostrant l'agenda de $mes de $any";
   });
?>
```

## Rutes amb paràmetres opcionals

Podem definir rutes amb **paràmetres opcionals** com:

```
example.com/categoria/php
example.com/categoria/php/2
```

A vegades s'especifica la pàgina de la categoria i altres no simulant el funcionament d'un paginador.

En Laravel, els **paràmetres opcionals** s'indiquen amb un interrogant **?** al final.

```php
<?php
   Route::get('categoria/{categoria}/{pagina?}', function ($categoria, $pagina = 1) {
       return "Mostrant categoria $categoria i pàgina $pagina";
   });
?>
```

> Alerta! Cal posar un **valor per defecte** als paràmetres opcionals.

## Referències

* **Documentació de Laravel:** [Routing](https://laravel.com/docs/5.7/routing)
* **Llibre Lavarel 5 (Antonio Javier Gallego):** [Rutas](https://ajgallego.gitbooks.io/laravel-5/content/capitulo_1_rutas.html)