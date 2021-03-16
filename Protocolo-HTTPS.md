Primero de todo debemos asegurarnos de tener activo el modulo SSL. En caso de no tenerlo activo debemos hacer uso del comando a2enmod ssl y lreiniciar el servidor Apache para que se ejecute correctamente.

![](img/1.png)

Lo siguiente que haremos será hacer una copia de la configuración que tenemos por defecto para nuestro Virtual Host y modificarlo como nos apetezca. Para esto, iremos al directorio /etc/apacha2/sites-available/ y usamos el comando cp default-ssl.conf desplieguecrdhttps.conf.

![](img/2.png)

Ahora para que todo funcione correctamente, iremos al fichero que hemos creado y editaremos distintas líneas como Servername, DocumentRoot, SSLEngine, SSLCertificateFile y SSLCertificateKeyFile, de tal forma que quede de la siguiente forma:

![](img/3.png)

Por último, nos queda activar nuestro Virtual Host recién creado, lo cual lo haremos mediante el comando a2ensite desplieguecrdhttps.conf. Como aun no hemos creado los correspondientes archivos .crt y .key, no reiniciaremos el servidor Apache pues comenzará a dar errores a causa de esto.

![](img/4.png)

Como hemos dicho anteriormente, necesitamos nuestros ficheros .crt y .key que crearemos a través del siguiente comando:

![](img/5.png)

Una vez hecho esto podemos reiniciar nuestro servidor Apache sin tener la preocupación de que se muestre un error, pudiendo acceder ahora a nuestro Virtual Host para ver el resultado.

![](img/6.png)

Para lo siguiente que hay que explicar imaginaremos el hipotetico caso de que tenemos otro Virtual Host con el protocolo http, y queremos que todo el tráfico que reciba este sea redirigido al Virtual Host que hemos creado anteriormente. Para hacer debemos añadir la siguiente línea al fichero .conf de este Virtual Host:

![](img/7.png)

Una vez hecho esto, se reinicia nuestro servidor Apache y podemos revisar con normalidad que todo funciona correctamente y que la redirección se realiza.
