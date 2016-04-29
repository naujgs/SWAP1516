#Práctica 5
##Replicación de bases de datos MySQL
***
A la hora de hacer copias de seguridad de nuestras bases de datos (BD) MySQL, una opción muy común suele ser la de usar una réplica maestro-esclavo, de manera que nuestro servidor en producción hace de maestro y otro servidor de backup hace de esclavo.

Podemos hacer copias desde el servidor de backup sin que se vea afectado el rendimiento del sistema en producción y sin interrupciones de servicio.

Los objetivos concretos de esta práctica son:
* Copiar archivos de copia de seguridad mediante ssh.
* Clonar manualmente BD entre máquinas.
* Configurar la estructura maestro-esclavo entre dos máquinas para realizar el clonado automático de la información.
