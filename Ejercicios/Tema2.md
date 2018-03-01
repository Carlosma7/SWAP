# Ejercicios Tema 2 - SWAP
*Carlos Morales Aguilera* - 02/03/2018

## Ejercicios T2.1
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

## Ejercicios T2.2
**Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad.**

* **PM2**: administrador de procesos de producción que se utiliza para administrar aplicaciones realizadas en Node.js, mediante el control de clústers. También permite monitorizar y agrupar aplicaciones, administrar registros, étc.
* **Apache Mesos**: administrador de código abierto que corre en nodos de clúster y los administra, dotándolos de aplicaciones para manejar recursos y planificar. Da lugar a otros frameworks como Apache Aurora o Marathon.
* **Spring**: framework administrador de código abierto para desarrollar aplicaciones implementadas en Java. Realiza también tareas de de inversión de control.
* **Terracotta**: en este caso, se trata de una empresa. Se encargan de investigar y desarrollar software para el crecimiento de escalabilidad, disponibilidad y desarrollo de apliaciones *Big-Data*.
