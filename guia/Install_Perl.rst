Instalación de PERL y los modulos necesarios
==============================================

**En oracle linux**:, Es mejor instalar todos los modulos de PERL desde el CPAN

Instalamos dependencias::

	yum -y install lynx make gcc perl-YAML perl-CPAN-DistnameInfo perl-Test-Mock-LWP gcc-c++ cpan perl-Time-HiRes perl-Version-Requirements perl-CPAN

Configuramos Perl respondiendo con Enter cuando nos haga alguna pregunta (dejando los defaults)::

	perl -MCPAN -e shell
	Terminal does not support AddHistory.

	cpan shell -- CPAN exploration and modules installation (v1.9800)
	Enter 'h' for help

Instalamos algunos módulos básicos y actualizamos::

	cpan[1]> install PAR::Dist Archive::Tar

	cpan[2]> install CPAN::Meta

	cpan[3]> reload CPAN

	cpan[4]> install Test::Pod

	cpan[5]> install Test::Pod::Coverage

	cpan[6]> install PAR::Dist Archive::Tar

	cpan[7]> exit

Recomendable tener a mano el sitio de cpan https://metacpan.org/ si vas a desarrollar/implementar soluciones con Perl, en el encontraras todo tipo de módulos para descargar.

Lista los modulos::

	cpan -l 

Eliminar instalar::

	$ perl -MCPAN -e shell

	cpan[1]>install App::pmuninstall
	cpan[2]>quit
	Usage.
	pm-uninstall [options] Module ...

Instalamos los modulos requeridos por OCS Inventory::

	cpan[1]> install XML::Simple
	cpan[1]> install Compress::Zlib
	cpan[1]> install DBI version
	cpan[1]> install DBD::mysql
	cpan[1]> install Apache::DBI
	cpan[1]> install Net::IP
	cpan[1]> install SOAP::Lite
	cpan[1]> install Mojolicious::Lite
	cpan[1]> install Plack::Handler
	cpan[1]> install Archive::Zip
	cpan[1]> install YAML
	cpan[1]> install XML::Entities

Instalar el EPEL para Oracle Linux 7
++++++++++++++++++++++++++++++++++++++++

Download the EPEL repository::

	wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

Install the EPEL repository::

	rpm -Uvh epel-release-7*.rpm

Agregue el siguiente repositorio::

	vi /etc/yum.repos.d/epel.repo

	[ol7_developer_EPEL]
	name=Oracle Linux $releasever Developement Packages ($basearch)
	baseurl=http://yum.oracle.com/repo/OracleLinux/OL7/developer_EPEL/$basearch/
	gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
	gpgcheck=1
	enabled=1

Ahora debe instalar este paquete que es necesario **mod_perl**::

	yum install mod_perl.x86_64


yum whatprovides Compress-Zlib

yum info perl-IO-Compress.noarch
