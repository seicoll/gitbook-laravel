# Plantilles amb Blade

> Laravel utilitza **Blade** per a la definició de plantilles en les vistes. 

Aquesta llibreria permet:
  * Realitzar tota classe d'operacions amb les dades.
  * Substitució de seccions de les plantilles per altre contingut.
  * Herència entre plantilles.
  * Definició de layouts o plantilles base.
  * etc.

Els fitxers de vistes que utilitzen el sistema de plantilles Blade han de tenir l'**extensió** `.blade.php`. 
* Aquesta extensió no s'haurà d'incloure a l'hora de fer referència a una vista des del fitxer de rutes o des d'un controlador. 
* És a dir, utilitzarem `view('home')`tant si el fitxer es diu `home.php` com `home.blade.php`.

## Mostrar dades

El mètode més bàsic que tenim a Blade és el de mostrar dades, per això utilitzarem les claus dobles (\{\{\}\}) i dins d'elles escriurem la variable o funció amb el contingut a mostrar:

```
Hola {{ $name }}.
L'hora actual és {{ time() }}.
```

* Com hem vist podem mostrar el contingut d'una variable o fins i tot cridar a una funció per mostrar el seu resultat. 

## Mostra una dada només si existeix

Per comprovar que una variable existeix o té un determinat valor podem utilitzar l'operador ternari de la forma:

`{{ isset($name) ? $name : 'Valor por defecte' }}`

O simplement utilitzar la notació que inclou Blade per a aquest fi:

`{{ $name or 'Valor por defecte' }}`

## Comentaris

Per escriure **comentaris** en Blade s'utilitzen els símbols `{{--` i `--}}`, per exemple:

`{{-- Aquest comentari no es mostrarà en HTML --}}`

## Estructures de control

**Blade** ens permet utilitzar l'estructura **_if_** de les següents formes:

``` 
@if( count($users) === 1 )
    Solo hay un usuario!
@elseif (count($users) > 1)
    Hay muchos usuarios!
@else
    No hay ningún usuario :(
@endif
``` 

En els següents exemples es pot veure com realitzar bucles tipus **_for_** , **_while_** o **_foreach_**:

``` 
@for ($i = 0; $i < 10; $i++)
    El valor actual és {{ $i }}
@endfor

@while (true)
    <p>Sóc un bucle while infinit!</p>
@endwhile

@foreach ($users as $user)
    <p>Usuari {{ $user->name }} amb identificador: {{ $user->id }}</p>
@endforeach
``` 

Aquesta són les estructures de control més utilitzades. A més d'aquestes Blade defineix algunes més que podem veure directament en la seva documentació: https://laravel.com/docs/5.7/blade#control-structures

## Incloure una plantilla dins d'una altra plantilla

En Blade podem indicar que s'**inclogui una plantilla dins d'una altra plantilla**, per això disposem de la instrucció `@include`:

`@include('view_name')`

A més podem passar-li una matriu de dades a la vista a carregar utilitzant el segon paràmetre del mètode `include`:

`@include('view_name', array('some'=>'data'))`

Aquesta opció és molt útil per crear vistes que siguin reutilitzables o per separar el contingut d'una vista en diversos fitxers.

## Layouts

Blade també ens permet la definició de **layouts** per crear una estructura HTML base amb seccions que seran emplenades per altres plantilles o vistes filles. 

Per exemple, podem crear un **layout amb el contingut principal o comú** de la nostra web (head, body, etc.) i definir una sèrie de seccions que seran omplerts per altres plantilles per completar el codi. 

Aquest layout **pot ser utilitzat per a totes les pantalles del nostre lloc web**, el que ens permet que a la resta de plantilles no hàgim de repetir tot aquest codi.

A continuació s'inclou un exemple d'una plantilla tipus layout emmagatzemada en el fitxer `resources/views/layouts/master.blade.php`:

```html
<html>
    <head>
        <title>El meu web</title>
    </head>
    <body>
        @section('menu')
            Contingut del menu
        @show

        <div class="container">
            @yield('content')
        </div>
    </body>
</html>
``` 

Posteriorment, en una altra plantilla o vista, podem indicar que extengui el layout que hem creat (amb `@extends('layouts.master')`) i que completi les dues seccions de contingut que havíem definit:

``` 
@extends('layouts.master')

@section('menu')
    @parent
    <p>Este condenido es añadido al menú principal.</p>
@endsection

@section('content')
    <p>Este apartado aparecerá en la sección "content".</p>
@endsection
``` 

Com es pot veure, les vistes que extenem un layout simplement han de sobreescriure les seccions del layout. 

* La directiva `\@section` permet anar afegint contingut en les plantilles filles
* Mentre que `@yield` serà substituït pel contingut que s'indiqui. 
* El mètode `@parent`càrrega en la posició indicada el contingut definit pel pare per a aquesta secció.

El mètode `@yield` també permet establir un contingut per defecte mitjançant el seu segon paràmetre:

`@yield('section', 'Contenido por defecto')`


---
`asset()` construirà la URL completa:

`<link rel="stylesheet" href="{{ asset('css/app.css')}}`


## Referències

* **Llibre Lavarel 5 (Antonio Javier Gallego):** [Plantillas mediante Blade](https://ajgallego.gitbooks.io/laravel-5/content/capitulo_1_plantillas.html)


