Crea un servidor web utilizando nginx. Tu servidor web deberá cumplir con los siguientes requisitos:

**•Deberá servir contenido estático alojado en el directorio /var/www/**

Para eso, he instalado el nginx con sudo apt install nginx, una vez instalado entro de la carpeta /var/www he creado dos carpetas independetienes una para ser y la otra para onoser, con los comandos sudo mkdir ser, sudo mkdir onoser.
**•	Crear un fichero index.html que ser sirva desde http://<IP de tu servidor>. Un html sencillo servirá (no es el objetivo de esta práctica ver qué tal programas en HTML).**

Dentro de la carpeta de ser, he creado un archivo index.html con el comando sudo nano index.html y lo he rellenado con un poco de datos para que se vea en la página, después he puesto la máquina en adaptador puente  y desde Google he abierto el archivo.

**•	Clona el repositorio siguiente https://github.com/pmolrua/Chrono y que tu servidor muestre la página web del repositorio en la siguiente dirección web: http://<IP de tu servidor>/Chrono**
Para hacer esto, descargado el Chrono con gitclone a la carpeta /var/www/html, el comando que utilitzado es sudo giit clone https://github.com/pmolrua/Chrono.git


**•	En http://<IP de tu servidor>/test.php guarda el fichero test.php que puedes descargarte de esta práctica y configura el servidor para que funcione PHP.
**
Los he pasado con el comando scp, scp test.php 192.168.5, después lo he movido a dentro del www con el comando mv, mv testphp /var/www. Para que me funcione correctamente he cambiado la función del php, para ello he editado el archivo default que esta en, cd /etc/ngin/sites-enabled después un nano para modificar el archivo.


**•	Descarga el fichero 404.html y configura nginx para que muestre dicho fichero cuando se acceda a una url que no existe (y solo en ese caso, no directamente).**
He descargado el fichero 404.html  lo he enviado a la carpeta www, y para que funcione en todas las páginas, me ido al archivo default  con cd /etc/nginx/sites-enabled , después sudo nano default y he modificado el archivo añadiéndole 
`error_page 404 /404.html;
location= /404.html {
	root /var/www;
	internal;`
  
•	Crea un certificado autofirmado y configura nginx para usar https.
**
Para empezar, he instalado en el openssl con sudo apt instal openssl, una vez lo tenemos creamos la llave publica y el certificado a través del comando sudo #openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-clave.com.key -out /etc/ssl/certs/certificado.com.pem, una vez creados, vamos a la carpeta default con cd /etc/nginx/sites-enabled , después sudo nano default y le añadimos la key y el certificado el en el archivo.


**•	Configura nginx para redirigir todo el tráfico http a la versión https, haciendo que toda la navegación en el sitio web sea forzosamente segura.
**
Para ello, como sigo en la carpeta sites-enabled, directamente con un nano default ya entro al archivo, lo he modificado añadiendo el return 301


**•	Crea un directorio admin, haz que cuando se acceda a él nginx liste su contenido y guarda en él algunas imágenes.
**
Me ha costado encontrar el código, lo que he hecho es crear una carpeta en www con sudo mkdir prueba1.txt, y varios archivos mas para comprobar. Después he encontrado el código, he ido al archivo default con cd /etc/nginx/sites-enabled , después sudo nano default. Una vez dentro he añadido el location y el autoindex.


**•	Protege el acceso al directorio admin por usuario y contraseña utilizando nginx. Incluye, como mínimo, el usuario "ser" con contraseña "1234".
**
Según he encontrado y me ha funcionado, primero ejecutamos el siguiente comando sudo sh -c “echo -n ‘ser’>> /etc/nginx/.htpasswd” para crear el usuaro ser y  después hacemos este comando sudo passwd  -apr1>> /etc/nginx/.htpasswd” y este para añadirle la contraseña 1234. Para terminar, abrimos el archivo default y añadimos lo siguiente:
`auth_basic “Restricted”;
auth_basic_user_file /etc/nginx/.htpasswd;`
