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

  1.  En mi maquina virtual con el sistema Debian, ejecuto el comando ``apt-get update; apt-get install zenloadbalancer``
  2.  Tras instalarlo, accederemos a su interfaz de gestion con la direccion ``http://<dir_ip_balanceador>:444``. Las credenciales por defecto son ``admin:admin``
  3.  Para la creación y configuración de una ip virtual, hacemos clic en ``Settings > Interfaces > Add virtual network interface``.
  4.  Para la creación y configuración de un *farm* (usando la recién creada ip virtual) lo haremos haciendo clic en:`` Manage > Farms > Add farm``, especificando el *profile* a usar y otras configuraciones.
  5.  *Asignación de real servers*. Dentro de la configuración del *farm* está la opción ``Add real server``, que usaremos para añadir cada real server. En este punto debemos tener los hosts y el servicio a balancear instalados y debidamente configurados en cada backend.
  6.  Para comprobar su funcionamiento lo haremos comprobando que atacando a la ip definida en el *farm* esten sirviendo los distintos real servers.

###Ejercicio 4.5
**Probar las diferentes maneras de redirección HTTP. ¿Cuál es adecuada y cuál no lo es para hacer balanceo de carga global? ¿Por qué?**  

Tenemos varias maneras de hacer redirecciones: puedes usar meta refresh, JavaScript, o incluso redirecciones 302 (temporales). Sin embargo, las únicas que pasan la prueba de los buscadores son las 301.

La diferencia está en que una redirección 301 transmite todo el valor de enlace de la antigua URL a la nueva (se dice que al menos el 90% del valor). Y esto no sería importante sino fuera porque los buscadores calculan la popularidad de una página basándose en enlaces.

Cuando un buscador se encuentra con una redirección 301 reacciona de esta manera:

  + Elimina la antigua página de su índice – De esta forma la página no volverá a aparecer en las páginas de resultados.
  + Incluye la nueva página en su índice – Para en adelante tenerla en cuenta al confeccionar los resultados de búsqueda.
  + Transfiere el valor de la antigua página a la nueva – Y con esto me refiero a la popularidad que dan los enlaces a las páginas, la cual afecta directamente a los rankings.

###Ejercicio 4.5
**Buscar información sobre los bloques de IP para los distintos países o continentes. Implementar en JavaScript o PHP la detección de la zona desde donde se conecta un usuario**

Para este script hára falta tener en tu servidor el archivo ``GeoIPLocation Library``
``scritp
  <?php
  error_reporting(E_ALL & ~E_NOTICE);
  include("geoiploc.php");
    if (empty($_POST['checkip']))
    {
          $ip = $_SERVER["REMOTE_ADDR"];
    }
    else
    {
          $ip = $_POST['checkip'];
    }
  ?>
  Tu dirección IP es: <?php echo($ip); ?> <br>
  Tu País es : <?php echo(getCountryFromIP($ip, " NamE"));?>
   (<?php echo(getCountryFromIP($ip, "code"));?>)
``
