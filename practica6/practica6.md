# Práctica 6


## Configuración del RAID por sofware

Para configurar el RAID primero nos vamos en VirtualBox a la máquina que queramos -->configuración-->almacenamiento -->controlador SATA--> agregar disco duro-->nuevo

Ahora arrancamos la máquina y entramos para instalar el software necesario para
configurar el RAID:
**sudo apt-get install mdadm**

Ahora ya podemos crear el RAID 1, usando el dispositivo /dev/md0, indicando el
número de dispositivos a utilizar (2), así como su ubicación:
**sudo mdadm -C /dev/md0 --level=raid1 --raid-devices=2 /dev/sdb /dev/sdc**
**sudo mkfs /dev/md0**
Ahora ya podemos crear el directorio en el que se montará la unidad del RAID:

**sudo mkdir /dat**
**sudo mount /dev/md0 /dat**
Para comprobar el estado del RAID, ejecutaremos:
**sudo mdadm --detail /dev/md0**
Para finalizar el proceso, conviene configurar el sistema para que monte el dispositivo
RAID creado al arrancar el sistema. Para ello debemos editar el archivo /etc/fstab y
añadir la línea correspondiente para montar automáticamente dicho dispositivo.
Conviene utilizar el identificador único de cada dispositivo de almacenamiento en lugar
de simplemente el nombre del dispositivo (aunque ambas opciones son válidas). Para
obtener los UUID de todos los dispositivos de almacenamiento que tenemos, debemos
ejecutar la orden:
**ls -l /dev/disk/by-uuid/**

Anotaremos el correspondiente al dispositivo RAID que hemos creado. Ahora ya
podemos añadir al final del archivo **/etc/fstab** la línea para que monte automáticamente
el dispositivo RAID.
Finalmente, una vez que esté funcionando el dispositivo RAID, podemos simular un
fallo en uno de los discos:
**sudo mdadm --manage --set-faulty /dev/md0 /dev/sdb**
como se puede ver en la siguiente captura (Failed Devices:1):

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica6/captura_1.png)

También podemos retirar “en caliente” el disco que está marcado como que ha fallado:
**sudo mdadm --manage --remove /dev/md0 /dev/sdb**

(Failed Devices:0):

![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica6/captura_2.png)

Y por último, podemos añadir, también “en caliente”, un nuevo disco que vendría a
reemplazar al disco que hemos retirado:
**sudo mdadm --manage --add /dev/md0 /dev/sdb**
En esta captura se puede apreciar el porcentaje de Rebuild Status
![img](https://github.com/alvarocarmona6/SWAP/blob/master/practica6/captura_3.png)


