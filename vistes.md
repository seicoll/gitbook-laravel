# Vistes

> Les **vistes** són la manera de presentar el resultat (una pantalla del nostre lloc web) de forma visual a l'usuari, el qual podrà interactuar amb ella i tornar a fer una petició. 

Les vistes a més ens permeten separar tota la part de presentació de resultats de la lògica (controladors) i de la base de dades (models). 

Per tant **no hauran de realitzar cap tipus de consulta ni processament de dades**, simplement rebran dades i els prepararan per a mostrar-los com HTML.

## Definir vistas

Les vistes s'emmagatzemen a la **carpeta** `resources/views`com fitxers PHP, i per tant tindran l'**extensió** .php. 

Contindran el codi HTML del nostre lloc web, barrejat amb els assets (CSS, imatges, Javascripts, etc., que estaran emmagatzemats a la carpeta `public`) i una mica de codi PHP (o codi Blade de plantilles, com veurem més endavant) per presentar les dades d'entrada com un resultat HTML.

A continuació s'inclou un exemple d'una vista simple que simplement mostrarà per pantalla `¡Hola <nom>!`, on `<nom>` és una variable de PHP que la vista ha de rebre com a entrada per poder mostrar-la.

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







`asset()` construirà la URL completa:

`<link rel="stylesheet" href="{{ asset('css/app.css')}}`