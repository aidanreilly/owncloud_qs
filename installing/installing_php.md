---
title: Installing and configuring PHP
parent: Installling and configuring the software
has_children: false
nav_order: 3
---

# Installing and configuring PHP

Note: ownCloud 10.4.1 on CentOS 8 requires PHP 7.3. PHP versions later than 7.3 are not supported. Check the [ownCloud Supported Prerequisties](https://doc.ownCloud.com/server/10.2/admin_manual/installation/system_requirements.html) for latest supported PHP version. 

Install the EPEL repository.

	sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

Next, install yum utils and enable the remi-repository:

	sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm

After installing yum-utils and Remi packages, search for available PHP modules:
	
	sudo dnf module list php

The available PHP modules, stream, and installation profiles are listed. Next, reset PHP to the base version:

	sudo dnf module reset php

Following reset, enable the PHP Remi 7.3 module. 
	
	sudo dnf module enable php:remi-7.3

To complete the PHP installation, install PHP, PHP-FPM (FastCGI Process Manager) and associated PHP modules: 

	sudo dnf install php php-opcache php-gd php-curl php-mysqlnd php-intl php-json php-ldap php-mbstring php-xml php-zip

Check that php-fpm is running:

	sudo systemctl status php-fpm

You should see a message that the php-fpm.service is active.  

`Active: active (running) since Mon 2020-06-01 22:40:24 GMT; 30s ago`

Verify the PHP version.

	php -v 

You should see a `PHP 7.3.18` message. 

Start up php-fpm:

	sudo systemctl start php-fpm

Next, set PHP-FPM to start up automatically at system boot time.

	sudo systemctl enable php-fpm

Configure SELinux to allow Apache to execute PHP code with PHP-FPM:
	
	setsebool -P httpd_execmem 1

Restart the Apache web server to allow Apache to start using PHP.
	
	sudo systemctl restart httpd