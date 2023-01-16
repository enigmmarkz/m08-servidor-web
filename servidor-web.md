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
  <pre><code>sudo apt-get update<code><pre>
  <pre><code>sudo apt-get upgrade<code><pre>
