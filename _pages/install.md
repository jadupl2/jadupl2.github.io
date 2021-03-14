---
layout: single
title: Installation Guide
limit: 1
paginate: true
show_excerpts: false
entries_layout: list
author_profile: true
tags:           sadm_daily_report script 
categories:     manpage scripts 
toc:            false
classes: wide

---


## Summary of installation

- Installation must be executed by 'root' user or with 'sudo'.
- We recommend using '/opt/sadmin', but you can select the directory of your choice.
- Instruction below assume you have chosen to install SADMIN in '/opt/sadmin' directory.
- Main components of SADMIN tools reside in one directory.
- We recommend 5Gb of free space for the SADMIN server and 400Mb for each client.
- Setup process create/modify the file (/etc/environment) to include 'SADMIN' environment variable.
- The installation process describe below is the same for an SADMIN server or client.
- The 'SADMIN' contain the installation directory path and is critical for all the tools to work.
- Directory '$SADMIN/bin' and $SADMIN/usr/bin is added to your PATH (via /etc/profile.d/sadmin.sh). 

## Installation requirements
- You need to have an internet access on the system you are installing.
- Some of the packages needed by SADMIN, may not be present on your system and will need to be downloaded.
  - On Redhat and CentOS the "EPEL repository" is activated only for the installation time.
  - On other distributions the packages needed are available in the distribution repository.

 
## Installation Method 1
Install using the github repository (Recommended)
```bash
    # cd /opt                                   # Change Dir. to /opt
    # git clone https://github.com/jadupl2/sadmin.git
    # /opt/sadmin/setup/setup.sh                # Run setup script
```

## Installation Method 2 
Install using the downloaded 'tgz' file   
```bash
    # cp sadmin_xx.xx.xx.tgz /opt               # Copy sadmin tgz to /opt
    # mkdir /opt/sadmin                         # Create sadmin directory
    # cd /opt/sadmin                            # Change Dir. to /opt/sadmin
    # tar -xvzf ../sadmin_xx.xx.xx.tgz          # Untar tgz
    # /opt/sadmin/setup/setup.sh                # Run setup script
```

## The Setup script

- The setup script will ask questions regarding your environment.  
- Your answers are store in the SADMIN configuration file ($SADMIN/cfg/sadmin.cfg).  
- The SADMIN configuraion file is used by the web interface and the SADMIN tools.  
- The scripts you will create will also use it, it add flexibility to your SADMIN environment.  
- Don't worry, the configuration can be modified afterward if you need to.  
- The setup script can be run more than once, so don't worry if you made a mistake, just run it again.  
- If there are missing packages, the setup program will install them for you.  
- You will be asked what type of installation you want, a 'SADMIN server' or a 'SADMIN client'.  
- If you are installing a 'SADMIN server':  
    - Setup script will install and configure for you the 'Mariadb' (Database) and an Apache Web Server.  
    - When installation is finished you will have a working Web SADMIN environment.  


