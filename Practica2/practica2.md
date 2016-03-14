#Practica 2

Practica realizada por Juan González Serrano, para la asignatura de Servidores Webs de Áltas Prestaciones

##Ejercicio 1

**Configuración de ssh para acceder sin que solicite contraseña**

En este ejercicio lo que vamos hacer es crear un par de claves *publica/privada*.
Primero en el equipo 1 y luego en el equipo 2. De forma que podamos acceder del uno
al otro mediante *ssh* sin necesidad de autentificarnos en cada intento.

Nos vamos a la maquina 1 y en ella ejecutaremos el comando ***ssh-keygen -t dsa***
