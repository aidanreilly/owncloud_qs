---
title: Connecting to ownCloud using the desktop client or app
has_children: true
nav_order: 5
---

# Connecting to ownCloud using the desktop client or app

You can access ownCloud on desktop or mobile using the following links: 

|Operating System|Download link|
|---|---|
|Windows|[Desktop Client for Windows](https://download.ownCloud.com/desktop/stable/ownCloud-2.6.1.13407.13049.msi)|
|Mac OSX|[Desktop Client for Mac OSX](https://download.ownCloud.com/desktop/stable/ownCloud-2.6.1.13096.pkg)|
|Linux|[Desktop Client for Linux](https://software.opensuse.org/download.html?project=isv:ownCloud:desktop&package=ownCloud-client)|
|iOS|[Apple Appstore](https://apps.apple.com/app/id1359583808)|
|Android|[Google Play](https://play.google.com/store/apps/details?id=com.ownCloud.android)|

To install the desktop client on CentOS 8 from source, enter the following at the command line as root user:

	cd /etc/yum.repos.d/
	wget https://download.opensuse.org/repositories/isv:ownCloud:desktop/CentOS_8/isv:ownCloud:desktop.repo
	yum install ownCloud-client