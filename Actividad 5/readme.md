# ACTIVIDAD 5
### Crea un directorio llamado "dir1" y otro llamado "dir2"
sudo mkdir /var/www/dir1
sudo mkdir /var/www/dir2
sudo chmod 755 /var/www/dir1
sudo chmod 755 /var/www/dir2
	
### Explica qué diferencia existe entre ambos.:
<Directory /var/www/example1>
Order Deny,Allow
Deny from All
Allow from 192.168.1.100
</Directory>
- Order Deny,Allow: Primero se procesan las directivas Deny y luego las Allow.
- Deny from All: Bloquea todo el tráfico.
- Allow from 192.168.1.100: Luego, permite específicamente el acceso desde esta IP.

<Directory /var/www/example1>
Order Allow,Deny
Deny from All
Allow from 192.168.1.100
</Directory>
- Order Allow,Deny: Se procesan primero las directivas Allow y luego Deny.
- Deny from All: Bloquea todo el tráfico.
- Allow from 192.168.1.100: Este Allow no tiene efecto porque Deny se procesa después y anula el acceso.
		
### Para dir1
#### Permite el acceso de las peticiones provenientes de 10.3.0.100
#### Permite el acceso desde "marisma.intranet"
#### Permite el acceso desde cualquier subdominio de "marisma.intranet"
#### Permite el acceso de las peticiones provenientes de "10.3.0.100" con máscara "255.255.0.0"

<VirtualHost *:80>
    ServerName dir1.local
    DocumentRoot /var/www/dir1

    <Directory /var/www/dir1>
        Order Deny,Allow
        Deny from All
        Allow from 10.3.0.100
        Allow from marisma.intranet
        Allow from .marisma.intranet
        Allow from 10.3.0.0/16
    </Directory>
</VirtualHost>


### Modifica la configuración de forma que el acceso a dir1:
#### Se permita a "marisma.intranet" y no se permita desde 10.3.0.101"


<Directory /ruta/a/dir1>
    Require host marisma.intranet
    Require not ip 10.3.0.101
</Directory>
	
### Modifica la configuración de forma que el acceso a dir2:
#### Se permita a "10.3.0.100/8" y no a "marisma.intranet"

sudo nano /etc/apache2/sites-available/dir2.conf

    <Directory /var/www/dir2>
        Order Deny,Allow
        Deny from All
        Allow from 10.3.0.0/8
        Deny from marisma.intranet
    </Directory>
</VirtualHost>
