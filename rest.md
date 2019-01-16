# API REST

**RESTful** (de l’anglès **RE**presentational **S**tate **T**ransfer)

> **REST **no és un protocol, sinó un conjunt de regles i principis que permeten desenvolupar serveisweb fent servir HTTP com a protocol de comunicacions entre el client i el servei web, i es basa a definir accions sobre recursos mitjançant l’ús dels mètodes GET, POST, PUT i DELETE, inherents d'HTTP.

Per a REST, qualsevol cosa que es pugui identificar amb un URI (de l’anglès Uniform Resource Identifier) es considera un recurs i, per tant, es pot manipular mitjançant accions (també anomenades verbs) especificades a la capçalera HTTP de les peticions seguint el següent conjunt de regles i principis que regeixen REST:

La url no ha d'indicar l'operació a realitzar. 
El **mètodes (verbs) del protocol HTTP** especifiquen les accions sobre els recursos.

Segons els estàndards de HTTP, els mètodes s'han d'utilitzar per:

* **GET**: consulta el recurs, n'obté la representació (XML, JSON, HTML, PDF, GIF, JPG, PNG, etc.).
* **POST**: crea un recurs nou
* **PUT**: modifica un recurs. El substitueix **per complet** o el crea si no existeix.
* **PATCH**: modifica un recurs. Modificar parts del recurs.
* **DELETE**: esborra un recurs

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