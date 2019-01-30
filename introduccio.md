# Introducció

## Què és Laravel?

> Laravel és un **framework** de codi obert pel desenvolupament d'aplicacions i serveis web amb PHP.

Va ser creat l'any 2011 per Taylor Otwell inspirant-se en **Ruby on Rails** i **ASP.Net**.

**Principals característiques i avantatges:**
* Evita la repetició de codi.
* S'aprèn ràpidament.
* Disposa de mecanismes de seguretat (autenticació d'usuaris, etc).
* Utilitza el patró **MVC** (Model Vista Controlador).
* Permet la integració de llibreries.
* Requereix coneixements de **PHP** i programació orientada a objectes (**POO**).

![](/assets/laravel.png)

## El patró MVC (Model - Vista - Controlador)

> MVC són les sigles de **model-vista-controlador** (**_model-view-controler_**) que
consisteix en un patró d'arquitectura del software.


* L'**arquitectura de software**, a semblança dels plànols d'un edifici o construcció, defineix la forma com s'organitzen, interactuen i es relacionen entre si les parts del software.


* **MVC** permet:
  * No barrejar llenguatges de programació en el mateix codi.
  * Separar les dades i la lògica de negoci d'una aplicació de la interfície d'usuari.


* **MVC** divideix les aplicacions en 3 nivells o capes:
  * **Modelo (Model)**:
    * Representa la lògica de negoci o lògica de l'aplicació.
    * És l'encarregat d'accedir de forma directa a les dades actuant com "mitjancer" amb la base de dades.


* **Vista (View)**:
  * És l'encarregada de mostrar la informació a l'usuari de forma gràfica.


* **Controlador (Controller)**:
  * És l'intermediari entre la vista i el model.
  * És l'encarregat de gestionar les peticions de l'usuari sol·licitant les dades al model i lliurar-les a la vista per tal que aquesta, ho mostri a l'usuari.


## MVC: Funcionament

![Model MCV](https://i0.wp.com/www.magarrent.com/wp-content/uploads/2016/12/0-Selection_001.png?fit=964%2C519&ssl=1)

1. L'**usuari** des del navegador accedeix una pàgina web.
2. Accedim a una **ruta** (ex: /, /usuaris, /registre).
3. Aquesta ruta té un **controlador** associat al qual se'ns envia.
4. Si el controlador vol accedir a la base de dades, demana al **model** (Ex: Model Usuari) les dades.
5. El **model** s'encarrega d'interactuar amb la base de dades i retornar la informació al controlador per ser manipulada.
7. El **controlador** rep la informació i l'envia a la vista (una pàgina html).
8. El **controlador** configura la **vista** i la retorna al navegador en formato HTML.