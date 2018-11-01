Deploying database server
============================

El servidor de inventario de OCS necesita una base de datos para almacenar información del inventario

Agregue el repositorio de MariaDB en /etc/yum.repos.d/::

	vi /etc/yum.repos.d/MariaDB.repo

	[mariadb]
	name = MariaDB
	baseurl = http://yum.mariadb.org/10.1/centos7-amd64
	gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
	gpgcheck=1

Instalar los requisitos del servidor de base de datos
++++++++++++++++++++++++++++++++++++++++++++++++++++++

El servidor de base de datos actualmente solo puede ser MySQL 5.4 o superior.


Nota: 
	en OracleLinux/Redhat/Centos 7, mariadb está disponible en EPEL. necesita instalar este repositorio para instalar el servidor de base de datos.


En OracleLinux/Redhat/Centos 7 puede usar "yum" para instalar mariadb::

	yum install -y mariadb-server

Launch MariaDB
+++++++++++++++

Primer paso que necesitamos para launchr MariaDB. En OracleLinux/Redhat/Centos 7, debe habilitar e iniciar mariadb primero::

	systemctl status mariadb
	systemctl enable mariadb
	systemctl start mariadb

En la instalación de mysql hay un paso que le pide que coloque la contraseña de root para Mysql (no lo olvide). Cuando culmina la instalación corremos el script.::

	mysql_secure_installation


Configure el servidor de la base de datos en un solo servidor
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Esta parte es solo si desea instalar el servidor de la base de datos, el servidor de comunicaciones y la consola de administración en un solo servidor.

Primer paso para crear la base de datos::

	mysql -uroot -p

Creamos la Base de Datos::

	CREATE DATABASE ocsweb;

OCS necesita un usuario para usar la base de datos "ocsweb"::

	CREATE USER 'ocs'@'localhost' IDENTIFIED BY 'ocs';


Este usuario necesita todos los privilegios en la base de datos "ocsweb"::

	GRANT ALL PRIVILEGES ON ocsweb.* TO 'ocs'@'localhost' WITH GRANT OPTION;


No olvides aplicar los parámetros::

	FLUSH PRIVILEGES;


Nota: 
	Este servidor será utilizado por el servidor de administración y el servidor de comunicación para conectarse a la base de datos. Si no desea utilizar los ocs de usuario de MySQL predeterminados con la contraseña ocs, debe actualizar en el archivo
/etc/apache2/conf-avaible/z-ocsinventory-server.conf. No te olvides de habilitar también tu configuración y reiniciar apache. Consulte Asegure su OCS Inventory NG Server para obtener toda la información sobre las modificaciones de los archivos de configuración.



Configurando el servidor de la base de datos para el servidor OCS separado
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


Esta parte es solo si desea instalar el servidor de bases de datos, el servidor de comunicaciones y la consola de administración en un servidor separado

Primer paso para crear la base de datos::

	CREATE DATABASE ocsweb;

Para un servidor separado, debe tener dos usuarios si utiliza un servidor diferente para la base de datos, el servidor de comunicaciones y la consola de administración::

	CREATE USER 'ocs'@'CommunicationServerIP' IDENTIFIED BY 'ocs';
	CREATE USER 'ocs'@'AdministrationConsoleIP' IDENTIFIED BY 'ocs';

Nota: 
	si desea implementar OCS en solo dos servidores, solo necesita crear un usuario con la IP del servidor de comunicaciones/consola de administración si instala un servidor de base de datos y otro servidor para la consola de administración/servidor de comunicaciones.

Entonces el usuario necesita todos los privilegios en la base de datos "ocsweb"::

	GRANT ALL PRIVILEGES ON ocsweb.* TO 'ocs'@'CommunicationServerIP' WITH GRANT OPTION;
	GRANT ALL PRIVILEGES ON ocsweb.* TO 'ocs'@'AdministrationConsoleIP' WITH GRANT OPTION;

No olvides aplicar los parámetros::

	FLUSH PRIVILEGES;


**En su servidor de comunicaciones/servidor de la consola de administración:** debe cambiar el host de la base de datos en el archivo /etc/apache2/conf-avaible/z-ocsinventory-server.conf::

	PerlSetEnv OCS_DB_HOST YourDatabaseServerIP


No olvides activar tu conf con el siguiente comando::

	a2enmod z-ocsinventory-server.conf


Reinicia tu servicio de apache para activar la configuración.::

	systemctl restart apache2


**En su servidor de comunicaciones/servidor de la consola de administración:** debe cambiar el host de la base de datos en el archivo /usr/share/ocsinventory-reports/ocsreports/dbconfig.inc.php::

	$_SESSION["SERVEUR_SQL"]="YourDatabaseServerIP";


Nota: 
	Este servidor será utilizado por el servidor de administración y el servidor de comunicación para conectarse a la base de datos. Si no desea utilizar los ocs de usuario de MySQL predeterminados con la contraseña ocs, debe actualizar en el archivo /etc/apache2/conf-avaible/z-ocsinventory-server.conf. No te olvides de habilitar también tu configuración y reiniciar apache. Consulte Asegure su OCS Inventory NG Server para obtener toda la información sobre las modificaciones de los archivos de configuración.

