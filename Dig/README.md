### 1. Obtén la dirección IP de los siguientes dominios: www.uhu.es, www.us.es, es.wikipedia.org


```bash
dig +short www.uhu.es
dig +short www.us.es
dig +short es.wikipedia.org
```
![](imagenes/Screenshot_1.png)

| www.uhu.es | 150.214.167.13 |
| www.us.es | 193.147.175.38 |
| es.wikipedia.org | 185.15.58.224 |

### 2. Obtén la dirección y los servidores DNS que corresponden a los siguientes dominios:  net, com, us.es, wikipedia.org.

Para obtener los servidores DNS de dominios:

```bash
dig +short net NS
dig +short com NS
dig +short us.es NS
dig +short wikipedia.org NS
```
![](imagenes/Screenshot_2.png)
![](imagenes/Screenshot_3.png)
![](imagenes/Screenshot_4.png)
![](imagenes/Screenshot_5.png)

### 3. Averigua los registros MX de los siguientes dominios:  uhu.es, us.es, wikipedia.org

```bash
dig +short uhu.es MX
dig +short us.es MX
dig +short wikipedia.org MX
```
![](imagenes/Screenshot_6.png)

### 4. Obten la dirección IPV6 de www.isc.org

```bash
dig +short www.isc.org AAAA
```
![](imagenes/Screenshot_7.png)

### 5. Muestra los servidores de correo de yahoo.com

```bash
dig +short yahoo.com MX
```
![](imagenes/Screenshot_8.png)

### 6. Muestra la información asociada con la dirección 75.126.153.206

```bash
dig -x 75.126.153.206
```
![](imagenes/Screenshot_9.png)

### 7. Muestra la dirección de www.google.es utilizando uno de los servidores DNS de google.com

```bash
dig www.google.es NS
```
![](imagenes/Screenshot_18.png)

```bash
dig @ns1.google.com www.google.es
```
![](imagenes/Screenshot_19.png)

### 8. Muestra información sobre el TTL de drive.google.com. Ejecútalo en varias ocasiones y comprueba cómo cambia el valor

![](imagenes/Screenshot_11.png)

### 9. Muestra los registro type NS de redhat.com

![](imagenes/Screenshot_12.png)

### 10. Muestra todos los registros de redhat

```bash
dig redhat.com ANY +noall +answer
```
![](imagenes/Screenshot_20.png)

Como podemos obtener todos los resultados juntos, preguntamos uno a uno a cada uno de los registros.

```bash
dig redhat.com A +noall +answer
dig redhat.com MX +noall +answer
dig redhat.com NS +noall +answer
etc
```

![](imagenes/Screenshot_21.png)

### 11. Crea un fichero de texto que contenga los dominios

```bash
nano domains.txt

redhat.com
google.com
amazon.com
wikipedia.org
```
![](imagenes/Screenshot_14.png)

### 12. Haz una consulta con dig empleando el fichero anterior

![](imagenes/Screenshot_15.png)
![](imagenes/Screenshot_16.png)
![](imagenes/Screenshot_17.png)
