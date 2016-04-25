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

###1.1Ejecutar Apache Benchmark
Una vez conocemos Apache Benchmark, procederemos a ejecutarlo. Introduciremos una imagen en el directorio web de los servidores y al ejecutar Apache Benchmark le pediremos esa imagen.
Primero lo ejecutaremos contra un servidor final, luego contra el balanceador de carga con nginx funcionando y luego contra el balanceador de carga con haproxy funcionando.

>Si durante la ejecucion del benchmark en nuestra maquina anfitriona, ejecutaremos *top* en el servidor final, veremos todos los procesos que se generan por las peticiones del benchmark.

><p align="center">
  <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica4/img/ab_top.png" width=600px>
  </p>

Una vez finaliza la ejecucion del Apache Benchmark, nos aparecera en pantalla la informacion que este a obtenido de la ejecución

<p align="center">
  <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica4/img/ab_ejecucion1.png" width=600px>
  </p>

En la imagen vemos la ejecucion de Apache Benchmark con un millon de peticiones de mil en mil. Pero para el desarrollo de la practica realizaremos **1000 peticiones de 100 en 100**.

En las siguientes tablas, se recogen los datos de las ejecuciones con las distintas configuraciones

| ab Servidor Solo | Time Taken for Test (s) | Failed requests | Request per second (/s) |
|------------------|:-----------------------:|:---------------:|:-----------------------:|
| Medición 1       |                  11,339 |               0 |                   88,19 |
| Medición 2       |                  11,509 |               0 |                   88,89 |
| Medición 3       |                  11,141 |               0 |                   89,76 |
| Medicion 4       |                  11,016 |               0 |                   90,77 |
| Medicion 5       |                  11,239 |               0 |                   88,97 |
|   **Media**      |      **11,249**         |  **0,000**      |      **89,316**         |
|**Desviacion**    |      **0,188**          |  **0,000**      |      **0,985**          |

Ahora los datos de la ejecucion contra el balanceador de carga con *nginx.*

| ab Servidor Solo | Time Taken for Test (s) | Failed requests | Request per second (/s) |
|------------------|:-----------------------:|:---------------:|:-----------------------:|
| Medición 1       |                  27,677 |               0 |                   36,13 |
| Medición 2       |                  27,319 |               0 |                    36,6 |
| Medición 3       |                  27,441 |               0 |                   36,44 |
| Medicion 4       |                  28,051 |               0 |                   35,65 |
| Medicion 5       |                  27,230 |               0 |                   36,72 |
|   **Media**      |      **27,544**         |  **0,000**      |      **36,308**         |
|**Desviacion**    |      **0,330**          |  **0,000**      |      **0,429**          |

Y ahora contra el balanceador de carga con *haproxy*



| ab Servidor Solo | Time Taken for Test (s) | Failed requests | Request per second (/s) |
|------------------|:-----------------------:|:---------------:|:-----------------------:|
| Medición 1       |                  29,728 |               0 |                   33,64 |
| Medición 2       |                  31,592 |               0 |                   31,65 |
| Medición 3       |                  30,355 |               0 |                   32,94 |
| Medicion 4       |                  32,030 |               0 |                   31,22 |
| Medicion 5       |                  30,582 |               0 |                    32,7 |
|   **Media**      |      **30,857**         |  **0,000**      |      **32,430**         |
|**Desviacion**    |      **0,938**          |  **0,000**      |      **0,984**          |

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

##2º Comprobar el rendimineto de servidores web con Siege

Siege es una herramienta de generación de carga HTTP para benchmarking. Se trata de una utilidad de línea de comandos, similar en interfaz al Apache Benchmark, aunque con opciones de ejecución ligeramente diferentes.

Para poder ejecutarlo, primero deberemos instalarlo. Para ello escribiremos el comando:
```sh
apt-get install siege
```

Para ejecutarlo, escribiremos el siguiente comando:
```sh
siege <opciones de ejecucion> <direccion destinataria>
```

* Las opciones de ejecucion que utilizaremos seran -b -t60S -v
  + **-b** ejecutaremos los tests sin pausas con lo que comprobaremos el rendimiento general
  + **-t60s** ejecutaremos *siege* durante 60 segundos
  + **-v** le indicamos que nos muestre mas informacion
* Direccion o identificador del servidor al que enviaremos las peticiones

###2.1Ejecutar Siege

La manera de proceder sera igual que con *Apache Benchmark*. Primero ejecutaremos *Siege* contra un servidor final, luego contra el balanceador de carga con *nginx* y luego contra el balanceador de carga con *haproxy*.

| Maquina 1      | Availability | Response Time | Transaction rate | Failed transact | Longest Transact |
|:---------------|-------------:|--------------:|-----------------:|----------------:|-----------------:|
| Medición 1     |       100,0% |          0,17 |            88,41 |               0 |             0,63 |
| Medición 2     |       100,0% |          0,17 |            86,26 |               0 |             0,42 |
| Medición 3     |       100,0% |          0,17 |            86,98 |               0 |             0,46 |
| Medición 4     |       100,0% |          0,17 |            87,68 |               0 |             1,12 |
| Medición 5     |       100,0% |          0,19 |            79,50 |               0 |            12,45 |
| **Media**      |   **1,000**  |   **0,174**   |    **85,766**    |    **0,000**    |     **3,016**    |
| **Desviación** |   **0,000**  |   **0,009**   |     **3,593**    |    **0,000**    |     **5,281**    |

| Balanceador (nginx) | Availability | Response Time | Transaction rate | Failed transact | Longest Transact |
|:----------------|-------------:|--------------:|-----------------:|----------------:|-----------------:|
| Medición 1      |       100,0% |          0,44 |            34,32 |               0 |             0,80 |
| Medición 2      |       100,0% |          0,42 |            35,82 |               0 |             0,79 |
| Medición 3      |       100,0% |          0,41 |            36,09 |               0 |             0,74 |
| Medición 4      |       100,0% |          0,41 |            36,18 |               0 |             0,73 |
| Medición 5      |       100,0% |          0,42 |            35,91 |               0 |             0,77 |
|**Media**        | **1,000**    | **0,420**     |  **35,664**      |  **0,000**      |   **0,766**      |
|**Desviación**   | **0,000**    | **0,012**     |  **0,765**       |  **0,000**      |   **0,030**      |

| Balanceador (haproxy) | Availability | Response Time | Transaction rate | Failed transact | Longest Transact |
|:-------------------|-------------:|--------------:|-----------------:|----------------:|-----------------:|
| Medición 1         |       100,0% |          0,40 |            37,40 |               0 |             0,50 |
| Medición 2         |       100,0% |          0,39 |            38,16 |               0 |             0,49 |
| Medición 3         |       100,0% |          0,40 |            37,54 |               0 |             0,48 |
| Medición 4         |       100,0% |          0,41 |            36,61 |               0 |             0,58 |
| Medición 5         |       100,0% |          0,39 |            38,23 |               0 |             0,46 |
|**Media**           | **1,000**    | **0,398**     |  **37,588**      |  **0,000**      |   **0,502**      |
| **Desviación**     | **0,000**    | **0,008**     |   **0,658**      |  **0,000**      |   **0,046**      |

Por ultimo, compararemos los datos obtenidos con las tres configuraciones mediante graficas.

  <p align="center">
  <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica4/img/siege_dispo_med.png">
  <h3>Media</h3>
  </p>
