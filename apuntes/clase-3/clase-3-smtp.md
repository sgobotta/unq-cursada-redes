# Redes

## Clase 3 - Correo

> **SMTP - POP3 - IMAP**

### Protocolos

+   **SMTP** para enviar correos a un servidor  
    +   Socket **TCP**
    +   Puerto: **25**
    +   El diálogo es en **ASCII**
    +   Emulación posible con **telnet**
+   **Pop3** (Post Office Protocol) para recibir correos desde un servidor **Puerto:** 110
+   **IMAP** (Interactive Mail Access Protocol) para recibir correos desde un  servidor **Puerto:** 143

### Roles

+   **MUA** Mailing User Agent??
+   **MDA** Mail Delivery Agent
+   **MTA** Message transfer agent: cuando un servidor recibe un correo que no puede alojar, lo envía al dominio de destino que corresponde.

### Flujo de envío

+   **Cliente** - Establecimiento de conexión a puerto 25 SMTP
+   **Server** - 220 Servidor SMTP listo para conexión
+   **Client** - Comando de saludo: HELO (delata el protocolo SMTP de diálogo)
+   **Client** - MAIL FROM
+   **Server** - Status 250: ok
+   **Client** - RCPT TO: enviar a destinatario
+   **Server** - El recipiente está (250 Ok) o no (550)
+   **Client** - DATA
+   **Client** - comando QUIT para cerrar
+   **Server** - 221 Destino cerrando

### Historia

**Request form commentary**

+   RFC 821 Protocolo de transmisión SMTP (el flujo de envío)
+   RFC 822 Formato de Mensaje (lo que va dentro de DATA)


### Sistema de correo

+   Edición de mensajes
+   Tansferencia
+   generación de inormes (logs)
    +   Envoltura
    +   destino prioridad seguridad

Subsistema transferencia:

+   Distribución: **SMTP**, **ESMTP**
+   Entrega Final
    +   **POP3:** Descarga en cliente
    +   **IMAP:** Conexión permanente

Subsistema de Usuario

+   Formato MIME


### Mensajería

+   **Discusión:** recibir pero no escribir
    **Difusión:** recibir y escribir

SMTP Extendido: se inicia con EHLO en lugar de HELO


### MIME

**Multipurpose Internet Mail Extensions**

