# Trabajo - SWAP
*Carlos Morales Aguilera*

## Hosting web

### ¿Qué es un hosting web?
Para explicar este término pensaremos en una analogía muy sencilla: En nuestro ordenador almacenamos una serie de archivos, supongamos que algunos de ellos compartidos con otros usuarios, y necesitamos que el ordenador esté siempre dispobile para que el resto de usuarios puedan acceder a ellos. En este principio se basa el hosting web.

***Hosting web*** es un espacio de almacenamiento en un servidor dedicado y conectado a la red, de forma que cualquier usuario pueda acceder a los documentos almacenados en él a través de una conexión a Internet a través de la página web alojada en él. Dicho servidor deberá estar conectado las 24h y tener la máxima disponibilidad posible.

### Tipos de hosting web
Dentro de la misma filosofía de hosting web ya mencionada, podemos distinguir varios tipos según la metodología o características:
* ***Servidor dedicado***: Un servidor dedicado exclusivamente para un único cliente. Altamente recomendados para sitios web con gran cantidad de tráfico.
* ***Hosting compartido***: Existen servidores que alojan varias páginas web de distintos clientes y que comparten recursos entre dichas páginas web.
* ***Servidor virtual VPS***: Consiste en un servidor físico que se divide en distintas máquinas o servidores virtuales independientes que trabajan de manera grupal. No se comparten recursos con otras páginas web y el hardware de las máquinas virtuales es del mismo servidor físico.
* ***Hosting business***: Combina cPanel con aprendizaje sobre hosting web compartido, es la mejor alternativa para grandes empresas con un gran tráfico.

### ¿Qué debo tener en cuenta a la hora de contratar un hosting web?
Como es normal, existen diferentes situaciones y por lo tanto diferentes tipos de variables a tener en cuenta a la hora de contratar un servicio de hosting web:

* ***Espacio web***: Espacio de almacenamiento necesario para tu página web y documentos, cada servidor ofrece un espacio y precios distintos.
* ***Correo***: Número de cuentas de correo que ofrece el servidor, variará entre distintos planes.
* ***Panel de control***: Un panel de control de administración de tu host es esencial a la hora de configurar los servicios y características que ofrecerá tu servidor web. Dependiendo del servicio y el plan, la administración puede correr a cuenta del cliente o del administrador del host. Generalmente el administrador gestiona el servidor web y cede al cliente la administración sobre su página web.
* ***Tráfico***: Es un factor clave a la hora de contratar un servicio, pues un servidor que no cumpla con los requisitos podría ocasionar una mala experiencia con la página web del cliente, y por el contrario la contratación de un servicio excesivo supondría unos gastos innecesarios y un servidor que no se ajusta a las necesidades del cliente.

### Servicios de Hosting web

***Hostinger*** es una empresa que ofrece un servicio de espacio virtual dedicado al hosting web. Una alternativa inicial para alojar nuestra página web, ya que ofrece un servicio gratuito de hosting web básico. Obviamente si planeamos conseguir un mayor soporte y desarrollo existen planes premium a los que acceder. Hostinger se encarga completamete del alojamiento web y nos ofrece una interfaz bastante sencillar para la administración de nuestra página web.

***OVH*** se presenta como una alternativa no gratuita de Hostinger, ofreciendo planes de un precio mínimo con un gran soporte. Esta empresa francesa ofrece servidores dedicados, alojamiento compartido y VPS.

### Herramientas de administración de un Hosting Web

Dependiendo de las distintas necesidades se han desarrollado herramientas con características y funcionalidades distintas para la adminitración y desarrollo del hosting web. En la siguiente tabla se pueden observar algunas de las herramientas más conocidas:


[![Imagen 1](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/tabla_herramientas.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/tabla_herramientas.png?raw=true)

Cabe destacar que se emplean distintos lenguajes de programación para el *back-end* del hosting. Por otro lado podemos destacar ***cPanel*** y ***Plesk*** como principales herramientas, ofreciendo mayor funcionalidad *IPv6* y *Multi-servidor*. Cabe destacar que la mayoría de estas herramientas son desarrolladas bajo **Linux**.

En nuestro trabajo trataremos principalmente dos herramientas, una de código libre y otra no: ***cPanel*** y ***VestaCP***.

### cPanel
Como su nombre indica, ***cPanel*** es un panel de control dirigido a la administración y control de hosting web, implementado en Linux que utiliza una interfaz gráfica propia.

Funciona tanto en servidores dedicados como en máquinas virtuales y ofrece servicios de *Apache*, *PHP*, *MySQL*, *PostgreSQL*, *perl* y *BIND* (*DNS*). Por otro lado, su soporte de Email incluye *POP3*, *IMAP*, *SMTP*.
 
***cPanel*** es accesible via web en el puerto 2082 o via https en el puerto 2083.

Como podemos observar, ***cPanel*** posee un gran panel de opciones entre los que podemos destacar:

[![Imagen 2](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/cPinterface.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/cPinterface.png?raw=true)

1. Barra de navegación: Permite la modificación de ajustes y cuenta personal. Inclute una búsqueda y otros elementos de configuración.
2. Barra lateral: Incluye dos botones principales, accesos directos a *Home* o menú principal y *User Manager* o menú de usuario que dirige a un panel de preferencias de usuario.
3. Información general: Usuario actual, nombre del dominio principal, directorio *home*, último log, étc.
4. Características: Lista todas las funcionalidades disponibles en grupos de distintos tipos de funcionalidad.
5. Estadísticas: Muestra las estadísticas principales de uso de su *host*.

**Principales ventajas de *cPanel***
* Interfaz gráfica de usuario: Dispone de un gran conjunto de funcionalidades que se muestran mediante uso de interfaces sencillas e intuitivas.
* Administración sencilla de la web: La administración de la web se puede gestionar en tres grandes bloques siendo *Email*, *Documentos* (Configuración *FTP*) y *Dominios* (Gestión de *DNS*, *add-ons*).
* Modularización: cPanel integra **Fantastico**, que permite la instalación de *scripts* y módulos de terceros que añaden nuevas funcionalidades al sistema, todo esto con un instalador sencillo que se encarga de resolver referencias.
* Seguridad: Directorios protegidos mediante contraseñas en tu web, administrador que rechaza *IPs*, *SSH*, *SSL/TLS*, protección *Hotlink*, claves *GnuPG* y protección ante terceros.
* Estadísticas e informes detallados.
* Multi-servidor: Permite la gestión de distintos servidores desde un único punto, permitiendo gestionar distintos servidores desde un mismo panel.
* Cortafuegos: Permite la creación de filtros personalizados complejos con la ayuda de numerosas herramientas.

### VestaCP

***VestaCP*** se presenta con un panel de control más sencillo que ***cPanel***, sin embargo es una de las mejores alternativas tratándose de un panel de control gratuito.

Posee una traducción a 26 lenguajes y monitorización mediante *Monit*, *Webalizer* y otras herramientas. Está desarrollado en *PHP* y posee herramientas de *Anti-Spam* y *Antivirus*. A diferencia de ***cPanel*** presenta una base de datos basada en *PostgreSQL* (o *MySQL* en las últimas versiones).

***VestaCP*** posee también conexión *FTP* y está basado en ***nginx*** y ***Apache***.

Una de las principales desventajas de ***VestaCP*** es que la configuración de cortafuegos es muy sencilla y limitada, ya que está basada en *Iptables* y *Fail2ban*, configuraciones ya existentes en *Linux* que no suponen una gran mejora.

**Instalación VestaCP**

La instalación de ***VestaCP*** es un proceso muy simple consistente en  ir a la dirección https://vestacp.com/install/ y en la sección **ADVANCED INSTALL SETTINGS** seleccionar la configuración deseada para nuestro servidor.

Una vez realizada la elección de la configuración de nuestro servidor, presionaremos en el botón *Generate Install Command* y se nos mostrará un serie de órdenes a ejecutar en nuestra terminal de la forma:

[![Imagen 3](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/generacion.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/generacion.png?raw=true)

Ejecutando los comandos, tras una configuración de aproximadamente 10 minutos, nuestro servidor de ***VestaCP*** estará configurado, a continuación accedemos a la dirección *IP* de nuestro servidor en el puerto **8083** para logearnos como administrador.

[![Imagen 4](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/login.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/login.png?raw=true)

Una vez logueados pasamos a la pantalla de administración de nuestro servidor:

[![Imagen 5](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/main.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/main.png?raw=true)

Así visualizariamos nuestra página web:

[
![Imagen 6](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/localhost.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Trabajo/Imagenes/localhost.png?raw=true)

A continuación enlazo a un vídeo personal en *Youtube* donde se puede observar detenidamente cada una de las secciones que ***VestaCP*** presenta:

[Demostración VestaCP Youtube](https://youtu.be/ftJEeK_e5xg)

En ella visualizaremos las siguientes opciones:
* **USER**: Permite la administración de usuarios y configuración de los mismos, además podemos ver de forma genérica las estadísticas correspondientes a cada uno.
* **WEB**: Muestra la configuración de las webs alojadas en nuestro servidor y permite la gestión de las mismas.
* **DNS**: Realiza las funciones de direccionamiento de nuestras páginas web.
* **MAIL**: Configuración de nuestro cliente de correo, en este caso simple, indicamos a que correo se realiza la gestión.
* **DB**: Administración de la base de datos de nuestro servidor, el cual hemos configurado en la instalación.
* **CRON**: Gestión de procesos *crontab* en nuestro servidor gestionados por ***VestaCP***, tal y como lo haríamos en *Linux*.
* **BACKUP**: Permite la creación y almacenamiento de copias de seguridad de nuestro servidor, nos permite solicitar una y posteriormente descargarla cuando deseemos.
* **Packages**: Administración de los distintos paquetes o complementos instalados en nuestro servidor, y su información relacionada.
* **IP**: Gestión de las *IP* asociadas a nuestro servidor y su estado.
* **Graphs**: Gráficas de uso de los distintos componentes de nuestro servidor.
* **Estadísticas**: Estadísticas de usabilidad y rendimiento de nuestro servidor.
* **Log**: Reporte e información sobre procedimientos, acciones y errores en nuestro servidor.
* **Updates**: Progamación de actualizaciones de las distintas secciones de nuestro servidor.
* **Firewall**: Gestión y creación de distintos filtros de cortafuegos mediante reglas *IPTABLES*. Además, podemos gestionar las *IP* baneadas.
* **Apps**: Aplicaciones de terceros u otros softwares externos a ***VestaCP***, mediante la interfaz de ***Softaculous***.
* **Server**: Gestión de nuestro servidor y sus distintos componentes, permite la administración de cada sección del mismo y su programación.


**Principales ventajas de *cPanel***
* Interfaz gráfica de usuario: Dispone de una interfaz muy sencilla e intuitiva para usuarios.
* Administración sencilla de la web: La administración de la web se lleva a cabo mediante secciones dentro de nuestro panel.
* Modularización: Al igual que ***cPanel***, con la integración en este caso de ***Softaculous***, permite la adicción de modulos de terceros que añaden funcionalidad a nuestro servidor.
* Seguridad: Permite una gestión muy controlada de la seguridad de nuestro servidor, sin embargo las funcionalidades están más limitadas que en ***cPanel*** y requiere una mayor cantidad de conocimiento del comando *IPTABLES* por parte del administrador.
* Estadísticas e informes, aunque menos detallados.


### Referencias utilizadas
* https://es.godaddy.com/blog/que-es-el-hosting-web-y-para-que-sirve/
* http://carlos-mau.blogspot.com.es/2015/01/hostinger-que-es.html
* https://es.wikipedia.org/wiki/CPanel
* https://es.wikipedia.org/wiki/OVH
* https://www.hostname.cl/web-hosting/cpanel
* https://blog.nerion.es/panel-de-control-hosting-vestacp-manual
