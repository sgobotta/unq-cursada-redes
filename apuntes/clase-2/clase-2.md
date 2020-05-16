# Redes

## Clase 2 - HTTP

### Definiciones simples

+   HyperText Transfer Protocol
+   No orientado a conexión

### Actores

+   User Agent: el navegador

### Servicios

+   Servicio http sin seguridad: puerto 80 de tcp
+   Servicio http con seguridad: puerto 443 de tcp
+   Servicio FTP: 20 tcp

### Contenido

+   MIME (Multipurpose Internet Mail Extensions) como contenedor de contenido

### Estado

+   Http es un protocolo sin estado, no guarda información
+   Cookies: información que un servidor puede almacenar en el sistema cliente por algún tiempo determinado

### Estándares

Forma en que dialoga

+   HTTP/0.9 Pre-93
    +   método GET
+   RFC 1945 (HTTP/1.0, 1996)
    +   Se crean el resto de los métodos
+   RFC 2616 (HTTP/1.1, 1999)
    +   Soporta: Name bases Virtual Hosting (más de un host virtual en el mismo servidor)
+   RFC 2774 (HTTP/1.2, 2000)
    +   PEP (protocol extension protocol), ni se usa aparentemente.
+   HTTP 2.0 buscar!
    +   Permite además de diálogo con ASCII, dialogo en Binario (mejora la performance de transferencia)

> https://www.rfc-editor.org


### Status

+   **1xx** Mensajes de conexión rechazada
+   **2xx** Operación exitosa
+   **3xx** Redirecciones
+   **4xx** Errores de cliente
+   **5xx** Errores de servidor

> 301 redirección incondicional del servidor
> 302 redirección por el cliente

### Glosario

+   **Relación IP/Puerto => Socket**
