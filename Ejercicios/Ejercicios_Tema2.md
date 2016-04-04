#Ejercicios Tema 2

###Ejercicio 2.1

**Calcular la disponibilidad del sistema si tenemos dos réplicas de cada elemento (en total 3 elementos en cada subsitema).**

  Para calcular la disponibilidad dando un porcentaje, usamos la formula ``100-(tiempo_caida / periodo_tiempo) * 100``

  De esta forma hemos rellenado los datos de la siguiente tabla:

  Componente   | Availability  
  :------------|:--------------
  Web          |85%            
  Application  |90%            
  Database     |99.9%          
  DNS          |98%            
  Firewall     |85%            
  Switch       |99%            
  Data Center  |99.99%         
  ISP          |95%            

  La disponibilidad sera: ``85% * 90% * ... * 99.99% * 95% = 59.87%``
  Para mejorar la disponibilidad del sistema, lo que haremos sera cada elemento. Por lo que la *Availability* de cada uno de ellos se calculara de la siguiente forma ``AS= AC1+((1-AC1)*AC2)`` Por ejemplo, el calculo de la *disponibilidad web* seria: ``85%+((1-85%)*85%) = 97.75%``

  Asi que tras replicar todos los elementos de nuestro sistema, se nos queda la siguiente tabla:

  Componente   | Availability  
  :------------|:--------------
  Web          |97.75%            
  Application  |90%            
  Database     |99.9%          
  DNS          |98%            
  Firewall     |97.75%            
  Switch       |99%            
  Data Center  |99.99%         
  ISP          |95%

Y la disponibilidad del sistema sera: **79.10%**

Por ultimo, volveremos a replicar cada elemento de nuestro sistema (3 elementos en cada subsistema). Lo que nos dara la siguiente tabla de disponibilidad:

Componente   | Availability  
:------------|:--------------
Web          |99.66%            
Application  |99.9%            
Database     |99.99%          
DNS          |99.99%            
Firewall     |99.66%            
Switch       |99.99%            
Data Center  |99.99%         
ISP          |99.987%

**97.9%** disponibilidad del sistema

###Ejercicio 2.2

**Buscar frameworks y librerias para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad**


<p align="center">
<img src="https://www.fullstackpython.com/img/django-logo-positive.png" alt="" width="300" height="150">
</p>
  * **Django** es un framework de desarrollo web de código abierto, escrito en Python, que respeta el patrón de diseño conocido como modelo *vista–controlador*. Fue desarrollado en origen para gestionar varias páginas orientadas a noticias de la World Company de Lawrence, Kansas, y fue liberada al público bajo una licencia BSD en julio de 2005; el framework fue nombrado en alusión al guitarrista de jazz gitano Django Reinhardt.
  La meta fundamental de Django es facilitar la creación de sitios web complejos. Poniendo énfasis en el re-uso, la conectividad y extensibilidad de componentes, el desarrollo rápido y el principio *No te repitas*. Python es usado en todas las partes del framework, incluso en configuraciones, archivos, y en los modelos de datos.

  Sitio oficial: [djangoproject](https://www.djangoproject.com/)


  <p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/en/thumb/9/9e/JQuery_logo.svg/1280px-JQuery_logo.svg.png" alt="" width="300" height="150">
  </p>
  * **Jquerry**  es software libre y de código abierto. Que posee una doble licencia (la Licencia MIT y la Licencia Pública General de GNU v2), permitiendo su uso en proyectos libres y privados. jQuery, al igual que otras bibliotecas, ofrece una serie de funcionalidades basadas en JavaScript que de otra manera requerirían de mucho más código, es decir, con las funciones propias de esta biblioteca se logran grandes resultados en menos tiempo y espacio.

  Sitio oficial: [jQuery](https://jquery.com/)


###Ejercicio 2.3

**¿Como analizar el nivel de carga de cada uno e los subsitemas en el servidor? Buscar herramientas y aprender a usarlas... ¡o recordar como usarlas!**

  En mi caso encontre la apliacion *Sisoft Sandra*.
  Sisoft Sandra nos permite obtener el rendimiento de varios dispositivos de nuestro ordenador como puede ser el procesador, la memoria o los discos duros, y compararlo con el obtenido por otros equipos.
  Sisoft Sandra también nos muestra información sobre la configuración del software del sistema como puede ser información sobre DirectX, el uso de memoria o el sistema operativo.

  Sitio oficial: [Sisoft Sandra](http://www.sisoftware.co.uk/)

###Ejercicio 2.4

**Buscar ejemplos de balanceadores software y hardware**

####Balanceadores Software:
  + **HAProxy:** software de código abierto que proporciona alta disponibilidad de equilibrador de carga y el servidor proxy de TCP y HTTP basado en aplicaciones que se propaga a las solicitudes a través de múltiples servidores. Está escrito en C y tiene reputación de ser rápido y eficiente (en términos de uso del procesador y la memoria).

  + **nginx:** es un servidor web/proxy inverso, ligero de alto rendimiento y un proxy para protocolos de correo electrónico (IMAP/POP3)

  Es software libre y de código abierto; también existe una versión comercial distribuida bajo el nombre de nginx plus3. Es multiplataforma, por lo que corre en sistemas tipo Unix (GNU/Linux, BSD, Solaris, Mac OS X, etc.) y Windows.

####Balanceadores Hardware:
  + **KEMP Load Balancer:**
    - Layer 4 and Layer 7 Load Balancing and Cookie Persistence
    - SSl offload/SSL Acceleration
    - Application Acceleration: HTTP Caching, Compression & IPS Security
    - WAF ( Web Application Firewall)
    - Global Server Load Balancing
    - Edge Security Pack (Microsoft TMG Replacement)
    - Application Health Checking
    - Adaptative (Server Resource) Load Balacing
    - Content Switching
