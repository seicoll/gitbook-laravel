# Seguretat en serveis REST

Una de les principals característiques dels serveis RESTful respecte a la resta de serveis de comunicacions és que els serveis REST mantenen la informació sobre el seu estat en la banda del client, el servidor no manté cap informació al voltant de l'estat. Això implica que el client ha de proveir de tota la informació necessària per fer la petició del recurs.

## HTTP Basic authentication
El mecanisme més bàsic és la utilització de l'autenticació del protocol HTTP. Aquest mecanisme incorpora a la capçalera HTTP la informació relativa a usuari:password codificada en base64.

```
GET / HTTP/1.1
Host: servidor.cat
Authorization: Basic dXN1YXJpX2FwaTpjbGF1X3NlZ3VyYQ==
```

En l'anterior exemple podem veure la capçalera que es correspondria si el nostre servei es trobés a **_servidor.cat_** i la informació de l'usuari es troba codificada en base64  **_dXN1YXJpX2FwaTpjbGF1X3NlZ3VyYQ==_** que si decodifiquéssim obtindríem **_usuari_api:clau_segura_**

Encara que les credencials estiguin codificades, això no vol dir que estiguin xifrades. Resulta molt fàcil obtenir l'usuari i la clau d'una autenticació bàsica [Decode base64]. No s'ha d'utilitzar aquest esquema d'autenticació en HTTP pla, només s'hauria d'emprar mitjançant SSL/TLS que proporciona comunicacions segures mitjançant protocols criptogràfics.

## HMAC
Un dels principals inconvenients de l'autenticació bàsica és que cal enviar la contrasenya dins de la capçalera de cada sol·licitud. A més aquesta informació no es troba protegida contra manipulacions. Una altra forma de fer-ho és emprant **HMAC** (hash based message authentication), en aquest cas, en lloc d'enviar contrasenyes, en realitat s'envia una versió hash de la contrasenya amb informació addicional. Per exemple, imagineu-vos que tenim les següents credencials: **usuari-> joan** i com a **contrasenya-> secret**. Suposem que intentem accedir a un recurs protegit **/usuaris/joan/registresfinancers**. Primer necessitem obtenir tota la informació necessària i concatenar-la. 

```
GET+/usuaris/joan/registresfinancers
```

Prenem el verb **HTTP** i la **URL** actual, podem afegir-hi informació com la data/hora actual, un numero aleatori o un hash **md5** de cos del missatge per prevenir atacs per modificació o per replay. Un cop obtinguda aquesta informació ens cal calcular el **hmac**:

`digest = base64encode (hmac("sha256","secret","GET+/usuaris/joan/registresfinancers"))`

Ara es pot enviar aquesta informació a traves de la capçalera HTTP:

```
GET /usuaris/joan/registresfinancers HTTP/1.1
Host: servidor.cat
Authorization: hmac joan:[digest]
```

En aquest moment el servidor reconeix que l'usuari **_joan_** intenta accedir a un recurs. Aquest servidor pot generar de nou aquest digest, ja que disposa de tota la informació. (Noteu que la contrasenya està xifrada al servidor i el servidor necessita conèixer-lo, per això se n'anomena secret i no contrasenya).

Si algú intercepta aquesta conversa no podria utilitzar la informació de la connexió per canviar les dades financeres del **_joan_** via POST o PUT, o visualitzar la informació d'un altre usuari, ja que això canviaria el digest. L'únic que es podria fer seria accedir a la informació d'en **_joan_** tantes vegades com es vulgués, ja que no canvia el digest. Per això moltes vegades s'envia més informació, com l'hora actual.

`digest = base64encode (hmac("sha256","secret","GET+/usuaris/joan/registresfinancers+10jan201611:59:45+123456"))`

Afegim dos nous fragments d'informació en el càlcul del digest. La data actual i un número que només es pot emprar un sol cop.

```
ET /usuaris/joan/registresfinancers HTTP/1.1
Host: servidor.cat
Authorization: hmac joan:123456:[digest]
Date: 20 jan  2016 11:59:45
```

El servidor pot reconstruir el digest de nou, però aquest cop el client envia un número i la data. Si la data enviada no es troba dins d'un determinat rang respecte el servidor (10 minuts), el servidor pot ignorar el missatge, ja que segurament es tractaria d'un replay d'un missatge generat anteriorment (també pot ser un error en la data/hora del client)

El número només el podem emprar un cop de forma que si volem accedir al mateix recurs un altre cop, cal canviar aquest numero. D'aquesta forma si en el mateix segon s'intenta accedir al mateix recurs ho detectaríem ja que el digest seria diferent. Així mateix evitaríem els atacs per replay.

## OAuth

Un dels inconvenients del **HMAC** és que no hi ha més contrasenyes, sinó que només hi ha secrets. Quan es descobreix el secret de **_joan_**, tothom pot accedir a aquest compte. Una forma d'evitar això és utilitzar **tokens** temporals, de forma que l'usuari **_joan_** demana al servidor un recurs per a un **token** i **secret** particulars per accedir.

**Oauth** és un mecanisme que permet crear **tokens** temporals, de forma que s'ha convertit en un esquema comú per a l'autenticació i l'autorització encara que resulta una mica més complexa la seva implementació. Existeixen moltes implementacions ja desenvolupades en diferents llenguatges.

## OAuth2
Es tracta d'una nova implementació de OAuth que ha canviat completament la seva estructura. Aquesta nova via resulta més fàcil d'implementar i mantenir, encara que aquesta no s'ha convertit en standard i actualment s'està utilitzant en molts llocs aquest mètode basat en els diferents esborranys. 

##Consideracions

L'autenticació bàsica i **OAuth** haurien d'anar protegides sempre mitjançant **SSL/TLS**, en lloc d'emprar **HTTP**. Emprar nombres nonces pot millorar la seguretat, sempre i quan s'emmagatzemi i es compari en el servidor. Un problema habitual quan s'utilitzen finestres de temps en les peticions, és la sincronia del servidor i el client, sobretot quan el client no té establerta correctament l'hora. Per això cal assegurar-se que tant client com servidor utilitzen sistemes **NTP** per mantenir la sincronia horària.
 

**Més informació:**
[ REST Cookbook ]
[ Def. SSL/TLS ]
[ REST a la pràctica ]