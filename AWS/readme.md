# Practica 1 AWS

Antes de comenzar, actualizamos la lista de paquetes disponibles en el sistema.

```
sudo apt update
```

![](/imagenes/Screenshot_1.png)

```
sudo apt upgrade
```

![](/imagenes/Screenshot_2.png)

A continuación, instalamos Apache.

```
sudo apt-get install apache2
```

![](/imagenes/Screenshot_3.png)

# Configuración de MySQL

Procedemos a instalar PHP, MySQL y MariaDB.

```
sudo apt-get install php8.3 libapapche2-mod-php8.3 php8.3-mysql
```

![](/imagenes/Screenshot_4.png)

```
sudo apt-get install libaprutil1-dbd-mysql
```
![](/imagenes/Screenshot_4.5.png)

```
sudo apt-get install mariadb-server mariadb-client -y
```

![](/imagenes/Screenshot_17.png)

Activamos los servicios necesarios.

```
sudo systemctl enable apache2
```

```
sudo systemctl enable mysql
```

![](/imagenes/Screenshot_6.png)

Ingresamos a MySQL.

```
sudo mysql -u root -p
```

Creamos una base de datos.

```
create database defaultsite_db;
```

![](/imagenes/Screenshot_7.png)

Asignamos permisos adecuados al usuario administrador.

```
GRANT SELECT, INSERT, UPDATE, DELETE ON defaultsite_db.* TO 'defaultsite_admin'@'localhost' IDENTIFIED BY 'usuario';
```

```
GRANT SELECT, INSERT, UPDATE, DELETE ON defaultsite_db.* TO 'defaultsite_admin'@'localhost.localdomain' IDENTIFIED BY 'password';
```

```
flush privileges;
```

![](/imagenes/Screenshot_8.png)

Accedemos a la base de datos y creamos la tabla para almacenar credenciales de usuarios.

```
use defaultsite_db;
```
```
create table mysql_auth ( username varchar(191) not null, passwd varchar(191), groups varchar(191), primary key (username) );
```
![](/imagenes/Screenshot_9.png)


Para mayor seguridad, generamos un hash de la contraseña.

```
htpasswd -bns siteuser siteuser
```

![](/imagenes/Screenshot_10.png)

Insertamos los datos en la tabla correspondiente.

```
INSERT INTO `mysql_auth` (`username`, `passwd`, `groups`) VALUES('siteuser', '{SHA}tk7HEH6Wo7SKT6+3FHCgiGnJ6dA=', 'sitegroup');
```

![](/imagenes/Screenshot_11.png)

Habilitamos los módulos necesarios y reseteamos apache.

```
sudo a2enmod dbd
```

```
sudo a2enmod authn_dbd
```

```
sudo a2enmod socache_shmcb
```

```
sudo a2enmod authn_socache
```

![](/imagenes/Screenshot_21.png)
![](/imagenes/Screenshot_13.png)

Creamos el directorio protegido.

```
sudo mkdir /var/www/html/protegido
```

```
sudo chown -R www-data:www-data /var/www/html/protegido
```

![](/imagenes/Screenshot_14.png)

Editamos la configuración de Apache.

```
sudo nano /etc/apache2/sites-available/000-default.conf
```

Añadimos lo siguiente:

```
DBDriver mysql
DBDParams "dbname=defaultsite_db user=defaultsite_admin pass=usuario"

DBDMin 4
DBDKeep 8
DBDMax 20
DBDExptime 300

<Directory "/var/www/html/protecteddir">
AuthType Basic
AuthName "MySQL"
AuthBasicProvider socache dbd
AuthnCacheProvideFor dbd
AuthnCacheContext my-sql
Require valid-user
AuthDBDUserPWQuery "SELECT passwd FROM mysql_auth WHERE username = %s"
</Directory>
```
![](/imagenes/Screenshot_12.png)

Y reiniciamos Apache.

```
sudo systemctl restart apache2
```

![](/imagenes/Screenshot_13.png)

Ahora, al acceder al directorio protegido vía web, se solicitarán credenciales de usuario.

![](/imagenes/Screenshot_16.png)

# Configuración de SSL

Activamos el módulo SSL y reiniciamos nuevamente.

```
sudo a2enmod ssl
```

![](/imagenes/Screenshot_17.png)

Generamos un certificado SSL autofirmado. Durante la configuración, nos aseguramos de ingresar el nombre de dominio o IP en "Common Name".

```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
```

```
Country Name (2 letter code) [XX]:ES
State or Province Name (full name) []:Huelva
Locality Name (eg, city) [Default City]:Huelva
Organization Name (eg, company) [Default Company Ltd]:La Marisma
Organizational Unit Name (eg, section) []:ASIR
Common Name (eg, your name or your server's hostname) []:3.84.60.22
Email Address []:webmaster@example.com
```

![](/imagenes/Screenshot_18.png)

Editamos la configuración de Apache para habilitar SSL y añadimos el siguiente bloque dentro de un VirtualHost en el puerto 443.

```
sudo nano /etc/apache2/sites-available/000-default.conf
```

```
<VirtualHost *:443>
   ServerName 3.84.60.22

   SSLEngine on
   SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
   SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key
</VirtualHost>
```

![](/imagenes/Screenshot_19.png)

Verificamos la configuración y reiniciamos Apache.

```
sudo apache2ctl configtest
```

```
sudo systemctl reload apache2
```

Con esto, el certificado SSL autofirmado queda configurado correctamente y lo confirmamos entrando desde el navegador usando la IP del server entrando con los credenciales.

![](/imagenes/Screenshot_20.png)
