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
