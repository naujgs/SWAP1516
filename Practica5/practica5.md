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
