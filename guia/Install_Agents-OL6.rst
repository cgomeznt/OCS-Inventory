Para instalar debe hacer esto::

	yum install -y nmap perl perl-Net-IP.noarch perl-Proc-Daemon.noarch perl-XML-Simple.noarch

Estos RPM los debe descargar de forma manual y luego instalar::

	# rpm -ivh libx86-1.1-9.el6.remi.i686.rpm
	advertencia:libx86-1.1-9.el6.remi.i686.rpm: CabeceraV4 DSA/SHA1 Signature, ID de clave 00f97f56: NOKEY
	Preparando...               ########################################### [100%]
	   1:libx86                 ########################################### [100%]

	# rpm -ivh monitor-edid-3.0-2.el6.remi.i686.rpm
	advertencia:monitor-edid-3.0-2.el6.remi.i686.rpm: CabeceraV4 DSA/SHA1 Signature, ID de clave 00f97f56: NOKEY
	Preparando...               ########################################### [100%]
	   1:monitor-edid           ########################################### [100%]

	# rpm -ivh perl-Ocsinventory-Agent-2.1-2.el6.remi.noarch.rpm
	advertencia:perl-Ocsinventory-Agent-2.1-2.el6.remi.noarch.rpm: CabeceraV3 DSA/SHA1 Signature, ID de clave 00f97f56: NOKEY
	Preparando...               ########################################### [100%]
	   1:perl-Ocsinventory-Agent########################################### [100%]

	# rpm -ivh ocsinventory-agent-2.1-2.el6.remi.x86_64.rpm
	advertencia:ocsinventory-agent-2.1-2.el6.remi.x86_64.rpm: CabeceraV3 DSA/SHA1 Signature, ID de clave 00f97f56: NOKEY
	Preparando...               ########################################### [100%]
	   1:ocsinventory-agent     ########################################### [100%]

Configurar el agente OCS::

	# vi /etc/ocsinventory/ocsinventory-agent.cfg
	#
	# OCS Inventory "Unix Unified Agent" Configuration File
	#
	# options used by cron job overides this (see /etc/sysconfig/ocsinventory-agent)
	#

	# Server URL, unconmment if needed
	# server = your.ocsserver.name
	# local = /var/lib/ocsinventory-agent
	basevardir = /var/lib/ocsinventory-agent

	# Administrative TAG (optional, must be filed before first inventory)
	tag = PC

	# How to log, can be File,Stderr,Syslog
	logger = Stderr
	logfile = /var/log/ocsinventory-agent/ocsinventory-agent.log

	server=192.168.0.21

Por ultimo ejecutar el agente y dejar una tarea cron::

	# ocsinventory-agent 





