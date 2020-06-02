---
title: Configuring Apache
parent: Installling and configuring the software
has_children: false
nav_order: 2
---

# Configuring Apache

Verify Apache is installed and running. Enter the following at the command line:

	sudo systemctl start httpd

You should see the apache server active on default port 80: 

`Active: active (running) since Mon 2020-06-01 22:22:43 GMT; 2s ago`

If Apache is not installed, please follow the instructions described in [Prerequisites](prereqs.md)

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
