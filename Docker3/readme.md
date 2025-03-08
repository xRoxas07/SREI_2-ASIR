# Docker 3

## Descargar imágenes
Para descargar las imágenes de Ubuntu, hello-world y nginx, ejecuta:

```bash
docker pull ubuntu
docker pull hello-world
docker pull nginx
```
![](imagenes/Screenshot_1.png)

## Mostrar un listado de todas las imágenes
Para listar todas las imágenes descargadas en el sistema:

```bash
docker images
```
![](imagenes/Screenshot_2.png)

## Ejecutar contenedores hello-world con nombres específicos
Ejecuta tres contenedores de `hello-world`, asignándoles nombres personalizados:

```bash
docker run --name myhello1 hello-world

docker run --name myhello2 hello-world

docker run --name myhello3 hello-world
```
![](imagenes/Screenshot_6.png)
![](imagenes/Screenshot_3.png)
![](imagenes/Screenshot_4.png)
## Mostrar los contenedores en ejecución
Para ver los contenedores inactivos ya hello-world es un image que se para cuando ejecuta su funcion para:

```bash
docker ps -a
```
![](imagenes/Screenshot_5.png)

## Detener contenedores
Para detener los contenedores `myhello1` y `myhello2`:

```bash
docker stop myhello1

docker stop myhello2
```
![](imagenes/Screenshot_7.png)

## Borrar el contenedor “myhello1”

```bash
docker rm myhello1
```

## Mostrar nuevamente los contenedores en ejecución

```bash
docker ps -a
```
![](imagenes/Screenshot_8.png)

## Borrar todos los contenedores
Para eliminar todos los contenedores, incluidos los detenidos:

```bash
docker rm $(docker ps -aq)
```
![](imagenes/Screenshot_9.png)
