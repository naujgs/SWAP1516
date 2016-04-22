#Práctica 4
>Practica realizada por *Juan González Serrano*, para la asignatrua de Servidores Webs de Altas Prestaciones

***
Para la realizacion de esta practica lo que haremos sera ejecutar los Benchmark desde la maquina anfitriona, contra los servidores.
***

##1º Comprobar el rendimineto de servidores web con Apache Benchmark

Apache Benchmark (ab) es una utilidad que se instala junto con el servidor Apache y permite comprobar el rendimiento de cualquier servidor web, por sencillo o complejo que sea.

En el caso de no tener instalado el Apache Benchmark, ejecutaremos el siguiente comando en nuestra terminal:

```sh
apt-get install apache2-utils
```

Para ejecutarlo, debemos entrar en un terminal y ejecutar el comando **ab** de la siguiente forma:
```sh
ab -n <nº de peticiones> -c <nº concurrencia> <direccion destinataria>
```
* **nº de peticiones:** es el nº total de peticiones que se enviara al servicor destinatario
* **nº de concurrencia:** cantidad de peticiones que se enviaran al servidor destinatario, en cada solicitud
* **direccion destinataria:** direccion o identificador del servidor al que enviaremos las peticiones

Por ejemplo, para enviarle mil peticiones a google, de cien en cien, ejecutaremos el comando: ```ab -n 1000 -c 100 http://www.google.com```
