---
title: Installing and configuring PHP
parent: Installing and configuring the software
has_children: false
nav_order: 3
---

# Installing and configuring PHP

> Note: ownCloud 10.4.1 on CentOS 8 requires PHP 7.3. PHP versions later than 7.3 are not supported. Check the [ownCloud Supported Prerequisties](https://doc.ownCloud.com/server/10.2/admin_manual/installation/system_requirements.html) for latest supported PHP version. 

1. Install the EPEL repository.
```shell
	sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
```

2. Next, install yum utils and enable the remi-repository.
```shell
	sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
```

3. After installing yum-utils and Remi packages, search for available PHP modules.
```shell
	sudo dnf module list php
```
The available PHP modules, stream, and installation profiles are listed. 

4. Next, reset PHP to the base version.
```shell
	sudo dnf module reset php
```

5. After resetting the base PHP version, enable the PHP Remi 7.3 module. 
```shell	
	sudo dnf module enable php:remi-7.3
```

6. To complete the PHP installation, install PHP, PHP-FPM (FastCGI Process Manager) and associated PHP modules.
```shell
	sudo dnf install php php-opcache php-gd php-curl php-mysqlnd php-intl php-json php-ldap php-mbstring php-xml php-zip
```

7. Check that php-fpm is running.
```shell
	sudo systemctl status php-fpm
```
You should see a message that the php-fpm.service is active: 
`Active: active (running) since Mon 2020-06-01 22:40:24 GMT; 30s ago`

8. Verify the PHP version.
```shell
	php -v 
```
You should see a message with the PHP version - `PHP 7.3.18`. 

9. Start up php-fpm.
```shell
	sudo systemctl start php-fpm
```

10. Next, set PHP-FPM to start up automatically at system boot time.
```shell
	sudo systemctl enable php-fpm
```

11. Configure SELinux to allow Apache to execute PHP code with PHP-FPM.
```shell	
	setsebool -P httpd_execmem 1
```

12. Restart the Apache web server to allow Apache to start using PHP.
```shell	
	sudo systemctl restart httpd
```