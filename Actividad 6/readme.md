# Actividad 6

### Escribe las expresiones regulares para los siguientes supuestos:
### Directorios en /www/ cuyo nombre consista en tres dígitos.
^/www/\d{3}$

### Ficheros: *.gif, *.jpeg, *.jpg, *.png
\.(gif|jpe?g|png)$

### Escribe una directiva para redireccionar todos los GIF a ficheros JPEG en otro servidor
RewriteEngine On
RewriteRule ^(.+)\.gif$ http://otro-servidor.com/$1.jpg [R=301,L]

### Ficheros cuyo nombre corresponda con números enteros y decimales
^\d+(\.\d+)?$

### Números de teléfono en el formato Americano: 123-123-1234
^\d{3}-\d{3}-\d{4}$

### Palabras
\b\w+\b

### Códigos hexadecimales de color de 24 o 32 bits
#[a-fA-F0-9]{6}([a-fA-F0-9]{2})?

### Palabras de 4 letras
\b\w{4}\b

### Número entero sin signo
\b-?\d+\b

### Número entero con signo
\b-?\d+(\.\d+)?([eE]-?\d+)?\b

### Números reales
\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b

### Número reales con exponente
^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$

### Email
\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b

### Números del 0 a 255
^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$
