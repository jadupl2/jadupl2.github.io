---
layout: single
title: SADMIN Requirements
limit: 1
paginate: false
show_excerpts: false
entries_layout: list
author_profile: true
tags:           requirements 
categories:     requirements
toc:            true
---


Requirements
When you run the setup script to install SADMIN Tools, one of the first question you will be asked, is to indicate if you want to do a Client or a Server installation. Depending on your response, the require packages will be different. Below is a list of requirements for each type of installation.

IMPORTANT :
You need to have an internet access on the system you are installing.
Some of the packages needed by SADMIN, may not be present on your system and will need to be downloaded.
On Redhat and CentOS the "EPEL repository" is activated only for the installation time.
On other distributions the packages needed are available in the distribution repository.
{: .notice--warning}


Whether you are installing a SADMIN client or a server, they both need "python3" and the "lsb_release" command installed.
So the first thing the setup script will do, is to verify if they are installed, if there not they will be installed.
If it's not able to installed them, you will be notified and the script will terminate.


<br>

---

<a name="clientreq"></a> 
## SADMIN Client Installation

The SADMIN client will install these packages, if they are not installed.
To verify if all the SADMIN requirements are met, you can run the script 'sadm_check_requirements.sh'.
It will give you a status of what package are already installed and the one that will be installed.

| rpm package	    | repository	| deb package	| repository  |
| :---              |:---:          | :---          | :---:       | 
| redhat-lsb-core   |	Base	    | lsb-release	| Base |
| nmon	            | EPEL	        | nmon	        | Base |
| ethtool	        | Base	        | ethtool	    | Base |
| net-tools	        | Base	        | net-tools	    | Base |
| sudo	            | Base	        | sudo	        | Base |
| lshw	            | Base	        | lshw	        | Base |
| parted	        | Base	        | parted	    | Base |
| mailx	            | Base	        | mailutils	    | Base |
| mutt	            | Base	        | mutt	        | Base |
| gawk	            | Base	        | gawk	        | Base |
| curl	            | Base	        | curl	        | Base |
| bc	            | Base	        | bc	        | Base |
| openssh-clients	| Base	        | openssh-client| Base |
| dmidecode	        | Base	        | dmidecode	    | Base |
| sysstat	        | Base	        | sysstat	    | Base |
| perl	            | Base	        | perl-base	    | Base |
| perl-libwww-perl	| Base	        | libwww-perl	| Base |
| util-linux	    | Base	        | util-linux	| Base |   
   

<br>

---

<a name="serverreq"></a> 
## SADMIN Server Installation

<br>

The SADMIN server must meet all the client requirements (Server is also a client) and the packages below.
To verify if all the SADMIN requirements are met, you can run the script 'sadm_check_requirements.sh'.
It will give you a status of what package are already installed and the one that will be installed.
The Web Server and the Database will be installed, created and configured for you.

| rpm package	        | repository	| deb package	| repository  |
| :---                  |:---:          | :---          | :---:       | 
| 'httpd httpd-tools'	| Base	        | 'apache2 apache2-utils libapache2-mod-php'|	Base |
| rrdtool	| Base	| rrdtool	| Base |
| arp-scan	| Base	| arp-scan	| Base |
| fping	| Base	| 'fping monitoring-plugins-standard'	| Base |
| 'php php-common php-cli php-mysqlnd php-mbstring'	| Base | 'php php-mysql php-common php-cli'	|Base |
| mariadb-server	| Base	| 'mariadb-server mariadb-client'|	Base |

