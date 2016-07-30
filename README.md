# freebsd-pf-spanish-keynotes

Notas generales
===============

Macros
------
virtualbox_if = vboxnet0


Tablas
------

table <virtualbox> const { 192.168.56.0/24 }

NAT
===

Masquerading
------------

nat on wlan0 from <virtualbox> -> (wlan0)

nat on tun0 from <virtualbox> -> (tun0)

nat on re0 from <virtualbox> -> (re0)


Redirecciones
-------------

rdr on $virtualbox_if proto tcp from <virtualbox> to 192.168.56.1 port 3306 -> 127.0.0.1 \
           port 3306

Filtrado
========

block in all

pass in on $virtualbox_if from <virtualbox>

pass in from self keep state

pass out from self keep state

pass out all keep state

