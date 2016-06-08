#Ejercicios Tema 6

###Ejercicio 6.3

**Buscar información acerca de los tipos de ataques más comunes en servidores web, en qué consisten, y cómo se pueden evitar.**

Los ataques más comunes son:

  * **Ataque por Injection**: es una técnica para modificar una cadena de consulta de base de datos mediante la inyección de código en la consulta. Para evitarlos podemos tomar las siguientes medidas:

    + Escapar los caracteres especiales utilizados en las consultas SQL como puden ser las comillas dobles o las simples
    + Delimitar los valores de las consultas
    + Asignar mínimos privilegios al usuario que conectará con la base de datos
    + Verificar siempre los datos que introduce el usuario

  * **DDoS**: Denegación de Servicio consiste en inundar un sitio con solicitudes externas, por lo que ese sitio no podría estar disponible para los usuarios reales. Para evitar este tipo de ataques podemos utilzar alguna herramienta como DDoS Kona Site Defender que mitiga los ataques DDoS por medio de la absorción del tráfico DDoS dirigido al nivel de aplicación, el desvío de todo el tráfico DDoS dirigido al nivel de red, como inundaciones SYN o inundaciones UDP, y la autenticación del tráfico válido en el extremo de la red.

  * **Fuerza bruta**: este tipo de ataque intenta "romper" todas las combinaciones posibles de nombre de usuario + contraseña en una página web. Un ejemplo reciente de este tipo de ataques a sido el de hackeo de las cuentas de los famosos en ICloud. Para evitar este tipo de ataques es recomendable tener contraseñas seguras, es decir una contraseña que contenga letras mayúsculas y minúsculas, números y símbolos.
