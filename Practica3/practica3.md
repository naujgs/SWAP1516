#Práctica 3
>Practica realizada por *Juan González Serrano*, para la asignatrua de Servidores Webs de Altas Prestaciones

##1º Instalación del servidor web nginx

Para la instalación usaremos *apt-get*. Aunque lo primero sera improtar la clave del repositorio donde se encuentra el software.
```sh
cd /tmp/
wget http://nginx.org/keys/nginx_signing.key
sudo apt-key add /tmp/nginx_signing.key
rm -f /tmp/nginx_signing.key
```
  <p align="center">
  <img src="https://github.com/naujgs/SWAP1516/blob/master/Practica3/img/nginx_import_llave.jpg">
  </p>

Ahora, añadimos el repositorio al fichero *```/etc/apt/source.list```*. Para ello nos logueamos como root(```sudo su```) y ejecutaremos los siguientes comandos:
```sh
echo "deb http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list
echo "deb-src http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list
```
<p align="center">
<img src="https://github.com/naujgs/SWAP1516/blob/master/Practica3/img/nginx_add_repos.jpg">
</p>

Por ultimo procederemos a la instalacion del paquete *nginx*:

```sh
apt-get update
apt-get install nginx
```
## 2º Configurado de *nginx* como balanceador de carga

El proceso de configuracion que se explica es para ```nginx v 1.8.0```

La configuracion de *nginx* no nos vale tal cual está. Ya que corresponde a una funcionalidad de servidor web, asi que tenemos que modificar el fichero de configuracion ```/etc/nginx/conf.d/default.conf```. Deberemos eliminar el contenido del fichero al 100%, para crear la configuracion que necesitamos.
Yo lo que hare sera cambiar el nombre del fichero por *bk_default.conf*. Esto lo hare con el comando ```mv default.conf bk_default.conf```

<p align="center">
<img src="https://github.com/naujgs/SWAP1516/blob/master/Practica3/img/nginx_cambiar_nom_fich_conf.jpg">
</p>

Una vez echo esto, creamos un nuevo fichero que se llamara *default.conf* y que contendra nuestra configuracion para que nginx funcione como balanceador.

Primero definiremos que maquinas forman nuestro cluster web, indicando las IP de todos los servidores finales de nuestra granja web. Esto lo haremos en la seccion *Upstream* .

```sh
upstream apaches {
  server 172.16.91.128;
  server 172.16.91.129;
}
```
A continuación programamos la seccion *"server"*. Donde le indicaremos que use ese grupo definido antes (*upstream*) como las maquinas a las que debe repartir el trafico.

Es importante definir el *"upstream"* al principio del fichero de configuración, fuera de sección *"server"*. También es importante que para que el proxy_pass funcione correctamente, indiquemos que la conexión entre nginx y los servidores finales sea HTTP 1.1 . Así como especificarle que debe eliminar la cabecera *Connection* (hacerla vacía) para evitar que se pase al servidor final la cabecera que indica el usuario. Así pues, el fichero de configuración debe quedar con el contenido siguiente*

```sh
server{
  listen 80;
  server_name balanceador;

  access_log /var/log/nginx/balanceador.access.log;
  error_log /var/log/nginx/balanceador.error.log;
  root /var/www/;

  location /
  {
    proxy_pass http://apaches;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_http_version 1.1;
    proxy_set_header Connection "";
  }
}
```
<p align="center">
<img src="https://github.com/naujgs/SWAP1516/blob/master/Practica3/img/nginx_conf.jpg">
</p>

El metodo de balanceo es *round-robin*, con la misma prioridad para todos los servidores.

Una vez realizada la configuracion, procedemos a reiniciar el servicio para que se apliquen los cambios en la configuracion.

```sh
sudo service nginx restart
```

Si lo hemos echo todo bien en el fichero de configuracion, el servicio se reiniciara sin problema. Si no es asi, revisaremos nuestro fichero, corregiremos el problema y volveremos a intentar reiniciar el servicio *nginx*.

Llegados a este punto, nos iremos a la maquina terminal en la que configuramos el **crontab** y comentaremos la linea que generaba la actualizacion de nuestro directorio web en ambas maquinas. Con la finalidad de que ambas maquinas sirvan paginas web distintas.
Entraremos en el directorio web de cada maquina y modificaremos las webs que sirven, con la intencion de identificarlas. De esta forma confirmaremos que nginx esta balanceando las solicitudes.

Por ultimo, abriremos una terminal en nuestra maquina anfitriona, y escribiremos el comando ```curl http://<ip_balanceador>```. Este comando nos mostrara en el terminal el codigo de la pagina web.

<p align="center">
<img src="https://github.com/naujgs/SWAP1516/blob/master/Practica3/img/nginx_prueba_balanceo.jpg">
</p>


En la imagen superior vemos como el balanceador nos da las webs de ambas maquinas.
