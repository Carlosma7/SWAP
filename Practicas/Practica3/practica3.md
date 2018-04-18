# Práctica 3 - SWAP
*Carlos Morales Aguilera* - 17/04/2018

## Configurar una máquina e instalar nginx como balanceador de carga
En esta práctica se nos propone utilizar un balanceador de carga para dirigir el tráfico que acceda a nuestra granja web conformada por las máquinas *swap1* y *swap2* configuradas en la práctica anterior.

Para ello necesitaremos una nueva máquina sobre la que instalar el software de balanceo de carga, en este apartado, ***nginx***. La máquina que hará de balanceo, poseerá de *S.O.* *Ubuntu Server*, salvando una principal diferencia frente a las máquinas anteriores: La máquina balanceadora no tendrá instalado el paquete **LAMP**, para evitar instalar **Apache** y así mismo, no ocupar el puerto *80* con *Apache*.

Una vez creada la máquina, instalaremos ***nginx*** en la misma con la orden:
```
sudo apt-get install nginx
```
 Posteriormente, una vez instalado ***nginx*** en nuestra máquina, tendremos que definir la funcionalidad de nuestro balanceador de carga, para ello necesitaremos definir la configuración del mismo, indicando los servidores, puerto y otras configuraciónes en el archivo **/etc/nginx/conf.d/default.conf**. (Este archivo a veces puede no crearse en la instalación, como en nuestro caso. Para resolver este problema simplemente lo crearemos usando la orden *sudo nano /etc/nginx/conf.d/default.conf* y editándolo).
 
En nuestro caso la configuración queda de la forma:

[![Imagen 1](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/1.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/1.png?raw=true)

Una vez configurado y realizando la orden *sudo dhclient* para actualizar la configuración de red, podemos comprobar la red a la que realizar la solicitud (al balanceador de carga):

[![Imagen 2](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/2.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/2.png?raw=true)

A continuación realizaremos una petición al servidor para comprobar que recibe la solicitud el balanceador de carga:

[![Imagen 3](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/3.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/3.png?raw=true)

Como podemos observar, ***nginx*** no devuelve la información correspondiente, por lo que está actuando como servidor web, para solucionar esto, debemos configurarlo como balanceador de carga. Para ello vamos a modificar la configuración en el fichero **/etc/nginx/nginx.conf** (comentamos la línea *include /etc/nginx/sites-enabled/\**).

[![Imagen 4](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/4.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/4.png?raw=true)

Finalmente ya tenemos nuestro balanceador de carga correctamente configurado, y procedemos a realizar simplemente dos peticiones para ver que se reparten mediante ***round-robin***, devolviendo el fichero **/var/www/html/index.html** de la máquina correspondiente. Podemos observar que en dos peticiones, devuelve el fichero correspondiente a cada máquina, y observamos que máquina recibe cada petición.

| [![Imagen 5](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/5.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/5.png?raw=true)  | [![Imagen 6](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/6.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/6.png?raw=true) |
|:---:|:---:|

## Configurar una máquina e instalar haproxy como balanceador de carga
Nuevamente crearemos una nueva máquina sobre la que instalar el software de balanceo de carga, en este caso ***haproxy***.

Una vez creada la máquina, instalaremos ***haproxy*** en ella con la orden:

```
sudo apt-get install haproxy
```

Una vez realizada la instalación, se nos habrá guardado la configuración por defecto de ***haproxy***, configuración no válida para nuestra tarea, por lo que la modificaremos y definiremos la configuración deseada en el fichero **/etc/haproxy/haproxy.cfg** de la siguiente forma:

[
![Imagen 7](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/7.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/7.png?raw=true)

Podemos observar que definimos los dos servidores *swap1* y *swap2* como los servidores de nuestra granja web, utilizando el puerto 80 de los mismos.

A continuación, debemos activar el servicio de ***haproxy***, para ello utilizaremos como superusuario la siguiente orden:

```
sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg
```

Nuevamente, realizada la configuración, realizaremos la petición al balanceador de carga, y obtendremos respuestas diferentes dependiendo del servidor al que corresponda según ***round-robin***:

| [![Imagen 8](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/8.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/8.png?raw=true)  | [![Imagen 9](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/9.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/9.png?raw=true) |
|:---:|:---:|

## Someter a la granja web a una alta carga, generada con la herramienta Apache Benchmark, teniendo primero nginx y después haproxy.

Ahora comprobaremos la eficiencia de cada uno de los balanceadores de carga vistos, utilizando para ello la herramienta ***Apache Benchmark***, mandando múltiples solicitudes al servidor que hace de balanceador de carga con la orden:

```
# Para el balanceador de nginx
ab -n 1000 -c 10 http://192.168.56.102/index.html
# Para el balanceador de haproxy
ab -n 1000 -c 10 http://192.168.56.105/index.html
```

Quedando como instrucción genérica:

```
ab -n 1000 -c 10 http://IP_SERVIDOR_BALANCEO/index.html
```

A continuación observamos los resultados:

| [![Imagen 10](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/10.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/10.png?raw=true)  | [![Imagen 11](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/11.png?raw=true)](https://github.com/Carlosma7/SWAP/blob/master/Practicas/Practica3/Imagenes/11.png?raw=true) |
|:---:|:---:|

Como podemos observar, se obtienen unos resultados más veloces en ***haproxy***, debiéndose principalmente a que recibe un mayor número de peticiones en menor tiempo, resultando más eficiente. Podemos contemplar que pese a ser mínima la diferencia, en un caso real con problemas más grandes la diferencia podría llegar a ser muy grande, pero dependiendo del problema convendría utilizar un software u otro.
