# Middlewares (Filtres)

> Els **Middleware** són un mecanisme proporcionat per Laravel per **filtrar les peticions HTTP** que es realitzen a una aplicació. 

Un filtre o **_middleware_** es defineix com una classe PHP emmagatzemada en un fitxer dins de la carpeta `app/Http/Middleware`. 

Cada **_middleware_** s'encarregarà d'aplicar un tipus concret de filtre i de decidir què fer amb la petició realitzada: 
  * permetre la seva execució 
  * no permetre-la donant un error o redireccionar a una altra pàgina

Ens podem imaginar els middlewares com portes per les quals ha de passar la petició HTTP abans de poder accedir al controlador.

## Midlewares per defecte

**Laravel** inclou diversos filtres per defecte, un d'ells és l'encarregat de realitzar l'**autenticació dels usuaris**. 

Aquest middleware el podem aplicar sobre una ruta, un conjunt de rutes o sobre un controlador en concret. 

Aquest middleware s'encarregarà de filtrar les peticions a aquestes rutes: 
  * en cas d'estar loguejat i tenir permisos d'accés li permetrà continuar amb la petició
  * en cas de no estar autenticat el redireccionarà al formulari de login

Laravel inclou altres middleares que podem trobar a la carpeta `app/Http/Middleware`, els quals els podem modificar o ampliar la seva funcionalitat. 

## Definir un nou Middleware

A part dels middlewares que ja venen per defecte amb Laravel, podem crear els nostres propis middlewares.

Per crear un nou middleware podem utilitzar la comanda de Artisan:

`php artisan make:middelware MyMiddleware`

Aquesta comanda crearà la classe `MyMiddleware` dins de la carpeta `app/Http/Middleware` amb el següent contingut per defecte:

```php
<?php

namespace App\Http\Middleware;

use Closure;

class MyMiddleware
{
    /**
     * Handle an incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Closure  $next
     * @return mixed
     */
    public function handle($request, Closure $next)
    {
        return $next($request);
    }
}
```

El codi generat per Artisan ja ve preparat perquè puguem escriure directament la implementació del filtre a realitzar dins de la funció `handle`. 

Com podem veure, aquesta funció només inclou el valor de retorn amb una crida a `return $next($request);`, que el que fa és continuar amb la petició i executar el mètode que ha de processar-la. 

Com entrada la funció `handle`rep dos paràmetres:
  * `$request`: En la qual ens vénen tots els paràmetres d'entrada de la petició.
  * `$next:` El mètode o funció que ha de processar la petició.

Per exemple podríem crear un filtre que redirigeixi a l'home si l'usuari té menys de 18 anys i en un altre cas que li permeti accedir a la ruta:

```php
public function handle($request, Closure $next)
{
    if ($request->input('age') < 18) {
        return redirect('home');
    }

    return $next($request);
}
```

Com hem dit abans, **podem fer tres coses amb una petició**:
  * Si tot és correcte permetre que la petició continuï retornant: 
    
    `return $next($request);`

  * Realitzar una redirecció a una altra ruta per no permetre l'accés: 
    
    `return redirect('home');`

  * Llançar una excepció o cridar al mètode `abort` per a mostrar una pàgina d'error:
    
    `abort(403, 'Unauthorized action.');`
    
## Utilització del Middleware
  
Laravel permet la utilització de Middleware de **tres formes diferents**:
  * global
  * associat a rutes o grups de rutes
  * associat a un controlador o un mètode d'un controlador

En els tres casos serà necessari registrar primer el Middleware a la classe `app/Http/Kernel.php`.

### Middleware global

Per fer que un Middleware s'executi amb **totes les peticions HTTP** realitzades a una aplicació simplement l'hem de registrar a l'array `$middleware` definit en la classe `app/Http/Kernel.php`. 

Per exemple:

```php
protected $middleware = [
    \Illuminate\Foundation\Http\Middleware\CheckForMaintenanceMode::class,
    \Illuminate\Foundation\Http\Middleware\ValidatePostSize::class,
    \App\Http\Middleware\TrimStrings::class,
    \Illuminate\Foundation\Http\Middleware\ConvertEmptyStringsToNull::class,
    \App\Http\Middleware\TrustProxies::class,
    \App\Http\Middleware\MyMiddleware::class,
];
```

En aquest exemple hem registrat la classe `MyMiddleware` al final de l'array. Si volem que el nostre middleware s'executi abans que un altre filtre simplement haurem de col·locar-abans en la posició de l'array.

### Middleware associat a rutes

En el cas de voler que el nostre middleware **s'executi només quan es cridi a una ruta o un grup de rutes** també haurem de registrar-lo en el fitxer `app/Http/Kernel.php`, però a l'array `$routeMiddleware`. 

A l'afegir-lo a aquest array a més haurem de assignar-li un nom o clau, que serà el que després utilitzarem associar amb una ruta.

En primer lloc afegim el nostre filtre a l'array i li assignem el nom "es_major_d_edad":

```php
protected $routeMiddleware = [
    'auth' => \Illuminate\Auth\Middleware\Authenticate::class,
    'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
    'bindings' => \Illuminate\Routing\Middleware\SubstituteBindings::class,
    'can' => \Illuminate\Auth\Middleware\Authorize::class,
    'guest' => \App\Http\Middleware\RedirectIfAuthenticated::class,
    'throttle' => \Illuminate\Routing\Middleware\ThrottleRequests::class,
    'es_major_d_edad' => \App\Http\Middleware\MyMiddleware::class,
];
```

Un cop registrat nostre middleware ja el podem utilitzar **en el fitxer de rutes** `app/Http/routes.php` mitjançant la clau o nom assignat, per exemple:

```php
Route::get('dashboard', function () {
    //...
})->middleware('es_major_d_edad');
```

* En l'exemple anterior hem assignat el middleware amb clau **_es_major_d_edad_** la ruta ___dashboard___. 
* Com es pot veure s'utilitza el mètode `middleware()`, en el qual indiquem el middleware a aplicar. 
* Si la petició supera el filtre llavors s'executarà la funció associada.

Per associar un filtre amb una ruta que utilitza un **mètode d'un controlador** es realitzaria de la mateixa manera:

```php
Route::get('profile', 'UserController@showProfile')->middleware('auth');
```

Si volem **associar diversos middlewares amb una ruta** simplement hem d'afegir un array amb les claus dels middlewares. Els filtres s'executaran en l'ordre indicat en aquest array:

```php
Route::get('dashboard', function () {
    //...
})->middleware(['auth', 'es_mayor_de_edad']);
```



### Middleware dins de controladors

També és possible indicar el middleware a utilitzar **des de dins d'un controlador**. 

En aquest cas els filtres també hauran d'estar registrats en l'array `$routeMiddleware` del fitxer `app/Http/Kernel.php`. 

Per utilitzar-los es recomana **realitzar l'assignació en el constructor del controlador** i assignar els filtres utilitzant la seva clau mitjançant el mètode `middleware()`. 

Podrem indicar que es filtrin tots els mètodes, només alguns, o tots excepte els indicats, per exemple:

```php
class UserController extends Controller
{
    /**
     * Instantiate a new UserController instance.
     *
     * @return void
     */
    public function __construct()
    {
        // Filtrar tots els mètodes
        $this->middleware('auth');

        // Filtrar només aquests mètodes...
        $this->middleware('log', ['only' => ['fooAction', 'barAction']]);

        // Filtrar tots els mètodes excepte...
        $this->middleware('subscribed', ['except' => ['fooAction', 'barAction']]);
    }
}
```


## Referències

* **Llibre Lavarel 5 (Antonio Javier Gallego):** [Middleware o filtros](https://ajgallego.gitbooks.io/laravel-5/content/capitulo_2_filtros.html)