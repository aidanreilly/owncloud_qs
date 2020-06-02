---
title: Configuring MariaDB
parent: Installling and configuring the software
has_children: false
nav_order: 4
---

# Configuring MariaDB

Verify that MariaDB is installed.

```shell
	systemctl status mariadb
```
You should see a message that the database is active and running. 

	Active: active (running) since Mon 2020-06-01 22:31:25 GMT; 24s ago

If MariaDB is not installed, please follow the instructions described in [prerequisite](prerequisites.md)

Next, set MariaDB to start up automatically at system boot time.

```shell
	systemctl enable mariadb
```

Log in to the MariaDB database engine.

```shell
	mysql -u root -p
```

Create an ownCloud database, and add an admin user:  

```
	MariaDB [(none)]> CREATE DATABASE ownCloud_db;
	MariaDB [(none)]> GRANT ALL ON ownCloud_db.* TO 'owncloud_admin'@'localhost' IDENTIFIED BY 'YourStrongP@ssword';
	MariaDB [(none)]> FLUSH PRIVILEGES;
	MariaDB [(none)]> EXIT;
```