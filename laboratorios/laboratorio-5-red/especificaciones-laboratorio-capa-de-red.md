# Laboratorio 5 - Red

> 13 de Junio, 2020
> Santiago Botta

## Subneteo y Direccionamiento IP

> Una empresa tiene su sede central en Buenos Aires y una sede en la ciudad de La Plata. Cada una de ellas tendrá una red local, la de BA de 110 equipos entre computadoras personales y servidores, y la de La Plata de 50 PCs. Se deben conectar las dos sedes mediante un enlace dedicado punto a punto. Además, la sede de BA tendrá otra LAN con 18 servidores para una Intranet que no requerirá acceso a Internet. El enlace a Internet de toda la red será contratado a un proveedor de servicios en BA. Adicionalmente La Sede de La plata tiene 3 oficinas que deben estar vinculado con La Plata por medio de enlaces punto a punto en las cuales solo va a tener 1 PC . La conexión de Internet esta en la sede de Buenos Aires. El proveedor le ha asignado a la empresa la red IP `208.101.21.0/24` para ser utilizada. Se pide:
>
> 1. Diseñe el diagrama lógico de la red, incluyendo el equipamiento necesario de nivel IP.
> 2. Diseñe el plan de numeración para la red realizando el subnetting que considere necesario. Tenga en cuenta que para los vínculos utilizaremos mini-redes privadas para no malgastar los números públicos.
> 3. Diseñe las rutas necesarias de configurar en cada equipo, para que el trabajo este operativo.
> 4. Implemente en el simulador packet-tracer el diseño realizado.

Se cuenta con un bloque de direcciones `208.101.21.0/24`.

```txt
direcciones públicas a repartir                 208.101.21.0/24    254 hosts disponibles

direcciones privadas a repartir para LAN        192.168.0.0/24     254 hosts disponibles

direcciones privadas a repartir para enlaces    172.30.0.0/24      254 hosts disponibles
```

### Buenos Aires

+ LAN de 110 equipos (computadores personales y servidores).
+ LAN 18 servidores (intranet).
+ Enlace a Internet con proveedor.

```txt
#0 subred lan     208.101.21.0/25     126 hosts usables

#1 subred lan     208.101.21.192/27   30 hosts usables

#2 red wan        208.101.21.224/30   2 hosts usables       (internet)
```

#### Router 0 Buenos Aires

```txt
Eth     0/0     208.101.21.126/25     (enlace a red de computadores y servidores local)
Eth     0/1     ---
Eth     1/0     172.30.0.2/30         (enlace a intranet)
Eth     1/1     172.30.0.5/30         (enlace a router de Enlace La Plata)
```

Tabla de Ruteo

```txt
Hacia red     192.168.0.0/27        por 172.30.0.1
```

#### Intranet Router

```txt
Eth     0/0     192.168.0.30/27       (enlace a intranet)
Eth     0/1     172.30.0.1/30         (enlace a router 0)
```

Tabla de Ruteo

```txt
Hacia red     208.101.21.0/25       por 172.30.0.2/30
```

### La Plata

+ 50 equipos.
+ 3 Enlaces punto a punto para cada una de las 3 oficinas, de 1 equipo cada una.

```txt
#0 subred         208.101.21.128/26   62 hosts usables

#1 red enlace     208.101.21.232/30   2 hosts usables       (oficina 1)

#2 red enlace     208.101.21.236/30   2 hosts usables       (oficina 2)

#3 red enlace     208.101.21.240/30   2 hosts usables       (oficina 3)
```

#### Router 0 La Plata

```txt
Eth     0/0     208.101.21.129/26   (enlace a equipos de sede La Plata)
Eth     0/1     172.30.0.17/30      (enlace a router wan La Plata)
Eth     1/0     172.30.0.1/30       (enlace a router LP Oficinas)
```

Tabla de Ruteo

```txt
Hacia red     208.101.21.232/30     por 172.30.0.2
Hacia red     208.101.21.236/30     por 172.30.0.2
Hacia red     208.101.21.240/30     por 172.30.0.2
Hacia red     0.0.0.0               por 172.30.0.18  (hacia Router WAN)
```

#### Router Oficinas

```txt
Eth     0/0     172.30.0.2/30          (enlace a router 0 LP)
Eth     0/1     172.30.0.5/30          (enlace a router Oficina 1)
Eth     1/0     172.30.0.9/30          (enlace a router Oficina 2)
Eth     1/1     172.30.0.13/30         (enlace a router Oficina 3)
```

```txt
Hacia red     208.101.21.0/25       por 172.30.0.1/30
Hacia red     208.101.21.128/26     por 172.30.0.1/30
Hacia red     208.101.21.232/30     por 172.30.0.6/30
Hacia red     208.101.21.236/30     por 172.30.0.10/30
Hacia red     208.101.21.240/30     por 172.30.0.14/30
```

#### Oficina 1

```txt
LP - Oficina 1 - PC1      IP      208.101.21.234/30
                          Gateway 208.101.21.233
```

#### Router Oficina 1

```txt
Eth     0/0     172.30.0.6/30       (enlace a Router Oficinas)
Eth     0/1     208.101.21.233/30   (enlace a dispositivo Oficina 1)
```

```txt
Hacia red     208.101.21.0/25       por 172.30.0.1
Hacia red     208.101.21.128/26     por 172.30.0.1
```

#### Oficina 2

```txt
LP - Oficina 2 - PC1      208.101.21.238/30
                          Gateway 208.101.21.237
```

#### Router Oficina 2

```txt
Eth     0/0     172.30.0.10/30      (enlace a Router Oficinas)
Eth     0/1     208.101.21.237/30   (enlace a dispositivo Oficina 2)
```

```txt
Hacia red     208.101.21.0/25       por 172.30.0.1
Hacia red     208.101.21.128/26     por 172.30.0.1
```

#### Oficina 3

```txt
LP - Oficina 3 - PC1      208.101.21.242/30
                          Gateway 208.101.21.241
```

#### Router Oficina 3

```txt
Eth     0/0     172.30.0.14/30      (enlace a Router Oficinas)
Eth     0/1     208.101.21.241/30   (enlace a dispositivo Oficina 3)
```

```txt
Hacia red     208.101.21.0/25       por 172.30.0.1
Hacia red     208.101.21.128/26     por 172.30.0.1
```

> Nota sobre oficinas:
>
> No se provee interconexión entre oficinas.

### Router WAN: Buenos Aires - Proveedor Internet

```txt
Eth 0/0       172.30.0.14
Eth 0/1       172.30.0.XX     (hacia cable modem)
```

### Router WAN: Buenos Aires - La Plata

+ Enlace dedicado punto a punto.

```txt
#0 red enlace     208.101.21.228/30   2 hosts usables

Eth     0/0     172.30.0.6/30             (enlace a router 0 BA)
Eth     0/1     172.30.0.9/30             (enlace a WAN a La Plata)
Eth     1/0     172.30.0.13/30            (enlace con proveedor de Internet)
```

Tabla de Ruteo

```txt
Hacia red     208.101.21.0/25       por 172.30.0.5
Hacia red     208.101.21.128/26     por 172.30.0.10
Hacia red     208.101.21.232/30     por 172.30.0.10
Hacia red     208.101.21.236/30     por 172.30.0.10
Hacia red     208.101.21.240/30     por 172.30.0.10
Hacia red     0.0.0.0/0             por 172.30.0.13
```

### Router WAN: La Plata - Buenos Aires

+ Enlace dedicado punto a punto.

```txt
#0 red enlace     208.101.21.228/30   2 hosts usables

Eth     0/0     172.30.0.10/30          (enlace a WAN a Buenos Aires)
Eth     0/1     172.30.0.18/30          (enlace a router 0 LP)
```

Tabla de Ruteo

```txt
Hacia red     208.101.21.0/25       por 172.30.0.9         (hacia Sede BA)
Hacia red     208.101.21.128/26     por 172.30.0.17
Hacia red     208.101.21.232/30     por 172.30.0.17
Hacia red     208.101.21.236/30     por 172.30.0.17
Hacia red     208.101.21.240/30     por 172.30.0.17
Hacia red     0.0.0.0/0             por 172.30.0.9         (hacia Sede BA)
```

> Nota sobre la entrega:
>
> Al principio se utilizaron IPs dinámicas. Llegado el caso de Sede La Plata me tomé el trabajo de investigar DHCP y las IPs para la Sede La Plata fueron asignadas automáticamente.
