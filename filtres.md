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

