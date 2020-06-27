# Laboratorio 6 - VLan

> Santiago Botta

## Asignación de Dispositivos e IPs

Se crean 6 dispositivos hosts con ips:

```txt
10.1.0.10/8
10.2.0.10/8
10.3.0.10/8
10.1.0.11/8
10.2.0.11/8
10.3.0.11/8
```

Se asignan 2 switches

```txt
Switch0
Puerto 1 10.1.0.10
Puerto 2 10.2.0.10
Puerto 3 10.3.0.10

Switch1
Puerto 1 10.1.0.11/8
Puerto 2 10.2.0.11/8
Puerto 3 10.3.0.11/8
```

**1)** A continuación el resultado de las priemeras pruebas sobre la implementación

Se realizan llamados ping desde `10.1.0.10/8` hacia los demás dispositivos. Las respuestas llegan con normalidad y las tablas de ARP de los dispositivos se populan. La máquina host guarda las relaciones IP - MAC Address de las otras 5 máquinas. Mientras que cada una de las máquinas receptoras guarda la relación IP - MAC Address de la máquina emisore de los paquetes ping (*ICMP*).
Se configura en el Switch0 dos VLan (`Administracion` y `Gestion`). Se repite el procedimiento de ping y todo funciona con normalidad, igual que antes.
Se corrobora que las VLan existen utilizando el comando `show vlan`. Ambas, en cada switch se visualizan como `active`.

**2)** Ejecutamos el comando `show vlan` y nos muestra el siguient output

```txt
Switch#show vlan

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/5, Fa0/6, Fa0/7, Fa0/8
                                                Fa0/9, Fa0/10, Fa0/11, Fa0/12
                                                Fa0/13, Fa0/14, Fa0/15, Fa0/16
                                                Fa0/17, Fa0/18, Fa0/19, Fa0/20
                                                Fa0/21, Fa0/22, Fa0/23, Fa0/24
                                                Gig0/1, Gig0/2
2    Administracion                   active
3    Gestion                          active
1002 fddi-default                     active
1003 token-ring-default               active
1004 fddinet-default                  active
1005 trnet-default                    active

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
2    enet  100002     1500  -      -      -        -    -        0      0
3    enet  100003     1500  -      -      -        -    -        0      0
1002 fddi  101002     1500  -      -      -        -    -        0      0
1003 tr    101003     1500  -      -      -        -    -        0      0
1004 fdnet 101004     1500  -      -      -        ieee -        0      0
1005 trnet 101005     1500  -      -      -        ibm  -        0      0

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------

Remote SPAN VLANs
------------------------------------------------------------------------------

Primary Secondary Type              Ports
------- --------- ----------------- ------------------------------------------
```

Se observa en la sección de ***VLAN*** que en la columna ***Ports*** todo los puertos pertenecen a la VLAN 1, es decir, la VLAN por defecto, o sea que sí se encuentran en el mismo segmento de red. En la `VLAN 2 Administracion`  y `VLAN 3 Gestion` no se observan puertos del switch asignados.

Para poder asignar la pertenencia de un puerto a una vlan de la manera que se solicita en la práctica se creó una VLAN más, de manera que la Vlan 4 exista. Anteriormente se creó `VLAN 2 Administración` y `VLAN 3 Gestion`. Se crea una nueva `VLAN 4 Dirección` en ambos switches.

Observamos en las tablas de VLAN de los switches que los puertos están ahora asignados a las vlan 2, 3 y 4.

### Switch0

```txt
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/4, Fa0/5, Fa0/6, Fa0/7
                                                Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Fa0/24, Gig0/1, Gig0/2
2    Administracion                   active    Fa0/1
3    Gestion                          active    Fa0/2
4    Direccion                        active    Fa0/3
1002 fddi-default                     active
1003 token-ring-default               active
1004 fddinet-default                  active
1005 trnet-default                    active
```

### Switch1

```txt
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/4, Fa0/5, Fa0/6, Fa0/7
                                                Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Fa0/24, Gig0/1, Gig0/2
2    Administracion                   active    Fa0/1
3    Gestion                          active    Fa0/2
4    Direccion                        active    Fa0/3
1002 fddi-default                     active
1003 token-ring-default               active
1004 fddinet-default                  active
1005 trnet-default                    active
```

**4)** Se repite la experiencia del PING desde `10.1.0.10` y todas las solicitudes responden con `timeout`.

> Se procede a modificar las interfaces `GigabitEthernet 0/1` en ambos switches para que el acceso de switchport se realice a través de la `vlan 2`.

**5)** Se repite la experiencia de PING, desde la máquina con IP address `10.1.0.10/8` hacia el resto de los equipos.

Se prueba primer realizar un ping hacia la dirección `10.2.0.10/8`. La respuesta es timeout. El segundo, tercer y cuarto intento se realizan a las direcciones `10.3.0.10/8`, `10.2.0.11/8` y `10.3.0.11/8` respectivamente. En todos los casos devuelve `timeout`. Esto se debe a que esas direcciones están asignadas a vlan distintas que `vlan 2`, por lo tanto el switch no puede referenciarlas.

Se intenta finalmente realizar un ping a la máquina con ip `10.1.0.11/8` y la respuesta son 4 ping positivos. En éste caso hay respuesta dado que esa IP fue asignada a la `vlan 2` en el puerto `0/1` del segundo switch `Switch1`.

> Para interconectar los switch se pueden interconectar más puertos, tanto FastEthernet como GigabitEthernet entre los switches, asignándoles a cada uno una de las vlan que aún no han sido asignadas (`vlan 2`, `vlan 3`). Otro método es asignar un switch intermedio entre los switches, asignándoles también el etiquetado de las 3 vlan.

**6)** Se realizan cambios para vincular los switches a cada vlan de modo físico.

La prueba de ping se vuelve a realizar entre las máquinas con direcciones `10.1.0.10/8` y `10.1.0.11/8`, pertenecientes a `vlan 2`. No se detectan cambios en las cabeceras. El único cambio se observa al llegar a la máquina de destina, donde los campos para MAC Address e IP se cambian, asignando la direccion de MAC Address e IP de la máquina que originalmente realizó el envío del mensaje `ICMP`.

**7)** Se modifica la red con el comando dado por `switchport mode trunk` en cada vínculo entre switches: `GigabitEthernet 0/1`, `GigabitEthernet 0/2` y `FastEthernet 0/24`.

Se observa que los mensajes ping entre dispositivos de `vlan 2` se dan normalmente. Por otro lado, los mensajes ping entre dispositivos de `vlan 3` y `vlan 4` devuelven `timeout` como resultado.

En general, no es posible acceder con mensajes `ICMP` entre vlans.

**8)** Se configura un router y sus puertos a las interfaces de los switches, como indica la figura. Ademá se re-configuran las máscaras de todas las máquinas para que la red sea `/16` y se los agregan gateways apropiados a cada máquina de cada switch.

Ahora cada máquina puede enviar mensajes `ICMP` con la otra máquina de su VLAN. Cuando se intenta enviar mensajes `ICMP` a máquinas fuera de la VLAN, la respuesta es de `timeout`.
