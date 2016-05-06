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
    <img src="https://github.com/naujgs/SWAP1516/blob/master/Practicas/Practica6/img/add_hardDisk2.png">
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
