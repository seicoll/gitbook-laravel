# Instal·lació 

## Requeriments Laravel

Per la instal·lació de Laravel és molt important tenir en compte les **versions**:
* Laravel 5.3: PHP >= 5.6.4
* Laravel 5.5: PHP >= 7.0
* Laravel 5.6: PHP >= 7.1
* **Laravel 5.7: PHP >= 7.1.3**

A més, també són necessàries les següents **extensions**:

* OpenSSL PHP Extension
* PDO PHP Extension
* Mbstring PHP Extension
* Tokenizer PHP Extension
* XML PHP Extension
* Ctype PHP Extension
* JSON PHP Extension
* BCMath PHP Extension

Si utilitzes Ubuntu 14 o menor [actualitza la teva versió de PHP a la 7.0](https://www.digitalocean.com/community/tutorials/how-to-upgrade-to-php-7-on-ubuntu-14-04).

Caldran els paquets següents:

`$ sudo apt-get install php-mbstring php-zip php-xml`

> Tots aquest requiriments són satisfets per la màquina virtual [Laravel Homestead](https://laravel.com/docs/5.7/homestead).

## Homestead

L'equip de Laravel ens ofereix una màquina virtual anomenada **Homestead**, per facilitar-tos la preparació de l'entorn de desenvolupament en Laravel.

>**Homestead** és una "Box de Vagrant".
>**Vagrant** és una capa per sobre de Virtualbox o VMWare que ens permet crear entorns de desenvolupament i les **_Boxs_** són imatges de sistemes operatius ja instal·lats.

**Software inclòs:**

* **Ubuntu 18.04**
* **Git**
* **PHP 7.3**
* PHP 7.2
* PHP 7.1
* PHP 7.0
* PHP 5.6
* Nginx
* Apache (Optional)
* **MySQL**
* MariaDB (Optional)
* Sqlite3
* PostgreSQL
* **Composer**
* Node (With Yarn, Bower, Grunt, and Gulp)
* Redis
* Memcached
* Beanstalkd

**Més informació:** [Laravel Homestead](https://laravel.com/docs/5.7/homestead)

## Instal·lació i configuració

Utilitzarem **[Composer](https://getcomposer.org/)** per descarregar-nos i instal·lar el Framework Laravel.

> **Composer** és una eina per a la gestió de dependències en PHP. Us permet declarar les llibreries de què depèn del vostre projecte i gestionar-les (instal·lar-les/actualitzar-les).

![](/assets/logo-composer.png)

### 1. Instal·lar el gestor de paquets Composer
Instal·la Composer a la teva màquina seguint la [documentació oficial](https://getcomposer.org/download/).

```
  php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
  php -r "if (hash_file('sha384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
  php composer-setup.php
  php -r "unlink('composer-setup.php');"
```

### 2. Instal·lar Laravel
Instal·la la darrera versió de Laravel seguint [documentació oficial](https://laravel.com/docs/5.7#installing-laravel) o bé seguint alguna d'aquestes dues formes:

#### 2.1 Via Laravel Installer

1. Primer es descarrega l'instal·lador de Laravel utilitzant Composer:
  `composer global require "laravel/installer"`

  Laravel s'instal·la a `$HOME/.config/composer` però per poder executar les properes comandes necessitarem tenir `$HOME/.config/composer/vendor/bin` al nostre $PATH.

2. Inserta això al teu `$HOME/.profile`:
  `PATH=$PATH:~/.config/composer/vendor/bin`
  Fes logout/login del sistema per activar aquests canvis.

3. Crea una app Laravel a la carpeta on guardaràs els teus projectes:
  `$ laravel new blog`
  Ens crea un nou directori amb la instal·lació de Laravel i totes les seves dependències.

#### 2.2 Via Composer Create-Project

1. Situa't a la carpeta del projecte i executa la comanda de Composer `create-project` en el terminal:
  `$ composer create-project --prefer-dist laravel/laravel blog`
    * `blog` s'ha de substituir pel nom del teu projecte.

Això ens descarregarà l'última versió de Laravel i crearà una carpeta anomenada `blog` amb tot el contingut ja preparat.

### 3. Servidor de desenvolupament local

Si teniu PHP instal·lat localment i voleu utilitzar el servidor de desenvolupament integrat de PHP per a servir la vostra aplicació, podeu utilitzar la comanda Artisan `serve`.

1. Arrenca l'aplicació de prova (inicia un petit servidor de desenvolupament a `http://localhost: 8000`):

  `$ php artisan serve`

2. Comprova la app amb el navegador a:
  `http://localhost:8000`

![](/assets/laravel-homepage.png)


### 4. Configuració
Finalitza la configuració de Laravel seguint la [documentació](https://laravel.com/docs/5.7#configuration).


#### Application Key

Ens hem d'assegurar que estigui correctament configurat és la key o clau de l'aplicació. Aquesta clau és una cadena de 32 caràcters que s'utilitza per codificar les dades. En cas de no establir-la (revisar la variable `APP_KEY` definida en el fitxer `.env`) la nostra aplicació no serà segura.
Per crear-la simplement hem d'executar la següent comanda a la carpeta arrel de la nostra aplicació:

`php artisan key: generate`

