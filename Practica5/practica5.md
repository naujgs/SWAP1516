#Práctica 5
>Practica realizada por *Juan González Serrano*, para la asignatura de Servidores Webs de Altas Prestaciones

***

###1º Creación de una Base de Datos e insertado de datos

Para la realización de esta practica, necesitaremos tener instalado el MySQL server en los dos servidores finales. En el caso de que no lo tengamos, podremos instalarlo con el comando:
```sh
sudo apt install mysql-server
```

Crearemos una base de datos en MySQL e insertaremos algunos datos. De esta forma, tendremos información con la cual hacer las copias de seguridad.
En todo momento usaremos la interfaz de linea de comandos del MySQL.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/bd_crear.png">
    <p> Creación de base de datos e inserción de datos</p>
</div>

Ya tenemos una pequeña base de datos con algunos datos.

###2º Replicación de una Base de Datos con *mysqldump*

**mysqldump** es una herramienta para clonar las bases de datos que tenemos en nuestras maquinas.
Forma parte de los programas de cliente de *MySQL*. Permite el volcado de una o varias base de datos, con la intención de crear copias de seguridad o para transferir datos a otro servidor *SQL* (no necesariamente un servidor *MySQL*)

*mysqldump* tiene una gran cantidad de opciones, por lo que para obtener información podremos consultar la siguiente dirección:

http://dev.mysql.com/doc/refman/5.0/es/mysqldump.html

También podemos consultar el manual en linea

```sh
mysqldump --help
```

La sintaxis de uso es la siguiente:

```sh
mysqldump <base_datos> -u root -p > <path_destino_copia>
```

Esto puede ser suficiente, pero tenemos que tener en cuenta que los datos pueden estar actualizándose constantemente en el servidor de BD principal. Por lo que, antes de hacer la copia de seguridad en el archivo *.SQL* debemos evitar que se acceda a la BD para cambiar nada.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/bd_bloquear.png">
    <p> Bloqueo actualización base de datos</p>
</div>

Ahora procederemos a crear una copia local de nuestra base de datos. Para ello, primero nos loguearemos como *root*

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/mysqldump_local.png">
    <p> Ejecución de <i>mysqldump</i></p>
</div>

A continuación comprobamos que se haya creado la copia de la base de datos en el directorio especificado

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/mysqldump_local_comprobacion.png">
    <p> Comprobación creación copia BD <i>mysqldump</i></p>
</div>

Una vez ya hemos creado nuestra copia, procedemos a desbloquear las tablas:

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/bd_desbloquear.png">
    <p> Desbloqueo actualización base de datos</p>
</div>

Ahora, nos iremos a la maquina de backup (maquina2) y copiaremos el fichero *.SQL* que hemos creado en la maquina maestra (maquina1). Para ello utilizaremos **scp** con la siguiente sintaxis:

```sh
scp [[user@]host1:]file1 ... [[user@]host2:]file2
```

+ **[user@]host1:]file1**
      El origen, donde se especifica él archivo o archivos que serán copiados, puede o no contener la información del ordenador remoto, y también puede contener la información del usuario que es dueño del archivo o archivos en el ordenador remoto. Si el usuario no esta especificado, entonces por defecto usará los datos del usuario actual en el ordenador donde estas escribiendo el comando. Y si ningún ordenador remoto es especificado, entonces buscará el archivo localmente
+ **[[user@]host2:]file2**
      El destino, donde se especifica la vía donde los archivos serán copiados, es decir el destino de los mismos, y de nuevo, puede o no contener la información sobre el ordenador remoto y el usuario en ese ordenador. Al igual que fuera explicado arriba, si el usuario no se especifica pero si el nombre o el IP de un ordenador, en ese caso tratará de obtener acceso a ese ordenador remoto usando las credenciales del usuario actual, y si no se especifica ordenador remoto, se asume que el destino de los archivos es local.

En la siguiente imagen podemos ver un ejemplo de ejecución. Primero ejecutando el comando desde la maquina *maestro* y luego desde la maquina *esclavo*

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/scp_demostracion.png">
    <p> Envío copia base de datos con herramienta SCP</p>
</div>


Pero si nos fijamos, la copia de la base de datos la hice en el directorio */root/* pero las copias las realizo al directorio personal. Esto se debe a que tenia problemas de permisos al directorio *root*.
En ese caso, la solución seria enviar la copia a cualquier directorio del equipo remoto y después conectarnos por ssh y así colocarlo en el directorio idóneo.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/scp_ejecucion.png">
    <p> Envío copia base datos | Reubicación son ssh</p>
</div>

Ya hemos realizado la copia.
Es importante destacar que el archivo *.SQL* de copia de seguridad tiene formato de texto plano, e incluye las sentencias SQL para restaurar los datos contenidos en la BD en otra máquina. Sin embargo, la orden *mysqldump* no incluye en ese archivo la sentencia para crear la BD. Por lo que nosotros tendremos que crear primero la BD y después restaurarla.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/mysqldump_crear_bd_remota.png">
    <p> Creo la base de datos en el equipo remoto</p>
</div>

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/bd_restauracion_bk.png">
    <p> Restauración, en equipo remoto, de la base de datos con la información del equipo maestro</p>
</div>

Accederemos a la base de datos y consultaremos su contenido para comprobar que el proceso se ha realizado con éxito.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/bd_bk_comprobacion.png">
    <p> Contenido de la base de datos en el equipo backup</p>
</div>

También podemos hacer la orden directamente usando un “pipe” a un ssh para exportar los datos al mismo tiempo (siempre y cuando en la máquina secundaria ya hubiéramos creado la BD):

```sh
mysqldump ejemplodb -u root -p | ssh equipoDestino mysql
```

###3º Replicación de una Base de Datos mediante una configuración *maestro-esclavo*

La opcion anterior es tan valida como cualquier otra y funciona perfectamente. Pero es demasiado *manual*.
Por ello *MySQL* nos ofrece la opción de configurar el demonio para hacer replicación de las *BD* sobre un esclavo a partir de los datos que almacena el maestro. Esto transforma el proceso manual realizado en el punto anterior, en un proceso completamente automatico.
Para ello realizaremos una serie de configuraciones tanto en el servidor principal como en el secundario.

>Un requisito para empezar, es que ambas maquinas tengan clonadas las base de datos. Esto ya lo tenemos, pues lo hemos hecho en el apartado anterior.

Lo primero que haremos, sera configurar el *MySQL* del equipo maestro. Para ello editaremos como *root* el fichero **/etc/mysql/my.cnf**

* **Paso 1**

Comentamos el parametro **bind-address**. Este sirve para que escuche a un servidor.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/conf_mysql_master_bindAddress.png">
    <p> Configurado <i>MySQL</i> equipo maestro</p>
</div>

* **Paso 2**

Le indicamos el archivo donde almacenar el log de errores. De esta forma, si por ejemplo al reiniciar el servicio cometemos algún error en el archivo de configuración, en el archivo de log nos mostrará con detalle lo sucedido.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/conf_mysql_master_logError.png">
    <p> Configurado <i>MySQL</i> equipo maestro</p>
</div>

* **Paso 3**

Establecemos el identificador del servidores

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/conf_mysql_master_serverId.png">
    <p> Configurado <i>MySQL</i> equipo maestro</p>
</div>

* **Paso 4**

Le indicamos el archivo de registro binario.El registro binario contiene toda la información que está disponible en el registro de actualizaciones, en un formato más eficiente y de una manera que es segura para las transacciones.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/conf_mysql_master_logBin.png">
    <p> Configurado <i>MySQL</i> equipo maestro</p>
</div>


Tras realizar estas configuraciones, guardamos el fichero y reiniciamos el servicio, con uno de los dos comandos siguientes:
```sh
 sudo service mysql restart
 /etc/init.d/mysql restart
```
Si no nos ha dado ningún error la configuración del maestro, podemos pasar a hacer la configuración del *mysql* del esclavo. Para ello editaremos como *root* el fichero **/etc/mysql/my.conf**

La configuración es similar a la del maestro, con la diferencia del *Paso 2 (server-id)* que en este caso es **2**

Tras realizar los cambios en la configuración reiniciamos el servicio y si no nos da ningun error es que hemos tenido exito en la configuración.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/reinicio_mysql_slave_after_conf.png">
    <p> Reinicio del servicio <i>MySQL</i> tras realizar cambios en configuracion</p>
</div>

Volvemos al equipo *maestro*, donde creamos un usuario y le damos permisos de acceso a la replicación.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/demonio_mysql_conf_master.png">
    <p> Creación de usuario en BD del equipo maestro<i>maestro</i>, con permisos de acceso a la replicación</p>
</div>

Para finalizar la configuracion en el *maestro*, obtenemos los datos de la base de datos que vamos a replicar. Para posteriormente usarlos en la configuración del equipo *esclavo*.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/demonio_mysql_datos_master.png">
    <p> Reinicio del servicio <i>MySQL</i> tras realizar cambios en configuracion</p>
</div>

Ahora nos vamos a la maquina *esclava*, entramos en el *mysql* y le damos los datos del *maestro*. Para versiones anteriores de **mysql5.5** los datos los podemos introducir directamente en el archivo de configuración. En nuestro caso los introduciremos en el entorno de *mysql*. *(Debemos tener mucho cuidado con la IP, "master_log_file" y el "master_log_pos" del maestro)*
```sh
mysql> CHANGE MASTER TO MASTER_HOST='192.168.31.200',
MASTER_USER='esclavo', MASTER_PASSWORD='esclavo',
MASTER_LOG_FILE='bin.000003', MASTER_LOG_POS=501,
MASTER_PORT=3306;
```

Los datos que ponemos en *MASTER_LOG_FILE* y en *MASTER_LOG_POS* son los que obtuvimos del *maestro* con la orden ```SHOW MASTER STATUS```

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/demonio_mysql_conf_slave.png">
    <p> Configuracion de BD en equipo esclavo</p>
</div>

Por ultimo arrancamos el *esclavo*, para que los demonios de *MySQL* de ambas maquinas repliquen automaticamente los datos que se introduzcan/modifiquen/borren en el servidor maestro:

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/demonio_mysql_inicio_slave.png">
    <p> Inicialización del esclavo</p>
</div>


Para finalizar, volvemos al equipo *maestro* y volvemos a activar las tablas para que puedan meterse nuevos datos en el maestro.

<div align="center">
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica5/img/demonio_mysql_desbloqueo_tablas.png">
    <p> Desbloqueo de tablas equipo <i>maestro</i></p>
</div>

Ahora, podemos hacer pruebas en el maestro y deberían replicarse en el esclavo automáticamente.
