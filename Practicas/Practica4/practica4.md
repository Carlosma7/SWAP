# Práctica 3 - SWAP
*Carlos Morales Aguilera* - 25/04/2018

## Crear e instalar en la máquina 1 un certificado SSL autofirmado para configurar el acceso HTTPS a los servidores. Una vez configurada la máquina 1, se debe copiar al resto de máquinas servidoras y al balanceador de carga. Se debe configurar nginx adecuadamente para aceptar y balancear correctamente tanto el tráfico HTTP como el HTTPS.

Inicialmente, habrá que instalar ***SSL*** en nuestra máquina para poder trabajar con él, por  lo que lo instalamos en nuestra máquina *swap1* con la orden:

```
sudo a2enmod ssl
```

[![Imagen 1](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/1.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/1.png?raw=true)

Vemos que una vez ejecutado nos solicita reiniciar el servicio de apache, por lo que ejecutaremos la orden:

```
sudo service apache2 restart
```

Una vez reiniciado el servicio, necesitaremos configurar la conexión ***SSL***, para ello necesitaremos crear una clave y un certificado propios de la máquina *swap1* para poder conectarnos a ella mediante ***https***, para ello ejecutaremos la orden:

```
sudo mkdir /etc/apache2/ssl
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
```

La configuración nos solicitará cierta información a rellenar para la configuración de ***SSL*** sobre nosotros:

[![Imagen 2](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/2.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/2.png?raw=true)

Una vez hemos creado el certificado **apache.crt** y la clave **apache.key** en el directorio **/etc/apache2/ssl**, procedemos a modificar la configuración por defecto de ***SSL***.

A continuación modificaremos el fichero **/etc/apache2/sites-available/default-ssl.conf** para modificar dicha configuración por defecto, y modificaremos las líneas:

```
SSLCertificateFile /etc/apache2/ssl/apache.crt
SSLCertificateKeyFile /etc/apache2/ssl/apache.key
```

[
![Imagen 3](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/3.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/3.png?raw=true)

Una vez modificada la configuración, ejecutamos ***SSL*** con dicha configuración con la orden:

```
sudo a2ensite default-ssl.conf
```

[
![Imagen 4](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/4.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/4.png?raw=true)

Nuevamente nos solicitará que reiniciemos el servicio, por lo que una vez lo reiniciemos (*sudo service apache2 reload*), ya podremos realizar peticiones a la máquina *swap1* con ***https***:

[
![Imagen 5](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/5.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/5.png?raw=true)

A continuación procederemos a configurar el balanceador ***nginx***, para ello copiaremos los ficheros de configuración **apache.crt** y **apache.key** creados en la máquina *swap1* (con ***SSH*** o ***rsync***) en nuestro caso en la carpeta que hemos creado **/etc/apache2/ssl**.

Ya copiados ambos ficheros, procederemos a modificar la configuración del servidor de balanceo como en la práctica anterior, editando el fichero de configuración de ***nginx***, **/etc/nginx/conf.d/default.conf**.

Para ello indicaremos que escuche el puerto ***443*** perteneciente a ***https*** e indicaremos los ficheros copiados de la máquina 1 con las líneas:

```
listen 443 ssl;
ssl_certificate /etc/apache2/ssl/apache.crt
ssl_certificate_key /etc/apache2/ssl/apache.key
```

Al final obtenemos una configuración de la forma:

[
![Imagen 6](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/6.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/6.png?raw=true)

A continuación observamos que indiferentemente el servidor de balanceo resuelve peticiones de ***http*** y ***https*** procediendo según corresponda:

| [![Imagen 7](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/7.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/7.png?raw=true)  | [![Imagen 8](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/8.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/8.png?raw=true) |
|:---:|:---:|

## Configurar las reglas del cortafuegos con IPTABLES para asegurar el acceso a uno de los servidores web, permitiendo el acceso por los puertos de HTTP y HTTPS a dicho servidor. Esta configuración se hará en una de las máquinas servidoras finales (p.ej. en la máquina 1), y se debe poner en un script con las reglas del cortafuegos que se ejecute en el arranque del sistema (según la versión de Linux, se llevará a cabo de una forma u otra).

Para poder configurar las reglas del cortafuegos en la máquina *swap1*, necesitaremos crear un fichero nuevo con el que definir las reglas con la orden ***iptables***, de forma que elimine las reglas anteriores, deniege todas las peticiones y únicamente permita localhost, abriendo sólo los puertos 22 (***SSH***), 80 (***HTTP***) y 443 (***HTTPS***):

[![Imagen 9](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/9.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica4/Imagenes/9.png?raw=true)

Una vez realizada la configuración la ejecutaremos al inicio de la máquina, utilizando para ello un demonio, para ello modificaremos los permisos de ejecución del fichero permitiendo su ejecución como script, lo copiaremos al directorio **/etc/init.d/** y actualizaremos los demonios del sistema, para ello utilizaremos las órdenes:

```
sudo chmod a+x config_firewall.sh
sudo cp config_firewall.sh /etc/init.d/
sudo update-rc.d config_firewall.sh defaults
```
