---
title: Installing and configuring ownCloud
parent: Installing and configuring the software
has_children: false
nav_order: 5
---

# Installing and configuring ownCloud

1. Download the latest ownCloud package.
```shell
	wget https://download.owncloud.org/community/ownCloud-10.4.1-qa.tar.bz2
```

2. Extract the `ownCloud-10.4.1.tar.bz2` tarball file to the /var/www/ directory.
```shell
	sudo tar -jxf ownCloud-10.4.1.tar.bz2 -C /var/www/
```

3. Configure the Apache webserver to serve the application by creating a new deployment configuration. 
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

4. Allow the Apache webserver to write to ownCloud’s directory under SELinux.
```shell
	sudo setsebool -P httpd_unified 1
```