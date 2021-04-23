---
title:          setup.sh
layout:         single
date_created:   2021-03-22
date_updated:   2021-03-22 
show_excerpts:  false
entries_layout: list
tags:           tools
categories:     utilities
author_profile: false
toc:            false
classes:        wide
sidebar:
  title:        "Documentation"
  nav:          sidebar-manpage
---

## Before you install

* [SADMIN tools reside in one directory](/assets/doc/pdf/sadmin_directory_structure.pdf) (recommend '/opt/sadmin'), but you can install it in the directory of your choice.
* For **the server installation we recommended at least 2Gb** of free space and **1Gb for the client**.
* The 'SADMIN' environment variable is critical for the SADMIN tools and contain the installation directory name.
* The setup script will make sure that this environment variable is defined and persistent after a reboot.
  * It create a script ([/etc/profile.d/sadmin.sh](https://www.sadmin.ca/img/sadmin_sh.png)) that's executed every time you login.
    * To ease the use of the SADMIN tools, directories '$SADMIN/bin' & $SADMIN/usr/bin are added to the PATH.
  * It also modify the '[/etc/environment](http://wsadmin.maison.ca/img/etc_environment.png)' so it contain SADMIN install directory.
* The installation process MUST be executed by the 'root' user.
* **IMPORTANT : You need to have an internet access on the system you are installing.**  
  * The setup script, may need to download and install some [packages needed by SADMIN](https://www.sadmin.ca/www/requirements.php).
    * On Redhat and CentOS the "EPEL repository" is activated only for the installation time.
    * On other distributions the packages needed are available in the distribution repository.
* Instructions below assume you have chosen to install SADMIN tools in '/opt/sadmin' directory..

<br>

### Running the setup script
* Setup ask several questions regarding your environment and store answers in the SADMIN configuration file ($SADMIN/cfg/sadmin.cfg).  
* Here's the [output running the setup script](https://www.sadmin.ca/doc/pdf/sadm_client_install_centos7.pdf) to install a SADMIN client on a CentOS 7 system.
* This file is used by the web interface, the SADMIN scripts, libraries and the new scripts you will create.  
* This configuration can be modified when ever you need to.  
* The setup script can be run more than once, so don't worry if you made a mistake, just run it again.
* If there are missing packages, the setup program will download and install them for you.
* You will be asked what type of installation you want, a 'SADM server' or a 'SADMIN client'.
* If you are installing a 'SADMIN server', the 'Mariadb' (Database) and the Apache Web Server will be installed and configure for you.  
* When installation is finished you will have a working Web SADMIN environment at 'http://sadmin'.

After the installation is terminated, you need to log out and log back in before using SADMIN Tools or type the command below.  
This will make sure "SADMIN" environment variable is define (The dot and the space are important).  
    `sudo . /etc/profile.d/sadmin.sh` 

<br>

