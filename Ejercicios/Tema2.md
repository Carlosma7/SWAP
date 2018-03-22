# Ejercicios Tema 2 - SWAP
*Carlos Morales Aguilera* - 02/03/2018

## Ejercicio T2.1
**Calcular la disponibilidad del sistema si tenemos dos réplicas de cada elemento (en total 3 elementos en cada subsistema).**

***Disponibilidades Iniciales***


| *Component* | *Availability* |
|----------------|-----------------|
| Web | 85% |
| Application | 90% |
| Database | 99.9% |
| DNS | 98% |
| Firewall | 85% |
| Switch | 99% |
| Data Center | 99.99% |
| ISP | 95% |

***Con 2 elementos en cada subsistema***


| *Component* | *Availability* |
|----------------|-----------------|
| Web | 97.75% |
| Application | 99% |
| Database | 99.9999% |
| DNS | 99.96% |
| Firewall | 97.75% |
| Switch | 99.99% |
| Data Center | 99.99% |
| ISP | 99.75% |

 1. Replicar los elementos dos veces, para ello primero replicaremos uno, y posteriormente lo volveremos a replicar.

	***As = Ac1 + ((1 - Ac1) x Ac2)***
	
	Por ejemplo, Web.
	*Web = 85% + ((1 - 85%) x 85%)* => *Web = 97.75%*
	
	Volvemos a replicar.
	*Web = 97.75% + ((1 - 97.75%) x 85%)* => *Web = 99.6625%*
	
	Repetiremos este paso con los distintos elementos que hay en el sistema.

	***Con 3 elementos en cada subsistema***

	|  *Component* | *Availability* |
	| ----------------|-----------------|
	|  Web | 99.6625% |
	|  Application | 99.9% |
	|  Database | 99.9999999% |
	|  DNS | 99.9992% |
	|  Firewall | 99.6625% |
	|  Switch | 99.9999% |
	|  Data Center | 99.999999% |
	|  ISP | 99.9875% |
	
 2. Calcular la disponibilidad del sistema con todos los elementos.
	
	***As = Ac1 + Ac2 + Ac3 + ... + AcN***
	
	En nuestro caso:
	*As = Web x Application x Database x DNS x Firewall x Switch x Data Center x ISP*
	
	*As = 99.6625% x 99.9% x 99.9999999% x 99.9992% x 99.6625% x 99.9999% x 99.999999% x 99.9875%*
	
	**As = 99.2135155%**

## Ejercicio T2.2
**Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad.**

* **PM2**: administrador de procesos de producción que se utiliza para administrar aplicaciones realizadas en Node.js, mediante el control de clústers. También permite monitorizar y agrupar aplicaciones, administrar registros, étc.
* **Apache Mesos**: administrador de código abierto que corre en nodos de clúster y los administra, dotándolos de aplicaciones para manejar recursos y planificar. Da lugar a otros frameworks como Apache Aurora o Marathon.
* **Spring**: framework administrador de código abierto para desarrollar aplicaciones implementadas en Java. Realiza también tareas de de inversión de control.
* **Terracotta**: en este caso, se trata de una empresa. Se encargan de investigar y desarrollar software para el crecimiento de escalabilidad, disponibilidad y desarrollo de apliaciones *Big-Data*.

## Ejercicio T2.3
**¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor?**

Existen diferentes formas de poder analizar los niveles de carga, para ello distinguiremos principalmente dos tipos:

1. Herramientas Linux: Algunas de las herramientas empleadas en otras asignaturas como Sistemas Operativos, nos permiten ver información de los distintos procesos, y cargar del propio sistema.

* **ps**: Muestra un resumen de los distintos procesos del sistema, con la opción *-e* muestra todos los procesos existentes. Mas información sobre [ps].

[ps]:http://francisconi.org/linux/comandos/ps

* **top**: Es una herramienta que permite ver información en tiempo real acerca de los distintos procesos del sistema, con las correspondientes opciones permite visualizar una determinada información de los procesos, como pueda ser comprobar el nombre, el tiempo que llevan o la carga que suponen entre muchos otros. Mas información sobre [top].

[top]:https://geekytheory.com/funcionamiento-del-comando-top-en-linux

2. Herramientas externas: Existen determinadas herramientas o programas externos a *Linux*, los cuales permiten monitorizar los procesos existentes y sus características.

* **Ganglia**: Es una herramienta distribuida y escalable con el objetivo de monitorizar en tiempo real los subsistemas de un servidor, clúster o redes.

* **Zabbix**: Es una herramienta de monitorización de servidores, hardware y servicios de red, basado en otras herramientas como SQL, programado en C y soportando numerosos protocolos que recogen desde *HTTP* hasta *SMTP* por ejemplo.

* **Nagios**: Herramienta de monitorización de redes, cuya principal característica es que se trata de una herramienta de código abierto, y que gestiona tanto hardware como software de las distintas redes.

## Ejercicio T2.4

**Buscar ejemplos de balanceadores software y hardware (productos comerciales).**

* Balanceadores de Software: LVS (Linux Virtual Server), Ultra Monkey (fork de LVS), Pound (menos conocido), HaProxy (muy conocido), Pen, Nginx (muy conocido).

* Balanceadores de Hardware: LoadMaster, Load Balancer ADC (perteneciente a Barracuda), CISCO (gran cantidad de diferentes balanceadores).

**Buscar productos comerciales para servidores de aplicaciones.**

* JavaEE: Basado en él, encontramos numerosos productos, como pueden ser GlassFish, TomEE (Apache), JBoss AS (RedHat) o WebSphere (IBM), entre muchos otros, ofrece una gran variedad.

* Zope: Destinado a la creación de sitios y aplicaciones web.

* django: Desarrollado en Python, destinado al desarrollo web.

* BlueBream: Basado en Zope 3, es de código abierto.

**Buscar productos comerciales para servidores de almacenamiento.**

* Microsoft Azure: Servicio en la nube alojado en los centros de datos de Windows.

* Cloudsigma: Poco conocido, se trata de un servicio en la nube suizo.

* DigitalOcean: Proveedor de servidores virtuales basados en la nube de origen estadounidense.