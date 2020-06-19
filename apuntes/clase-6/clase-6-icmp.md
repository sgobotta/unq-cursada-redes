# Redes

## Clase 6 - ICMP y DHCP

### ICMP

#### Cabecera de mensaje ICMP

+ Tipo (8bits)
+ Código (8bits)
+ Checksum (16 bits)
+ sin usar
+ Cabecera internet + 64 bits tde datos del datagrama original

#### Tipos de mensaje

En el campo tipo, el valor indica qué tipo de mensaje es:

+ **`0` Respuesta de Eco (Echo Reply)**
+ **`3` Destino inaccesible (Destination Unrecheable)**
+ **`4` Disminución del tráfico desde el origen (Source Quench)**
+ **`5` Redireccionar, cambio de ruta (Redirect)**
+ **`8` Solicitud de eco (Echo)**
+ **`11` Tiempo excedido para un datagrama (Time Exceeded)**
+ `13` Solicitud de marca de tiempo (Timestamp)

> **los mensajes principales de ICMP**

### DHCP

> *Broadcasting para obtener IP.*

Se conoce de antemano el puerto donde se reciben los pedidos de mensajes `DHCP`.

1. La máquina de origen envía el mensaje `DHCPDISCOVER` hacia todas las máquinas de mi red **(broadcast)**. El server lo recibe (o aquellas máquinas que tienen el puerto abierto).
2. El servidor envía en **broadcast** el mensaje `DHCPOFFER`, con la MAC address de la máquina objetivo.
3. Se solicita la IP, mediante `DHCPREQUEST`.
4. Se obtiene la IP, `DHCPPACK`.

#### Asignación

+ **Manual:** asigna una ip fija a una máquina determinada. Se hace manualmente o por MAC Address.
+ **Automática:** asigna permanentemente una IP a una MAC Address.
+ **Dinámica:** se determina un rango de direcciones IP y cada computadora está configurada para solicitar su dirección IP al servidor. El procedimiento usa un concepto de un intervalo de tiempo controlable (alquiler de IP).

> Algunos dispositivos, tales como servidores, deberán estar estáticamente asignados.
>
> Utiliza protocolo de capa 4, UDP en el puerto `68` respondiendo a las peticiones del puerto `67`.
