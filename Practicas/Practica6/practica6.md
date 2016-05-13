#Práctica 6
>Practica realizada por *Juan González Serrano*, para la asignatura de Servidores Webs de Altas Prestaciones

***

###1º Configuración del RAID por software

Como se ha indicado, partimos de una máquina virtual ya instalada y configurada a la que, estando apagada, añadiremos dos discos del mismo tipo y capacidad.

Primero nos vamos a la configuracion de la maquina virtual.

<div align="center">
    <img width="500px" src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/add_hardDisk1.png">
    <p> Creación de disco duro</p>
</div>

En la ventana de ajustes que se nos habre, presionamos el boton *+Add...*

<div align="center">
    <img width="500px" src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/add_hardDisk2.png">
    <p> Creación de disco duro</p>
</div>

Se nos abrira un asistente para la creacion de *"hardware"* vitualizado. En la primera ventana elegiremos crear una unidad **Hard Disk**. Del tipo **SCI**. Despues nos preguntara si crear una unidad virtual nueva, usar una existente o usar una unidad fisica, elegiremos la opcion de **Crear una unidad virtual nueva**. Le daremos el **mismo tamaño** que el **disco** virtual de **nuestra maquina**. Por ultimo le damos un nombre, dejaremos el que le da por defecto.

Como tenemos que crear dos discos duros virtuales iguales, repetiremos el mismo proceso eligiendo las mismas opciones.
Tras haber creado los dos discos duros virtuales, el panel de configuración quedaria de la siguiente forma:

<div align="center">
    <img width="500px" src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/add_hardDisk.png">
    <p> Panel configuración con discos duros virtales para el <i>RAID</i></p>
</div>

Ahora arrancamos la maquina virtual.
Le instalamos el software necesario para configurar el *RAID*
```sh
sudo apt-get install mdadm
```

>Si durante el proceso de insalacion pregunta si deseas intalar *Postfix*, elegimos la opcion *Sin configurar*

Ahora buscamos la información de los dos con el comando ```sudo fdisk -l```

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/hardDisk_info.png">
    <p>Informacion de los discos duros que detecta el sistema</p>
</div>

Como vemos, detecta 3 discos. El primero es en el que esta instalado el sistema, por eso nos muestra su tabla de particiones. Y los otros 2 son los que hemos creado, y por eso todavia no tienen tabla de particiones. Estan vacios.

Ahora ya podemos crear el *RAID 1*. Para ello *"crearemos"* un dispositivo nuevo, ```/dev/md0```, que *"contendra"* los dos discos que hemos creado, ```/dev/sdb``` y ```/deb/sdc```

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/raid1_create.png">
    <p>Creamos el <i>RAID1</i></p>
</div>

>En este punto, el dispositivo se habrá creado con el nombre /dev/md0, sin embargo, en cuanto reiniciemos la máquina, Linux lo renombrará y pasará a llamarlo /dev/md127

Una vez creado el dispositivo *RAID*, y como aún no habremos reiniciado la máquina, usaremos */dev/md0* para darle formato.

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/raid1_formato.png">
    <p>Damos formato al <i>RAID1</i></p>
</div>

Por defecto, *mkfs* inicializa un dispositivo de almacenamiento con formato *ext2*. Ahora ya podemos crear el directorio en el que se montará la unidad del *RAID*.

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/raid1_dir.png">
    <p>Creamos el directorio donde montar <i>RAID1</i></p>
</div>

Podemos comprobar que el proceso se ha realizado adecuadamente, y también los parámetros con los que Linux ha conseguido montarlo usando la orden ```sudo mount```

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/raid1_dir_comprob.png">
    <p>Comprobamos el exito al montar <i>RAID1</i></p>
</div>

Para comprobar el estado del RAID, ejecutaremos el comando ```sudo mdadm --detail /dev/md0```

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/raid1_state.png">
    <p>Comprobamos el estado del <i>RAID1</i></p>
</div>

Para finalizar el proceso, conviene configurar el sistema para que monte el dispositivo *RAID* creado al arrancar el sistema. Para ello debemos editar el archivo **/etc/fstab** y añadir la línea correspondiente para montar automáticamente dicho dispositivo. Conviene utilizar el identificador único de cada dispositivo de almacenamiento en lugar
de simplemente el nombre del dispositivo (aunque ambas opciones son válidas).

Para obtener los UUID de todos los dispositivos de almacenamiento que tenemos, debemos ejecutar el comando ```ls -l /dev/disk/by-uuid/```

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/raid1_info_hardDisk.png">
    <p>Información sobre los dispositivos de almacenamiento</p>
</div>

En la imagen vemos la informacion de la unidad donde se encuentra el sistema *(../sda1)*, la unidad de *swaping* *(../sda5)* y la unidad de nuestro *RAID* *(../md0)*

Anotaremos el correspondiente al dispositivo RAID que hemos creado. Ahora ya podemos añadir al final del archivo */etc/fstab* la línea para que monte automáticamente el dispositivo RAID, que será similar a:
```sh
UUID=ccbbbbcc-dddd-eeee-ffff-aaabbbcccddd /dat ext2 defaults 0 0
```

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/raid1_conf_arranq.png">
    <p>Insercion <i>RAID1</i> para montaje de este al arranque del sistema</p>
</div>

Ya esta todo configurado y listo para que funcione nuestro sistema *RAID1*. Ahora lo que haremos sera reiniciar nuestra maquina y realizaremos pruebas de fayos de disco en el *RAID*

>Tras reiniciar nuestra maquina, volvemos a ejecutar el comando ```sudo mount```. Vemos como el sistema le a cambiado el nombre a nuestra unidad *RAID1*
<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/raid1_dir_comprob_post_reBoot.png">
    <p>Comprobamos el exito al montar <i>RAID1</i> tras reinicio sistema</p>
</div>

###2º Pruebas de fayo en discos del sistema *RAID*

Finalmente, una vez que esté funcionando el dispositivo RAID, podemos simular un fallo en uno de los discos:
```sh
sudo mdadm --manage --set-faulty /dev/md0 /dev/sdb
```
<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/said1_fallo_hardDisk.png">
    <p>Simulado fallo disco duro de un <i>RAID</i></p>
</div>

Tras ejecutar el comando, comprobamos el estado del *RAID* y podemos ver como nos indica que la unidad */dev/sdb* esta en *estado de fallo*

También podemos retirar *“en caliente”* el disco que está marcado como que ha fallado:
```sh
sudo mdadm --manage --remove /dev/md0 /dev/sdb
```

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/said1_borrado_hardDisk.png">
    <p>Simulado retirada disco duro de un <i>RAID</i></p>
</div>

Tras ejecutar el comando, comprobamos el estado del *RAID* y podemos ver como la unidad */dev/sdb* no aparece

Y por último, podemos añadir, también *“en caliente”*, un nuevo disco que vendría a reemplazar al disco que hemos retirado:
```sh
sudo mdadm --manage --add /dev/md0 /dev/sdb
```

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/said1_add_hardDisk.png">
    <p>Simulado inserción disco duro de un <i>RAID</i></p>
</div>

Tras ejecutar el comando, comprobamos el estado del *RAID* y podemos ver como la unidad */dev/sdb* vuelve a aparecer.

###3º Configuración del servidor *NFS*

Lo primero que haremos sera instalar el servidor *NFS* ejecutaremos el comando:
```sh
sudo apt-get install nfs-common nfs-kernel-server
```

Antes de arrancar el servicio NFS, es necesario indicar qué carpetas deseamos compartir y si queremos que los usuarios accedan con permisos de solo lectura o de lectura y escritura. También existe la posibilidad de establecer desde qué PCs es posible conectarse. Estas opciones se configuran en el archivo **/etc/exports**.
Si no realizamos la configuracion, antes de iniciar el servicio, no nos dejara

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/nfs_error_preConfig.png">
    <p>Error al tratar de arrancar el servicio antes de configurarlo</p>
</div>

El fichero de configuracion es ``` /etc/exports```. En cada línea del archivo de configuración del servidor NFS */etc/exports*, se puede especificar:

* La carpeta que se quiere compartir
* El modo en que se comparte (solo lectura 'ro' o lectura y escritura 'rw' )
* Desde qué PC o PCs se permite el acceso (nombre o IP del PC o rango de IPs)

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/nfs_config_clean.png">
    <p>Fichero configuracion por defecto</p>
</div>

En nuestro caso, compartiremos el directorio del *RAID1* con la maquina dos. Para ello escribiremos la siguiente linea en el fichero de configuracon.

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/nfs_config_add_machine2.png">
    <p>Configuracion servicio *NFS*</p>
</div>

>Como vemos, le damos permisos de lectura y escritura

Ahora si que podremos iniciar el servicio.

<div align="center">
    <img  src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/nfs_start.png">
    <p>Iniciar servicio *NFS*</p>
</div>
