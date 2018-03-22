# Práctica 2 - SWAP
*Carlos Morales Aguilera* - 22/03/2018

## Creación de un fichero *tar* con ficheros locales de un equipo remoto

En ocasiones, necesitaremos copias de seguridad de nuestro servidor principal, las cuales no deben de ser almacenadas en el mismo, ya que reducirían la memoria y rendimiento del mismo, por lo que es de interés realizar copias de seguridad en servidores de almacenamiento o secundarios.

Para ello se proponen una serie de métodos de sincronización, entre los cuales empezaremos comentando la copia de archivos mediante *SSH*.

El método más simple consiste en comprimir la información en un fichero *tar*, y que dicho elemento sea transferido mediante conexión remota al servidor de almacenamiento.

Inicialmente tenemos un escenario como el siguiente:

[![Imagen 1](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/1.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/1.png?raw=true)

A continuación, se muestran ambas máquinas principal (*swap1*, a la izquierda) y secundaria (*swap2*, a la derecha), se comunican en el envío de la carpeta con una imagen. En este caso, la máquina principal se encarga de realizar la compresión y envío del paquete a la máquina secundaria. Desde esta segunda máquina realizamos la descompresión del paquete y comprobamos que se ha envíado la información correctamente:

| [![Imagen 2](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/2.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/2.png?raw=true)  | [![Imagen 3](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/3.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/3.png?raw=true) |
|:---:|:---:|

Como podemos ver, este proceso supone un trabajo extra por parte de la máquina principal, lo cual reduce, aunque sea en pequeña medida, el rendimiento del mismo. En nuestro caso esto supone un rendimiento mínimo, pero en servidores con grandes conjuntos de información puede llegar a suponer un proceso tedioso, reduciendo gravemente el rendimiento de nuestro servidor.

## Clonado de información mediante *rsync*

Como alternativa más eficiente surge esta nueva herramienta, la cual se encarga de realizar sincronizaciones entre máquinas, y que podemos aprovechar para realizar clonado de información entre el servidor y las máquinas secundarias.

### Instalación de rsync

La instalación de *rsync* es un proceso simple en máquinas **Linux**, para ello simplemente habrá que utilizar el instalador *apt* con la orden ***sudo apt-get install rsync***.

[![Imagen 4](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/4.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/4.png?raw=true)

### Clonado de carpetas entre máquinas

Una vez instalado rsync, en la máquina secundaria realizaremos un clonado simple de los archivos de la máquina principal, en este caso de la carpeta ***/var/www/html/*** como en el anterior ejemplo.

Lo primero que tendremos que hacer, es nombrar al usuario como administrador de dicha carpeta, para ello utilizaremos la orden de **Linux** ***chown*** con permisos de administrador.

``` Linux
sudo chown carlos:carlos -R /var/www/html/
```

[![Imagen 5](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/5.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/5.png?raw=true)

A continuación llevaremos a cabo la clonación de dicho directorio por completo, para ello simplemente utilizaremos *rsync* de la forma:

```
rsync -avz -e ssh 192.168.1.100:/var/www/html/ /var/www/html/
```

En este caso intentaremos copiar la carpeta **/var/www/** para demostrar la necesidad de la orden ***chown*** explicada anteriormente.

[![Imagen 6](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/6.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/6.png?raw=true)

Como se puede observar, se producirá un error, esto se debe a que estamos haciendo una conexión al usuario *carlos* del servidor, y la carpeta **/var/www/** no pertenece a dicho usuario, por lo que no tiene acceso para hacer la copia, sin embargo el contenido de la carpeta **/var/www/html/** se clona correctamente debido a la utilización anteriormente de la orden ***chown***.

A continuación, podemos comprobar la funcionalidad de distintas opciones de *rsync* como pueden ser:
* --delete: Elimina aquellos archivos que no se encuentran en el servidor del que se realiza la clonación.
* --exclude: Indica aquellas carpetas/archivos a omitir en el clonado.

En el siguiente ejemplo, podemos ver una estructura simple de directorios con tres carpetas nombras en orden (*carpeta1*, *carpeta2*, *carpeta3*), nuestra intención será copiar las dos primeras carpetas y excluir la tercera. Además podemos ver que inicialmente tenemos una serie de archivos en nuestra máquina secundaria, eliminamos todos y dejamos únicamente el archivo ***ejemplo.html*** para comprobar el funcionamiento del *--delete*:

| [![Imagen 7](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/7.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/7.png?raw=true)  | [![Imagen 8](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/8.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/8.png?raw=true) |
|:---:|:---:|

Como se puede observar, al no existir el archivo ***ejemplo.html*** en la máquina principal, dicho archivo es eliminado en la clonación para que dicha clonación sea perfecta. Por otro lado podemos contemplar que se han copiado los directorios correspondientes con su contenido, a excepción del directorio *carpeta3*, debido a su exclusión en la sincronización.

## Configuración de acceso SSH sin confirmación de contraseña

Hasta ahora hemos comprobado las posibilidades que ofrece la conexión remota mediante *SSH*, pero si queremos automatizar una determinada nos encontramos ante un problema: Autenticación en las conexiones.

SSH permite mediante el uso de configuración de claves pública y privada, generándolas en la máquina principal, y copíandolas en la máquina secundaria, permitiendo realizar las conexiones sin petición de contraseña, ya que la verificación se realiza mediante la comprobación de las claves generadas.

Para ello podemos dividir este proceso en dos partes:

1. Generar las claves privada y pública en la máquina a la que queremos acceder mediante *SSH*, en este caso nuestra máquina principal. Podemos escoger entre varios tipos de clave según el protocolo de *SSH* a emplear, en nuestro caso utilizaremos claves para el protocolo 2 de *SSH*, del tipo ***rsa*** (difiere del tipo ***rsa1*** básicamente en el tipo de cifrado y como se comparten dichas claves, en el caso de ***rsa*** se emplea el algoritmo de *Diffie-Hellman*).
Además, escogeremos el directorio donde almacenar las claves (en nuestro caso, escogemos el proporcionado por defecto), y el *passphrase* a utilizar, pero como buscamos conectarnos sin contraseña, lo dejaremos vacío.
2. Copiar la clave pública al equipo remoto, dándole permisos si fuera necesario.


| [![Imagen 9](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/9.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/9.png?raw=true)  | [![Imagen 10](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/10.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/10.png?raw=true) |
|:---:|:---:|

## Programar tareas con crontab

Como es de esperar, estas tareas realizadas, no deben ser realizadas manualmente por una persona cada *x* tiempo, por lo que se espera que dichas tareas sean automatizadas. Para ello disponemos de las tareas con ***crontab***, el cual permite realizar una orden cada determinada cantidad de tiempo indicada en el mismo.

El formato que sigue una orden de ***crontab*** es

```
Minuto Hora DiaMes Mes DiaSemana Usuario Orden
```

Para realizar la sincronización tal y como se propone en el guión de la práctica solo será necesario escribir una línea en el fichero **/etc/crontab** de la máquina secundaria, con el formato anteriormente explicado, y que realice la sincronización tal y como se ha explicado en apartados anteriores con *rsync*.

[![Imagen 11](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/11.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica2/Imagenes/11.png?raw=true)
