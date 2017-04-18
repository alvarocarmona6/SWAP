# Práctica 3 

En esta practica he trabajado con dos balanceadores de carga nginx y haproxy teniendo que configurar cada uno de ellos para su correcto
funcionamiento. Para ello me he creado una maquina virtual nueva con ubuntu server pero sin instalarle LAMP asignandole a esta una nueva IP en mi red (192.168.1.102)
## Nginx

Para instalar el balanceador nginx he usado los siguientes comandos : **sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get
autoremove** y **sudo apt-get install nginx**. Una vez instalado en el archivo */etc/nginx/conf.d/default.conf* he eliminado el contenido que tenía y he añadido el siguiente: 
![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica3/configuracion_nginx.png)

Una vez configurado he comprobado su comportamiento con curl viendo que cambia de máquina 1 a máquina 2.Con ab (Apache benchmark) medimos su rendimiento   **ab -c 200  -n 100000 IPbalanceador** donde c es la concurrencia y n las peticiones totales:
![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica3/P3nginx.png)

Para poder utilizar haproxy hay que parar nginx con **sudo systemctl stop nginx**

## Haproxy

Instalamos haproxy con el siguiente comando : **sudo apt-get install haproxy** , una vez instalado correctamente cambio el archivo de  configuración */etc/haproxy/haproxy.cfg y lo dejo así: ![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica3/configuracion_haproxy.png)
Después de la configuración lanzamos el servicio con **sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg** y utilizamos el comando curl para ver que funciona correctamente.
Medimos su rendimiento con ab como en nginx (mismos parámetros) ![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica3/P3haproxy.png) 


## Comparación de los balanceadores
Puedo decir que Haproxy es mejor que nginx ya que me ha tardado menos ( 53,923 segundos respecto a los 76,274 segundos del nginx ) con los mismos parámetros es decir he sometido a la misma carga los dos balanceadores.
