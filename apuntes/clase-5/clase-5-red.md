# Redes

## Clase 5 - Nivel de Red

> Direccionamiento y posicionamiento (identificación) de dispositivos

Utiliza el protocolo de comunicación **IP** (principal), además utiliza protocolos de control: **ICMP**, **IGMP**.

### Datagrama IP, estructura de la cabecera

Todos los protocolos auxiliaros hacen uso de datagramas para transmitir información, excepto **ARP** y **RARP**.

+ **Versión 4**
+ **Longitud de 32 bits**
+ Campos de Fragmentación: Identificació, DF, MF, Desplazamiento. Fragmento. Cuando un paquete supera el límite soportado por IP, se utiliza éste campo para fragmentarlos.
+ Tiempo de vida (TTL): cuenta saltos hacia atrás, se descarta cuando es cero (0). Util para desechar paquetes que recaen en loop de direccionamientos.
+ Protocolo: indica a qué protcolo pertenecen los datos (el contenido del paquete). **UDP** o **TCP**.
+ Checksum: comprueba la integridad de la cabecera, pero no de los datos
+ Direcciones de **Origen**, 32 bits cada una.
+ Direcciones de **Destino**, 32 bits cada una.

#### Tipos de Protocolo

+ IP en IP encapsulados
+ TCP
+ UDP
+ ST Stream
+ EGP (Exterior Gateway Protocol)
+ ISO-TP4 (Transporte del modelo OSI)

#### Opciones de la cabecera IP

+ Record Route: anota va anotando en al cabecera IP las direcciones IP de los routers por donde pasa el datagrama.
+ Timestamp: va anotando la ruta y además pone una marca de tiempo en cada router.
+ Strict source routing: la cabecera contiene las direcciones IP de los routers por los que debe pasar el datagrama. Ha de pasar por esos y sólo esos.
+ Loose source routing: la cabecera lleva una lista de routers por los que debe pasar el datagrama, pero puede pasar además por otros.

#### Direcciones IPv4

Están formadas por 4 bytes, que se representan por cuatro números decimales.

| Rango                       | Uso                                    |
| --------------------------- | -------------------------------------- |
| 0.0.0.0 - 233.255.255.255   | Direcciones Unicast  (Clases A, B, C)  |
| 224.0.0.0 - 239.255.255.255 | Direcciones Multicat (Clase D)         |
| 240.0.0.0 - 255.255.255.254 | Reservado, no se usa (Clase E)         |
| 255.255.255.255             | Dirección broadcast                    |

Clase A: 128 a 191, máscara 255.0.0.0     (8 bits)
Clase B: 192 a 223, máscara 255.255.0.0   (16 bits)
Clase C: 224 a 239, máscara 255.255.255.0 (24 bits)

#### Estructura de las direcciones IPv4

Tienen dos partes, la parte red y la parte host.

| Red (n bits) | Host (32-n bits) |
| ------------ | ---------------- |

+ La longitud de cada parte se indica mediante un parametro denominado mascara.
+ La mascara tiene tambien una longitud de 32 bits y está formada por un conjunto de unos seguidos de un conjunto de ceros.
+ Como la dirección IP, la máscara también se representa por cuatro números decimales.
+ La máscara no aparece en los paquetes IP, solo se especifica en las interfaces y las rutas.

### Enrutamiento

> + Enrutamiento básico
> + Toma de decisión del camino que los paquetes toman hacia destino.

Para la configuración inicial el host sabe:

+ Su dirección IP: `147.156.135.22` (Oblitgatoria)
+ Su máscara: `255.255.255.0` (Oblisgatoria)
+ Su router por defecto `147.156.135.1` (Puede no estar)

Cuando host quiere enviar un paquete:

1. Extrae del paquete la dirección de destino.
2. Extrae la dirección de destino la parte Red (aplica un AND entre la máscara propia y el IP de destino).

... completar

#### Orden de enrutamiento

Ejemplos de reglas:

```txt
147.156.135.0/24 > eth0
200.234.12.0/24> 147.156.135.1

# Gateway
0.0.0.0/0 > 147.156.135.1
```

### Subredes y Máscaras

> La mascara delimita el tamaño de la red. Es una parte del proceso de enrutamiento.
> **Subnet:** partir una red en varias redes de `n` direcciones.

### Protocolos de control y resolución de direcciones

traducen direcciones de red en direcciones de enlace: **ARP**, **RARP**, **BOOTP** y **DHCP** (Capa Aplicación), protocolos de capa de **Enlace**.

Aprenden diferentes formas de llegar a cierto destino y deciden cuál es el óptimo para llegar (Ej: si la conexión es por Gigabits, cuántos saltos entre routers hay entre origen y destino, etc.)

Existe routing interno y externo.

### Fragmentación

### Protocolos de Routing

> Comunicación con otros routers para conocer los mejores caminos a destino

Intercambian información necesaria para calcular las rutas más óptimas: **RIP**, **OSPF**, **IS-IS**, **BGP**.

### Protcolo IPv6

> Evolución y/o propuesta de cambio de IPv4

+ El 72% de Inernet utiliza la versión 4 del protocolo IP, el 28% restante usa IPv6.
+ En algún momento toda la red de Internet utilizará la versión 6.
