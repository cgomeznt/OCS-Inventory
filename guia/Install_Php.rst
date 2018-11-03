Instalación de PHP5.X y los modulos necesarios
==============================================


Instalar PHP 7.X
+++++++++++++++++++++++

En OracleLinux se puede contigurar su repo para la instalación de PHP. Los repositorios de PHP contienen las últimas compilaciones de versiones estables de PHP de la comunidad, incluida la extensión oci8 para la base de datos Oracle. Se proporcionan sin apoyo.

Available PHP Releases
PHP Version	Oracle Linux Release	Repository Name
7.2	Oracle Linux 7	ol7_developer_php72
7.1	Oracle Linux 7	ol7_developer_php71
7.0	Oracle Linux 7	ol7_developer_php70
7.2	Oracle Linux 6	ol6_developer_php72
7.1	Oracle Linux 6	ol6_developer_php71
7.0	Oracle Linux 6	ol6_developer_php70


Instalación
+++++++++++++++++++


Para instalar PHP desde este repositorio, asegúrese de tener el último archivo de repositorio del servidor Oracle Linux Yum y habilite el repositorio apropiado.

Por ejemplo, para instalar PHP 7.1 en Oracle Linux 7, ejecute estos comandos como usuario root::

	cd /etc/yum.repos.d
	mv public-yum-ol7.repo public-yum-ol7.repo.bak
	wget http://yum.oracle.com/public-yum-ol7.repo
	yum install -y yum-utils
	yum-config-manager --enable ol7_developer_php71

Instalamos los siguientes componentes que son necesarios para OCS Inventory::

	yum install -y php php-common php-zip php-gd php-mbstring php-soap php-mysql php-xml

**IMPORTANTE** podemos la instalación de PHP 7.x, pero no es estable con OCS Inventory 2.5

Instalar PHP 5.X
+++++++++++++++++++++++
Vamos a instalar PHP 5.X con la ayuda de los repos de remi.::

	yum install -y  http://rpms.remirepo.net/enterprise/remi-release-7.rpm

Instalamos yum-utils::

	yum install -y yum-utils

Habilitamos el repositorio del PHP que requerimos instalar::

	yum-config-manager --enable remi-php55   # [Install PHP 5.5]
	yum-config-manager --enable remi-php56   # [Install PHP 5.6]
	yum-config-manager --enable remi-php72   # [Install PHP 7.2]

Instalamos los siguientes componentes que son necesarios para OCS Inventory::

	yum-config-manager --enable remi-php56   # [Install PHP 5.6]
	yum install -y php php-common php-zip php-gd php-mbstring php-soap php-mysql php-xml

Reiniciamos el Apache.::

	systemctl restart httpd

Vamos hacer una prueba para certificar que php esta integrado con apache.::

	vi /var/www/html/testphp.php

	<?php
	// Muestra toda la informacion de PHP
	phpinfo();
	// Muestra la informacion de los modulos
	phpinfo(INFO_MODULES);
	?>

Tips::

	yum whatprovides php-curl

	yum info php-common
