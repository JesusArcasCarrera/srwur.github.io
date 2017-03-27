---
layout:     post
title:      Configurar sitios con Virtual Host
date:       2017-03-26 18:00:00
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


# Configurar sitios con Virtual Host Apache

[Ver post Configurar sitios con Virtual Host](./2017-03-27-configurar-sitios-virtual-host.md)

Edito el archivo `/etc/httpd/conf/httpd.conf` y descomento la linea

> #Include conf/extra/httpd-vhosts.conf

  Creo una carpeta `nue` en raiz y le doy permisos

> sudo chmod 711 /nue

  edito el archivo `/etc/httpd/conf/httpd.conf`
