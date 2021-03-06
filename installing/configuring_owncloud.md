---
title: Configuring the ownCloud server IP address
parent: Installing and configuring the ownCloud software
has_children: false
nav_order: 6
---

# Configuring the ownCloud server IP address

To allow users to access the ownCloud server application over the network, you must update the trusted domains list in `config.php` with the host IP address.

On the host machine that the ownCloud server is installed on, enter the following at the command line:
```shell	
	ip addr show
```
The host IP address is displayed beside the relevant network interface, for example, 192.168.1.76. Add this server IP address underneath the loopback address in `config.php`:
```shell
	sudo nano /var/www/ownCloud/config/config.php
```
Add the IP address underneath the default loopback address of 127.0.0.1:
```
  'trusted_domains' => 
  array (
    0 => '127.0.0.1',
    1 => '192.168.1.76'
  ),

```
Then, restart Apache: 
```shell
	sudo systemctl restart httpd
```

Configuring the ownCloud server web address for access outside of the local network is beyond the scope of this quickstart guide. To learn more, visit [Changing your ownCloud URL](https://doc.ownCloud.com/server/admin_manual/installation/changing_the_web_route.html).