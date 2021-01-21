# Wordpress con Bitnami

En esta práctica se va a montar un sitio Wordpress utilizando una ami creada Bitnami.

## Preparando la AMI

Para empezar, tenemos que ir a la página web de Bitmani y entrar en el stack de [Wordpress](https://bitnami.com/stack/wordpress/cloud/aws/amis).

Dentro tenemos varias opciones para escoger, seleccionamos la opción **On the cloud** > **Single-Tier**.

A continuación veremos una lista de AMIs de diferentes lugares, cuando hayamos decidido cual utilizar, pulsamos en el enlace que hay al lado y nos llevará a la página de AWS para montar la máquina.

Cuando estemos creando la instancia tenemos que asegurarnos de que la máquina va a tener los puertos **22 (SSH)**, **80 (HTTP)**, y **443 (HTTPS)**.

## Acceso a la máquina y sitios web
Después de esto podremos iniciar nuestra instancia. Con ella en funcionamiento, necesitamos el usuario y contraseña que está usando la máquina para poder conectarnos a ella, para saber esto tenemos que seleccionar nuestra máquina e ir a la pestaña **Acciones** > **Monitoreo y solución de problemas** > **Obtener registros del sistema**

Al entrar en esta opción, se nos abrirá una nueva  pestaña en la que veremos una consola que nos mostrará la contraseña que se ha creado para el usuario y el nombre del usuario, estos parámetros cambian cada vez que se utiliza una nueva AMI.

Si accedemos a la dirección IP o DNS públicos de nuestra AMI podremos ver la ventana de instalación de Wordpress.

Lo que tenemos que hacer ahora es poder acceder al phpMyadmin que contiene nuestra AMI, para ello tenemos que hacer uso de un túnel SSH, el cual al conectarnos a el, podremos acceder al panel de control de phpMyadmin.

Para crear el túnel debemos ejecutar el siguiente comando en una terminal:

>ssh -N -L 8080:127.0.0.1:80 -i clave_aws.pem bitnami@ip_maquina

Donde **clave_aws.pem** es la ruta hasta donde se encuentra nuestro archivo con la clave de Amazon Web Service y **ip_maquina** el nombre DNS o la dirección IP pública de nustra AMI. Con esto haremos que nuestro puerto 8080 y dirección localhost sean enlazados con la dirección de la máquina y su puerto 80, de tal forma que cuando accedamos al navegador y vayamos a la URL 127.0.0.1:8080 vayamos al panel de control de phpMyadmin.

De esta forma podemos utilizar una AMI para crear nuestro sitio de Wordpress y poder administrarlo con las herramientas necesarias.
