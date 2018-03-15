# Práctica 1 - SWAP
*Carlos Morales Aguilera* - 11/03/2018

## Instalación de las máquinas virtuales
Para la realización de las prácticas he escogido la herramienta de virtualización de máquinas ***VirtualBox***. Para ello instalaremos dos máquinas con el Sistema Operativo *Ubuntu Server 16.04.3*.

### Creación de una máquina virtual

Inicialmente seleccionaremos en el botón *Nueva*, para crear una nueva máquina virtual, y le asignaremos el espacio de memoria deseado, en nuestro caso, el estrictamente recomendado. Para ello crearemos un disco virtual al que se le asigna 8 GB de memoria recomendado de forma automática.

| [![Imagen 1](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/1.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/1.png?raw=true)  | [![Imagen 2](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/2.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/2.png?raw=true) |
|:---:|:---:|

Posteriormente, seleccionaremos la opción de imagen de disco virtual (el SO de Ubuntu Server que instalaremos posteriormente), y seleccionaremos que el almacenamiento se realice de forma dinámica en el disco duro.

Por último, introduciremos el nombre de la imagen creada y le asignaremos una memoria de disco duro virtual, y posteriormente crearemos finalmente la imagen.
| [![Imagen 3](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/3.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/3.png?raw=true)  | [![Imagen 4](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/4.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/4.png?raw=true) | [![Imagen 5](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/5.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/5.png?raw=true) |
|:---:|:---:|:---:|

### Instalación de Ubuntu Server

Una vez creada la imagen, seleccionaremos la imagen a instalar en nuestra máquina virtual ya creada, para ello seleccionaremos la máquina, presionaremos en *Configuración*, a continuación, nos dirigiremos a la pestaña de *Almacenamiento*, seleccionaremos en el disco vacío debajo de *Controlador: IDE*, y presionando en el símbolo del disco en la derecha de la pantalla, abriremos el explorador de archivos y seleccionaremos la imagen de **Ubuntu Server 16.04.3** anteriormente descargada.

![Imagen 6](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/6.png?raw=true)

A continuación, iniciaremos la máquina creada con la imagen asignada e instalaremos *Ubuntu Server*.

Inicialmente, seleccionaremos el idioma español e iniciamos la instalación de *Ubuntu Server* :

| [![Imagen 7](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/7.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/7.png?raw=true)  | [![Imagen 8](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/8.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/8.png?raw=true) |
|:---:|:---:|

Para empezar seleccionaremos el idioma de nuestro servidor de ubuntu, 
y realizaremos el proceso de detección de nuestro teclado, y poserteriormente elegiremos el nombre de nuestra máquina.
| [![Imagen 9](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/9.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/9.png?raw=true)  | [![Imagen 10](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/10.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/10.png?raw=true) | [![Imagen 11](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/11.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/11.png?raw=true) |
|:---:|:---:|:---:|

A continuación indicaremos nuestro nombre, nick y contraseña de usuario que usaremos para loguearnos dentro de la máquina.
| [![Imagen 12](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/12.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/12.png?raw=true)  | [![Imagen 13](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/13.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/13.png?raw=true) | [![Imagen 14](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/14.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/14.png?raw=true) |
|:---:|:---:|:---:|

Continuaremos indicando que no sea cifrada la carpeta personal del usuario, indicando la zona horaria y utilizando todo el disco para la instalación de nuestra máquina.

| [![Imagen 15](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/15.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/15.png?raw=true)  | [![Imagen 16](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/16.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/16.png?raw=true) | [![Imagen 17](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/17.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/17.png?raw=true) |
|:---:|:---:|:---:|

Ahora elegiremos el disco a particionar e indicaremos que no deseamos usar ningún proxy HTTP.

Posteriormente, seleccionaremos los paquetes necesarios para la instalación, para ello escogeremos las opciones *LAMP Server* y *SSH Server*.
| [![Imagen 18](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/18.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/18.png?raw=true)  | [![Imagen 19](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/19.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/19.png?raw=true) | [![Imagen 20](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/20.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/20.png?raw=true) |
|:---:|:---:|:---:|

Para finalizar, introduciremos la contraseña para el usuario root en *MySQL*, en nuestro caso la misma que el usuario creado anteriormente, e indicaremos que sí queremos instalar el menú *Grub* de Ubuntu y finalizaremos la instalación.
| [![Imagen 21](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/21.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/21.png?raw=true)  | [![Imagen 22](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/22.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/22.png?raw=true) |
|:---:|:---:|

----------

### Conexión de ambas máquinas
Al finalizar la instalación, la primera comprobación que haremos es la de que nuestras máquinas soporten *Apache*, para ello comprobaremos con **Apache2**:

[![Imagen 23](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/apache.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/apache.png?raw=true)


Tras esto, nos encontramos que la máquina no es capaz de conectarse con nuestra otra máquina, con internet, ni con el host de ambas.

Inicialmente visualizaremos las redes disponibles con la orden **ifconfig**, con la que podemos observar las redes configuradas.

Para permitir la conexión entre ambas máquinas, tendremos que definir una nueva red que permita interconectar las máquinas, para ello, editaremos el fichero **/etc/network/interfaces**, definiendo la red de la forma:

~~~
auto enp0s8
iface enp0s8 inet static
address 192.168.1.100
gateway 192.168.1.1
netmask 255.255.255.0
network 192.168.1.0
broadcast 192.168.1.255
~~~
Para permitir la conexión de la otra máquina únicamente cambiaremos la dirección *address* de la forma:

~~~
address 192.168.1.101
~~~

Para reflejar los cambios en las máquinas,  tendremos que reiniciar ambas máquinas, con la orden **sudo reboot** (asignando permiso de superusuario).

Ahora podemos observar que podemos conectarnos entre las máquinas, ya sea con una orden *ping*, *ssh* o *curl*:
[
![Imagen 24](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/conexion_1_a_2.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/conexion_1_a_2.png?raw=true)

A continuación, para tener acceso a internet, tendremos configurar en **VirtualBox** un nuevo adaptador de red interna, y además tendremos que añadir nuevamente información a nuestro fichero **/etc/network/interfaces**:

~~~
post-up route del default dev $IFACE
~~~

Nuevamente ejecutamos la orden **sudo reboot**.

Con esto ya podríamos conectarnos a internet y hacer *ping*, por ejemplo, a *www.google.com*:
[
![Imagen 25](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/conexion_internet.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/conexion_internet.png?raw=true)

Por último, para poder acceder al host, tendremos que añadir una nueva red a la máquina virtual, del tipo anfitrión, una vez realizada esta modificación dentro del mismo **VirtualBox**, podremos realizar conexiones al host (en mi caso, 192.168.1.39):
[
![Imagen 26](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/conexion_host.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/conexion_host.png?raw=true)

***Nota***: Para poder realizar la conexión con el host, tras definir la red, habrá que ejecutar la orden **sudo dhclient** (asignando permiso de superusuario) para reiniciar el cliente y reconocer la red.

----------

### Tareas a realizar
* **Conexión mediante SSH**:

	Vamos a realizar una conexión mediante SSH de la primera máquina *swap1* a la segunda máquina *swap2* y crearemos un fichero cualquiera con la orden *touch*, luego desde la segunda máquina visualizaremos el fichero para ver que se ha generado correctamente:
	
| [![Imagen 27](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/ssh_maquina1.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/ssh_maquina1.png?raw=true)  | [![Imagen 28](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/ssh_maquina2.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/ssh_maquina2.png?raw=true) |
|:---:|:---:|


* **Conexión mediante cURL entre máquinas**:
	Para comprobar la conexión mediante cURL entre ambas máquinas, crearemos un fichero html de ejemplo en la máquina *swap2*, dentro del fichero **/var/www/html/**. Una vez creado, realizaremos las conexión desde la máquina *swap1* para visualizar dicho fichero:

| [![Imagen 29](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/conexion_curl.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/conexion_curl.png?raw=true)  | [![Imagen 30](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/ejemplo_html.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/ejemplo_html.png?raw=true) |
|:---:|:---:|


* **Descarga de fichero mediante cURL**:
	Como ya hemos conectado anteriormente las máquinas a internet, realizaremos el ejemplo propuesto en el guión de la práctica, descargando el logo de *Google*:

[
![Imagen 31](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/descarga_curl.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/descarga_curl.png?raw=true)

----------
### Resultado final

* **Redes**:
[
![Imagen 32](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/redes.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/redes.png?raw=true)

*  **/etc/network/interfaces**:
[
![Imagen 33](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/interfaces.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica%201/Imagenes/interfaces.png?raw=true)
