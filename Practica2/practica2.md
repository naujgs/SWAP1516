#Practica 2
> Practica realizada por *Juan González Serrano*, para la asignatura de Servidores Webs de Altas Prestaciones

##Ejercicio 1
###Configuración de ssh para acceder sin que solicite contraseña

En este ejercicio lo que vamos hacer es crear un par de claves *publica/privada*. He intercambiaremos las claves publicas entre ambos, utilizando la herramienta **ssh-copy-id**. De forma que podamos acceder del uno al otro mediante *ssh* sin necesidad de autentificarnos en cada intento.

Nos vamos a la maquina 1 y en ella ejecutaremos el comando ***ssh-keygen -t dsa***. Nos preguntara por la ubicación donde deseamos que guarde los ficheros. En mi caso lo dejo en blanco, por lo que lo creara en mi directorio. Luego nos preguntara por una clave, dicha clave sera solicitada siempre que deseemos utilizar el par de claves, en mi caso lo dejo en blanco, por lo que no me solicitara ninguna clave. Finalmente nos genera dos ficheros:
* **~/.ssh/id_dsa**: Para la clave privada
* **~/.ssh/id_dsa.pub**: Para la clave publica.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/keygen_ssh_equi1.jpg)

Realizamos el mismo proceso en el equipo 2.

Una vez hemos creado el par de claves, lo que haremos sera copiar nuestra clave publica en el equipo remoto. De esta forma, no sera necesario volver a identificarse cuando vayamos a realizar una conexión ssh. Para ello ejecutaremos el comando **ssh-copy-id usuario@IP_remota**. Esta orden la ejecutaremos en ambos equipos.

En la siguiente imagen podemos ver el resultado de la ejecución.
![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/ssh_envio_clavePublica.jpg)

Como podemos ver, únicamente nos pide la clave del usuario remoto para establecer la conexión ssh.
En la imagen de abajo vemos como al realizar una conexión ssh ya no nos pide identificación.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/ssh_conexion_conClave.jpg)
***
##Ejercicio 2
###Probar el funcionamiento de la copia de archivos por ssh

En el caso que necesitemos crear un tar.gz de un equipo y dejarlo en otro pero no disponemos de espacio en disco local, podemos usar ssh para crearlo directamente en el equipo destino. Para ello, deberemos indicar al comando tar que queremos que use stdout como destino y mandar con una pipe la salida al ssh. La sintaxis del comando seria:

```sh
tar czf - \<directorio\> | ssh \<equipoDestino\> 'cat > ~/tar.tgz'
```
Para la realización de este ejercicio he creado, en el equipo 1, un directorio *Ejemplo Copia* en el que he creado un fichero de texto y he copiado el fichero de configuración del servicio ssh.

Y sera este fichero el que comprima y guarde en la maquina 2. Para demostrar el buen funcionamiento, mostrare el contenido del directorio personal en la maquina 2.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/compresion_remoto_antes.jpg)

En la siguiente imagen vemos la ejecución de la orden para la compresión de nuestros directorio de prueba y como no se crea ningún fichero en este.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/compresion_creacion.jpg)

Y por ultimo comprobamos el contenido de nuestro equipo remoto, en el que si vemos que se ha creado el fichero comprimido.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/compresion_remoto_despues.jpg)
***
##Ejercicio 3
###Clonado de una carpeta entre las dos maquinas

Para la realización de este ejercicio utilizaremos la herramienta **rsync**. Así que procederemos a su instalación. Para ello, primero haremos un **update** y un **upgrade** de nuestro sistema. Y luego ejecutaremos la orden **sudo apt-get install rsync**. Yo, en mi caso, ya la tengo instalada en ambas maquinas. Por lo que procederé directamente a su ejecución.

La sintaxis del comando que ejecutaremos sera:


```sh
rsync -avz -e ssh \<equipoRemoto\> \<dir_Remota\> \<dir_local\>
```

En este ejercicio creare un directorio en la maquina 2 y lo clonare en la maquina 1. Dicho directorio contendrá un fichero de texto y una copia del fichero de configuración del servicio apache.

[!img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/clonar_contenido_dir.jpg)

Una vez tenemos nuestro directorio ejecutamos nuestra orden. Para ello nos vamos al equipo 1 y ejecutamos la orden. Tras la cual copiara el contenido del directorio, que esta en el equipo 2.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/clonado_ok.jpg)

En la imagen podemos ver el contenido del directorio antes y después de ser clonado.
***
##Ejercicio 4
###Establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas

Para la realización de este ejercicio, crearemos un script con una orden similar a la ejecutada en el ejercicio anterior. Con la finalidad de que nos copie en el directorio ```/var/www``` de nuestra maquina (equipo 1) el contenido del /directorio ```var/www``` de la maquina remota (equipo2).

```sh
rsync -avz -e ssh juan2@172.16.91.129:/var/www /var/www
```
Una vez creado nuestro script, le damos permisos de ejecución.

```sh
sudo chmod a+x script_backup.sh
```

Tambien tendremos que cambiar el usuario del directorio **www** y sus sucesores, en ambas maquinas. Esto lo hacemos porque este directorio pertenece al usuario *root* y realizando este cambio nos evitamos conflictos de usuarios al ejecutar nuestro script y la tarea programada.
Este cambio se realiza con el comando **chown** culla sintaxis es la siguiente:

```sh
chown -R <nuevo_usuario> <fichero>
```

Por ultimo lo que haremos sera añadir la tarea al demonio cron. Para ello ejecutaremos el comando **crontab -e**. Elegiremos el editor de textos y se nos abrira el fichero **crontab**. Aqui escribiremos la sentencia para que nos ejecute nuestro script cada hora.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/crontab_modificado.jpg)

Por ultimo podemos comprobar en la imagen de abajo, como se ejecuta correctamente nuestra tarea programada.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/tarea_programada.jpg)

Tenemos que copiar el usuario del directorio "html" en ambos equipos


http://apuntes-para-no-olvidar.blogspot.com.es/2011/02/cambio-de-propietario-en-una-carpeta.html
