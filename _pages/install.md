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
## Before you install

* The [SADMIN tools reside in one directory](/assets/img/directory_structure.png), we recommend using  '/opt/sadmin', but you can install it in the directory of your choice.
* We recommend around 5Gb of free space for the SADMIN server and 200Mb for each client.
* The 'SADMIN' environment variable is critical for the SADMIN tools and contain the installation directory name.
* The setup script will make sure that this environment variable is defined and persistent after a reboot.
  * It create a script "[/etc/profile.d/sadmin.sh](https://sadmin.ca/assets/img/files/etc_profile_d_sadmin_sh.png)" that's executed every time you login.
    * To ease the use of the SADMIN tools, directories '$SADMIN/bin' & $SADMIN/usr/bin are added to the PATH.
  * It also modify the "[/etc/environment](https://sadmin.ca/assets/img/files/etc_environment.png)" so it contain SADMIN install directory.
* The installation process MUST be executed by the 'root' user.
* **IMPORTANT : You need to have an internet access on the system you are installing.**  
  * The setup script, may need to download and install some [packages needed by SADMIN](https://sadmin.ca/_pages/requirements).
    * On Redhat and CentOS the "EPEL repository" is activated only for the installation time.
    * On other distributions the packages needed are available in the distribution repository.
* Instructions below assume you have chosen to install SADMIN tools in '/opt/sadmin' directory..

[Back To The Top](#top_of_page)

## Summary of installation

- Installation must be executed by 'root' user or with 'sudo'.
- Instruction below assume you have chosen to install SADMIN in '/opt/sadmin' directory.
- We recommend using '/opt/sadmin', but you can select the directory of your choice.
- We recommend 5Gb of free space for the SADMIN server and 400Mb for each client.
- Setup process modify the file "[/etc/environment](/assets/img/files/etc_environment.png)" to include 'SADMIN' environment variable.
- The 'SADMIN' environment variable contain the installation directory path.
- The installation process is the same for an SADMIN server or client.
- Directory '$SADMIN/bin' and $SADMIN/usr/bin is added to your PATH (via "[/etc/profile.d/sadmin.sh](/assets/img/files/etc_profile_d_sadmin_sh.png)"). 

## Installation requirements
- You need to have an internet access on the system you are installing.
- Some of the packages needed by SADMIN, may not be present on your system and will need to be downloaded.
  - On Red Hat and CentOS the "EPEL repository" is activated only for the installation time.
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


<br>

---

### Running the setup script
* Setup ask several questions regarding your environment and store answers in the SADMIN configuration file ($SADMIN/cfg/sadmin.cfg).  
* Here's the [output running the setup script](https://sadmin.ca/assets//pdf/setup_centos7.pdf) to install a SADMIN client on a CentOS 7 system.
* This file is used by the web interface, the SADMIN scripts, libraries and the new scripts you will create.  
* This configuration can be modified when ever you need to.  
* The setup script can be run more than once, so don't worry if you made a mistake, just run it again.
* If there are missing packages, the setup program will download and install them for you.
* You will be asked what type of installation you want, a 'SADM server' or a 'SADMIN client'.
* If you are installing a 'SADMIN server', the 'Mariadb' (Database) and the Apache Web Server will be installed and configure for you.  
* When installation is finished you will have a working Web SADMIN environment at 'http://sadmin'.

After running the setup script, you need to log out and log back in before using SADMIN Tools or type the command below.  

    `sudo . /etc/profile.d/sadmin.sh`   
This will make sure "SADMIN" environment variable is define (The dot and the space are important).  

[Back To The Top](#top_of_page)



## Update to the latest release  

### Method 1  
Use the 'git pull' command (Recommended)

To always get the latest version of SADMIN, use the 'git pull' command (recommended).
```bash
    # cd $SADMIN
    # /opt/sadmin# git pull origin master
    From https://github.com/jadupl2/sadmin
    * branch            master     -> FETCH_HEAD
    Updating 1f8e79d..38034ee
    Fast-forward
    bin/sadm_uninstall.sh | 16 +++++++++-------
    1 file changed, 9 insertions(+), 7 deletions(-)
```

### Method 2  
**Use SADMIN updater**  
Update your system using the SADMIN updater (sadm_updater.sh).
We have a dedicated section for the updater in our manual, take a look at it.

### SADMIN Support  
Should you ran into problem while installing or running the SADMIN tools, please run the 
'sadm_support_request.sh', attach the resulting log to an email with a description of your 
problem or question and sent it to [sadmlinux@gmail.com](mailto:sadmlinux@gmail.com). 
We will get back to you as soon as possible.  
