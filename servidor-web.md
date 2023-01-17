# Enunciado
Crea un servidor web utilizando nginx. Tu servidor web deberá cumplir con los siguientes requisitos:

- Deberá servir contenido estático alojado en el directorio /var/www/
- Crear un fichero index.html que ser sirva desde http://<IP de tu servidor>. Un html sencillo servirá (no es el objetivo de esta práctica ver qué tal programas en HTML).
- Clona el repositorio siguiente https://github.com/pmolrua/Chrono y que tu servidor muestre la página web del repositorio en la siguiente dirección web: http://<IP de tu servidor>/Chrono
En http://<IP de tu servidor>/test.php guarda el fichero test.php que puedes descargarte de esta práctica y configura el servidor para que funcione PHP.
- Descarga el fichero 404.html y configura nginx para que muestre dicho fichero cuando se acceda a una url que no existe (y solo en ese caso, no directamente).
- Crea un certificado autofirmado y configura nginx para usar https.
- Configura nginx para redirigir todo el tráfico http a la versión https, haciendo que toda la navegación en el sitio web sea forzosamente segura.
- Crea un directorio admin, haz que cuando se acceda a él nginx liste su contenido y guarda en él algunas imágenes.
- Protege el acceso al directorio admin por usuario y contraseña utilizando nginx. Incluye, como mínimo, el usuario "ser" con contraseña "1234".

Todos los pasos anteriores vas a poder probarlos sin ningún problema en tu máquina. Los siguientes pasos no podrás probarlos directamente, sino que necesitarás modificar el fichero de hosts para poder hacer que los dominios que se utilizan en las siguientes secciones redirijan a la misma máquina que has utilizado hasta ahora.
- Todo lo que había hasta ahora deberá ser accesible desde https://ser
- Crea un nuevo servidor virtual que responda a peticiones realizadas a https://onoser. Incluye un nuevo index.html, diferente del creado anteriormente. Incluye también el test.php en dicho dominio.
Al finalizar la práctica, deberás tener lo siguiente configurado (este listado es solo un resumen de lo anterior):
1. https://ser/index.html -> Página creada por ti
2. https://ser/Chrono -> Sacado del repositorio de GitHub
3. https://ser/test.php -> Descargado de esta página
4. https://ser/admin/ -> Un directorio con fotos que está protegido por contraseña y lista su contenido automáticamente.
5. https://ser/* -> Una página 404 descargada de aquí también.
6. https://onoser/index.html -> Una pequeña web creada por ti y diferente de la anterior.
7. https://onoser/test.php -> Otra vez el test.php que te has descargado de aquí.

Deberás crear un repositorio de GitHub privado y darme permisos para acceder a él (usuario pablo-molins). Incluye en tu repositorio un fichero README.md con las explicaciones de qué tienes que hacer para cumplir con lo especificado. Incluye, así mismo, los ficheros de configuración de nginx que modifiques, así como una copia de tu carpeta /var/www y todo su contenido. Sube como respuesta a esta tarea la URL de tu repositorio.

# Explicaciones y procedimientos
## Primero de todo asegurar que el sistema está actualizado
<pre><code>sudo apt-get update
sudo apt-get upgrade</code></pre>
## Instalar paquete Nginx y acceder al servidor
<pre><code>sudo apt-get install nginx
192.168.141.13 (ip de linux server donde está instalado nginx) en el navegador del host (Windows)</code></pre>
## Para servir contenido estático en el directorio /var/www/ y añadir index.html hay que modificar el documento default con:
<pre><code>sudo nano /etc/nginx/sites-available/default</code></pre>

## y editar esta línea:
<pre><code>root /var/www/html;</code></pre>

## dejándola así:
<pre><code>root /var/www</code></pre>

## y editar el contenido del claudátor de location:
<pre><code>location / {</code></pre>

## dejándola así:
<pre><code>location / {
    index index.html
    }</code></pre>

## Reiniciar servicio Nginx para aplicar cambios:
<pre><code>sudo systemctl restart nginx.service</code></pre>

## Instalar git con
<pre><code>sudo apt-get install git</code></pre>

## Clonar https://github.com/pmolrua/Chrono con:
<pre><code>cd /home/provaserver
sudo git clone https://github.com/pmolrua/Chrono</code></pre>

## Editar documento default de nuevo y dentro del claudátor de server añadir:
<pre><code>server {
    location /Chrono {
        root /rutadelacarpeta/Chrono
        index index.htm index.php index.html;
    }
}</code></pre>

## Reiniciar servicio Nginx para aplicar cambios:
<pre><code>sudo systemctl restart nginx.service</code></pre>

## Guardar fichero test.php en http://192.168.141.13/test.php y configurar el servidor para funcionar con PHP

<pre><code>scp provaserver@192.168.141.13:/
guardar fichero php en /var/www/
</code></pre>

### Instalar paquetes de PHP
<pre><code>sudo apt-get install php8.1-fpm
sudo apt-get install php8.1-cli</code></pre>

### Volvemos a editar el archivo default y dentro del claudátor de server añadimos:
<pre><code>server {
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;  
        include fastcgi.conf;  
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;  
    }  
}</code></pre

### Reiniciar servicio Nginx para aplicar cambios:
<pre><code>sudo systemctl restart nginx.service</code></pre> 

## Descargar archivo 404.html y moverlo al directorio /var/www
    
### Volvemos a editar el archivo default y dentro del claudátor de server, debajo de la línea server_name añadimos:    
<pre><code>server {
    error page 404 /404.html;
    location = /var/www/404.html {
       root /var/www/404.html;
       internal;
    }
}</code></pre>

## Crear certificado autofirmado y configurar nginx para usar https, instalar openssl y configurarlo, seguir los comandos:
    
<pre><code>sudo apt-get install openssl
cd /etc/ssl
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
</code></pre>

### Volvemos a editar el fichero default y dentro del claudátor de server, al principio de todo añadimos:
<pre><code>server {
    listen 443 ssl;
</code></pre>

### Y justo encima de location / añadimos:
<pre><code>server {
    ssl_certificate /etc/ssl/cert.pem;
    ssl_certificate_key /etc/ssl/key.pem;
</code></pre>

##

<pre><code></code></pre>
<pre><code></code></pre>
<pre><code></code></pre>
<pre><code></code></pre>
<pre><code></code></pre>
<pre><code></code></pre>
<pre><code></code></pre>
