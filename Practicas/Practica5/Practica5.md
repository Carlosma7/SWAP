
# Práctica 5 - SWAP
*Carlos Morales Aguilera* - 12/05/2018

## Crear una BD con al menos una tabla y algunos datos

Para crear una base de datos con ***MySQL*** es necesario haber instalado en nuestro servidor dicha funcionalidad, la cual ya tenemos instalada mediante la instalación de ***LAMP*** inicialmente en la máquina.

Para esta práctica, con el objetivo de facilitar el trabajo, hemos creado dos nuevas máquinas, a las que hemos denominado *maestro* y *esclavo*, según a función de cada una (principalmente con el objetivo de no tener que desconfigurar el cortafuegos de la práctica anterior).

Ejecutamos el inicio de ***MySQL*** con la orden:

```
mysql -u root -p
```

Tras ejecutarla estaremos trabajando en nuestra *BD*, por lo que crearemos inicialmente una nueva base de datos, en este caso, de una plantilla de jugadores de fútbol:

```
create database plantilla;
```

Posteriormente, entraremos en dicha *BD* que hemos creado para poder operar sobre ella:

```
use plantilla;
```

A continuación crearemos una tabla que hemos denominado *jugadores* e insertado dos instancias de la misma:

```
create table jugadores(Nombre varchar(50), Posicion varchar(50));
insert into jugadores values("Carlos Morales", "Mediocentro Ofensivo");
insert into jugadores values("Felipe Martin", "Portero");
```

A continuación se muestra el resultado de la creación:

[![Imagen 1](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/1.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/1.png?raw=true)

## Realizar la copia de seguridad de la BD completa usando mysqldump en la máquina principal y copiar el archivo de copia de seguridad a la máquina secundaria

Inicialmente realizaremos una copia de nuestra *BD* en nuestra máquina, para ello ejecutaremos la orden:

```
mysqldump contactos -u root -p > /tmp/contactos.sql
```

Posteriormente, procederemos a realizar la copia de dicho fichero a nuestra máquina *esclavo*, utilizando para ello la orden [SCP], para a continuación, crear una *BD* con el mismo nombre de la *BD* de la máquina *maestro* y realizar la copia en ella a través del fichero:

[SCP]:https://geekytheory.com/copiar-archivos-a-traves-de-ssh-con-scp

```
scp 192.168.1.108:/tmp/plantilla.sql /tmp/
```

## Restaurar dicha copia de seguridad en la segunda máquina (clonado manual de la BD), de forma que en ambas máquinas esté esa BD de forma idéntica

Una vez recibido el fichero, ejecutamos a continuación la siguiente orden para restablecer la *BD* a través de la copia de seguridad del fichero:


```
mysql -u root -p plantilla < /tmp/plantilla.sql
```

Se muestra a continuación el proceso y resultado:

| [![Imagen 2](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/2.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/2.png?raw=true)  | [![Imagen 3](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/3.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/3.png?raw=true) |
|:---:|:---:|

## Realizar la configuración maestro-esclavo de los servidores MySQL para que la replicación de datos se realice automáticamente

Partiendo de que poseemos la misma *BD* en ambas máquinas sin conectar, procedemos a continuación a modificar el comportamiento de ***MySQL*** en ambas máquinas, para permitir la conexión entre ellas.

Para ello modificaremos el fichero **/etc/mysql/mysql.conf.d/mysqld.cnf** con las siguientes modificaciones:

* En caso de estar comentada, descomentaremos la línea *log_error = /var/log/mysql/error.log* para poder tener acceso al log en caso de producirse algún error en nuestra *BD*.
* Descomentar la línea *log_bin = /var/log/mysql/bin.log* que nos permita acceder al registro binario del *log*.
* Comentar la línea *bind-address 127.0.0.1* que obliga a escuchar en un servidor.
* En el caso de la máquina *maestro*, descomentar la línea *server-id = 1*, y en el caso de la máquina *esclavo*, descomentar la misma línea y cambiar el id a 2.

Posteriormente reiniciaremos ambas *BD* con la orden:

```
/etc/init.d/mysql restart
```

A continuación, procederemos a crear el usuario *esclavo* que permita acceder a la *BD*, para ello nos iremos a la máquina *maestro*, iniciaremos ***MySQL*** y escribiremos las siguientes órdenes:

```
CREATE USER esclavo IDENTIFIED BY 'esclavo';
GRANT REPLICATION SLAVE ON *.* TO 'esclavo'@'%' IDENTIFIED BY 'esclavo';
FLUSH PRIVILEGES;
FLUSH TABLES;
FLUSH TABLES WITH READ LOCK;
```

A continuación mostraremos el estado del usuario *maestro* con la orden:

```
SHOW MASTER STATUS;
```

[![Imagen 4](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/4.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/4.png?raw=true)

El fichero y posición del estado del usuario *maestro* definirá posteriormente parte de la configuración en el servidor *esclavo*.

A continuación, en la máquina *esclavo*, dentro de ***MySQL***, estableceremos como usuario *maestro* el usuario *esclavo* creado anteriormente, para ello ejecutaremos la orden:

```
CHANGE MASTER TO MASTER_HOST='192.168.31.200', MASTER_USER='esclavo', MASTER_PASSWORD='esclavo', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=980, MASTER_PORT=3306;

START SLAVE;
```

[![Imagen 5](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/5.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/5.png?raw=true)

Una vez realizada la configuración, desbloquearemos las tablas en la máquina *maestro* utilizando la orden en ***MySQL***:

```
UNLOCK TABLES;
```

A continuación, comprobamos que la configuración se ha producido correctamente, para ello ejecutaremos la orden:

```
SHOW SLAVE STATUS\G;
```

Nos fijaremos ahora en el campo **Seconds_Behind_Master** si es distinto de *NULL*, lo cual significará que está correctamente configurado:

[![Imagen 6](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/6.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/6.png?raw=true)

Por último, para comprobar que funciona correctamente, mostramos la tabla en el *esclavo*, introduciremos una nueva fila en el *maestro* y volvemos a comprobar en el *esclavo* que se ha actualizado:

[![Imagen 7](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/7.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica5/Imagenes/7.png?raw=true)
