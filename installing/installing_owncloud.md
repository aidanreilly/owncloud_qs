---
title: Installing and configuring ownCloud
parent: Installing and configuring the software
has_children: false
nav_order: 5
---

# Installing and configuring ownCloud

Download the latest ownCloud package.

```shell
	wget https://download.owncloud.org/community/ownCloud-10.4.1-qa.tar.bz2
```

Extract the `ownCloud-10.4.1.tar.bz2` tarball file to the /var/www/ directory:

```shell
	sudo tar -jxf ownCloud-10.4.1.tar.bz2 -C /var/www/
```

Configure the Apache webserver to serve the application by creating a new deployment configuration. 

```shell
	sudo nano /etc/httpd/conf.d/ownCloud.conf
```

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

```shell
	sudo systemctl restart httpd
```

Allow the Apache webserver to write to ownCloud’s directory under SELinux:

```shell
	sudo setsebool -P httpd_unified 1
```