---
title: Installling and configuring the software
has_children: false
nav_order: 3
---

#Installling and configuring the software

Note: This QuickStart was tested on CentOS 8, package release 147.8.1.el8_1. To install ownCloud on CentOS, you must have root access on the host machine.

##Updating CentOS

Update your CentOS software packages. This will minimime software installation conflicts.  

	sudo dnf update

##Configuring Apache

Verify Apache is installed and start it running. Enter the following at the command line:

	sudo systemctl start httpd

You should see the apache server active on default port 80: 

`Active: active (running) since Mon 2020-06-01 22:22:43 GMT; 2s ago`

If Apache is not installed, please follow the instructions described in [prerequisite](prerequisites.md)

Enable the Apache server to start up automatically at system boot time.

	sudo systemctl enable httpd

Update the host firewall to allow requests to the apache web server.

	sudo firewall-cmd --permanent --zone=public --add-service=http
	sudo firewall-cmd --permanent --zone=public --add-service=https
	sudo firewall-cmd --reload

Update Apache to listen on port 8080. Add a new line to httpd.conf below the default `Listen 80` entry.

	sudo nano /etc/httpd/conf/httpd.conf 

	Listen 80
	Listen 8080

Open a browser and check that Apache is available at http://127.0.0.1:8080. You should see a test page. This means that Apache is running and succesfully configured.  

##Installing and configuring PHP

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

##Configuring MariaDB

Verify that MariaDB is installed.

	systemctl status mariadb

You should see a message that the database is active and running. 

	Active: active (running) since Mon 2020-06-01 22:31:25 GMT; 24s ago

If MariaDB is not installed, please follow the instructions described in [prerequisite](prerequisites.md)

Next, set MariaDB to start up automatically at system boot time.

	systemctl enable mariadb

Log in to the MariaDB database engine.

	mysql -u root -p

Create an ownCloud database, and add an admin user:  

	MariaDB [(none)]> CREATE DATABASE ownCloud_db;
	MariaDB [(none)]> GRANT ALL ON ownCloud_db.* TO 'owncloud_admin'@'localhost' IDENTIFIED BY 'YourStrongP@ssword';
	MariaDB [(none)]> FLUSH PRIVILEGES;
	MariaDB [(none)]> EXIT;

##Installing and configuring ownCloud

Download the latest ownCloud package.

	wget https://download.owncloud.org/community/ownCloud-10.4.1-qa.tar.bz2

Extract the `ownCloud-10.4.1.tar.bz2` tarball file to the /var/www/ directory:

	sudo tar -jxf ownCloud-10.4.1.tar.bz2 -C /var/www/

Configure the Apache webserver to serve the application by creating a new deployment configuration. 

	sudo nano /etc/httpd/conf.d/ownCloud.conf

Append the following to `ownCloud.conf`:

```
Alias /ownCloud "/var/www/ownCloud/"

<Directory /var/www/ownCloud/>
  Options +FollowSymlinks
  AllowOverride All

 <IfModule mod_dav.c>
  Dav off
 </IfModule>

 SetEnv HOME /var/www/ownCloud
 SetEnv HTTP_HOME /var/www/ownCloud

</Directory>
```

Save and exit the file, and restart the webserver.

	sudo systemctl restart httpd

Allow the Apache webserver to write to ownCloud’s directory under SELinux:

	sudo setsebool -P httpd_unified 1

##Configuring the ownCloud IP address

To allow users to access the ownCloud application over the network, you must update the trusted domains list in `config.php` with the host IP address.

On the host machine that onwCloud is installed on, enter the following at the command line:
	
	ip addr show

The host IP address is displayed beside the relevant network interface, for example, 192.168.1.76. Add this server IP address underneath the loopback address in `config.php`:

	sudo nano /var/www/ownCloud/config/config.php

Add the IP address underneath the default loopback address of 127.0.0.1:

```
  'trusted_domains' => 
  array (
    0 => '127.0.0.1',
    1 => '192.168.1.76'
  ),

```

Then, restart Apache: 

	sudo systemctl restart httpd

Finally, visit 127.0.0.1/owncloud in a browser on the host machine where you installed ownCloud. Enter an admin username and password when prompted to do so. 

Note: Configuring ownCloud web addresses and access over the open internet is beyond the scope of this Quickstart guide. To learn more, visit [Changing Your ownCloud URL](https://doc.ownCloud.com/server/admin_manual/installation/changing_the_web_route.html)