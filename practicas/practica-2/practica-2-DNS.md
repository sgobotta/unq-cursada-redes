# Redes de Computadoras

> Santiago Botta

## Practica II - DNS


### Problema 1

**Mediante una búsqueda localice la página web de NIC Argentina. Se pide:**  
**a)** Encontrar la Razón Social del dominio pagina12.com.ar  
**b)** ¿Qué direcciones IP tienen los DNS del dominio inti.gob.ar?  
**c)** Encontrar si se encuentra disponible el dominio greenpeace.org.ar  
**d)** Encontrar los requisitos necesarios para registrar un dominio .ar  
**e)** ¿Adónde debe registrar un dominio edu.ar?

**a)** Ingresando en la web de `nic.ar` es posible consultar un dominio y, si ya está siendo utilizado, nos provee algunos datos. Por ejemplo, consultando `pagina.12.com.ar` podemos obtener datos de dominio como, nombre y apellido: `EDITORIAL LA PAGINA SA`, razón social: **30612700776**, fecha de alta: `01/01/1996`, fecha de vencimiento: `10/03/2021`.

**b)** Los servidores DNS de inti.gob.ar:
+   dnsexterno1.inti.gob.ar.
    +   **IP Address:** 200.10.161.45
+   dnsexterno2.inti.gob.ar.
    +   **IP Address:** 200.10.161.46

**c)** El dominio `greempeace.org.ar` no se encuentra disponible y los datos de dominio son:
+   **Nombre y Apellido:** FUNDACION GREENPEACE ARGENTINA
+   **CUIT/CUIL/ID:** 33634172349
+   **Fecha de Alta: 28/11**/2014
+   **Fecha de vencimiento:** 28/11/2020 

**d)** El instructivo para registrar un dominio `.ar` se encuentra en la siguiente url: **https://nic.ar/es/ayuda/instructivos/habilitacion-de-zonas-especiales** y es necesario contar con Clave Fiscal Nivel 2 para los casos de residentes en el país, de lo contrario es necesario seguir otro instructivo indicado también en la dirección detallada anteriormente.

**e)** Los registros para dominios `edu.ar` son gestionados por la Asociación Redes de Interconexión Universitaria (ARIU). Es necesario primero consultar los procedimientos y guías del solicitante y luego llevar a cabo el registro en el siguiente formulario: **https://riu.edu.ar/dominios-edu-ar/registro-y-delegacion-de-nombres-del-subdominio-edu-ar/**


### Problema 2

**Consulta DNS. Explique brevemente cuál es la consulta y qué significa la respuesta:**

```bash
$ nslookup -q=cname www.anta.gov.ar
Server: o200.prime.com.ar
Address: 200.44.0.108
Non-authoritative answer:
www.anta.gov.ar canonical name = heidi.anta.gov.ar
Authoritative answers can be found from:
anta.gov.ar nameserver = deisy.anta.gov.ar
anta.gov.ar nameserver = samantha.anta.gov.ar
deisy.anta.gov.ar internet address = 200.10.166.34
samantha.anta.gov.ar internet address = 200.10.166.31
```

En éste caso se esta llevando a cabo una consulta o query por `canonical name` (CNAME), utilizando el programa `nslookup` pasando como argumento `www.anta.gov.ar`. La respuesta nos dice que:
+   `Server`: se refiere al servidor desde donde se está realizando la consulta
+   `Address`: nos detalla la dirección del server que está realizando la consulta
+   `Non-authoritative answer` nos comunica que el servidor desde el que solicitamos la consulta no se encuentra en la lista de servidores "oficiales" o autoritarios del dominio que estamos consultando, por lo tanto la respuesta *no autoritaria* o *no acreditada*.
    +   La respuesta contiene un nombre canónico a `www.anta.gov.ar`, llamado `heidi.anta.gov.ar`.
+   A continuación, la respuesta nos indica cómo obtener una respuesta autoritaria, es decir, de servidores acreditados u oficiales a devolver respuestas de `www.anta.gov.ar`, estos son sus name server con sus ips:
    +   **NS:** `deisy.anta.gov.ar`, **IP:** `200.10.166.34`
    +   **NS:** `samantha.anta.gov.ar`, **IP:** `200.10.166.31`


### Problema 3

**Encontrar la dirección IP de los servidores de correo electrónico del dominio facebook.com ¿Cómo lo hizo?**

Utilizando el programa `nslookup` es posible utilizar la query `mx` para obtener datos sobre el servicio de mail exchange de un servidor dado, en éste caso el que se encuentra bajo el nombre `facebook.com`:

```bash
$ nslookup
set q=mx
facebook.com
# Respuesta sobre el servicio de mail exchanger con prioridad 10 en `smtpin.vvv.facebook.com.`
facebook.com	mail exchanger = 10 smtpin.vvv.facebook.com.
```


### Problema 4

**El siguiente es un extracto de un archivo de log generado por un servidor DNS que recibe consultas. Explique brevemente qué
significa cada línea.**

```text
Aug 03 10:21:47.999 client 200.11.114.35#51521: query: dymail.com.ar IN MX
Aug 03 10:21:48.397 client 200.11.114.35#51526: query: segemar.inpa.com.ar IN A
Aug 03 10:21:48.440 client 200.11.114.35#51527: query: shell.com IN MX
Aug 03 10:21:48.443 client 200.11.114.35#51528: query: dymail.com.ar IN MX
Aug 03 10:21:48.657 client 200.11.114.35#51530: query: gina.inpa.com.ar IN A
Aug 03 10:21:48.662 client 200.11.114.35#51531: query: earthlink.com IN MX
Aug 03 10:21:48.699 client 200.11.114.22#1028: query: clarin.com IN MX
Aug 03 10:21:48.732 client 200.11.114.22#1028: query: smtp.agea.com.ar IN A
Aug 03 10:21:49.904 client 200.11.114.14#32943: query: pop3.inpa.com.ar IN A
Aug 03 10:21:50.958 client 200.11.114.205#1806: query: www.clarin.com IN A
```

+   `Aug 03 10:21:47.999 client 200.11.114.35#51521: query: dymail.com.ar IN MX`  
    *Registro de un pedido realizado por el cliente con IP address `200.11.114.35`, consultando por los servidores de mail exchange para el servidor con nombre `dymail.com.ar`, el día 3 de Agosto a las 10:21:47*

+   `Aug 03 10:21:48.397 client 200.11.114.35#51526: query: segemar.inpa.com.ar IN A`  
  *Registro de un pedido realizado por el cliente con IP address `200.11.114.35`, consultando por la dirección de servidor con nombre `segemar.inpa.com.ar`, el día 3 de Agosto a las 10:21:48*

+   `Aug 03 10:21:48.440 client 200.11.114.35#51527: query: shell.com IN MX`  
  *Registro de un pedido realizado por el cliente con IP address `200.11.114.35`, consultando por los servidores de mail exchange para el servidor con nombre `shell.com`, el día 3 de Agosto a las 10:21:48*

+   `Aug 03 10:21:48.443 client 200.11.114.35#51528: query: dymail.com.ar IN MX`  
  *Registro de otro pedido realizado por el cliente con IP address `200.11.114.35`, consultando nuevamente por los servidores de mail exchange para el servidor con nombre `dymail.com.ar`, el día 3 de Agosto a las 10:21:48*

+   `Aug 03 10:21:48.657 client 200.11.114.35#51530: query: gina.inpa.com.ar IN A`  
  *Registro de un pedido realizado por el cliente con IP address `200.11.114.35`, consultando por la dirección de servidor con nombre `gina.inpa.com.ar`, el día 3 de Agosto a las 10:21:48*

+   `Aug 03 10:21:48.662 client 200.11.114.35#51531: query: earthlink.com IN MX`  
  *Registro de un pedido realizado por el cliente con IP address `200.11.114.35`, consultando por los servidores de mail exchange para el servidor con nombre `earthlink.com`, el día 3 de Agosto a las 10:21:48*

+   `Aug 03 10:21:48.699 client 200.11.114.22#1028: query: clarin.com IN MX`  
  *Registro de un pedido realizado por el cliente con IP address `200.11.114.22`, consultando por los servidores de mail exchange para el servidor con nombre `clarin.com`, el día 3 de Agosto a las 10:21:48*

+   `Aug 03 10:21:48.732 client 200.11.114.22#1028: query: smtp.agea.com.ar IN A`  
  *Registro de un pedido realizado por el cliente con IP address `200.11.114.22`, consultando por la dirección de servidor con nombre `smtp.agea.com.ar`, el día 3 de Agosto a las 10:21:48*

+   `Aug 03 10:21:49.904 client 200.11.114.14#32943: query: pop3.inpa.com.ar IN A`  
  *Registro de un pedido realizado por el cliente con IP address `200.11.114.14`, consultando por la dirección de servidor con nombre `pop3.inpa.com.ar`, el día 3 de Agosto a las 10:21:49*

+   `Aug 03 10:21:50.958 client 200.11.114.205#1806: query: www.clarin.com IN A`  
  *Registro de un pedido realizado por el cliente con IP address `200.11.114.205`, consultando por la dirección de servidor con nombre `www.clarin.com`, el día 3 de Agosto a las 10:21:50*


### Problema 5

**Para cada ítem, indicar si es verdadero o falso. Justificar.**

+   **SOA:** Identifica al servidor autoritario de una zona y sus parámetros de configuración.
  **Verdadero**. Un registro `SOA` identifica el servidor autoritario en su respuesta bajo el atributo `origin`, y la configuración de éste contempla: versión serial de la configuración, dirección de correo, y tiempos de refresco, expiración, entre otros, en segundos. Todo servidor dns puede tener su propio registro soa configurado.

+   **NS:** Identifica servidores de nombres autorizados para una zona.
  **Verdadero**. Identifica los **nombres** de los servidores con autoridad para una zona, o las **IP**, según se hayan asignado en el registro NS del servidor al que se realiza la consulta.
+   **A:** Asocia un nombre de dominio FQDN con una dirección IP.
    **Verdadero**. Actúa como un puntero hacia una dirección IP dado un nombre.
+   **CNAME:** Permite asignar uno o más nombres a una máquina.
    **Verdadero**. Es un alias para un nombre de máquina.


### Problema 6

**¿Qué sucede cuando un servidor DNS secundario de una zona no se comunica con el primario después de 5 minutos? ¿Y de 5 horas? ¿Y de 5 días? Asuma los siguientes valores del registro SOA de esa zona:**

```bash
Serial = 7741266
Refresh = 7200 (segundos) # 2 horas
Retry = 1800 (segundos)   # 1/2 hora
Expire = 86400 (segundos) # 1 día
```

Los valores indicados especifican cómo se va a comportar el servidor secundario en cuanto a la información que contiene del servidor primario. El valor retry denota la tolerancia de información potencialmente desactualizada, es decir, necesita corroborar cada dos horas que la información que tiene acerca del servidor primario está actualizada. Si no pudo refrescar esa información en el período indicado por refresh (2 horas), volverá a intentarlo cada media hora. Pasado un día la información sobre ése servidor primaria caducará.
Asumo que *no se comunica con el primario* se refiere a que su último intento de refrescar (**refresh**) no tuvo éxito, por lo tanto:
    + si pasaron 5 minutos desde el último refresh sin éxito, esperar `30 minutos` para reintentar.
    + pasadas 5 horas, el servidor secundario habrá intentado conectarse cada media hora y lo seguirá haciendo.
    + pasados 5 días ya no podrá conectarse, dado que la información del servidor primario caduca en `1 día`, según el valor declarado en `Expire`.


### Problema 7

**Se tiene un servidor dns autoritativo para la zona ernest.homedns.org.**

```
ernest.homedns.org 1w IN SOA    ernest.homedns.org root.ernest.homedns.org (
                                    2005091900; serial
                                    3h; refresh
                                    1h; retry
                                    1w; expire
                                    1h; neg cache
                                )
ernest.homedns.org    IN NS     leonov.ernest.homedns.org.
gagarin               IN A      192.168.0.1
leonov                IN A      192.168.0.2
armstrong             IN A      192.168.0.5
time                  IN CNAME  leonov.ernest.homedns.org
imap                  IN CNAME  mail.google.com
```

**a)** ¿Cuáles son los servidores DNS de esta zona? Incluya nombre y dirección IP.  
**b)** ¿Qué va a responder un servidor DNS si se le pregunta por el registro A = armstrong.ernest.homedns.org?  
**c)** ¿Qué va a responder si se le pregunta por el registro A = time.ernest.homedns.org?  


**a)** Los servidores DNS de ésta zona son:
+   nombre: `leonov`, ip: `192.168.0.2`

**b)** El servidor responderá con la dirección `192.168.0.5` ante una consulta de tipo `A` en `armstrong.ernest.homedns.org`.

**c)** Ante una consulta de tipo `A` con valor `time.ernest.homedns.org`, el servidor averiguará qué es `time`, que tiene nombre canónico `leonov.ernest.homedns.org`. Luego, la consulta de tipo `A` se estaría referenciando con el valor `leonov.ernest.homedns.org` y la respuesta sería `192.168.0.2`.


### Problema 8

**El archivo "db.midominio.local" contiene la siguiente información:**

```
midominio.local.    IN    SOA   servidor.midominio.local. (
                                    1       ;serial
                                    10800   ;3 horas
                                    900     ;15 minutos
                                    604800  ;1 semana
                                    86400   ;1 día
                                )
midominio.local.    IN    A     192.168.1.1
midominio.local.    IN    NS    servidor.midominio.local
```
**Se quiere añadir líneas al archivo para indicar:**  
**a)** Un nuevo servidor DNS de la zona midominio.local llamado ns1 que tiene dirección IP 192.168.1.5  
**b)** Un servidor Web llamado bender con dirección IP 192.168.1.10  
**¿Cómo serían esas líneas?**

**a)**
```
ns1.servidor.midominio.local    IN    A     192.168.1.5
```

**b)** 
```
bender                          IN    A     192.168.1.10
```


### Problema 9

**Un servidor DNS acepta consultas de parte de los clientes de un ISP. Estas consultas son recursivas. Para satisfacerlas, el servidor realiza consultas iterativas tratando de obtener la información de los usuarios. Una vez obtenida una respuesta de un servidor, este la cachea por el tiempo indicado de acuerdo con el estándar. Se realizan las siguientes consultas todas de tipo A, en orden:**

```
    www.microsoft.com
    www.ibm.com
    www.dc.uba.ar
    alice.ibm.com
    www.dm.uba.ar
```

**¿A los servidores de qué zonas se les preguntará cuando se hagan los pedidos? ¿Qué tipos de respuestas darán? Suponer que todas las respuestas existen, pasan al caché y no llegan a expirar.  
Asumir que hay servidores autoritativos para las zonas:** *(.) , com. , microsoft . com . , ibm. com . ,ar. , uba.ar , dc.uba.ar. , dm.uba.ar.*

Se efectuarán consultas a los servidores de las zonas: `.`, `com.`, `ar.` y `uba.ar.`.

+   Para `www.microsoft.com` se consultará a la zona `.`, luego la zona `com.` y luego `microsoft.com.`
+   Para `www.ibm.com` se consultará directamente a `com.`.
+   Para `www.dc.uba.ar` se consultará a la zona `.` acerca de la zona `ar.` que, a su vez, consultará directamente a la zona `uba.ar.`, luwgo `dc.uba.ar.`.
+   Para `alice.ibm.com` el servidor consultará a la zona `ibm.com.` previamente cacheada por la dirección de `alice.ibm.com`
+   Para `www.dm.uba.ar`, el servidor consultará a `uba.ar.` por la zona `dm.uba.ar`.

Observación: como el servidor ISP realiza consultas iterativas para satisfacer la necesidad de los clientes, solamente mantedrá en cache la dirección final obtenida, por ej: `www.dm.uba.ar` y no las direcciones de la zona `ar`, `uba` y `dm`, a través de los servidores root.


### Prolema 10

**Explicar brevemente el significado de cada entrada de la siguiente porción de un archivo de configuración de la base de datos del DNS para el dominio cs.vu.nl**

```
;Authoritative data for cs.vu.nl

cs.vu.nl.         86400   IN  SOA     star boss (9527,7200,7200,241920,86400)
cs.vu.nl.         86400   IN  TXT     "Divisie Wiskunde en Informatica."
cs.vu.nl.         86400   IN  TXT     "Vrije Universiteit Amsterdam."
cs.vu.nl.         86400   IN  MX      1 zephyr.cs.vu.nl.
cs.vu.nl.         86400   IN  MX      2 top.cs.vu.nl.

flits.cs.vu.nl.   86400   IN  HINFO   Sun Unix
flits.cs.vu.nl.   86400   IN  A       130.37.16.112
flits.cs.vu.nl.   86400   IN  A       192.31.231.165
flits.cs.vu.nl.   86400   IN  MX      1 flits.cs.vu.nl
flits.cs.vu.nl.   86400   IN  MX      2 zephyr.cs.vu.nl
flits.cs.vu.nl.   86400   IN  NX      3 top.cs.vu.nl
www.cs.vu.nl      86400   IN  CNAME   star.cs.vu.nl
ftp.cs.vu.nl      86400   IN  CNAME   zephyr.cs.vu.nl

rowboat                   IN  A       130.37.53.201
                          IN  MX      1 rowboat
                          IN  MX      2 zephyr
                          IN  HINFO   Sun Unix

little-sister             IN  A       130.37.62.23
                          IN  HINFO   Mac MacOS

laserjet                  IN  A       192.31.231.216
                          IN HINFO    "HP Laserjet IIISi" Propietary
```

+   `;Authoritative data for cs.vu.nl`  
  *Información de respuesta autoritativa para el servidor con nombre cs.vu.nl*

+   `cs.vu.nl.         86400   IN  SOA     star boss (9527,7200,7200,241920,86400)`  
  *Información del registro soa para el servidor DNS con nombre `cs.vu.nl.`*

+   `cs.vu.nl.         86400   IN  TXT     "Divisie Wiskunde en Informatica."`  
  *El registro TXT provee texto arbitrario proporcionado por el servidor, en éste caso el valor `"Divisie Wiskunde en Informatica."`*

+   `cs.vu.nl.         86400   IN  TXT     "Vrije Universiteit Amsterdam."`  
  *El registro TXT provee texto arbitrario proporcionado por el servidor, en éste caso el valor `"Vrije Universiteit Amsterdam."`*

+   `cs.vu.nl.         86400   IN  MX      1 zephyr.cs.vu.nl.`  
  *Registro de un servidor que provee el servicio de Mail Exchange para cs.vu.nl. de mayor prioridad*

+   `cs.vu.nl.         86400   IN  MX      2 top.cs.vu.nl.`  
  *Registro de un servidor que provee el servicio de Mail Exchange para cs.vu.nl. con menor prioridad que el anterior*

+   `flits.cs.vu.nl.   86400   IN  HINFO   Sun Unix`  
  *Este registro provee información del Host de flits.cs.vu.nl, en éste caso acerca del sistema operativo: Sun Unix*

+   `flits.cs.vu.nl.   86400   IN  A       130.37.16.112`  
  *Registro de dirección para el nombre flits.cs.vu.nl. con valor 130.37.16.112*

+   `flits.cs.vu.nl.   86400   IN  A       192.31.231.165`  
  *Registro de dirección para el nombre flits.cs.vu.nl. con valor 192.31.231.165*

+   `flits.cs.vu.nl.   86400   IN  MX      1 flits.cs.vu.nl`  
  *Registro de un servidor que provee el servicio de Mail Exchange para flits.cs.vu.nl. de mayor prioridad.*

+   `flits.cs.vu.nl.   86400   IN  MX      2 zephyr.cs.vu.nl`  
  *Registro de un servidor que provee el servicio de Mail Exchange para flits.cs.vu.nl. de menor prioridad que el anterior.*

+   `flits.cs.vu.nl.   86400   IN  MX      3 top.cs.vu.nl`  
  *Registro de un servidor que provee el servicio de Mail Exchange para flits.cs.vu.nl. de aún menor prioridad que el anterior.*

+   `www.cs.vu.nl      86400   IN  CNAME   star.cs.vu.nl`  
  *Registro de alias `www.cs.vu.nl` para el nombre `star.cs.vu.nl`.*

+   `ftp.cs.vu.nl      86400   IN  CNAME   zephyr.cs.vu.nl`  
  *Registro de alias `ftp.cs.vu.nl` para el nombre `zephyr.cs.vu.nl`.*

+   `rowboat                   IN  A       130.37.53.201`  
  *Registro de dirección para el nombre rowboat.cs.vu.nl con valor 130.37.53.201*

+   `rowboat                   IN  MX      1 rowboat`  
  *Registro de un servidor que provee el servicio de Mail Exchange para rowboat.cs.vu.nl. de mayor prioridad.*

+   `rowboat                   IN  MX      2 zephyr`  
  *Registro de un servidor que provee el servicio de Mail Exchange para rowboat.cs.vu.nl. de menor prioridad que el anterior.*

+   `rowboat                   IN  HINFO   Sun Unix`  
  *Este registro provee información del Host rowboat.cs.vu.nl., en éste caso acerca del sistema operativo: Sun Unix*

+   `little-sister             IN  A       130.37.62.23`  
  *Registro de dirección para el nombre little-sister.cs.vu.nl con valor 130.37.62.23*

+   `little-sister             IN  HINFO   Mac MacOS`  
  *Este registro provee información del Host little-sister.cs.vu.nl., en éste caso acerca del sistema operativo: Mac MacOS*

+   `laserjet                  IN  A       192.31.231.216`  
  *Registro de dirección para el nombre laserjet.cs.vu.nl con valor 192.31.231.216*

+   `laserjet                  IN HINFO    "HP Laserjet IIISi" Propietary`  
  *Este registro provee información del Host laserjet.cs.vu.nl., en éste caso acerca del sistema operativo: "HP Laserjet IIISi" Propietary*


### Problema 11

**A continuación se enumeran dos name servers. Se pide encontrar primero la dirección IP de un servidor de mails para el dominio uba.ar y luego la del nombre de dominio milagros.dc.uba.ar, explicite los servidores que se cachean y como se los aprovecha para acelerar la consulta. Suponga que ya está cacheada la dirección del name server de uba.ar.**

```
uba.ar. 1w              IN    SOA     uba.ar backup.servidormisterioso.ar admin.uba.ar(
                                          2005091900; serial
                                          3h; refresh
                                          1h; retry
                                          1w; expire
                                          1h; neg cache
                                      )
uba.ar.                 IN    NS      servidores.uba.ar
uba.ar.                 IN    MX      mailserver.uba.ar
rectorado               IN    CNAME   secretaria.uba.ar
dc.uba.ar.              IN    NS      servidores.dc.uba.ar
servidores              IN    A       208.25.19.1
servidores.dc.uba.ar.   IN    A       208.190.1.4
mailserver              IN    A       208.25.19.2
secretaria              IN    A       208.25.19.87

dc.uba.ar.              IN    SOA     dc.uba.ar mateo.dc.uba.ar(
                                          2005091900; serial
                                          3h; refresh
                                          1h; retry
                                          1w; expire
                                          1h; neg cache
                                      )
dc.uba.ar.              IN    NS      servidores.dc.uba.ar
dc.uba.ar.              IN    MX      mailserver.dc.uba.ar
servidores.dc.uba.ar.   IN    A       208.190.1.4
mailserver              IN    A       208.190.1.32
milagros                IN    A       208.190.1.15
morza                   IN    A       208.190.1.20
```

+   Dirección de correo para el dominio `uba.ar`

    +   *Se solicita a uba.ar una dirección para manejar intercambio de correo. El servidor responde con `mailserver.uba.ar`.*
    +   *Luego se solicita a `mailserver.uba.ar` una dirección para el servidor de intercambio de correo. El servidor responde que `servidores.uba.ar` maneja las resoluciones de nombres, en éste caso `mailserver`.*
    +   *Se solicita un servidor de intercambio de correo a `servidores.uba.ar`. El servidor responde con la dirección `200.25.19.1` y ante la respuesta exitosa se cachea `servidores.uba.ar` bajo la dirección.*
    +   *Se envía una solicitud por `mailserver.uba.ar` a `200.25.19.1 (servidores.uba.ar)`, se resuelve que la dirección para `mailserver` es `208.25.19.2`, se responde y se cachea mailserver.uba.ar con esa dirección.*

+   Dirección de correo para el dominio `milagros.dc.uba.ar`

    +   *Se solicita a uba.ar una dirección para manejar intercambio de correo en `milagros.dc.uba.ar`. El servidor responde que `dc.uba.ar` lo maneja `servidores.dc.uba.ar`*
    +   *Se solicita a uba.ar una dirección para el nombre `servidores.dc.uba.ar`. El servidor responde con `208.190.1.4`.*
    +   *Se solicita a `servidores.dc.uba.ar` una dirección para manejar intercambio de correo en `milagros.dc.uba.ar`. El servidor responde que se encuentra bajo el nombre `mailserver.dc.uba.ar`. Se cachea en `servidores.dc.uba.ar` la dirección `208.190.1.4` y ns `dc.uba.ar` en `servidores.dc.uba.ar`.*
    +   *Se solicita a `208.190.1.4` una dirección para el servidor con nombre `mailserver.dc.uba.ar`. El servidor responde con `208.190.1.32`.*

