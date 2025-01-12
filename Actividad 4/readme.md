# Actividad 4

### Busca información sobre las siguientes directivas. Indica para que se usan y escribe un ejemplo que hayas encontrado.

#### <IfModule>

- Valor por defecto: No tiene un valor por defecto. Debes configurarlo explícitamente en el archivo de configuración de Apache.
- Lugar donde se encuentra definida: Puedes definir esta directiva dentro del archivo de configuración principal de Apache (httpd.conf o apache2.conf) o dentro de los archivos de configuración de los hosts virtuales (sites-available en sistemas Debian/Ubuntu).

#### LoadModule

Uso: La directiva LoadModule se utiliza para cargar módulos adicionales en el servidor Apache.
Ejemplo: LoadModule rewrite_module modules/mod_rewrite.so 

#### Include

Uso: La directiva Include se utiliza para incluir archivos de configuración adicionales en el archivo de configuración principal de Apache.
Ejemplo: Include /etc/apache2/sites-enabled/*.conf 
	
#### <Directory>

Uso: La directiva <Directory> se utiliza para aplicar configuraciones específicas a un directorio en el sistema de archivos.
Ejemplo:
<Directory /var/www/html> 
Options Indexes 
FollowSymLinks 
AllowOverride 
All Require all granted 
</Directory> 

#### <Files>

- Uso: La directiva <Files> se utiliza para aplicar configuraciones específicas a archivos individuales.
- Ejemplo:
<Files "example.html">
 Header set Cache-Control "max-age=3600" 
</Files> 

#### <Location>

- Uso: La directiva <Location> se utiliza para aplicar configuraciones específicas a una URL o conjunto de URLs.
- Ejemplo:
<Location "/admin"> 
AuthType Basic 
AuthName "Restricted Access" 
AuthUserFile /etc/apache2/.htpasswd 
Require valid-user 
</Location> 
	
<VirtualHost>

- Uso: La directiva <VirtualHost> se utiliza para configurar hosts virtuales en Apache, lo que permite que un servidor web sirva diferentes sitios web en la misma máquina.
- Ejemplo:
<VirtualHost *:80> 
ServerName example.com 
DocumentRoot /var/www/example 
</VirtualHost> 
Este ejemplo configura un host virtual para el dominio example.com, con el directorio raíz del sitio web en /var/www/example.
	
¿Qué son los ficheros .htaccess?

Los archivos .htaccess son archivos de configuración que permiten modificar la configuración del servidor Apache en un directorio específico y sus subdirectorios. Estos archivos proporcionan una forma de realizar ajustes de configuración a nivel de directorio sin necesidad de acceder al archivo de configuración principal del servidor.
Los archivos .htaccess pueden contener una variedad de directivas de configuración, como reglas de reescritura de URL, autenticación de usuarios, control de acceso, configuraciones de seguridad y más. Permiten a los administradores de sitios web personalizar la configuración del servidor Apache para adaptarse a las necesidades específicas de sus sitios web sin afectar la configuración global del servidor.

