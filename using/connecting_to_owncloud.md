---
title: Connecting to ownCloud using the desktop client or app
has_children: false
nav_order: 3
---

# Connecting to ownCloud using the desktop client or app

To access ownCloud, download the appropriate application for your device or operating system: 

|Operating system|Download link|
|---|---|
|Windows|[Desktop client for Windows](https://download.ownCloud.com/desktop/stable/ownCloud-2.6.1.13407.13049.msi)|
|Mac OSX|[Desktop client for Mac OSX](https://download.ownCloud.com/desktop/stable/ownCloud-2.6.1.13096.pkg)|
|Linux|[Desktop client for Linux](https://software.opensuse.org/download.html?project=isv:ownCloud:desktop&package=ownCloud-client)|
|iOS|[Apple App Store](https://apps.apple.com/app/id1359583808)|
|Android|[Google Play](https://play.google.com/store/apps/details?id=com.ownCloud.android)|

**Table 2: ownCloud client applications**

To install the desktop client on CentOS 8 from source, enter the following at the command line as root user:

```shell
	cd /etc/yum.repos.d/
	wget https://download.opensuse.org/repositories/isv:ownCloud:desktop/CentOS_8/isv:ownCloud:desktop.repo
	yum install ownCloud-client
```

## Signing in to ownCloud

1. Launch the application on your device or computer. 
2. Enter the ownCloud server URL as provided by your administrator.
3. Enter your username and password as provided by your administrator.
