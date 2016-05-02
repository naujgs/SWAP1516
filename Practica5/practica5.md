#Práctica 5
>Practica realizada por *Juan González Serrano*, para la asignatrua de Servidores Webs de Altas Prestaciones

***

###1º Creacion de una Base de Datos e insertado de datos

Para la realizacion de esta practica, necesitaremos tener instalado el MySQL server en los dos servidores finales. En el caso de que no lo tengamos, podremos instalarlo con el comando:
```sh
sudo apt install mysql-server
```

Crearemos una base de datos en MySQL e insertaremos algunos datos. De esta forma, tendremos informacion con la cual hacer las copias de seguridad.
En todo momento usaremos la interfaz de linea de comandos del MySQL.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/bd_crear.png">
    <p> Creacion de base de datos e insercion de datos</p>
</div>

Ya tenemos una pequeña base de datos con algunos datos.

###2º Replicacion e una Base de Datos con *mysqldump*

**mysqldump** es una herramienta para clonar las bases de datos que tenemos en nuestras maquinas.
Forma parte de los programas de clente de *MySQL*. Permite el volcado de una o varias base de datos, con la intencion de crear copias de seguridad o para transferir datos a otro servidor *SQL* (no necesariamente un servidor *MySQL*)

*mysqldump* tiene una gran cantidad de opciones, por lo que para obtener informacion podremos consultar la siguiente direccion:

http://dev.mysql.com/doc/refman/5.0/es/mysqldump.html

Tambien podemos consultar el manual en linea

```sh
mysqldump --help
```

La sintaxis de uso es la siguiente:

```sh
mysqldump <base_datos> -u root -p > <path_destino_copia>
```

Esto puede ser suficiente, pero tenemos que tener en cuenta que los datos pueden estar actualizándose constantemente en el servidor de BD principal. Por lo que, antes de hacer la copia de seguridad en el archivo *.SQL* debemos evitar que se
acceda a la BD para cambiar nada.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/bd_bloquear.png">
    <p> Bloqueo actualización base de datos</p>
</div>

Ahora procederemos a crear una copia local de nuestra base de datos. Para ello, primero nos loguearemos como *root*

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/mysqldump_local.png">
    <p> Ejecucion de <i>mysqldump</i></p>
</div>

A continuacion comprobamos que se haya creado la copia de la base de datos en el directorio especificado

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/mysqldump_local_comprobacion.png">
    <p> Comprobacion creacion copia BD mysqldump</p>
</div>
