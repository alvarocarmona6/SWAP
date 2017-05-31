# Práctica 6


## Configuración del RAID por sofware

Para configurar el RAID primero nos vamos en VirtualBox a la máquina que queramos -->configuración-->almacenamiento -->controlador SATA--> agregar disco duro-->nuevo

Ahora arrancamos la máquina y entramos para instalar el software necesario para
configurar el RAID:
**sudo apt-get install mdadm**

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_1.png)

## Configuración del cortafuegos
Lo primero que he realizado es el script de cortafuegos con todas sus reglas en la siguiente captura de pantalla se puede apreciar claramente: 


![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_3.png)


Una vez realizado el script lo ejecutamos y con el comando **sudo iptables -L -n -v** comprobamos el estado de cortafuegos como vemos en la siguiente captura: 

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_2.png)



Una vez comprobado el funcionamiento utilizamos crontab para cada vez que la máquina se reinicia active el cortafuegos:

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_4.png)



