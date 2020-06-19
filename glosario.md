# Redes de Computadoras

## Glosario

### ICMP

ICMP (Internet Control Message Protocol) representaes un protocolo de soporte para IP. Es utilizado por dispositivos de red, incluídos los routers, para enviar mensajes de error e información operacional indicando éxito, fallas u optimización de saltos durante comunicaciones con una dirección IP.

Por ejemplo, se indica un error cuando un servicio solicitada no se encuentra disponible o un host o router no pudo ser alcanzado. Cada dispositivo que recibe un paquete IP decrementa el valor del campo `TTL` (Time To Live) de un datagrama. Otro ejemplo corriente de mensajes `ICMP` se da cuando éste campo alcanza el valor `0`: el paquete es descartado y un mensaje de `tiempo de tránsito ecxedido` es enviado a la dirección de origen.

### ISN (networking)

ISN es un número de 32 bit que representa el número inicial de secuencia (Initial Sequence Number), seleccionado pseudoaleatoriamente y unívocamente asignado al primer byte transmitido en cada conexión nueva durante una comunicación basada en TCP.

### Throughput

Usualmente representa un promedio y se mide en bits por segundo, en algunos casos en paquetes por segundo. El rendimiento o throughput es un indicador del desempeño y calidad de una conexión de red. Un índice alto de envíos de mensajes no satisfactorios indicaría un bajo rendimiento y un desempeño degradado.

### Wildcard mask

<div>Una máscara <b style="color:cornflowerblue">Wildcard</b> (<i style="color:cornflowerblue">wildcard mask,</i><i> </i>en inglés) es una máscara de bits que indica qué partes de una dirección IP están disponibles para examinar y tomar una determinada acción al respecto. Por ejemplo: indicar el tamaño de una red o una subred; indicar qué rango de direcciones IP deberían ser permitidas o no en una lista de control de acceso.</div><div><br></div><div><div><u>Ejemplo de aplicación:</u> si se quiere examinar un rango de redes, la combinación de la red <code>1.1.0.0</code> y máscara wildcard <code>0.0.255.255</code>, coincidirá con cualquier interfaz en el rango <code>1.1.0.0</code> a <code>1.1.255.255</code>.</div></div><br><p></p>
