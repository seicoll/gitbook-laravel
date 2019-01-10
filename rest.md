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


|  Mètode    |         Ruta      | Acció      | Controlador/Mètode|    |
|------------|:-----------------:|:-----------:|:-----:|:-----:|
| GET        | user              | index  | UserController@index    |Formulari creació                 |
| GET        | user/create       | create | UserController@create    | |
| POST       | user               | store| UserController@store| |
| GET        | user/{id}        | show| UserController@show| |
| GET        | user/{id}/edit   | edit| UserController@edit| |
| PUT/PATCH  | user/{id}   | update| UserController@update| |
| DELETE     | user/{id}   | destroy| UserController@destroy| |

## Referències

* https://otroespacioblog.wordpress.com/2013/05/22/conoce-un-poco-sobre-los-metodos-http-en-rest/