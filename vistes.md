# Vistes

> Les **vistes** són la manera de presentar el resultat (una pantalla del nostre lloc web) de forma visual a l'usuari, el qual podrà interactuar amb ella i tornar a fer una petició. 

Les vistes a més ens permeten separar tota la part de presentació de resultats de la lògica (controladors) i de la base de dades (models). 

Per tant **no hauran de realitzar cap tipus de consulta ni processament de dades**, simplement rebran dades i els prepararan per a mostrar-los com HTML.

## Definir vistas

Les vistes s'emmagatzemen a la **carpeta** `resources/views`com fitxers PHP, i per tant tindran l'**extensió** .php. 

Contindran el codi HTML del nostre lloc web, barrejat amb els assets (CSS, imatges, Javascripts, etc., que estaran emmagatzemats a la carpeta `public`) i una mica de codi PHP (o codi Blade de plantilles, com veurem més endavant) per presentar les dades d'entrada com un resultat HTML.

A continuació s'inclou un exemple d'una vista simple que simplement mostrarà per pantalla `¡Hola <nom>!`, on `<nom>` és una variable de PHP que la vista ha de rebre com a entrada per poder mostrar-la.

**resources/views/home.php**
```html
<html>
    <head>
        <title>La meva web</title>
    </head>
    <body>
        <h1>¡Hola <?php echo $nom; ?>!</h1>
    </body>
</html>
```

## Referenciar i retornar vistes

Un cop tenim una vista hem d'**associar-la a una ruta** per poder mostrar-la. 

Per això hem d'anar al fitxer `routes/web.php` com hem vist abans i escriure el següent codi:

```php
Route::get('/', function()
{
    return view('home', array('nom' => 'Javi'));
});
```


Estem definint que la vista es torni quan es faci una petició tipus GET a l'arrel del nostre lloc. 

El valor retornat per la funció genera la vista usant el mètode `view()` i la retorna.  
Aquesta funció rep com a **paràmetres**:

* El **_nom de la vista_** (en aquest cas `home`), el qual serà un fitxer emmagatzemat a la carpeta `views`.
  * Recordeu que la vista anterior d'exemple l'havíem guardat en `resources/views/home.php`. Per indicar el nom de la vista s'utilitza el mateix nom del fitxer però sense l'extensió `.php` ni la ruta `resources/view`.


* Com a segon paràmetre rep una matriu de **_dades que se li passaran a la vista_**. 
  * En aquest cas la vista rebrà una variable anomenada `$nom` amb valor "Javi".

En l'exemple, per carregar la vista emmagatzemada en el fitxer `home.php` la referenciem mitjançant el nom `home`, **sense la ruta** `resources/views`.

Les **vistes es poden organitzar en subcarpetes** dins de la carpeta `resources/views`.

Per exemple podríem tenir una carpeta `resources/views/user` i dins d'aquesta totes les vistes relacionades, com per exemple `login.php`, `register.php` o `profile.php`. 

Per **referenciar les vistes que estan dins de subcarpetes** hem d'utilitzar la notació tipus _"dot"_, en què les barres que separen les carpetes es substitueixen per punts. 

Per exemple, per fer referència a la vista `resources/views/user/login.php`faríem servir el nom `user.login`, o la vista `resources/views/user/register.php` la carregaríem de la forma:

```php
Route::get('register', function()
{
    return view('user.register');
});
```

## Passar dades a una vista

Per **passar dades a una vista** hem d'utilitzar el segon paràmetre del mètode `view`, el qual accepta un array associatiu. 

En aquest array podem afegir totes les variables que vulguem utilitzar dins de la vista, ja siguin de tipus variable normal (cadena, sencer, etc.) o un altre array o objecte amb més dades. 

Per exemple, per enviar a la vista `profile` totes les dades de l'usuari el qual té el `id` rebem a través de la ruta hauríem de fer:

```php
Route::get('user/profile/{id}', function($id)
{
    $user = // Carregar les ades de l'usuari a partir de $id
    return view('user.profile', array('user' => $user));
});
```

Laravel més ofereix una alternativa que crea **un notació una mica més clara**. 

En lloc de passar un array com a segon paràmetre podem utilitzar **el mètode `with`** per indicar una a una les variables o continguts que volem enviar a la vista:

```php
$view = view('home')->with('nombre', 'Javi');

$view = view('user.profile')
            ->with('user', $user)
            ->with('editable', false);

```

## Referències

* **Llibre Lavarel 5 (Antonio Javier Gallego):** [Vistas](https://ajgallego.gitbooks.io/laravel-5/content/capitulo_1_vistas.html)

