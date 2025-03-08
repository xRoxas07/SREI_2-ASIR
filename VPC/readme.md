## 1. Crear una VPC

Una VPC es una red virtual que permite a los usuarios crear y configurar redes privadas seguras dentro de la nube de AWS.

Vamos al menú del `AWS` y buscamos **VPC** y entramos.

En el menú de **VPC**, seleccionamos **Crear VPC**

![](imagenes/Screenshot_1.png)

En la página de `Configuración de la VPC`, configuramos los siguientes parámetros:

  - Nombre de la VPC: `proyecto`
  - Bloque de CIDR IPv4: `10.0.0.0/16`
  - Bloque de CIDR IPv6: `Sin bloque de CIDR IPv6`
  - Tenencia: `Predeterminado`

  - Número de zonas de disponibilidad (AZ): `2`
  - Cantidad de subredes públicas: `2`
  - Cantidada de subredes privadas: `2`
  -  Personalizar las zonas de disponibilidad
  - Primera zona de disponibilidad: `us-east-1a`
  - Segunda zona de disponibilidad: `us-east-1b`
  - Cantidad de subredes públicas: `2`
  - Cantidad de subredes privadas: `2`
  - 
![](imagenes/Screenshot_2.png)
![](imagenes/Screenshot_3.png)

  - Personalizar bloques de CIDR de subredes
    - Bloque de CIDR de la subred pública en us-east-1a: `10.2.0.0/24`
    - Bloque de CIDR de la subred pública en us-east-1b: `10.2.1.0/24`
    - Bloque de CIDR de la subred privada en us-east-1a: `10.2.2.0/24`
    - Bloque de CIDR de la subred privada en us-east-1b: `10.2.3.0/24`

  - Gateways NAT: `Ninguna`
  - Puntos de enlace de la VPC: `Ninguno`
  - Opciones de DNS
    - **Habilitar nombres de host DNS**: `Habilitado`
    - **Habilitar resolución de nombres DNS**: `Habilitado`



![](imagenes/Screenshot_4.png)
![](imagenes/Screenshot_5.png)


---

## 2. Crear una instancia EC2

Vamos al menú de AWS y buscamos `EC2` y entramos.

![](imagenes/Screenshot_6.png)

En el menú de **EC2 > Instancias > Instancia**, pulsamos en el botón **Lanzar instancias**.


En el menú de `Lanzar una instancia`, configuramos los siguientes configuración:
![](imagenes/Screenshot_38.png)
![](imagenes/Screenshot_39.png)
![](imagenes/Screenshot_40.png)
![](imagenes/Screenshot_41.png)
![](imagenes/Screenshot_42.png)

Podemos verificar que la instancia esté en ejecución cuando terminemos

![](imagenes/Screenshot_43.png)

Nos conectaremos a la instancia a traves de la coneccion ECS por la direccion IPV4

![](imagenes/Screenshot_44.png)

![](imagenes/Screenshot_45.png)

![](imagenes/Screenshot_46.png)


---

## 3. Instalación de WordPress en la instancia EC2

Actualizamos los paquetes del sistema

```bash
sudo apt update && sudo apt upgrade -y
```

![](imagenes/Screenshot_47.png)

Luego instalaremos Apache2

```bash
sudo apt install apache2 -y
```
![](imagenes/Screenshot_48.png)

Despues de la instalacion, activamos el servicio Apache2

```bash
sudo systemctl start apache2 && sudo systemctl enable apache2
```
![](imagenes/Screenshot_49.png)

Podremos verificar que todo esta correctamente configurado si vamos al navegador con la dirección IP de la instancia EC2 en el navegador.

![](imagenes/Screenshot_50.png)

Ahora para crear nuestra base, primero añadiremos el repositorio de PHP y lo instalaremos.

```bash
sudo add-apt-repository ppa:ondrej/php -y
```
```bash
sudo apt install php7.4 libapache2-mod-php7.4 php7.4-cli -y
```
![](imagenes/Screenshot_51.png)
![](imagenes/Screenshot_52.png)

Instalamos MySQL

```bash
sudo apt install php7.4-mysql -y
```

![](imagenes/Screenshot_53.png)

Y reiniciamos el servicio Apache2

```bash
sudo systemctl restart apache2
```

Podemos comprobamos que PHP está correctamente instalado con:

```bash
php -v
```

![](imagenes/Screenshot_54.png)

---

## 4. Creación de la base de datos

Volvemos al menú de AWS y buscamos `Aurora and RDS`

![](imagenes/Screenshot_55.png)

En el menú, seleccionaremos `Crear base de datos`
![](imagenes/Screenshot_56.png)


Configuraremos los siguientes parámetros:

![](imagenes/Screenshot_57.png)

![](imagenes/Screenshot_58.png)

![](imagenes/Screenshot_60.png)

![](imagenes/Screenshot_61.png)

![](imagenes/Screenshot_62.png)

![](imagenes/Screenshot_63.png)

Despues de la base de datos de nuestro AWS, entraremos en `Conmfigurar la conexion de EC2`, selecionamos nuestra MySQL y confirmaremos.
![](imagenes/Screenshot_65.png)
![](imagenes/Screenshot_64.png)
![](imagenes/Screenshot_66.png)
![](imagenes/Screenshot_67.png)

Comprabaremos que la funciona usando el comando en nuestra instancia:

```bash
mysql -h puerto_de_enlace -u admin -p
```
![](imagenes/Screenshot_68.png)
![](imagenes/Screenshot_70.png)


# Elastic File System (EFS)

En el menu del AWS entrremos al `EFS` y selecionamos `Crear un sistemas de archivos`

![](imagenes/Screenshot_69.png)

Usaremos nuestro VPC para el EFS
![](imagenes/Screenshot_71.png)
![](imagenes/Screenshot_72.png)

Iremos a la configuracion de nuestro VPC de `Grupos de seguridad`, entremos a un grupo `servidorwp-sg` para configurar las `Reglas de entrada` añadiendo los protocolos de HTTP, NFS Y SSH.
  
![](imagenes/Screenshot_74.png)
![](imagenes/Screenshot_73.png)


Volveremos al EFS y desde la parte inferior selecionaremos las configuracion de `Red` cambiaresmos a nuestras VPC
![](imagenes/Screenshot_75.png)
![](imagenes/Screenshot_76.png)
![](imagenes/Screenshot_77.png)

De nuevo en EFS, le daremos a `Asociar`, en tipom de montaje sera `a traves de IP` usando `us-east-1a`
![](imagenes/Screenshot_78.png)
![](imagenes/Screenshot_79.png)

## Montar EFS en la instancia

Volveremos a nuestra instacia e instalaremos NFS
![](imagenes/Screenshot_80.png)

Creamos un directorio para poder montar nuestro sistemas de datos para usar el comando que nos copiamos antes
![](imagenes/Screenshot_81.png)

## Instalacion del Wordpress

Descargaremos el archivo de instalacion
![](imagenes/Screenshot_82.png)

Descomprimimos el archivo y creamos un cliente MySQL para la base de datos de nuestro WordPress

![](imagenes/Screenshot_83.png)
![](imagenes/Screenshot_84.png)

Entramos en nuestro MySQL usando IP que nos dio el AWS cuando lo creamos
![](imagenes/Screenshot_85.png)

Cremos una nueva base de datos para nuestro Wordpress
![](imagenes/Screenshot_86.png)

Y con eso podremos acceder a nuestra pagina de Wordpress atravez de nuestro navegador y hacer las configuraciones iniciales
![](imagenes/Screenshot_87.png)


