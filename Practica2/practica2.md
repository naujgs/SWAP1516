#Practica 2
> Practica realizada por Juan González Serrano, para la asignatura de Servidores Webs de Áltas Prestaciones

##Ejercicio 1
###Configuración de ssh para acceder sin que solicite contraseña

En este ejercicio lo que vamos hacer es crear un par de claves *publica/privada*. He intercambiaremos las claves publicas entre ambos, utilizando la herramienta **ssh-copy-id**. De forma que podamos acceder del uno al otro mediante *ssh* sin necesidad de autentificarnos en cada intento.

Nos vamos a la maquina 1 y en ella ejecutaremos el comando ***ssh-keygen -t dsa***. Nos preguntara por la ubicacion donde deseamos que guarde los ficheros. En mi caso lo dejo en blanco, por lo que lo creara en mi directorio. Luego nos preguntara por una clave, dicha clave sera solicitada siempre que deseemos utilizar el par de claves, en mi caso lo dejo en blanco, por lo que no me solicitara ninguna clave. Finalmente nos genera dos ficheros:
* **~/.ssh/id_dsa**: Para la clave privada
* **~/.ssh/id_dsa.pub**: Para la clave publica.

![imagen](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/keygen_ssh_equi1.jpg)

Realizamos el mismo proceso en el equipo 2.

Una vez hemos creado el par de claves, lo que haremos sera copiar nuestra clave publica en el equipo remoto. De esta forma, no sera necesario volver a identificarse cuando vayamos a realizar una conexion ssh. Para ello ejecutaremos el comando **ssh-copy-id usuario@IP_remota**. Esta orden la ejecutaremos en ambos equipos.

En la siguiente imagen podemos ver el resultado de la ejecucion

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/ssh_envio_clavePublica.jpg)

Como podemos ver, unicamente nos pide la clave del usuario remoto para establecer la conexion ssh.
En la imagen de abajo vemos como al realizar una conexion ssh ya no nos pide identificacion.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/ssh_conexion_conClave.jpg)
***
##Ejercicio 2
###Probar el funcionamiento de la copia de archivos por ssh

En el caso que necesitemos crear un tar.gz de un equipo y dejarlo en otro pero no disponemos de espacio en disco local, podemos usar ssh para crearlo directamente en el equipo destino. Para ello, deberemos indicar al comando tar que queremos que use stdout como destino y mandar con una pipe la salida al ssh. La sintaxis del comando seria:

```sh
tar czf - \<directorio\> | ssh \<equipoDestino\> 'cat > ~/tar.tgz'
```
Para la realizacion de este ejercicio he creado, en el equipo 1, un directorio *Ejemplo Copia* en el que he creado un fichero de texto y he copiado el fichero de configuracion del servicio ssh.

Y sera este fichero el que comprima y guarde en la maquina 2. Para demostrar el buen funcionamiento, mostrare el contenido del directorio personal en la maquina 2.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/compresion_remoto_antes.jpg)

En la siguiente imagen vemos la ejecucion de la orden para la compresion de nuestros directorio de prueba y como no se crea ningun fichero en este.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/compresion_creacion.jpg)

Y por ultimo comprobamos el contenido de nuestro equipo remoto, en el que si vemos que se ha creado el fichero comprimido.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/compresion_remoto_despues.jpg)
***
##Ejercicio 3
###Clonado de una carpeta entre las dos maquinas

Para la realización de este ejercicio utilizaremos la herramienta **rsync**. Asi que procederemos a su instalacion. Para ello, primero haremos un **update** y un **upgrade** de nuestro sistema. Y luego ejecutaremos la orden **sudo apt-get install rsync**. Yo, en mi caso, ya la tengo instalada en ambas maquinas. Por lo que procedere directamente a su ejecucion.

La sintaxis del comando que ejecutaremos sera:

**rsync -avz -e ssh \<equipoRemoto\> \<dir_Remota\> \<dir_local\>**

En este ejercicio creare un directorio en la maquina 2 y lo clonare en la maquina 1. Dicho directorio contendra un fichero de texto y una copia del fichero de configuracion del servicio apache.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/clonar_contenido_dir.jpg)

Una vez tenemos nuestro directorio ejecutamos nuestra orden. Para ello nos vamos al equipo 1 y ejecutamos la orden. Tras la cual copiara el contenido del directorio, que esta en el equipo 2.

![img](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/clonado_ok.jpg)

En la imagen podemos ver el contenido del directorio antes y despues de ser clonado.
***
##Ejercicio 4
###Establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas
