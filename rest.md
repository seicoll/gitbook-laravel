# API REST

## Què és REST?

**RESTful** (de l'anglès **RE**presentational **S**tate **T**ransfer)

> **REST** és un conjunt de regles i principis que permeten desenvolupar serveis web fent servir **HTTP com a protocol de comunicacions** entre el client i el servei web. Es basa a definir accions sobre recursos mitjançant l'ús dels mètodes standards d'HTTP (GET, POST, PUT i DELETE).

Per a REST, qualsevol cosa que es pugui identificar amb un **URI** (de l'anglès **U**niform **R**esource **I**dentifier) es considera un **recurs** i, per tant, es pot manipular mitjançant accions (també anomenades verbs) especificades a la capçalera HTTP de les peticions seguint el següent conjunt de regles i principis que regeixen REST:

---
En l'arquitectura REST, existeix un servidor REST que proveeix accés als recursos i un client REST que accedeix a aquests recursos. Per fer-ho, cada recurs està identificat per una URL o identificadors globals. Per obtenir les dades, REST retorna els recursos en diverses representacions: mode text, en format JSON o en XML. Actualment JSON és el més popular i el que s'utilitza en la majoria de serveis web.

Un servei web REST és un model centrat bàsicament en les dades. Els recursos venen identificats per URLs i poden ser manipulats mitjançant accions especificades en la pròpia capçalera HTTP.

---

![](/assets/RESTful-API.png)

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

### Sintaxi JSON

La **sintaxi JSON** és similar a Javascript, ja que aquest model de representació en prové directament.

La sintaxi JSON deriva de la sintaxi de notació JavaScript:

* Les dades són parells nom/valor
* Les dades es separen per comes
* Els objectes estan envoltats dels símbols **{ }** 
* Els arrays estan envoltats dels símbols **[ ]**


**Exemple nom/valor:**

`"cognom" : "Puig"`


Els **valors** en JSON poden ser:

* Un **número**
* Una **cadena** de caràcters (entre símbols **" "** )
* Un **booleà** (true o false)
* Un **array** (entre els símbols **[ ]** )
* Un **objecte** (entre símbols **{ }** )


**Exemple objecte: **

`{"nom": "David","cognom1": "Vidal","cognom2": "Soler"}`


**Exemple array:**

```
"estudiants":[
    {"nom":"David", "cognom1":"Vidal", "cognom2":"Soler"},
    {"nom":"Roser", "cognom1":"Puig", "cognom2":"Ferrer"},
    {"nom":"Pere", "cognom1":"Serra", "cognom2":"Martí"}
]
```

## Codis de retorn HTTP

Alguns serveis REST utilitzen els codis d'estat definits en les especificacions del protocol HTTP per retornar al client el resultat de l'operació sol·licitada. En la capçalera es retorna el codi de resultat i en la part de dades es retorna un missatge o les dades propiament dites, segons estigui definida la API. 

Altres serveis retornen sempre el codi HTTP 200 de resposta correcta i dins de les dades en format JSON indiquen l'estat de la resposta que normalment s'acompanya d'una descripció. En podeu veure un exemple en els serveis web de Google Maps que trobareu en l'apartat d'exemples.

Els codis HTTP que es retornen són de 3 dígits i segueixen un esquema similar al següent:

* **Codi 1xx** - El servidor respon que està treballant en la petició
* **Codi 2xx** - El servidor ha pogut acomplir correctament amb la petició del client
* **Codi 3xx** - El servidor indica que pot acomplir la sol·licitud però que hi ha alguna tasca a fer prèviament. 
  * Per exemple, reenrutar la petició.
* **Codi 4xx** - El servidor indica que s'ha produït un error en la petició. 
  * Per exemple: 404 el recurs no existeix
* **Codi 5xx** - El servidor no pot respondre a la vostra petició. 

En les especificacions de la pròpia API s'indiquen els codis exactes de retorn i el motiu que l'ocasiona, per tal de poder-ho tractar en el client. Originalment els codis d'estat HTTP varen dissenyar-se per al món web exclusivament, encara que en l'actualitat s'utilitza en aplicacions híbrides de dispositiu mòbil/web. En l'apartat de més informació podeu trobar més orientacions sobre els codis d'estat dissenyats per al protocol HTTP/1.1

**Més informació**: [RFC HTTP/1.1. Response Status Code](https://tools.ietf.org/html/rfc7231#page-47)

## Exemple API


|  Mètode HTTP   |      Ruta / URI     | Operació    | Controlador/Mètode    | Descripció |
|------------|----------------|----------|-----------------------|---------|
| GET        | users           | index    | UserController@index  | Obtenir la llista de tots els usuaris|
| GET        | users/{id}      | show     | UserController@show   | Obtenir les dades de l'usuari que té el **id** indicat|
| GET        | users/create    | create   | UserController@create | Obtenir el formulari de creació |
| POST       | users     | store    | UserController@store  | Inserir l'usuari |
| GET        | users/{id}/edit | edit     | UserController@edit   | Obtenir el formulari d'edició de l'usuari que té el **id** indicat|
| **PUT**/PATCH | users/{id}      | update   | UserController@update | Modificar l'usuari que té el **id** indicat|
| DELETE     | users/{id}      | destroy  | UserController@destroy| Eliminar l'usuari que té el **id** indicat|

Les peticions a aquestes rutes **no tornaran una vista (amb HTML)**, sinó directament la dada o la llista de dades sol·licitades en format pla, en XML o en **JSON**.


## Rutes de recursos

Si volem definir una API cal que utilitzem el fitxer de rutes `routes/api.php` en lloc de `routes/web.php`.

**A totes les rutes** que especifiquem en `routes/api.php`**se'ls afegirà el prefix `api`**. Pel que si afegim la ruta `users` per tornar el llistat d'usuaris, per fer la consulta haurem d'accedir a `api/users`. 

Podem **definir totes les rutes** necessàries per un recurs utilitzant:

`Route::resource('users', 'UserController');`

* On 'users' és el **nom del recurs**, normalment amb plural.
* I 'UserController' és el **nom del controlador** associat.

En el cas de les API REST, **no sol ser necessari crear les rutes `create`i `edit`** per tant es pot utilitzar la següent definició de ruta:

`Route::apiResource('users', 'UserController');` 

Aquesta línia de ruta **crea per si sola múltiples rutes** per gestionar tots els tipus de peticions RESTful. A més, el controlador haurà de disposar de tots els mètodes necessaris per respondre a totes les peticions corresponents.

Amb la comanda `php artisan route:list` podem veure les **rutes generades**:

![](/assets/API_rutes.PNG)

## Controlador de recursos RESTful

Laravel incorpora un tipus especial de controlador, anomenat **controlador de recurs** (_recource controller_), que facilita la construcció de controladors tipus RESTful . 

Podem crear el **controlador del recurs** amb tots els mètodes necessaris utilitzant la comanda:

 `php artisan make:controller UserController --resource`
 
o bé

`php artisan make:controller UserController -r`

Això crearia el controlador `UserController` que (incloent tots els mètodes necessaris)

El controladors de recursos tindran per defecte **7 mètodes**:
* `index()`
* `create()`
* `store(Request $request)`
* `show($id)`
* `edit($id)`
* `update(Request $request, $id)`
* `destroy($id)`


## Referències

* **Llibre Lavarel 5 (Antonio Javier Gallego):** [Controladores de recursos RESTful](https://ajgallego.gitbooks.io/laravel-5/content/capitulo_5_rest.html)

* https://otroespacioblog.wordpress.com/2013/05/22/conoce-un-poco-sobre-los-metodos-http-en-rest/