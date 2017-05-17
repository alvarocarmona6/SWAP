# Práctica 4


## Instalar un certificado SSL autofirmado para configurar el acceso por HTTPS

Para generar un certificado ssl lo primero que hecho en la terminal es ejecutar los siguientes comandos: **a2enmod ssl** **service apache2 restart** , **mkdir /etc/apache2/ssl** **openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout
/etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt** , con esto último nos pide una serie de datos que introducimos según lo que viene en el guión.
Posteriormente Editamos el archivo de configuración del sitio default-ssl con: **nano /etc/apache2/sites-available/default-ssl**
Y agregamos estas lineas debajo de donde pone SSLEngine on:
**SSLCertificateFile /etc/apache2/ssl/apache.crt**
**SSLCertificateKeyFile /etc/apache2/ssl/apache.key**
Activamos el sitio default--ssl y reiniciamos apache:
**a2ensite default-ssl**
**service apache2 reload**
Una vez realizado todo esto comprobamos desde otra máquina virtual que a traves de /**curl -k https://ip_maquina/index.html** vemos que funciona(como se ve en la captura siguiente)


![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_1.png)

Una vez configurado he comprobado su comportamiento con curl viendo que cambia de máquina 1 a máquina 2.Con ab (Apache benchmark) medimos su rendimiento   **ab -c 200  -n 100000 IPbalanceador** donde c es la concurrencia y n las peticiones totales:
![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica3/P3nginx.png)

Para poder utilizar haproxy hay que parar nginx con **sudo systemctl stop nginx**

## Haproxy

Instalamos haproxy con el siguiente comando : **sudo apt-get install haproxy** , una vez instalado correctamente cambio el archivo de  configuración */etc/haproxy/haproxy.cfg y lo dejo así: ![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica3/configuracion_haproxy.png)
Después de la configuración lanzamos el servicio con **sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg** y utilizamos el comando curl para ver que funciona correctamente.
Medimos su rendimiento con ab como en nginx (mismos parámetros) ![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica3/P3haproxy.png) 


## Comparación de los balanceadores
Puedo decir que Haproxy es mejor que nginx ya que me ha tardado menos ( 53,923 segundos respecto a los 76,274 segundos del nginx ) con los mismos parámetros es decir he sometido a la misma carga los dos balanceadores.
