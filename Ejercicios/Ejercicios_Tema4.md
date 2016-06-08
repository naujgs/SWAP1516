#Ejercicios Tema 4

###Ejercicio 4.1

**Busca información sobre cuánto costaría en la actualidad un mainframe. Comparar precio y potencia entre esa máquina y una granja web de unas prestaciones similares**

Buscando he encontrado una noticia de 2011, en la que habla de un *"nuevo mainframe de bajo coste"*. Se trata del mainframe *zEnterprise 114* de IBM y dice que IBM firma un contrato de alquiler, con pagos mensuales, con quien este interesado.
El precio inicial del zEnterprise 114 es de 410 mil dólares e incluye tres años de mantenimiento y SW de virtualización.

Como hemos visto en clase, puede que sea mas barato tener un mainframe frente a una granja web. Pero si el mainframe nos da algún fallo, sufrimos el fallo en toda nuestra *"granja web"*.
Mientras si tenemos una granja web y sufrimos algun fallo en un equipo, el fallo solo existe en el equipo. El resto de la granja sigue funcionando sin problema.


###Ejercicio 4.2

**Busca información sobre precio y características de balanceadores hardware especificos. Compara las prestaciones que ofrecen unos y otros.**

**LM-5400 Server Load Balancer** – Se trata de un balanceador que proporciona un rendimiento con mejoras SSL. El LM-5400 está optimizado para entornos empresariales e infraestructuras de comercio electrónico de alta prestación. El LM-5400 cuenta tambien con las siguientes características:

  * 8 X GbE and 2x10GbE (SFP+) ports
  * Servers Supported: 1,000 Physical / 1,000 Virtual Servers
  * SSL TPS (1K Keys): 9,300
  * SSL TPS (2K Keys): 7,000
  * 10.2 Gbps L4 balancer throughput
  * L4 Concurrent Connections: 25,600,000
  * Precio:$17990

  **LM-2600 Balanceador de carga de servidores** - El LoadMaster 2600 está diseñado para cargas de trabajo en crecimiento con las siguientes características:

  * 4 puertos GbE
  * 1,7 Gbps L4 balanceador rendimiento
  * Solicitudes por segundo (HTTP): 69.000
  * Servidores soportados: 1.000 físico / virtual 500
  * Transacciones SSL por / segundo (TPS): 2.000
  * Precio:$6775.00

###Ejercicio 4.3
**Buscar información sobre los métodos de balanceo que implementan los dispositivos recogidos en el ejercicio 4.2**

Los métodos de balanceo que nos ofrecen los equipos comentados en el ejercicio anterior son:

  + Fuente-IP Hash
  + Capa7 Contenido de conmutación
  + Conmutación por error encadenado (Fijo Ponderación)
  + Adaptativo basado en atentes
  + Conexión menos
  + Conexion menos ponderada
  + Round Robin
  + Ponderada Round Robin

###Ejercicio 4.4
**Instala y configura en una maquina virtual el balanceado ZenLoadBaancer**


Para su instalación y posterior configuración he seguido los siguientes pasos:

  1º  En mi maquina virtual con el sistema Debian, ejecuto el comando ``apt-get update; apt-get install zenloadbalancer``
  2º Tras instalarlo, accederemos a su interfaz de gestion con la direccion ``http://<dir_ip_balanceador>:444``. Las credenciales por defecto son ``admin:admin``
