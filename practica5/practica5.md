# Práctica 5


## Crear una BD e insertar datos

Para crear una base de datos lo primero que tenemos que hacer es entrar en mysql con **mysql -uroot -p**

y vamos siguiendo el guión con los siguientes comandos:
**mysql> create database contactos;**
**mysql> use contactos;**
**mysql> create table datos(nombre varchar(100),tlf int);**
**mysql> show tables;**

+---------------------+

| Tables_in_contactos |

+---------------------+

| datos |

+---------------------+

1 row in set (0,00 sec)

**mysql> insert into datos(nombre,tlf) values ("pepe",95834987);**


**mysql> select * from datos;**


+---------+-----------+

| nombre | tlf |

+---------+-----------+

| pepe | 95834987 |

+---------+-----------+

3 rows in set (0,00 sec)

## Hacer una consulta
Para hacer una consulta ejecutaremos los siguientes comandos dentro de mysql:

**mysql> use contactos;**

**mysql> select * from datos;**

**mysql> describe datos;**

y nos saldrá lo que aparece en la siguiente captura: 

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica5/captura_1.png)

## Replicar una BD MySQL con mysqldump
MySQL ofrece la una herramienta para clonar las BD que tenemos en nuestra
maquina. Esta herramienta es mysqldump.
Lo primero que tenemos que hacer es entrar en mysql y ejecutar lo siguiente :
**mysql> FLUSH TABLES WITH READ LOCK;**
para evitar que se acceda a la base de datos.
Ahora ya sí podemos hacer el mysqldump para guardar los datos. En el servidor
principal (maquina1) hacemos:
**mysqldump ejemplodb -u root -p > /tmp/ejemplodb.sql**
Como habíamos bloqueado las tablas, debemos desbloquearlas (quitar el “LOCK”):
**mysql> UNLOCK TABLES;**
Ya podemos ir a la máquina esclavo (maquina2, secundaria) para copiar el archivo
.SQL con todos los datos salvados desde la máquina principal (maquina1):
**scp maquina1:/tmp/ejemplodb.sql /tmp/**
Ahora nos vamos a la máquina 2 y ejecutamos lo siguiente:
**mysql> CREATE DATABASE ‘ejemplodb’;** y
**mysql -u root -p ejemplodb < /tmp/ejemplodb.sql**

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_3.png)


Una vez realizado el script lo ejecutamos y con el comando **sudo iptables -L -n -v** comprobamos el estado de cortafuegos como vemos en la siguiente captura: 

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_2.png)



Una vez comprobado el funcionamiento utilizamos crontab para cada vez que la máquina se reinicia active el cortafuegos:

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_4.png)



