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

  ***Windows Server***

  Para agregar un filtro de paquetes, seguiremos los siguientes pasos:

    1.  Abrir *Enrutamiento y acceso remoto*.
    2.  En el árbol de consola, hacemos clic en **General**
          *Enrutamiento y acceso remoto/nombre de servidor/[IPv4 o IPv6]/General*
    3.  En el panel de detalles, hacemos clic con el boton secundadrio en la
        interfaz donde deseamos un filtro y a continuación, hacemos clic en
        **Propiedades**.
    4.  En la ficha **General**, haga clic en **Filtros entrantes** o
        **Filtros salientes**.
    5.  En el cuadro de diálogo **Filtros entrantes** o **Filtros salientes**,
        haga clic en **Nuevo**.
    6.  En el cuadro de diálogo **Agregar filtro IP**, escriba la configuración
        del filtro y, a continuación, haga clic en **Aceptar**.
    7.  En **Acción de filtrado**, seleccione la acción de filtrado apropiada y,
        a continuación, haga clic en **Aceptar**.

  Para obtener más información acerca del filtrado de paquetes, vea http://go.microsoft.com/fwlink/?LinkId=89010 (puede estar en inglés).
