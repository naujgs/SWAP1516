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
Una vez conocemos Apache Benchmark, procederemos a ejecutarlo contra uno de los servidores finales. Para ello iniciaremos una de nuestras maquinas finales *(por ejemplo la maquina1)*, pondremos a funcionar nuestro servidor Apache y desde la maquina anfitriona empezaremos a enviarle peticiones del Benchmark.

>Si durante la ejecucion del benchmark en nuestra maquina anfitriona, ejecutaremos *top* en el servidor final, veremos todos los procesos que se generan por las peticiones del benchmark.

><p align="center">
  <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica4/img/ab_top.png" width=600px>
  </p>

Una vez finaliza la ejecucion del Apache Benchmark, nos aparecera en pantalla la informacion que este a obtenido de la ejecución

<p align="center">
  <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica4/img/ab_ejecucion1.png" width=600px>
  </p>

En la siguiente tabla mostraremos algunos de los valores que obtenemos, de 5 ejecuciones del Apache Benchmark contra la maquina1

<table>
  <tr>
    <th>ab Servidor Solo<br></th>
    <th>Time Taken<br>for Test (s)<br></th>
    <th>Failed<br>requests<br></th>
    <th>Request per<br>second (/s)<br></th>
  </tr>
  <tr>
    <td>Medición 1<br></td>
    <td>426'042</td>
    <td>0</td>
    <td>2347'19<br></td>
  </tr>
  <tr>
    <td>Medición 2<br></td>
    <td>451'557</td>
    <td>0</td>
    <td>2214'56</td>
  </tr>
  <tr>
    <td>Medición 3<br></td>
    <td>438'673<br></td>
    <td>0</td>
    <td>2279'6</td>
  </tr>
  <tr>
    <td>Medicion 4<br></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Medicion 5<br></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Media</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Desviacion</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
