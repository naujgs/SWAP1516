#Ejercicios Tema 3

###Ejercicio 3.1

**Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.**

  + ***Windows***

    Para configurar el enrutamiento del trafico, en un servidor usaremos el comando:

    ```sh
    C:\> route
    ```
    Dicho comando tiene las siguientes opciones:
      - *PRINT*: imprime una ruta.
      - *ADD*: agrega una ruta.
      - *DELETE*: elimina una ruta.
      - *CHANGE*: modifica una ruta existente.

  + ***Linux***
  
    Para configurara el enrutamiento del trafico, en un servidor, usaremos el comando:

    ```sh
    $ route
    ```
    Dicho comando tiene las siguientes opciones:
      - *-n*: Muestra la tabla de enrutamiento en formato numérico .
      - *add*: Añade una nueva ruta a la tabla de enrutamiento.
      - *-e*: Muestra la tabla de enrutamiento en formato hostname.
      - *del*: Elimina una ruta de la tabla de enrutamiento.

###Ejercicio 3.2
**Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.**
