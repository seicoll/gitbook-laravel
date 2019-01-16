# Plantilles amb Blade

> Laravel utilitza **Blade** per a la definició de plantilles en les vistes. 

Aquesta llibreria permet realitzar tot tipus d'operacions amb les dades, a més de la substitució de seccions de les plantilles per altre contingut, herència entre plantilles, definició de layouts o plantilles base, etc.

Els fitxers de vistes que utilitzen el sistema de plantilles Blade han de tenir l'extensió .blade.php. Aquesta extensió tampoc s'haurà d'incloure a l'hora de fer referència a una vista des del fitxer de rutes o des d'un controlador. És a dir, utilitzarem view('home')tant si el fitxer es diu home.php com `home.blade.php`.

En general el codi que inclou Blade en una vista començarà pels símbols @o {{, el qual posteriorment serà processat i preparat per a mostrar-se per pantalla. Blade no afegeix sobrecàrrega de processament, ja que totes les vistes són preprocesadas i escorcollades, per contra ens brinda utilitats que ens ajudaran en el disseny i modularització de les vistes.

## Mostrar dades

El mètode més bàsic que tenim a Blade és el de mostrar dades, per això utilitzarem les claus dobles ({{}}) i dins d'elles escriurem la variable o funció amb el contingut a mostrar:
Hola {{ $name }}.
La hora actual es {{ time() }}.
Com hem vist podem mostrar el contingut d'una variable o fins i tot trucar a una funció per mostrar el seu resultat. Blade s'encarrega d'escapar el resultat cridant a htmlentitiesper prevenir errors i atacs de tipus XSS. Si en algun cas no volem escapar les dades haurem de trucar a:
Hola {!! $name !!}.
Nota: En general sempre haurem de fer servir les claus dobles, especialment si anem a mostrar dades que són proporcionats pels usuaris de l'aplicació. Això evitarà que injectin símbols que produeixin errors o injectin codi javascript que s'executi sense que nosaltres vulguem. Per tant, aquest últim mètode només hem de utilitzar-lo si estem segurs que no volem que s'escapi el contingut.

## Mostra una dada només si existeix

Per comprovar que una variable existeix o té un determinat valor podem utilitzar l'operador ternari de la forma:
{{ isset($name) ? $name : 'Valor por defecto' }}
O simplement utilitzar la notació que inclou Blade per a aquest fi:
{{ $name or 'Valor por defecto' }}

## Comentaris

Per escriure comentaris en Blade s'utilitzen els símbols `{{--` i `--}}`, per exemple:

`{{-- Aquest comentari no se mostrarà en HTML --}}`

## Estructures de control

**Blade** ens permet utilitzar l'estructura` if`de les següents formes:

``` 
@if( count($users) === 1 )
    Solo hay un usuario!
@elseif (count($users) > 1)
    Hay muchos usuarios!
@else
    No hay ningún usuario :(
@endif
``` 

En els següents exemples es pot veure com realitzar bucles tipus for , while o foreach :

``` 
@for ($i = 0; $i < 10; $i++)
    El valor actual es {{ $i }}
@endfor

@while (true)
    <p>Soy un bucle while infinito!</p>
@endwhile

@foreach ($users as $user)
    <p>Usuario {{ $user->name }} con identificador: {{ $user->id }}</p>
@endforeach
``` 

Aquesta són les estructures de control més utilitzades. A més d'aquestes Blade defineix algunes més que podem veure directament en la seva documentació: http://laravel.com/docs/5.1/blade

## Incloure una plantilla dins d'una altra plantilla

En Blade podem indicar que s'inclogui una plantilla dins d'una altra plantilla, per això disposem de la instrucció @include:

`@include('view_name')`

A més podem passar-li una matriu de dades a la vista a carregar usant el segon paràmetre del mètode include:

`@include('view_name', array('some'=>'data'))`

Aquesta opció és molt útil per crear vistes que siguin reutilitzables o per separar el contingut d'una vista en diversos fitxers.

## Layouts

Blade també ens permet la definició de layouts per crear una estructura HTML base amb seccions que seran emplenades per altres plantilles o vistes filles. Per exemple, podem crear un layout amb el contingut principal o comú de la nostra web ( head , body , etc.) i definir una sèrie de seccions que seran omplerts per altres plantilles per completar el codi. Aquest layout pot ser utilitzat per a totes les pantalles del nostre lloc web, el que ens permet que a la resta de plantilles no haguem de repetir tot aquest codi.

A continuació d'inclou un exemple d'una plantilla tipus layout emmagatzemada en el fitxer `resources/views/layouts/master.blade.php`:

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

Posteriorment, en una altra plantilla o vista, podem indicar que estengui el layout que hem creat (amb @extends('layouts.master')) i que completi les dues seccions de contingut que havíem definit en el mateix:

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

Com es pot veure, les vistes que estenen un layout simplement han de sobreescriure les seccions del layout . La directiva @sectionpermet anar afegint contingut en les plantilles filles, mentre que @yieldserà substituït pel contingut que s'indiqui. El mètode @parentcàrrega en la posició indicada el contingut definit pel pare per a aquesta secció.
El mètode @yieldtambé permet establir un contingut per defecte mitjançant el seu segon paràmetre:

`@yield('section', 'Contenido por defecto')`


---
`asset()` construirà la URL completa:

`<link rel="stylesheet" href="{{ asset('css/app.css')}}`


## Referències

* **Llibre Lavarel 5 (Antonio Javier Gallego):** [Plantillas mediante Blade](https://ajgallego.gitbooks.io/laravel-5/content/capitulo_1_plantillas.html)


