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

###1.1 Ejecutar Apache Benchmark contra un servidor final
Una vez conocemos Apache Benchmark, procederemos a ejecutarlo contra uno de los servidores finales. Introduciremos una imagen en el directorio web del servidor, y al ejecutar Apache Benchmark le pediremos esa imagen.
Iniciaremos una de nuestras maquinas finales *(por ejemplo la maquina1)*, pondremos a funcionar nuestro servidor Apache y desde la maquina anfitriona empezaremos a enviarle peticiones del Benchmark.

>Si durante la ejecucion del benchmark en nuestra maquina anfitriona, ejecutaremos *top* en el servidor final, veremos todos los procesos que se generan por las peticiones del benchmark.

><p align="center">
  <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica4/img/ab_top.png" width=600px>
  </p>

Una vez finaliza la ejecucion del Apache Benchmark, nos aparecera en pantalla la informacion que este a obtenido de la ejecución

<p align="center">
  <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica4/img/ab_ejecucion1.png" width=600px>
  </p>

En la siguiente tabla mostraremos algunos de los valores que obtenemos, de 5 ejecuciones del Apache Benchmark contra la maquina1.

| ab Servidor Solo | Time Taken for Test (s) | Failed requests | Request per second (/s) |
|------------------|:-----------------------:|:---------------:|:-----------------------:|
| Medición 1       |                  11,339 |               0 |                   88,19 |
| Medición 2       |                  11,509 |               0 |                   88,89 |
| Medición 3       |                  11,141 |               0 |                   89,76 |
| Medicion 4       |                  11,016 |               0 |                   90,77 |
| Medicion 5       |                  11,239 |               0 |                   88,97 |
|       Media      |          11,249         |      0,000      |          89,316         |
|    Desviacion    |          0,188          |      0,000      |          0,985          |

Ahora los datos de la ejecucion contra el balanceador de carga con *nginx.*

| ab Servidor Solo | Time Taken for Test (s) | Failed requests | Request per second (/s) |
|------------------|:-----------------------:|:---------------:|:-----------------------:|
| Medición 1       |                  27,677 |               0 |                   36,13 |
| Medición 2       |                  27,319 |               0 |                    36,6 |
| Medición 3       |                  27,441 |               0 |                   36,44 |
| Medicion 4       |                  28,051 |               0 |                   35,65 |
| Medicion 5       |                  27,230 |               0 |                   36,72 |
|       Media      |          27,544         |      0,000      |          36,308         |
|    Desviacion    |          0,330          |      0,000      |          0,429          |

Y ahora contra el balanceador de carga con *haproxy*



| ab Servidor Solo | Time Taken for Test (s) | Failed requests | Request per second (/s) |
|------------------|:-----------------------:|:---------------:|:-----------------------:|
| Medición 1       |                  29,728 |               0 |                   33,64 |
| Medición 2       |                  31,592 |               0 |                   31,65 |
| Medición 3       |                  30,355 |               0 |                   32,94 |
| Medicion 4       |                  32,030 |               0 |                   31,22 |
| Medicion 5       |                  30,582 |               0 |                    32,7 |
|       Media      |          30,857         |      0,000      |          32,430         |
|    Desviacion    |          0,938          |      0,000      |          0,984          |

Para que nos sea mas comodo visualizar los resultados, tenemos las siguientes tablas en las que comparamos la media y desviacion estantadar de los 3 datos que hemos tomado con las 3 configuraciones.

<p align="center">
  <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica4/img/ab_ttfr.png">
  </p>

Podemos ver como el servidor final tarda menos que el balanceador de carga en responder todas las peticiones. Esto se debe, a que el *"camino"* se se recorre a traves del balanceador de carga es mas largo.
Tambien podemos ver como *nginx* tarda menos que *haproxy*


  <p align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica4/img/ab_rps.png">
    </p>

Y aqui podemos ver como el servidor final responde mas peticiones por segundo que el balanceador de carga. Algo normal, debido a que este es mas rapido como hemos visto en la grafica anterior.
Tambien vemos que *nginx* responde mas peticiones por segundo que *haproxy*. Otro resultado igual de coherente, teniendo en cuenta la grafica anterior.


Ahora realizaremos la misma operacion, pero contra el balanceador de carga. Primero con el *nginx* en funcionamiento y luego con el *haproxy*.
