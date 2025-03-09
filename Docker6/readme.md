# Docker 6
---
# PRIMERA PRACTICA 
## Despliegue de páginas estáticas con docker

### Despliege de paginas estaticas con docker
Vamos a crear una pagina web asi que lo primera sera crear una carpeta para ello y un index dentro de ello
```
mkdir public_html
cd public_html
echo "<h1>Buenas</h1>" > index.html
```
[](imagenes/Screenshot_1.png)

Lo siguente sera crear la imagen para nuestra pagina que para eso usaremos un Dockerfile
[](imagenes/Screenshot_2.png)

Creamos la imagen donde este el archivo Dockerfile con:
```
docker build -t santricardo/aplicacionweb:v1 .
```
[](imagenes/Screenshot_3.png)


Podemos revisar que ha sido creado con:
```
docker image ls
```
[](imagenes/Screenshot_4.png)

Ahora creamos un contenedor con la imagen con:
```
docker run --name aplweb -d -p 80:80 santricardo/aplicacionweb:v1
```
[](imagenes/Screenshot_10.png)
[](imagenes/Screenshot_6.png)

### Distribucion de imagen
Ahora subiremos nuestra imagen a Docker
Primero iniciaremos sesion y lo publicaremos con:
```
docker login

docker push santricardo/aplicacionweb:v1
```
[](imagenes/Screenshot_12.png)


Podemos comprobar que se subido con:
```
docker search santricardo/aplicacionweb:v1
```
[](imagenes/Screenshot_13.png)

Con eso podemos descargar de vuelta nuestra imagen y modificar nevamente teniendo que eliminar el anterior contenedor
```
echo "<h1>Buenas 2</h1>" > index.html
docker build -t santricardo/aplicacionweb:v2 .

docker rm -f aplweb
docker run --name aplweb2 -d -p 80:80 santricardo/aplicacionweb:v2
```
[](imagenes/Screenshot_14.png)
[](imagenes/Screenshot_15.png)
[](imagenes/Screenshot_16.png)
[](imagenes/Screenshot_17.png)

Con la imagen nuevamente modificada podremos subirlo a Docker Hub como V2
```
docker push santricardo/aplicacionweb:v2
```
[](imagenes/Screenshot_18.png)

#SEGUNDA PRACTICA
##Creación de una nueva imagen a partir de un contenedor

Una forma de personalizar imagenes a partir de un contenedor seria:

1. Arrancar un conteneddor de una imagen origina como debian:
```
docker  run -it --name contenedor debian bash
```
[](imagenes/Screenshot_19.png)

2. Hacer modificaciones como actualizar o instalar paquetes:
```
apt update && apt install apache2 -y
echo "<h1>Curso Docker</h1>" > /var/www/html/index.html
exit
```
[](imagenes/Screenshot_20.png)
[](imagenes/Screenshot_21.png)

3. Con eso podemos crear una imagen personalisada de las modificaciones usando:
```
docker commit contenedor santricardo/aplicacionweb:v1
```
[](imagenes/Screenshot_22.png)
[](imagenes/Screenshot_23.png)


# TERCERA PRACTICA
## Distribución de imágenes

### Distribución a partir de un fichero

Podemos distribuir imagenes tambien como .tar usando:
```
docker save santricardo/aplicacionweb:v1 > myapache2.tar
```

Si me llega un fichero .tar puedo añadir la imagen a mi repositorio local:
```
docker load -i myapache2.tar
```
[](imagenes/Screenshot_24.png)

### Distribución usando Docker Hub

Tambien podemos distribuirlo atravez de Docker Hub:
```
docker login
docker push santricardo/aplicacionweb:v1
```
[](imagenes/Screenshot_25.png)

