<!-- notoc -->

# Capítol 3: Base de dades

## Índex

1. [Migracions](migracions.md)
* [Seeders](seeders.md)
* [Models](models.md)

## Configuració de la base de dades

En el fitxer de configuració `.env` hem d'indicar els paràmetres d'accés a la nostra base de dades i a més especificar quina és la connexió que s'utilitzarà per defecte. 

```
DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=nom-base-de-dades
DB_USERNAME=nom-usuari
DB_PASSWORD=password
```