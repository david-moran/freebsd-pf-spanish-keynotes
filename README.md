# freebsd-pf-spanish-keynotes

Notas generales
===============

Macros
------
Las macros son variables definidas por el usuario que pueden ser utilizadas posteriormente, tiene que ser definidas antes de ser usadas en el fichero pf.conf con el siguiente formato:

```
clave = valor
```

Por ejemplo:

```
virtualbox_if = vboxnet0
rdr on $virtualbox_if proto tcp from <virtualbox> to 192.168.56.1 port 3306 -> 127.0.0.1 \
           port 3306
```
           
Eso define una macro llamada virtualbox_if y se utiliza en una regla de redirección.

Tablas
------
Las tablas son conjuntos de objetos de red, conceptualmente se parecen a los ipset de iptables.
```
table <virtualbox> const { 192.168.56.0/24 }
```

NAT
===

Masquerading
------------
Las siguientes reglas:
```
nat on wlan0 from <virtualbox> -> (wlan0)
nat on tun0 from <virtualbox> -> (tun0)
nat on re0 from <virtualbox> -> (re0)
```

Se podrían traducir a "iptables" de la siguiente forma:
```
iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE
iptables -t nat -A POSTROUTING -o tun0 -j MASQUERADE
iptables -t nat -A POSTROUTING -o re0 -j MASQUERADE
```


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

