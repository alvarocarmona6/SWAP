# Práctica 3 

En esta practica he trabajado con dos balanceadores de carga nginx y haproxy teniendo que configurar cada uno de ellos para su correcto
funcionamiento. Para ello me he creado una maquina virtual nueva con ubuntu server pero sin instalarle LAMP asignandole a esta una nueva IP en mi red (192.168.1.102)
## Nginx

Para instalar el balanceador nginx he usado los siguientes comandos : **sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get
autoremove** y **sudo apt-get install nginx**. Una vez instalado en el archivo */etc/nginx/conf.d/default.conf* he eliminado el contenido que tenía y he añadido el siguiente: 
![img]()
