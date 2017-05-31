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
Una vez realizado todo esto comprobamos desde otra máquina virtual que a traves de **curl -k https://ip_maquina/index.html** vemos que funciona(como se ve en la captura siguiente)


![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_1.png)

## Configuración del cortafuegos
Lo primero que he realizado es el script de cortafuegos con todas sus reglas en la siguiente captura de pantalla se puede apreciar claramente: 


![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_3.png)


Una vez realizado el script lo ejecutamos y con el comando **sudo iptables -L -n -v** comprobamos el estado de cortafuegos como vemos en la siguiente captura: 

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_2.png)



Una vez comprobado el funcionamiento utilizamos crontab para cada vez que la máquina se reinicia active el cortafuegos:

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica4/captura_4.png)



