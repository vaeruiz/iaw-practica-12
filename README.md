# Wordpress con Bitnami

En esta práctica se va a montar un sitio Wordpress utilizando una ami creada con Bitnami.

## Preparando la AMI

Para empezar, tenemos que ir a la página web de Bitmani y entrar en el stack de [Wordpress](https://bitnami.com/stack/wordpress/cloud/aws/amis).

Dentro tenemos varias opciones para escoger, seleccionamos la opción **On the cloud** > **Single-Tier**.

A continuación veremos una lista de AMIs de diferentes lugares, cuando hayamos decidido cual utilizar, pulsamos en el enlace que hay al lado y nos llevará a la página de AWS para montar la máquina.

Cuando estemos creando la instancia tenemos que asegurarnos de que la máquina va a tener los puertos **22 (SSH)**, **80 (HTTP)**, y **443 (HTTPS)**.

## Acceso a la máquina y sitios web
Después de esto podremos iniciar nuestra instancia. Con ella en funcionamiento, necesitamos el usuario y contraseña que está usando la máquina para poder conectarnos a ella, para saber esto tenemos que seleccionar nuestra máquina e ir a la pestaña **Acciones** > **Monitoreo y solución de problemas** > **Obtener registros del sistema**

Al entrar en esta opción, se nos abrirá una nueva  pestaña en la que veremos una consola que nos mostrará la contraseña que se ha creado y el nombre del usuario de la máquina, estos parámetros cambian cada vez que se utiliza una nueva AMI.

Si accedemos a la dirección IP o DNS públicos de nuestra AMI podremos ver la ventana de instalación de Wordpress.

# Túnel SSH para el acceso a phpMyAdmin

Para tener una administración total de la base de datos de Wordpress nos podemos conectar a través de phpMyAdmin, sin embargo, ahora no podemos hacerlo porque la máquina rechazará las conexiones exteriores, para poder conectarnos a la herramienta tenemos que hacer uso de un túnel ssh, para crear el túnel debemos ejecutar el siguiente comando:

>ssh -N -L 8888:127.0.0.1:80 -i clave_aws.pem bitnami@ip_maquina

Con esto lo que hacemos es enlazar el puerto 80 del servidor al puerto 8888 de nuestra máquina y la dirección localhost (127.0.0.1), de esta manera, si accedemos al navegador y escribimos 127.0.0.1:8888 podremos acceder al login de phpMyAdmin de nuestro servidor a través del túnel que hemos creado.

En este caso las credenciales de inicio de sesión son el usuario root y la clave que nos ha asignado el sistema en el momento en el que se ha creado la instancia de Bitnami.

De esta forma podemos utilizar una AMI para crear nuestro sitio de Wordpress y poder administrarlo con las herramientas necesarias.
