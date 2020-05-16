# Redes de Computadoras

> Santiago Botta

## Práctica I - Introducción

### Problema 1

**Dos factores de red ejercen influencia en el rendimiento de un sistema cliente-servidor: el ancho de banda de la red (cuántos bits
por segundo puede transportar) y la latencia (cuánto tiempo toma al primer bit llegar del cliente al servidor). Mencione un ejemplo
de una red que cuente con ancho de banda y latencia altos. A continuación, mencione un ejemplo de una que cuente con ancho
de banda y latencia bajos.**

En una analogía donde los bits están representados por un flujo de agua, el ancho de banda representado por una tubería y la latencia por la longitud de esa tubería, se entiende que el ancho de banda es proporcional al grosor de la tubería (corre mas cantidad de agua, o bits, por segundo) y la latencia a la longitud de ésta (al ser más larga el flujo tardaría mas en llegar de un extremo al otro). Aunque en las redes éste ultimo punto de latencia no es tan acertado, dado que las líneas de comunicación son extensas, pero existen otros factores que provocan los retardos, es decir que tarde mas tiempo en llegar un mensaje de un origen a un destino

**Ancho de banda y latencia altos**

Una conexión orientada a conexión establecida por ethernet (alto ancho de banda) con un receptor ubicado en otro continente, es decir, existes varias inter-redes de por medio (alta latencia)

**Ancho de banda y latencia bajas**

Una conexión de voz establecida de punto a punto entre hosts hogareños (bajo ancho de banda), ambos ubicados en una misma área metropolitana (baja latencia).

### Problema 2

**¿Además del ancho de banda y la latencia, qué otros parámetros son necesarios para dar un buen ejemplo de la calidad de
servicio ofrecida por una red destinada a tráfico de voz digitalizada?**

En el ejemplo de una red destinada a tráfico de voz digitalizada se espera que el jitter, señal de ruido no deseada o fluctuación de retardo sea lo más balanceada posible, de manera que los paquetes de datos no lleguen ni muy pronto ni muy tarde.

### Problema 3

**Un factor en el retardo de un sistema de conmutación de paquetes de almacenamiento y reenvío es el tiempo que le toma
almacenar y reenviar un paquete a través de un conmutador. Si el tiempo de conmutación es de 10 μseg, ¿esto podría ser un
factor determinante en la respuesta de un sistema cliente-servidor en el cual el cliente se encuentre en Nueva York y el servidor en
California? Suponga que la velocidad de propagación en cobre y fibra es 2/3 de la velocidad de la luz en el vacío.**

Diez nanosegundos es una cifra imperceptible para un ser humano, tal como lo conocemos hoy en día. La distancia entre éstas dos ciudades es de aproximadamente 3.940 kilómetros en línea recta (irreal en el contexto de las redes) y la información viaja a través de un cable de cobre a 200.000 km/s. En un mundo idea sin tráfico en la red, un pedido de un cliente en California a un servidor en New York tardaría ((3.940km * 1seg) / 200.000km) 0.0197 segundos, que equivale a 197.000.000 µseg. Una sola conmutación de 10 nanosegundos sería imperceptible para una persona, por lo tanto no sería un factor determinante.

### Problema 4

**Un sistema cliente-servidor utiliza una red satelital, con el satélite a una altura de 40,000 km. ¿Cuál es el retardo en respuesta a
una solicitud, en el mejor de los casos?**

Suponemos que la velocidad de las ondas de radio es similar a la velocidad de la luz (300.000 km/s), sabemos que el satélite está a 40.000 km de altura pero desconocemos la distancia en la que los **hosts** se encuentran entre sí y tampoco a qué distancia están del satélite, pero asumo que en el mejor de los casos esa distancia es de 0km, no interactúan otras redes más que la del satélite en el medio, la latencia es ínfima y el servidor responde a *una increíble velocidad de 0ms, como si nada hubiera sucedido*.

El primero pedido de cliente tardaría 133.333,33 µseg ((40.000km * 1seg) / 300.000km) en viajar hasta el satélite, luego otros 133.333,33 µseg hasta llegar al servidor. El proceso se repite a la inversa para que la máquina cliente reciba una respuesta, por lo tanto el retardo de la solicitud es el mismo tiempo que el cliente tarda en llegar al servidor, 266.666,66 (133.333,33µseg * 2). El recorrido total sería de 533.333,32µseg.

### Problema 5

**Cuando cada persona tenga una terminal en casa conectada a una red de computadoras, serán posibles las consultas públicas
instantáneas sobre asuntos legislativos pendientes. Con el tiempo, las legislaturas existentes podrían eliminarse, para dejar que la
voluntad popular se exprese directamente. Los aspectos positivos de una democracia directa como ésta son bastante obvios;
analice algunos de los aspectos negativos.**

La identidad de las personas en el mundo virtual, o sea el espacio conectado entre redes, es dudoso: la digitalización de las comunicaciones permite mostrarle al mundo como somos, así como también nos permite re-inventar nuestra identidad hasta el punto de comunicarnos anónimamente con otras personas. La democracia propone un sistema donde cada persona tiene voz y voto en las decisiones que los gobiernos califican como populares. ¿Cómo podría implementarse la democracia tal como la conocemos pero en un mundo digitalizado, dónde los individuos podrían no ser quienes dicen ser? Una solución es mantener digitalmente una referencia en el mundo real por persona pero, ¿quién está a cargo de mantener y gestionar esa información tan personal? Creo que la democracia digital existe en la descentralización de las entidades que hoy tomaron y siguen tomando control sobre muchas de las bases económicas, comunicacionales, políticas, entre otras. pero es solo una vaga idea... Uno nunca está del todo seguro hasta que las cosas suceden.

### Problema 6

**Mencione dos razones para utilizar protocolos en capas.**

Una razón para utilizar protocolos en capas es que pueden ser reutilizados para los servicios que proveen las distintas capas. Retóricamente, ¿por qué combinaríamos **TCP** e **IP** en un servicio de una misma capa? Luego para servicios que necesiten utilizar el protoclo **UDP** deberíamos otra vez realizar una implementación entre la **Capa de transporte** y la **Capa de Red** que combine **UDP** con **IP**. 

Otra razón aún más importante está relacionada con la llegada de nuevas tecnologías. Si por ejemplo el día de mañana contamos con un nuevo dispositivo que dispara rayos laser con datos que viajan 10 veces más rápido que la velocidad de la luz y además soportan un ancho de banda inmenso, con un modelo en capas no tendríamos que re-implementar todos los servicios del modelo TCP/IP, sino que seguramente nos ocupemos de implementar el hardware y/o protocolos necesarios en la **Capa física/Enlace de datos** y/o en la **Capa de Red**: `al utilizar protocolos en capas, éstos serían facilmente reemplazables con el cambio de la tecnología (transparencia ante los cambios)`.

### Problema 7

**Al presidente de Specialty Paint Corp. se le ocurre la idea de trabajar con una compañía cervecera local para producir una lata de
cerveza invisible (como medida para reducir los desechos). El presidente indica a su departamento legal que analice la situación, y
éste a su vez pide ayuda al departamento de ingeniería. De esta forma, el ingeniero en jefe se reúne con su contraparte de la otra
compañía para discutir los aspectos técnicos del proyecto. A continuación, los ingenieros informan los resultados a sus respectivos
departamentos legales, los cuales a su vez se comunican vía telefónica para ponerse de acuerdo en los aspectos legales. Por
último, los dos presidentes corporativos se ponen de acuerdo en la parte financiera del proyecto. ¿Éste es un ejemplo de protocolo
con múltiples capas semejante al modelo OSI?**

Es semejante, pero no preciso si tenemos en cuenta la precisión y cantidad de capas con las que cuenta el modelo OSI (7 capas). En ésta analogía podemos entender a los ingenieros como entidades de la capa mas baja del modelo, los departamentos legales estarían en alguna capa intermedia, mientras que los presidentes representarían la capa mas alta del modelo. Se asemeja a un servicio orientado a conexión donde las diferentes capas interactúan para establecer comunicación entre los presidentes, mediante acuerdos y negociaciones realizadas en las capas inferiores.

### Problema 8

**Los Ministros de Relaciones Exteriores frecuentemente intercambian información relativa al desarrollo de las relaciones
diplomáticas entre los países que representan. El Canciller de Argentina desea entregarle cierta información a su par de Francia.
El Canciller argentino confecciona el mensaje en castellano y lo entrega a la Oficina de Traducciones del Consulado donde el
mismo es transcripto a un idioma común de intercambio entre traductores, para el caso, el idioma inglés. Luego de traducido el
mensaje es entregado por la OT a la Oficina Criptográfica, la cual se encarga de codificar el mensaje para evitar filtraciones de
seguridad. La OC a su turno entrega el mensaje ya encriptado a la Oficina de Comunicaciones la que se encarga de la transmisión
del mensaje, que es recibido por una dependencia similar en la Cancillería Francesa. Una vez recibido en Francia por la Oficina de
Comunicaciones, el mensaje es entregado a la Oficina Criptográfica la cual luego de descifrarlo lo entrega a la Oficina de
Traducciones desde donde, luego de traducido al idioma nativo, es recibido por el Canciller francés. ¿Es este un ejemplo de un
protocolo multicapa en el sentido del modelo OSI? En caso afirmativo determinar distintos niveles de comunicación. Para cada
nivel definir el servicio genérico que brinda y los protocolos utilizados.**

Si, se trata de un ejemplo semejante, pero sin brindar detalle sobre las capas de Red, Enlace y Física, dado que no se obtienen detalles sobre el tipo de servicio de mensajería (Red), ni "tracking" del estado de envío del mensaje o por todos los puntos en los que viaja hasta llegar (Enlace), ni tampocoe el medio por el cuál se realiza el envío de mensaje (Física). Los cancilleres son partícipes en los servicios de la **Capa de Aplicación**, los consulados realizan una negociación, en éste caso el idioma, como si se tratase de servicios en la **Capa de Presentación**. A su vez, las oficinas criptográficas brindan un servicio de encriptación/"desencriptación" que se podría corresponder a la **Capa de Sesión**. Finalmente la oficina de comunicaciones actúa como la **Capa de transporte**. Parece tratarse de un tipo de comunicación no orientada a conexión, donde el host de origen no recibe una notificación de recepción del mensaje.

### Problema 9

**¿Cuál es la diferencia principal entre comunicación orientada a la conexión y no orientada a ésta?**

La diferencia principal es que en una comunicación **orientada a conexión** primero es necesario establecer una comunicación entre el emisor y receptor para poder intercambiar mensajes. En cambio, en una comunicación **no orientada a conexión**, cada mensaje que un emisor desee enviar a un receptor viaja con la dirección del host de destino para ser enrutados a los nodos intermedios de la red que se utilice.

### Problema 10

**¿Qué significa “negociación” en el contexto de protocolos de red? Dé un ejemplo.**

La negociación en el contexto de protocolos se puede entender como una propuesta entre dos partes para entender qué parámetros van a utilizar, qué tamaño tendrán los mensajes o cuál será la calidad de servicio. Por ejemplo, en una comunicación orientada a conexión se establecerá cuál será el tamaño de los paquetes que se enviarán, o cuando una compañía de servicios de comunicación establece cuál será el ancho de banda de los recursos asociados.

### Problema 11

**En la figura 1-19 se muestra un servicio. ¿Hay algún otro servicio implícito en la figura? Si es así, ¿dónde? Si no lo hay, ¿por qué
no?**

Sí. Los servicios proporcionados por la capa `k - 1` para la capa `k` están implícitos, así como también los servicios proporcionados por las capas inferiores a las superiores. La figura es independiente al modelo del que se esté hablando, dado que tanto el modelo `OSI`, como el modelo `TCP/IP` y el modelo del libro interactúan de la misma manera, pero con más o menos jerarquía de capa, según a cual se refiera.

### Problema 12

**En algunas redes, la capa de enlace de datos maneja los errores de transmisión solicitando que se retransmitan las tramas
dañadas. Si la probabilidad de que una trama se dañe es p, ¿cuál es la cantidad media de transmisiones requeridas para enviar
una trama? Suponga que las confirmaciones de recepción nunca se pierden.**

Si contamos con una probabilidad `p` de que una trama se dañe, entonces eventualmente se requerirán `p` transmisiones hasta que ésta llegue correctamente. Esto no significa que un host emisor enviará `p` cantidad de mensajes para ganar tiempo en respuesta. Además de ser una solución poco eficiente tanto para los recursos de la máquina emisora como de la red, podría ocasionar una congestión en el equipo receptor, dado que podríamos encontrarnos en una situación donde el tráfico no sea regulado y éste último no sea lo suficientemente veloz para procesar tantos pedidos.

### Problema 13

**Si la unidad que se transmite al nivel de enlace de datos se denomina trama y la que se transmite al nivel de red se llama paquete,
¿las tramas encapsulan paquetes o los paquetes encapsulan tramas? Explique su respuesta.**

La **Capa de Enlace** se encuentra en un nivel inferior a la **Capa de Red**, en éste sentido el servicio que interactúa entre ellas transmitirá paquetes desde la **Capa de Red** hacia la **Capa de Enlace**. Ésta última transmitirá `tramas` (ráfagas de bits) hacia su capa inferior, por lo tanto los `paquetes` que se transmitieron desde la **Capa de Red** estarán encapsulados en `tramas` que la **Capa de Enlace** sabrá gestionar.

### Problema 14

**¿Cuál de las capas OSI maneja cada uno de los siguientes aspectos?:**  

**(a) Dividir en tramas el flujo de bits transmitidos.**  
**(b) Determinar la ruta que se utilizará a través de la subred**

**(a)** La **Capa de Enlace** de datos se encarga de dividir los datos que llegan de la capa superior (**Capa de Red**) en `tramas` para contar con una línea de comunicación que esté libre de errores de transmisión.  
**(b)** La **Capa de Red** determina cómo se encaminan los `paquetes`, pueden ser rutas estáticas o dinámicas.

### Problema 15

**Un sistema tiene una jerarquía de protocolos de n capas. Las aplicaciones generan mensajes con una longitud de M bytes. En
cada una de las capas se agrega un encabezado de h bytes. ¿Qué fracción del ancho de banda de la red se llena con
encabezados?**

Digamos que `m` es la cantidad de mensajes en un momento dado. El ancho de banda se llenará con `m * ((n * h) + M)`, donde el total de encabezados se observa como `n * h`, dado que en **cada capa** `n` se agrega un encabezado de tamaño `h`. La fracción de encabezados en un momento dado con `m` cantidad de mensajes se podría ver como `m * ((n * h) + M) / m * (n * h)`

### Problema 16

Mencione dos similitudes entre los modelos de referencia OSI y TCP/IP. A continuación mencione dos diferencias entre ellos.

La similitud mas intuitiva es que tanto el modelo `OSI` como el `TCP/IP` se basan en el concepto de una pila de protocolos independientes entre sí y ambos contemplan la **Capa de Red**, la **Capa de Transporte** y la **Capa de Aplicación**. Además, en ambos modelos, la **Capa de Transporte** y sus capas superiores tienen como finalidad proporcionar un servicio de transporte que sea independiente de la red.

En cuanto a las diferencias, la más intuitiva es la cantidad de capas, el modelo `OSI` tiene 7 capas, mientras que el modelo `TCP/IP` es una simplificación de éste, que cuenta con 4 capas. Las redes para el modelo `OSI` comenzaron a crearse a partir de las especificaciones, pero con el tiempo se dieron cuenta que la implementación no coincidía con las especificaciones, lo que llevó a intentar integrar subcapas dentro de las capas especificadas: no funcionó. En cambio el modelo `TCP/IP` surge a partir de la creación de protocolos, los cuales eventualmente encajaban perfecto en las especificaciones de las capas. Para describir la otra gran diferencia hay que recordar que en la **Capa de Transporte** existe visibilidad al usuario sobre éste servicio. El modelo `TCP/IP` soporta comunicación `orientada a conexión` y `no orientada a conexión` en ésta capa, mientras que el modelo `OSI` únicamente `orientada a conexión`. En contraste, en la **Capa de Red** el modelo `TCP/IP` solamente soporta comunicaciones `no orientadas a conexión`, mientras que el modelo `OSI` soporta ambas.

### Problema 17

**¿Cuál es la principal diferencia entre TCP y UDP?**

Si bien ambos protocolos están ubicados en la misma capa **Transporte**, `TCP` está orientado a conexión, además de mantener el flujo de los mensajes, mientras que `UDP` es un protocolo `no orientado a conexión`.

---

Hasta acá llegue, seguiré trabajando para una potencial re-entrega.
