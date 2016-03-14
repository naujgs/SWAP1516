#Practica 2

Practica realizada por Juan González Serrano, para la asignatura de Servidores Webs de Áltas Prestaciones

##Ejercicio 1

**Configuración de ssh para acceder sin que solicite contraseña**

En este ejercicio lo que vamos hacer es crear un par de claves *publica/privada*.
Primero en el equipo 1 y luego en el equipo 2. De forma que podamos acceder del uno
al otro mediante *ssh* sin necesidad de autentificarnos en cada intento.

Nos vamos a la maquina 1 y en ella ejecutaremos el comando ***ssh-keygen -t dsa***
Nos preguntara por la ubicacion donde deseamos que guarde los ficheros. En mi
caso lo dejo en blanco, por lo que lo creara en mi directorio.
Luego nos preguntara por una clave. Dicha clave sera solicitada siempre que deseemos
utilizar el par de claves. En mi caso lo dejo en blanco, por lo que no me solicitara
ninguna clave.
Finalmente nos genera dos ficheros:
* **~/.ssh/id_dsa**: Para la clave privada
* **~/.ssh/id_dsa.pub**: Para la clave publica.

**(Ver [Figura 1](https://github.com/naujgs/SWAP1516/blob/master/Practica2/img/keygen_ssh_equi1.jpg))** // Keygen_ssh_equi1

Sera el fichero *~/.ssh/id_dsa.pub* el que tendremos que copiar en el otro fichero
