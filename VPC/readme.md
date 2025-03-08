## 1. Crear una VPC

Una VPC es una red virtual que permite a los usuarios crear y configurar redes privadas seguras dentro de la nube de AWS.

Vamos al menú del `AWS` y buscamos **VPC** y entramos.

En el menú de **VPC**, seleccionamos **Crear VPC**

![](Screenshot_1.png)

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
![](Screenshot_2.png)
![](Screenshot_3.png)

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



![](Screenshot_4.png)
![](Screenshot_5.png)


---

## 2. Crear una instancia EC2

Vamos al menú de AWS y buscamos `EC2` y entramos.

![](Screenshot_6.png)

En el menú de **EC2 > Instancias > Instancia**, pulsamos en el botón **Lanzar instancias**.


En el menú de `Lanzar una instancia`, configuramos los siguientes configuración:
![](Screenshot_38.png)
![](Screenshot_39.png)
![](Screenshot_40.png)
![](Screenshot_41.png)
![](Screenshot_42.png)

Podemos verificar que la instancia esté en ejecución cuando terminemos

![](Screenshot_43.png)

Nos conectaremos a la instancia a traves de la coneccion ECS por la direccion IPV4

![](Screenshot_44.png)

![](Screenshot_45.png)

![](Screenshot_46.png)


---

## 3. Instalación de WordPress en la instancia EC2

Actualizamos los paquetes del sistema

```bash
sudo apt update && sudo apt upgrade -y
```

![](Screenshot_47.png)

Luego instalaremos Apache2

```bash
sudo apt install apache2 -y
```
![](Screenshot_48.png)

Despues de la instalacion, activamos el servicio Apache2

```bash
sudo systemctl start apache2 && sudo systemctl enable apache2
```
![](Screenshot_49.png)

Podremos verificar que todo esta correctamente configurado si vamos al navegador con la dirección IP de la instancia EC2 en el navegador.

![](Screenshot_50.png)

Ahora para crear nuestra base, primero añadiremos el repositorio de PHP y lo instalaremos.

```bash
sudo add-apt-repository ppa:ondrej/php -y
```
```bash
sudo apt install php7.4 libapache2-mod-php7.4 php7.4-cli -y
```
![](Screenshot_51.png)
![](Screenshot_52.png)

Instalamos MySQL

```bash
sudo apt install php7.4-mysql -y
```

![](Screenshot_53.png)

Y reiniciamos el servicio Apache2

```bash
sudo systemctl restart apache2
```

![](Screenshot_54.png)

- Comprobamos que PHP está correctamente instalado

```bash
php -v
```

![alt text](Screenshot_31.png)

---

## 4. Creación de la base de datos

- Vamos al menú de AWS y buscamos Aurora and RDS y entramos en el servicio.

![alt text](Screenshot_32.png)

- En el menú, buscaremos Bases de datos y seleccionaremos Crear base de datos

| ![alt text](Screenshot_33.png) | ![alt text](Screenshot_34.png) |
| --- | --- |

- En el menú de Crear base de datos, configuraremos los siguientes parámetros:
  - Método de creación de base de datos: Creación estándar

  ![alt text](Screenshot_35.png)

  - Opciones del motor
    - Tipo de motor: MySQL

    ![alt text](Screenshot_36.png)

    - Dejamos el resto por defecto.

    ![alt text](Screenshot_37.png)

  - Plantillas: Capa gratuita
  
  ![alt text](Screenshot_38.png)

  - Disponibilidad y durabilidad: Implementación de una instancia de base de datos de zona de disponibilidad única

  ![alt text](Screenshot_39.png)

  - Configuración
    - Identificador de instancias de bases de datos: serverwp-db
    - Nombre de usuario maestro: admin
    - Administración de credenciales: Autoadministrado
    - Contraseña maestra
  
  ![alt text](Screenshot_40.png)

  - Configuración de la instancia
  
  ![alt text](Screenshot_42.png)

  - Almacenamiento
  
  ![alt text](Screenshot_41.png)

  - Conectividad
    - Recurso de computación: No se conecte a un recurso informático EC2
    - Nube privada virtual (VPC): proyecto-vpc
    - Acceso público: No

  ![alt text](Screenshot_43.png)

    - Grupo de seguridad de VPC (firewall): Crear nuevo
    - Nuevo nombre del grupo de seguridad de VPC: serverwp-db-sg
  
  ![alt text](Screenshot_44.png)

    - Proxy de RDS

  ![alt text](Screenshot_45.png)

  - Bajamos hasta la pestaña Configuración adicional y configuramos:
    - Nombre de base de datos inicial: serverwpdb
  
  ![alt text](Screenshot_46.png)

  - Crear base de datos
  
  ![alt text](Screenshot_47.png)

  ![alt text](Screenshot_48.png)

- Configuramos la base de datos en nuestra máquina EC2

  - Entramos a la base de datos acciones > Configurar la conexión EC2
  
  ![alt text](Screenshot_49.png)

  - Elegimos nuestra instancia EC2 serverwp y damos en Continuar
  
  ![alt text](Screenshot_50.png)

  - Revisamos la configuración y damos en Configurar
  
  ![alt text](Screenshot_51.png)

![alt text](Screenshot_52.png)

- Actualizamos MySQL

```bash
sudo apt install mysql-client-core-8.0
```

- Comprobamos que funciona usando el siguiente comando en la terminal de nuestra instancia EC2

```bash
mysql -h puerto_de_enlace_BD -u admin -p
```

> Donde puerto_de_enlace_BD es el puerto de enlace de nuestra base de datos y admin es el usuario de la base de datos.
> 
> ![alt text](Screenshot_53.png)

![alt text](Screenshot_54.png)

