## Instalación de LAMP en Amazon Lab

En este tutorial, aprenderemos cómo configurar un entorno LAMP en una instancia de Amazon Lab utilizando los comandos proporcionados.


## Instalación de Apache2 y PHP
Paso 1: Actualización de Repositorios

    apt update


Paso 2: Instalación de Apache2

    apt install apache2 -y

Paso 3: Instalación de PHP y Módulos Necesarios


    apt install php libapache2-mod-php php-mysql -y

![Texto alternativo](/img/Captura1.png)

Paso 4: Edición del Sitio Web por Defecto (000-default.conf)

![Texto alternativo](/img/Captura2.png)

Edita el archivo de configuración del sitio web por defecto para añadir la directiva DirectoryIndex indicando la página PHP por defecto.



    nano /etc/apache2/sites-available/000-default.conf



Añade la siguiente línea dentro de la etiqueta <VirtualHost *:80>:

    #ServerName www.example.com
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    DirectoryIndex index.html index.php (Nota: Se debe añadir
    esta línea)
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>


![Texto alternativo](/img/Captura3.png)

Paso 5: Reinicio del Servicio Apache2



    systemctl restart apache2
![Texto alternativo](/img/Captura4.png)

Paso 6: Comprobación del Stack LAMP

Crea una página de prueba PHP en el directorio web por defecto:
![Texto alternativo](/img/Captura5.png)

    echo "<?php phpinfo(); ?>" > /var/www/html/info.php

![Texto alternativo](/img/Captura6.png)

Instalación de MariaDB
Paso 1: Actualización de Repositorios

![Texto alternativo](/img/Captura7.png)

    apt update

Paso 2: Instalación del Servidor de Base de Datos y Cliente



    apt install -y mariadb-server mariadb-client

Paso 3: Acceso a MariaDB desde la Consola del Servidor (como root)
![Texto alternativo](/img/Captura7.png)


    mariadb -u root


Paso 4: Cambio de Contraseña de Root
![Texto alternativo](/img/Captura9.png)


    ALTER USER 'root'@'localhost' IDENTIFIED BY 'nueva_contraseña';
    FLUSH PRIVILEGES;
    exit;

    

Instalación de PhpMyAdmin 
Paso 1: Instalación de PhpMyAdmin y Paquetes PHP Necesarios


    apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl -y

Paso 2: Configuración de PhpMyAdmin

Durante el proceso de instalación, elige "apache2" como servidor web y confirma el uso de "dbconfig-common" para configurar la base de datos.
![Texto alternativo](/img/capturad.png)

Paso 3: Configuración de Contraseña de PhpMyAdmin

Se te solicitará una contraseña para phpMyAdmin durante la instalación.

Paso 4: Acceso a PhpMyAdmin

Accede a phpMyAdmin desde tu navegador utilizando la siguiente URL: http://ip_servidor/phpmyadmin/


![Texto alternativo](/img/Captura11.png)
