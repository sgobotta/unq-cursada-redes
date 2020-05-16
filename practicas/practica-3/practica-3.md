# Redes de Computadoras

> Santiago Botta

## Practica III - Correo Electrónico

### Problema 1

**En los sistemas de correo electrónico todas las transferencias de correo se realizan usando SMTP, con la excepción de la entrega al usuario final.**

**a)** ¿Qué diferencia hay entre el Webmail, POP3 e IMAP, como soluciones para revisar el correo?  
**b)** ¿Cuáles se parecen más entre sí en cuanto a su forma de operar?  

**a)** La principal diferencia es que Webmail es un software, generalmente hosteado en los servidores de mailing que permite a usuarios acceder a su correo mediante un cliente web: es necesario estar conectado a una red para leer correos. En cambio, POP3 e IMAP son protocolos de entrada de correos. Un cliente desktop generalmente posee la capacidad de permitir a un usuario configurar su cuenta de correo, en la que debe seleccionar qué protocolo desea utilizar para recibir el correo: **IMAP** o **POP3**. A su vez, el servidor que gestiona el intercambio de correos debe permitir la utilización de éstos protoclos para que clientes desktop puedan comunicarse.  
**b)** POP3 e IMAP son los más parecidos entre si en el sentido en que son protocolos para el recupero de correo y ambos utilizan puertos de una máquina. Sin embargo existen diferencias entre ellos. Por ejemplo: POP3 se utiliza para descargar correos del servidor a una maquina local. Si bien esto aparenta ser una ventaja para ahorrar espacio en el servidor, moviendo los mensajes de allí a una máquina local, si utilizamos diferentes dispositivos para acceder al correo, por ejemplo un teléfono móvil, podríamos no encontrar correos que hayamos descargado desde nuestra máquina con POP3. IMAP resuelve eśte conflicto, pero presenta la desventaja de no descargar los correos: éstos permanecen en el servidor, y podrían ser de cantidad limitada dependiendo del servidor utilizado.


### Problema 2

**Estoy viajando y mi única forma de acceder al correo electrónico de la universidad es usando mi teléfono móvil. ¿Cuáles de las siguientes opciones es más eficiente?**

**c)** Acceso a SMTP  
**d)** Acceso a POP3  
**e)** Acceso a IMAP  
**f)** Acceso a message/HTML  

Si el teléfono es el único medio utilizado para acceder al correo, tanto POP3 como IMAP para la recepción serían buenas soluciones. Es posible que en nuestro viaje no contemos con conexión a internet y la descarga de correo con POP3 podría ser de gran utilidad. Si la conexión no sería un problema, una buena opción para gestionar la recepción de correo es configurarla con el protoclo IMAP y, eventualmente, no será un conflicto acceder al correo desde otro dispositivo además del teléfono móvil.


### Problema 3

**La incorporación al correo electrónico del formato HTML hizo posible enviar texto con formato e imágenes embebidas, algo imposible con anterioridad. Explicar cómo se puede lograr el envío y procesamiento de un nuevo formato de archivo (como la transición de texto a HTML) sin que esto implique un cambio en todos los servidores SMTP del mundo**

El envío y procesamiento de nuevos tipos de archivo se puede dar con la definición de encabezados RFC 822 agregados por MIME, dónde será necesario especificar cuál es la naturaleza del mensaje `Content-Type` y cómo se envuelve el mensaje para su transmisión `Content-Transfer-Enconding`.


### Problema 4

**Un usuario va a transmitir un correo electrónico a través de un sistema de correo web. ¿Qué protocolos de aplicación pueden verse involucrados hasta que dicho correo es recibido por un lector de correo convencional?**

Cuando un usuario envía un correo desde un sistema de correo web (webmail), los protocolos involucrados son:
+   `HTTP` cuando la aplicación web de correo envía un pedido al servidor que maneja el correo.
+   `SMTP` cuando el servidor de correo envía el correo al dominio indicado en la cabecera **To** del correo.

Luego, al recibir el correo, el usuario receptor podría estar utilizando cualquiera de los dos protocolos posibles para interactuar durante la recepción de correo: `POP3` o `IMAP`.

### Problema 5

**Interprete la siguiente secuencia de comandos realizadas desde un servidor cualquiera en Internet.**

```bash
$ telnet pop3.inta.gov 110
Trying 200.11.141.35...
Connected to pop3.inta.gov
Escape character is '^]'.
# El servidor responde `OK`, está listo para recibir comandos
+OK POP3 pop3.inta.gov v2001.78 server ready
# Intenta autenticarse con usuario `prueba`
user prueba
# El servidor responde `OK` y mensaje
+OK User name accepted, password please
# Intenta autenticarse con contraseña `xxxxxxx`
pass xxxxxxx
+OK Mailbox open, 7 messages
# Solicita el listado de correo
list
# El servidor responde con una lista de correos finalizada con `.`
+OK Mailbox scan listing follows
1 14391
2 3884
3 1079
4 1257
5 1085
6 1086
7 6634
.
# Cierra la conexión con el comando `quit`
quit
# EL servidor responde `OK` y el mensaje `Sayonara`
+OK Sayonara
Connection closed by foreign host.
```

Se agregan comentarios `(#)` durante la secuencia para denotar la interpretación.


### Problema 6

**Introduce las órdenes necesarias para, tras ejecutar en el computador labrdc01.redes.unq.edu.ar la orden telnet smtp.unq.edu.ar 25, enviar un correo electrónico a profes@redes.unq.edu.ar con asunto "Problema 4" y que incluya en el mensaje el texto: “Examen de redes”. El remitente del correo es alumno@redes.unq.edu.ar.**

```bash
$ telnet smtp.unq.edu.ar 25
EHLO hermes.correo.unq.edu.ar
MAIL FROM: <alumno@redes.unq.edu.ar>
RCPT TO: <profes@redes.unq.edu.ar>
DATA
Subject: Problema 4

Examen de redes

QUIT
```


### Problema 7

**Un usuario se sienta en su computadora hogareña. Consulta el estado del tiempo en la página del servicio meteorológico nacional, luego manda un mail usando un agente usuario a una dirección en el dominio dc.uba.ar.**  
**a)** ¿Cuántos flujos de datos desencadena el usuario?  
**b)** Describa una posible secuencia de mensajes DNS que se desencadenaría para concretar el envío del mail.  
*Asumir que las caches están vacías (DNS y HTTP)*


> **Ayuda:** *“A un conjunto de paquetes que van de un origen a un destino se le denomina flujo (Clark, 1988). En una red orientada a conexión, un flujo podría estar constituido por todos los paquetes de una conexión; o en una red sin conexión, un flujo serían todos los paquetes enviados de un proceso a otro. Podemos caracterizar las necesidades de cada flujo mediante cuatro parámetros principales: ancho de banda, retardo, variación del retardo (jitter) y pérdida. En conjunto, estos parámetros determinan la QoS (Calidad del Servicio, del inglés Quality of Service) que requiere el flujo.”*  
> **Redes de Computadoras. Quinta edición. 5.4.1 Requerimientos de la aplicación.**


**a)** La cantidad de flujos depende de la versión de protcolo HTTP que utilice tanto para las consultas de meteorología así como también dependerá del cliente que esté utilizando para el envío de correo. Supongamos que desde un navegador web se utiliza el protoclo HTTP 1.1 para realizar una consulta a **https://www.smn.gob.ar/**:
+   Existira al menos un flujo para conocer el servidor que gestiona la zona `gob.ar` y `smn.gob.ar` hasta encontrar la dirección del servicio web del servicio meteorológico nacional.
+   Luego se establecerá otra conexión con el sitio web del servicio meteorológico nacional para conocer el estado del tiempo y existirá un segundo flujo.
+   Luego, se desencadenará al menos 1 flujo por parte del srvidor DNS para saber qué dirección gestiona los servidores de la zona `dc.uba.ar.`.
+   Finalmente habrá un flujo más para realizar el envío de correo a los servidores de correo electrónico de la zona `dc.uba.ar.`.

**b)** Una posible secuencia de mensajes tendría la siguiente forma.

+   El cliente de correo web despacha un pedido HTTP hacia los servidores de correo del usuario actual. El servidor que gestiona su correo, a su vez, realiza un pedido SMTP para el envío del correo del cliente.
+   El servidor de correos de éste usuario intenta resolver el dominio `dc.uba.ar` con su resolver, preguntando por su Mail Exchanger (MX).
+   Alguno de los servidores root responderá que es la zona `ar.` quien gestiona lazona `dc.uba.ar`
+   El resolver reenvía el mismo pedido a la zona `.ar` y ésta responde que es `uba.ar.` quien gestiona los servidores de `dc.uba.ar`.
+   El resolver reenvía el mismo pedido a la zona `uba.ar.` y ésta responde que la resolución de nombres para la zona `dc.uba.ar` la gestiona a cabo `servidores.dc.uba.ar`.
+   El resolver pregunta a `dc.uba.ar` por la dirección del servidor `servidores.dc.uba.ar`. El servidor responde con una IP address.
+   El resolver reenvía el pedido de servidor de correos para el dominio `dc.uba.ar` y éste responde con el nombre de servidor `mailserver.dc.uba.ar`.
+   El resolver pregunta a `servidores.dc.uba.ar` por la dirección de `mailserver.dc.uba.ar`. El sercidor responde cona una IP address.
+   Se envía un pedido SMTP al servidor con la IP devuelta que corresponde a `mailserver.dc.uba.ar`, quien gestiona los servidores de correo electrónico para el dominio solicitado.
