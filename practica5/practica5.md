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

mysql> use contactos;

mysql> select * from datos;
mysql> describe datos;
y nos saldrá lo que aparece en la siguiente captura: 

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica5/captura_1.png)

## Configuración del cortafuegos
Lo primero que he realizado es el script de cortafuegos con todas sus reglas en la siguiente captura de pantalla se puede apreciar claramente: 


![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_3.png)


Una vez realizado el script lo ejecutamos y con el comando **sudo iptables -L -n -v** comprobamos el estado de cortafuegos como vemos en la siguiente captura: 

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_2.png)



Una vez comprobado el funcionamiento utilizamos crontab para cada vez que la máquina se reinicia active el cortafuegos:

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_4.png)



