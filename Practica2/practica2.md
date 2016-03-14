#Practica 2

Practica realizada por Juan González Serrano, para la asignatura de Servidores Webs de Áltas Prestaciones

##Ejercicio 1

**Configuración de ssh para acceder sin que solicite contraseña**

En este ejercicio lo que vamos hacer es crear un par de claves *publica/privada*.
E intercambiaremos las claves publicas entre ambos, utilizando la herramienta **rsync**.
De forma que podamos acceder del uno al otro mediante *ssh* sin necesidad de autentificarnos en cada intento.

Nos vamos a la maquina 1 y en ella ejecutaremos el comando ***ssh-keygen -t dsa***
Nos preguntara por la ubicacion donde deseamos que guarde los ficheros. En mi
caso lo dejo en blanco, por lo que lo creara en mi directorio.
Luego nos preguntara por una clave. Dicha clave sera solicitada siempre que deseemos
utilizar el par de claves. En mi caso lo dejo en blanco, por lo que no me solicitara
ninguna clave.
Finalmente nos genera dos ficheros:
* **~/.ssh/id_dsa**: Para la clave privada
* **~/.ssh/id_dsa.pub**: Para la clave publica.

![imagen](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/keygen_ssh_equi1.jpg)

Realizamos el mismo proceso en el equipo 2.

Una vez hemos creado el par de claves, lo que haremos sera copiar nuestra clave
publica en el equipo remoto. De esta forma, no sera necesario volver a identificarse
cuando vayamos a realizar una conexion ssh. Para ello ejecutaremos el comando **ssh-copy-id usuario@IP_remota**.
Esta orden la ejecutaremos en ambos equipos.


Sera el fichero *~/.ssh/id_dsa.pub* el que tendremos que copiar en el otro equipo
(maquina 2). Para ello nos conectaremos al equipo dos atraves de ssh, y le
enviaremos nuestra clave pública.
Ahora nos pedira que nos identifiquemos, pero al finalizar este ejercicio veremos
que esto dejara de ser asi.

Para conectarnos atraves de ssh, ejecutaremos el comando *ifconfig* y veremos cual
es la ip de nuestro equipo. En mi caso son:
* *Equipo 1* 172.16.91.128
* *Equipo 2* 172.16.91.129

Por lo que en la maquina 1 ejecutare el comando **ssh root@172.16.91.129**. En caso
de tener algun problema tendremos que irnos al directorio **/etc/ssh/sshd_config**
,poner el parametro **PermitRootLogin** a **yes** y reiniciar el servicio **service ssh restart**.

![imagen](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/ssh_permisosRoot.jpg)

A continuacion vemos como establecemos la conexion entre el equipo 1 y el 2.
![imagen](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/ssh_conexion.jpg)

Por ultimo lo que haremos sera enviar
