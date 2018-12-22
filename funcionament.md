<!-- notoc -->

# Funcionament bàsic

## Estructura de carpetes

En crear un nou projecte de Laravel se'ns generarà una estructura de carpetes i fitxers per
organitzar el nostre codi.

Alguns dels **arxius** que tenim directament a la carpeta arrel de Laravel són:

* **.env** - valors de configuració de l'aplicació. 
  * Permet canviar fàcilment la configuració i
tenir opcions diferents per a producció, per desenvolupament, etc. 
  * **Important**, aquest fitxer hauria d'estar al _.gitignore_.
  
  
* **composer.json** - Conté informació pel gestor de paquets **_Composer_**.

**Carpetes principals** de Laravel:

* `app` - arxius de l'aplicació (Controladors, Models, Middlewares, etc.)

* `bootstrap` - arxius del motor de Laravel. (No tocarem)

* `config` - arxius de configuració (Bases de dades, mails, etc.)

* `database` - tot el relacionat amb la **definició de la base de dades** del nostre projecte.
  Dins hi trobem tres carpetes: `factories`, `migrations` i `seeds`.


* `public` - arxius públics de la nostra aplicació. 
  * És l'única carpeta pública, l'única que hauria de ser **visible** al nostre servidor web i els podran veure tots els usuaris que accedeixin a la nostra aplicació. 
  * Hi trobem l'arxiu _index.php_, arxius CSS, Javascript, imatges, etc.


* `resources` - recursos de l'aplicació, com ara les **_Vistes_**.

* `routes` - arxius que defineixes totes les rutes del nostre lloc web.

* `storage` - arxius tals com memòria cau (caché), sessions, logs, etc. (No tocarem) 

* `tests` - arxius per realitzar tests automatitzats de la nostra aplicació amb PHPUnit. (No tocarem)

* `vendor` - les llibreries externes que gestiona **_Composer_** que són dependències de Laravel. (No s'ha de tocar)