# PRIMERA PRACTICA

## Almacenamiento con Docker Compose

### Definiendo volúmenes Docker con Docker Compose

Además de definir los `services`, en el fichero `docker-compose.yaml` podemos definir los volúmenes que vamos a necesitar en nuestra infraestructura. Además, podremos indicar qué volumen va a utilizar cada contenedor.

![](imagenes/Screenshot_1.png)

Iniciamos el escenario:

```bash
docker compose up -d
```
![](imagenes/Screenshot_2.png)

Si quereremos ver los contenedores activos:

```bash
docker compose ps
```
![](imagenes/Screenshot_3.png)

Y si queremos ver volúmenes creados:

```bash
docker volume ls
```
![](imagenes/Screenshot_4.png)

Podemos comprobar que efectivamente se ha realizado el montaje:
```bash
docker inspect -f '{{json .Mounts}}' contenedor_mariadb
```
![](imagenes/Screenshot_5.png)


Si se necesita reiniciar desde cero necitaremso borrar el volumen:

```bash
docker compose down -v
```
![](imagenes/Screenshot_6.png)


### Utilización de bind mount con Docker Compose

Ejemplo de bind mount en `docker-compose.yaml`:

![](imagenes/Screenshot_7.png)


Después de iniciar el escenario, el directorio `data` se habrá creado y contendrá los datos de MySQL.
![](imagenes/Screenshot_8.png)
![](imagenes/Screenshot_9.png)


---

# SEGUNDA PRACTICA

## Despliegue de Let's Chat

Para desplegar Let's Chat, ejecutar:

```bash
docker compose up -d
```

Si las imágenes no están disponibles localmente, se descargarán automáticamente.

Ver contenedores en ejecución:

```bash
$ docker compose ps
```
![](imagenes/Screenshot_10.png)
![](imagenes/Screenshot_11.png)


Accederemos desde el navegador a la aplicación.
![](imagenes/Screenshot_12.png)


Para detener y eliminar los contenedores al igual que los volumenes:

```bash
$ docker compose down
```:

```bash
$ docker compose down -v
```
![](imagenes/Screenshot_14.png)


---


# TERCERA PRACTICA

## Configuración del `docker-compose.yaml`

Para ejecutar guessbook con Docker Compose, se debe definir el siguiente archivo `docker-compose.yaml` dentro de su propio directorio:

![](imagenes/Screenshot_15.png)


Ejecutar el despliegue:

```bash
$ docker compose up -d
```
![](imagenes/Screenshot_16.png)

Y podremos ver desde el navegador que se habra mantenido algunos datos de otra practiga de guessbook:

![](imagenes/Screenshot_17.png)



Para detener y eliminar la aplicación y i es necesario eliminar los volúmenes:

```bash
$ docker compose down
```
```bash
$ docker compose down -v
```
![](imagenes/Screenshot_18.png)

