---
layout: post
title: "Installing Apache mod_auth_openidc OpenID Authentication"
description: ""
category: [Apache, Linux]
tags: []
---
{% include JB/setup %}



> Purpose: I wanted to use OpenID Authentication to restrict access to a few directories on my apache server



## First download the installer from github
```bash
wget https://github.com/pingidentity/mod_auth_openidc/releases/download/v1.8.7/libapache2-mod-auth-openidc_1.8.7-1ubuntu1.trusty.1_amd64.deb
```


### Install the package
```bash
sudo dpkg -i libapache2-mod-auth-openidc_1.8.7-1ubuntu1.trusty.1_amd64.deb
```


### Install Dependencies
```bash
sudo apt-get install -f
```

### Enable the module for apache
```bash
sudo a2enmod auth_openidc
```

### Restart Apache
```bash
service apache2 restart
```