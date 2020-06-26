# Redes de Computadoras

<!-- markdownlint-disable MD001 MD024 -->

> 14 de Junio, 2020.
> Santiago Botta

## Práctica VII - Lan, Enlaces, Pap

### Ejercicio 1

**¿Qué empresa fabrica el adaptador Ethernet (IEEE 802.3) de la computadora que usted usa
normalmente? Determine cuál es el prefijo (OUI) de la dirección asignado a este fabricante.**

En mi caso, no poseo un adaptador Ethernet. El adaptador utilizado en mi notebook fue fabicado por la empresa Intel, bajo el estándar `IEEE 802.11` (Wireless, soportando frecuencias `2.4Ghz` y `5.8Ghz`).

Mas información sobre el adaptador:

```bash
lspci -v
02:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
        Subsystem: Intel Corporation Wireless 8260
        Flags: bus master, fast devsel, latency 0, IRQ 129
        Memory at ef000000 (64-bit, non-prefetchable) [size=8K]
        Capabilities: <access denied>
        Kernel driver in use: iwlwifi
        Kernel modules: iwlwifi
```

El prefijo OUI (*Organizationally unique identifier*) es un número de 24 bits que identifica unívocamente al fabricante (son los primeros 3 octetos, o seis caracteres hexadecimales, del valor de MAC address). El valor designado a mi MAC address en sus primeros tres octetos es el `b8:8a:60`, que corresponde a la compañia **Intel Corporate**.

### Ejercicio 2

**El algoritmo para el cálculo del retardo para la transmisión en `CSMA/CD` es el siguiente:**

```ruby
if intentos <= 16 then
begin
  k := min(intentos, 10);
  r := random(0, (2^k)-1);
  retardo := r * ranura_de_tiempo;
  intentos := intentos + 1;
end;
```

**donde `r` es un número entero generado de manera aleatoria a partir de una función de distribución uniforme.**

1. **¿Qué relación encuentra entre el número de colisiones que sufre un transmisor y el tiempo que deberá esperar para intentar retransmitir una trama?**
2. **¿Qué tipo de prioridad implícita genera esto?**
3. **¿Qué ocurre en el protocolo si intentos es mayor que 16? ¿Porqué existe esta cota superior?**

> CSMA/CD (*Carrier sense multiple access with collision detection*)

1. Se puede observar que el tiempo de espera para los intentos de transmisión está indirectamente afectado por la cantidad de intentos, como se indica en el cálculo de `r`, que determina (*parcialmente*) el tiempo de retardo. No quiere decir que a más intentos incrementará el tiempo de retardo, dado que la aleatoreidad se da entre el valor `0` y el resultado de otro cálculo que involucra a `r`.
2. Si bien la aleatoreidad de la operación determina cierto grado de flexibilidad en el tiempo de retardo, se puede observar que existe más posibilidad de que el tiempo de retardo sea mayor a medida que el número de intentos de transmisión aumenta.
3. Existe una cota superior para no intentar retransmitir una trama por tiempo indefinido. Se realizan 16 intentos, si el tiempo de retardos calculado no es suficiente se descarta y no se vuelve a reintentar.

### Ejercicio 3

**Analizar la veracidad de la siguiente afirmación:**
*"En MAC 802.3 (CSMA/CD), si una trama es transmitida al medio físico sin colisiones puede asegurarse que la subcapa receptora la entrega correctamente a su capa superior"*

No. CSMA/CD es un sistema que detecta colisiones durante las tramas, pero no evita que hayan sido corrompidas en el transcurso por otros factores. Si una trama está corrupta, el chequeo de paridad o *Cycle Redundancy Check*, (ubicado en los últimos 4 bytes de la trama) no será positivo y la trama se descartará y no podrá ser despachada a la subcapa receptora. Asimismo la trama puede no haber sufrido colisiones pero otros factores evitaron su entrega a destino. Algunas de las causas de éstos fenómenos pueden ser:

+ reflexiones de señales: causados por cables mal formados, no terminados, impedancia.
+ ruido eléctrico: causado por luz fluorescente, redes eléctricas, rayos X.
+ malfuncionamiento de hardware

> Fuente: https://www.liveaction.com/docs/glossary/ethernet-ieee-802-3/frame-corruption/

### Ejercicio 4

**Dentro de un segmento de `LAN 802.3` un host envía a otro un mensaje de nivel de aplicación. Si uno de los frames Ethernet llega al destino y luego del chequeo del CRC es descartado. ¿Qué sucede con el frame original? ¿Y con el mensaje de nivel de aplicación?**

En cuanto al mensaje a nivel aplicación. El software utilizado determinará qué hace cuando no recibe una respuesta. Recordemos que en la capa de transporte es en el software utilizado en la capa aplicación donde reside la responsabilidad de realizar una acción frente al comportamiento (respuesta/sin respuesta) del protocolo de transporte.
Llegado el caso en el que un frame fue descartado, las acciones dependeran de los protocolos que se estén utilizando, por ejemplo:

+ Ethernet y otros protocolos de la `IEEE 802`: no especifican una acción específica de retransmisión, la trama es directamente descartada.
+ TCP: identifica pérdida de segmentos, los cuales contienen paquetes IP y éstos están encapsulados en tramas. De ésta manera los segmentos perdido son retransmitidos, ls paquetes IPs encapsulados nuevamente y las tramas generadas una vez mas para enviarse a través del medio físico.

### Ejercicio 5

**En una LAN FastEthernet (IEEE 802.3u) se pueden usar conexiones full-duplex tanto sobre UTP como sobre fibra óptica. ¿Porqué es posible esto? ¿Qué significa full-duplex cuando se trata de Ethernet?**

---

> Otras fuentes: https://www.youtube.com/watch?v=_b4dXKB8Pt8
