# Configuración HTTPS en servidor Apache - SSL
En caso de no disponer de un dominio para nuestro servidor, podemos optar por la opción de autofirmado para generar un certificado SSL propio sin una CA, ya que pueden ser de pago o algunos requerir una verificación (en caso de dominio).

## Activando el módulo SSL
Lo primero que debemos hacer en nuestro servidor Apache es activar el modulo SSL en caso de no tenerlo activo, hacemos uso del siguiente comando: `a2enmod ssl` y luego reiniciamos el servidor apache para hacer efectivo el cambio: `systemctl restart apache2`.

![](img/1.png)

## Configurando nuestro virtual host
Debemos realizar un serie de configuraciones sobre nuestro virtual host para prepararlo, suponiendo que ya tenemos un directorio root creado y un archivo html de prueba, procedemos a hacer una copia de la configuración por defecto para nuestro VH y modificarlo a gusto.  
Para ello nos ubicamos en el directorio `/etc/apacha2/sites-available/` y hacemos uso del comando `cp default-ssl.conf despliegueivhttps.conf`.

![](img/2.png)

Ahora editamos las siguiente líneas del fichero `despliegueivhttps.conf` creado en el paso anterior:  
- `Servername`: con el nombre de dominio para este VH.
- `DocumentRoot`: con la ubicación del directorio de nuesto VH.
- Asegurarnos que `SSLEngine` este en `on`.
- `SSLCertificateFile` y `SSLCertificateKeyFile`: cambiamos el nombre de los ficheros `.crt` y `.key` por el que vayas a utilizar al crear dichos ficheros en los siguientes pasos.

![](img/3.png)

Solo nos queda activar nuestro VH mediante el comando `a2ensite despliegueivhttps.conf` puesto que todavía no tenemos los archivos `.crt` y `.key` no reiniciaremos el servidor apache para evitar errores, lo haremos con posterioridad.

![](img/4.png)

## Creando los certificados
Para nuestro fichero `.crt` y `.key` hacemos uso del comando: `openssl req -x509 -nodes -days 365 -newkey rsa:4096 -keyout /etc/ssl/private/ssl-despliegueivhttps.key -out /etc/ssl/certs/ssl-despliegueivhttps.crt` con los nombre de archivo que hayamos configurado en el paso anterior.

![](img/6.png)

Ahora solo nos toca reiniciar el servidor apache e intentar acceder a nuestro VH para ver los resultados.

![](img/7.png)

Y si examinamos el certificado de la página podemos ver que aparecen los datos que hemos proporcionado al crear el certificado.

![](img/8.png)

## Redirigiendo a https desde http
Imaginemos que tenemos otro VH con el protocolo http, y queremos que todo el trafico sea redirijido a nuestro VH con https, para hacer esto solo nos bastaría con agregar la siguiente línea al fichero .conf de nuestro VH http: `redirect / https://www.despliegueivhttps.org` y reniciamos el servidor.

![](img/9.png)

Como se ve, se ha hecho la redirección con satisfacción.

![](img/10.png)
