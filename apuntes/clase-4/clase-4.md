# Redes

## Clase 4 - Nivel de transporte en Internet

### Repaso

HTTP -> protocolo TCP en algún puerto

El transporte va a tomar servicios de la capa inferior (Red) y los despacha a la capa superior.

DNS y DHCP -> protocolo UDP

La capa de transporte se interesa en que los paquetes **lleguen**.

### TCP y UDP

Servicios con distintos tipos de transporte

Cabeceras con identificación única:

+ sirve para saber si el paquete falló y entonces poder re-enviar ese mismo.

#### Multiplexación

Se realiza mediante el puerto (origen o destino) que puede valer de 0 a 65535.

Puertos del 0 al 1023 están reservados para servidores *bien conocidos* (well known ports)

Socket es la combinación entre una IP y un puerto: `147.156.135.22:1038`.

Darle a alguna entidad mas de un diálogo a la vez.

> Si tengo un IP y otro IP en otro extremo. Si la única referencia para llegar al otro equipo es el IP, voy a saber que llego al equipo pero no a qué servicio?
>
> Canales de diálogo

### TCP

+ orientado a conexión
+ necesita establecer conexión para poder enviar datos
+ espera que los paquetes lleguen en orden, en forma y completos

> **Los paquetes se llaman segmentos**

+ Control de flujo
+ Control de congestion
+ Conexion/Desconexión

#### Intercambio de datos y control de flujo

El dato que mandamos puede ser muy grande, en TCP se segmentan en varios fragmentos (TPDUs), enumerados, para luego re-ensamblarlos en destino.

TCP tiene un estado de conexión (en escucha, conectándome, en espera, cerrando, etc...)

#### Funciones

+ Retransmite segmentos perdidos o erróneos (malformados), eliminar duplicados.
  + Retransmisión con retroceso n: (avisa ack + tamaño ventana disponible)
  + Retransmisión selectiva: (avisa ack + tamaño ventana, y luego saltea algunos ack)
+ Gestiona los buffer
+ Controla la congestión

#### Cabecera TCP

+ **Pseudocabecera (porción de cabecera IP)**
  + IP de origen
  + IP de destino
  + Longitud segmento TCP
  + Campo protocolo (**00000110**)
+ Puerto de origen
+ Puerto de destino
+ Número de secuencia (orden)
+ Número de acuse de recibo: qué pieza quiere que le envíe
+ Tamaño de ventana (cantidad de segmentos?)
+ Checksum
+ **20 bytes**

**Algunos Flags:**

SYN: indica pedido de conexión
ACK: acuse de recibo

### UDP

+ no orientado a conexión
+ no importa si el paquete enviado se pierde
+ se utiliza en:
  + DNS
  + Apps en tiempo real: videollamada

Los paquetes se llaman **Datagramas** UDP. Contiene información pero no es parte de un todo, es un mensjae singular si se quiere.

#### Cabecera UDP

+ **Pseudocabecera (porción de cabecera IP)**
  + IP de origen
  + IP de destino
  + Longitud datagrama UDP
  + Campo protocolo (**00010001**)

> Es para calcular el checksum y evitar corrupciones en la entrega del datagrama.
> **00010001** indica que es UDP.

+ **Cabecera**
  + Puerto de origen
  + Puerto de destino
  + Longitud del datagrama
  + Checksum

### Capa de Transporte

+ Estos dos son los tipos de servicio de la capa de transporte.
+ Usa lo servicios del nivel de red, la comunicación es transparente al medio físico.
+ Se encarga del transporte de lo datos de extremo a extremo
