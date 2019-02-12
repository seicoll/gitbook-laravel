# Dades d'entrada

Laravel facilita l'accés a les dades d'entrada de l'usuari a través de només uns pocs mètodes. No importa el tipus de petició que s'hagi realitzat (POST, GET, PUT, DELETE), si les dades són d'un formulari o si s'han afegit a la _query string_, en tots els casos s'obtindran de la mateixa forma.

Per aconseguir accés a aquests mètodes Laravel utilitza **injecció de dependències**. Això és simplement afegir la classe `Request` al constructor o mètode del controlador en què el necessitem. Laravel s'encarregarà d'injectar aquesta dependència ja inicialitzada i directament podrem utilitzar aquest paràmetre per obtenir les dades d'entrada. 

A continuació s'inclou un exemple:

```
<?php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Routing\Controller;

class UserController extends Controller
{
    public function store(Request $request)
    {
        $name = $request->input('name');

        //...
    }
}
```

En aquest exemple com es pot veure s'ha afegit la classe `Request` com a paràmetre al mètode `store`. Laravel automàticament s'encarrega d'injectar aquestes dependències per la qual cosa directament podem usar la variable `$request` per obtenir les dades d'entrada.

## Obtenir els valors d'entrada

Per obtenir el valor d'una variable d'entrada d'un formulari fem servir el mètode `input()` indicant el nom de la variable:

```
$name = $request->input('name');

// O simplemente....
$name = $request->name;
```

També podem especificar un **valor per defecte** com a segon paràmetre:

`$name = $request->input('name', 'Pedro');`

## Obtenir dades agrupades

O també podem obtenir **totes les dades d'entrada a la vegada** (en una matriu) o només alguns d'ells:

```
// Obtenir tots: 
$input = $request->all();

// Obtenir només els camps indicats: 
$input = $request->only('username', 'password');

// Obtenir tots excepte els indicats:
$input = $request->except('credit_card')
```

Podem obtenir totes les dades d'entrada a la vegada i **assignar-los massivament a l'objecte**.

```
public function store (Request $request)
{
    $user = new User($request->all());
    $user->save();
}
```