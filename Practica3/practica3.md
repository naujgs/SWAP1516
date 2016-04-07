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
