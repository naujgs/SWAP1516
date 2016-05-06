#Práctica 6
##Discos en RAID
***
En esta práctica configuraremos dos discos en RAID 1 por software, usando una maquina virtual con Ubuntu server. Esta configuración RAID ofrece una gran seguridad al replicar los datos en los dos discos.

Los objetivos concretos de esta práctica son:
* Configurar dos discos en RAID 1. Los discos se añadirán a un sistema ya instalado y funcionando, de forma que en total tendremos tres discos (el sistema operativo estará ya instalado en /dev/sda y añadiremos dos discos más, que serán el /dev/sdb y el /dev/sdc, para configurar el dispositivo de almacenamiento RAID en estos dos discos nuevos de igual tamaño).
* Hacer pruebas de retirar y añadir un disco “en caliente”, y comprobar que el RAID sigue funcionando correctamente.
