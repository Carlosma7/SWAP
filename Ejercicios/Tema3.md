# Ejercicios Tema 3 - SWAP
*Carlos Morales Aguilera* - 23/03/2018

## Ejercicio T3.1
**Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.**

* **Windows**: En Windows poseemos herramientas propias de enrutamiento, como es Windows Server, existente en distintas versiones como la de 2008, hasta una de las más actuales como es la de [Windows Server 2016].

[Windows Server 2016]:http://blogs.itpro.es/readyplayerone/2015/10/03/servicios-de-enrutamiento-en-windows-server-2016/

* **Linux**: La configuración de las distintas redes de nuestro sistema se encuentra almacenado en el fichero **/etc/network/interfaces**, tal y como se ha visto en prácticas. El comando asociado a la configuración de redes es [route], el cual permite la manipulación de redes.

[route]:https://www.hscripts.com/es/tutoriales/linux-commands/route.html

* **Herramientas gráficas**: Existen además herramientas destinadas a estas funcionalidades con un entorno gráfico que facilita dicha tarea, como pueden ser **XORP**, **OpenGDB** o **Manage Engine**.

## Ejercicio T3.2
**Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.**

* **Windows**: Misma herramienta que en el ejercicio anterior, la configuración de filtrado se realiza a través de *Windows Server*.

* **Linux**: La administración del filtrado de paquetes se realiza con la orden de terminal [iptables], la cual permite la configuración de filtros mediante conjuntos de reglas simples, realizando entonces el filtrado indicado.

[iptables]:https://www.linuxito.com/seguridad/793-tutorial-basico-de-iptables-en-linux

* **Herramientas gráficas**: Probablemente la más conocida sea [Wireshark], aunque existen otras como *Shorewall*, que facilitan la configuración mediante un entorno gráfico simple.

[Wireshark]:https://geekytheory.com/tutorial-wirshark-1-instalacion/