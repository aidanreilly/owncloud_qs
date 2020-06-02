---
title: Installing and configuring MariaDB
parent: Installing and configuring the ownCloud software
has_children: false
nav_order: 3
---

# Installing and configuring MariaDB

1. Install MariaDB. See [Prerequisites](../prereqs.md) for complete installation instructions.

2. Verify that MariaDB is installed correctly.
```shell
	systemctl status mariadb
```
You should see a message that the database is active and running. 
`Active: active (running) since Mon 2020-06-01 22:31:25 GMT; 24s ago`

3. Set MariaDB to start up automatically at system boot time.
```shell
	systemctl enable mariadb
```

4. Lastly, create the database. Log in to the MariaDB database engine.
```shell
	mysql -u root -p
```
Create the database and add an admin user.
```
	MariaDB [(none)]> CREATE DATABASE ownCloud_db;
	MariaDB [(none)]> GRANT ALL ON ownCloud_db.* TO 'owncloud_admin'@'localhost' IDENTIFIED BY 'YourStrongP@ssword';
	MariaDB [(none)]> FLUSH PRIVILEGES;
	MariaDB [(none)]> EXIT;
```