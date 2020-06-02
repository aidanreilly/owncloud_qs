---
title: Installing and configuring Apache
parent: Installing and configuring the software
has_children: false
nav_order: 2
---

# Installing and configuring Apache

1. Install Apache. See [Prerequisites](../prereqs.md) for complete installation instructions.

2. Verify Apache is installed correctly. Enter the following at the command line:
```shell
	sudo systemctl start httpd
```
You should see the apache server active on default port 80: 
`Active: active (running) since Mon 2020-06-01 22:22:43 GMT; 2s ago`

3. Enable the Apache server to start up automatically at system boot time.
```shell
	sudo systemctl enable httpd
```

4. Update the host firewall to allow requests to the apache web server.
```shell
	sudo firewall-cmd --permanent --zone=public --add-service=http
	sudo firewall-cmd --permanent --zone=public --add-service=https
	sudo firewall-cmd --reload
```

5. Update Apache to listen on port 8080. Add a new line to httpd.conf below the default `Listen 80` entry.
```shell
	sudo nano /etc/httpd/conf/httpd.conf 
```
```
	# Change this to Listen on specific IP addresses as shown below to 
	# prevent Apache from glomming onto all bound IP addresses.
	#
	#Listen 12.34.56.78:80
	Listen 80
	Listen 8080
```

6. Open a browser and check that Apache is available at http://127.0.0.1:8080. You should see a test page. This means that Apache is running and succesfully configured.