# API REST

## Què és REST?

**RESTful** (de l’anglès **RE**presentational **S**tate **T**ransfer)

> **REST **no és un protocol, sinó un conjunt de regles i principis que permeten desenvolupar serveisweb fent servir HTTP com a protocol de comunicacions entre el client i el servei web, i es basa a definir accions sobre recursos mitjançant l’ús dels mètodes GET, POST, PUT i DELETE, inherents d'HTTP.

Per a REST, qualsevol cosa que es pugui identificar amb un URI (de l’anglès Uniform Resource Identifier) es considera un recurs i, per tant, es pot manipular mitjançant accions (també anomenades verbs) especificades a la capçalera HTTP de les peticions seguint el següent conjunt de regles i principis que regeixen REST:

---
REST prové de l'acrònim Representational State Transfer que és una arquitectura per al programari pensada per sistemes distribuïts. Aquesta arquitectura està basada en el protocol de comunicacions HTTP i es basa en la idea que cada component és un recurs i que cadascun d'ells pot accedir mitjançat una comunicació HTTP via mètodes standard. 
En l'arquitectura REST, existeix un servidor REST que proveeix accés als recursos i un client REST que accedeix a aquests recursos. Per fer-ho, cada recurs està identificat per una URL o identificadors globals. Per obtenir les dades, REST retorna els recursos en diverses representacions: mode text, en format JSON o en XML. Actualment JSON és el més popular i el que s'utilitza en la majoria de serveis web.

Un servei web REST és un model centrat bàsicament en les dades. Els recursos venen identificats per URLs i poden ser manipulats mitjançant accions especificades en la pròpia capçalera HTTP.

---

## Mètodes HTTP

La url no ha d'indicar l'operació a realitzar. 

El **mètodes (verbs) del protocol HTTP** especifiquen les accions sobre els recursos.

Segons els estàndards de HTTP, els mètodes s'han d'utilitzar en l'arquitectura REST són:

* **GET**: lectura i accés a un recurs, n'obté la representació (XML, JSON, HTML, PDF, GIF, JPG, PNG, etc.).
* **POST**: crea un recurs nou
* **PUT**: modifica un recurs. El substitueix **per complet** o el crea si no existeix.
* **PATCH**: modifica un recurs. Modificar parts del recurs.
* **DELETE**: elimina un recurs
* **OPTIONS**: per a d'altres operacions sobre un recurs.

## JSON

> **JSON** (prové de l'acrònim **J**ava**S**cript **O**bject **N**otation) és un standard obert basat en text per a l'intercanvi de dades i que pot ser directament llegit per humans. 

En realitat deriva del llenguatge Javascript, de la seva metodologia per representar objectes simples i llistes associatives, que n'anomena objects. 

Els arxius que representen estructures en aquest format utilitzen la **extensió _.json_**

El format JSON s'utilitza habitualment per serialitzar i transmetre dades estructurades en una connexió de xarxa.

**Exemple en JSON:**

```
{"estudiants":[
    {"nom":"David", "cognom1":"Vidal", "cognom2":"Soler"},
    {"nom":"Roser", "cognom1":"Puig", "cognom2":"Ferrer"},
    {"nom":"Pere", "cognom1":"Serra", "cognom2":"Martí"}
]}
```

JSON igual que XML és un llenguatge de representació de dades en mode text, però amb la diferencia que JSON no conté informació sobre capçaleres i resulta **un llenguatge més lleuger**, característica molt interessant per a la seva **transmissió més efectiva per la xarxa**, entre dispositius.

**Exemple en XML:**

```xml
<estudiants>
    <estudiant>
        <nom>David</nom> <cognom1>Vidal</cognom1> <cognom2>Soler</cognom2>
    </estudiant>
    <estudiant>
        <nom>Roser</nom> <cognom1>Puig</cognom1> <cognom2>Ferrer</cognom2>
    </estudiant>
    <estudiant>
        <nom>Pere</nom> <cognom1>Serra</cognom1> <cognom2>Martí</cognom2>
    </estudiant>
</estudiants>
```

## Exemple API


|  Mètode    |      Ruta      | Acció    | Controlador/Mètode    | Descripció |
|------------|----------------|----------|-----------------------|---------|
| GET        | users           | index    | UserController@index  | Llista de tots els usuaris|
| GET        | users/create    | create   | UserController@create | Formulari creació |
| POST       | users           | store    | UserController@store  | Processa les dades del formulari d'alta |
| GET        | users/{id}      | show     | UserController@show   | Mostra les dades de l'usuari que té el id indicat|
| GET        | users/{id}/edit | edit     | UserController@edit   | Formulari d'edició|
| **PUT**/PATCH | users/{id}      | update   | UserController@update | Processa les dades del formulari d'edició|
| DELETE     | users/{id}      | destroy  | UserController@destroy| Elimina l'usuari que té el id indicat|

## Rutes de recursos

`Route::resource('users', 'UserController');`

o bé

`Route::apiResource('users', 'UserController');` per no crear les rutes `create` i `edit` en el cas d'una API REST.

Podem crear una classe **controlador d'un recurs** amb tots els mètodes necessàris:

 `php artisan make:controller --resource UserController`
 

## Referències

* **Llibre Lavarel 5 (Antonio Javier Gallego):** [Controladores de recursos RESTful](https://ajgallego.gitbooks.io/laravel-5/content/capitulo_5_rest.html)

* https://otroespacioblog.wordpress.com/2013/05/22/conoce-un-poco-sobre-los-metodos-http-en-rest/