---
layout:     post
title:      Apache con PHP para pruebas en Archlinux
date:       2017-03-26 20:00:00
author:     SrWur
summary:    Configurando servidor apache con php para pruebas locales en Archlinux.
categories: apache,php,configuración,Archlinux

tags:
 - apache
 - servidor
 - php
 - servidor local
 - Archlinux
---


# Apache con PHP para pruebas en Archlinux

## Instalo Apache y php-apache

> sudo pacman apache php-apache

## Comentar Modulo
> #LoadModule unique_id_module modules/mod_unique_id.so

  en
> /etc/httpd/conf/httpd.conf

 Suele estar ya comentado.

## Modificar directorio
En `/etc/httpd/conf/httpd.conf` modificando en las lineas

~~~
DocumentRoot "/srv/http"
<Directory "/srv/http">
~~~
la ruta `/srv/http` por otra puedo cambiar la carpeta desde la que carga los documentos el servidor.

Es requisito que la carpeta tenga grupo `http` y acceso `Solamente Lectura`.

Si hay más de un *DocumentRoot* y *Directory* solo leera el último.

Yo lo dejo igual porque voy a usar los VirtualHost

> NOTA Creo que cuando se activa los VirtualHost deja de hacer caso al sitio definido en `/etc/httpd/conf/httpd.conf`

## Iniciar Servicio

> sudo systemctl enable httpd.service

o basta con

> sudo systemctl enable httpd

## Comprobar estado del Servicio

> systemctl status httpd

## Archivo de Prueba

Los archivos se guardan en

> /srv/httpd

## Configurar php-apache

Edito el archivo

> /etc/httpd/conf/httpd.conf

busco la linea

> LoadModule mpm_event_module modules/mod_mpm_event.so

la comento `#` si no lo esta y añado justo debajo las lineas
~~~
 LoadModule mpm_prefork_module modules/mod_mpm_prefork.so
 LoadModule php7_module modules/libphp7.so
 AddHandler php7-script php
 Include conf/extra/php7_module.conf
~~~

Reinicio el Servicio

> sudo systemctl restart httpd

## Para que reconozca por defecto index.php

Edito el archivo

> /etc/httpd/httd.conf

busco las lineas
~~~
<IfModule dir_module>
    DirectoryIndex index.html
</IfModule>
~~~

Añado tras `index.html` el `indexphp` o cualquier otro como `index.htm` quedando en

~~~
<IfModule dir_module>
    DirectoryIndex index.html index.php
</IfModule>
~~~

Reinicio el Servicio



# Configurar sitios con Virtual Host Apache

[Ver post Configurar sitios con Virtual Host](./2017-03-27-configurar-sitios-virtual-host.md)

# Páginas de interes

-   `https://wiki.archlinux.org/index.php/Apache_HTTP_Server`
