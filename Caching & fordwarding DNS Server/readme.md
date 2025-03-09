# Caching & fordwarding DNS Server
---
## Instalar BIND9
---
Primero actualizamos los paquetes e instalamos BIND9 despues:
```
sudo nano /etc/bind/named.conf.local
```
![](imagenes/Screenshot_1.png)

```
sudo apt install bind9 -y
```
![](imagenes/Screenshot_2.png)

Vefiricamos que BIND se esta ejecutando:
```
systemctl status bind9
```
![](imagenes/Screenshot_3.png)

---
## Configurar BIND9 como Servidor Caché
---
Empezaremos editaremos el archivo de configuracion y lo editaremos de esta manera:
```
sudo nano /etc/bind/named.conf.options
```
![](imagenes/Screenshot_4.png)

Comprobamos de que no haya habido ningun error de sintaxis y si no aparece nada esta bien
```
sudo named-checkconf
```
![](imagenes/Screenshot_5.png)

Con eso reiniciamos BIND y verificamos de vuelta
```
sudo systemctl restart bind9
systemctl status bind9
```
![](imagenes/Screenshot_6.png)

Ahora probaremos que puede resolver un dominio con google:
```
nslookup google.com 127.0.0.1
```
![](imagenes/Screenshot_7.png)

Y con eso revisamos el log:
```
sudo tail -f /var/log/syslog
```
![](imagenes/Screenshot_8.png)

----
## Configurar BIND9 como Servidor Forwarding
--- 
Volvemos a editar el archivo de configuracion y agregamos esto:
![](imagenes/Screenshot_9.png)

De nuevo comprobamos y reiniciamos:
```
sudo named-checkconf
sudo systemctl restart bind9
```
![](imagenes/Screenshot_10.png)
![](imagenes/Screenshot_11.png)

Y por ultimo hacemos una consulta:
```
nslookup facebook.com 127.0.0.1
```
![](imagenes/Screenshot_12.png)
