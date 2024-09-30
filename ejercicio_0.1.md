# INTRODUCCION 0.1

#### ¿Quién, dónde y cuándo se crea el primer servidor web?

El primer servidor web fue creado por Tim Berners-Lee en 1989 en el CERN (Organización Europea para la Investigación Nuclear) en Suiza. Este servidor permitió el intercambio de información a través de la web.

#### ¿Qué es pila de protocolos usados por http?

- **TCP** (Protocolo de Control de Transmisión): Proporciona comunicación confiable entre el cliente y el servidor.
- *IP* (Protocolo de Internet): Se encarga del direccionamiento y la entrega de paquetes.
- *TLS/SSL* (para HTTPS): Asegura la comunicación encriptada.
	
#### ¿Componentes de una URL?

Una URL (Localizador Uniforme de Recursos) tiene varios componentes:

- **Protocolo:** (EJ: http://, https://)
- **Nombre de dominio:** (EJ: www.ejemplo.com)
- **Puerto (opcional):** (EJ: :80 para HTTP)
- **Ruta:** (EJ: /ruta/al/recurso)
- **Parámetros de consulta (opcional):** (EJ: ?id=123)
- **Fragmento (opcional):** (EJ: #seccion)

#### ¿Pasos en la recuperación de una página web mediante HTTP?

1. **Resolución de DNS:** Se traduce el nombre de dominio a una dirección IP.
2. **Conexión TCP:** Se establece una conexión TCP con el servidor.
3. **Envio de solicitud HTTP:** El cliente envía una solicitud HTTP al servidor.
4. **Procesamiento en el servidor:** El servidor procesa la solicitud y envía una respuesta.
5. **Recepción de la respuesta:** El cliente recibe la respuesta y renderiza el contenido.
	
#### Diferencia entre páginas dinámicas y estáticas

- Páginas estáticas: Tienen contenido fijo, el mismo HTML se envía a todos los usuarios y cargan más rápido.
- Páginas dinámicas: Tienen contenido generado en tiempo real, puede cambiar según la interacción del usuario o el contexto y usan lenguajes de programación del lado del servidor (PHP, Python)
	
#### ¿Cómo usar telnet para acceder a un servidor web?
1. Cómo usar Telnet para acceder a un servidor web
Abrir la terminal:

En Windows, busca "Símbolo del sistema" o "CMD".
En macOS o Linux, abre la aplicación "Terminal".
Conectarse al servidor:

Comando:
telnet [nombre_del_dominio] 80

Enviar una solicitud HTTP:
- Una vez conectado, puedes escribir una solicitud HTTP. Por ejemplo, para obtener la página de inicio, escribe:

GET / HTTP/1.1
Host: www.ejemplo.com

#### Request. Métodos principales
- **GET:** Solicita datos de un recurso.
- **POST:** Envía datos al servidor (generalmente para crear o actualizar recursos).
- **PUT:** Actualiza un recurso existente.
- **DELETE:** Elimina un recurso.

#### Response. Códigos

- **200 OK:** Solicitud exitosa.
- **404 Not Found:** Recurso no encontrado.
- **500 Internal Server Error:** Error en el servidor.
- **301 Moved Permanently:** Recurso movido a otra URL.

#### Content type. Tipos principales
- **text/html:** Documento HTML.
- **application/json:** Datos en formato JSON.
- **image/jpeg:** Imagen JPEG.
- **application/xml:** Documento XML.
