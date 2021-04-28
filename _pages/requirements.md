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

Whether you are installing a SADMIN client or server, they both need "python3" and the 
"lsb_release" command installed. So the first thing the setup script will do, is to verify that 
they are installed, if there not the setup script will be installed them. If it's not able 
to installed them, you will be notified and the script will terminate. 
{: .text-justify}

Below is a list of all the packages needed. If you want to see what packages will be installed by 
the setup script before running it, you can run the command below. 
```bash
$SADMIN/bin/sadm_requirements.sh   
```

It will verify each package needed and will tell you which one will have to installed. For 
more info on this script [view the man page of sadm-check-requirements.sh](/_pages/man/sadm-check-requirements)"
{: .text-justify}

<br>

<a name="clientreq"></a> 
## SADMIN Client Installation

The SADMIN client will install these packages, if they are not installed.
To verify if all the SADMIN requirements are met, you can run the script 'sadm_requirements.sh'.
It will give you a status of what package are already installed and the one that will be installed.
{: .text-justify}

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
   

<a name="serverreq"></a> 
## SADMIN Server Installation


The SADMIN server must meet all the client requirements (Server is also a client) and the packages below.
To verify if all the SADMIN requirements are met, you can run the script 'sadm_requirements.sh'.
It will give you a status of what package are already installed and the one that will be installed.
The Web Server and the Database will be installed, created and configured for you.
{: .text-justify}

| rpm package	        | repository	| deb package	| repository  |
| :---                  |:---:          | :---          | :---:       | 
| 'httpd httpd-tools'	| Base	        | 'apache2 apache2-utils libapache2-mod-php'|	Base |
| rrdtool	| Base	| rrdtool	| Base |
| arp-scan	| Base	| arp-scan	| Base |
| fping	| Base	| 'fping monitoring-plugins-standard'	| Base |
| 'php php-common php-cli php-mysqlnd php-mbstring'	| Base | 'php php-mysql php-common php-cli'	|Base |
| mariadb-server	| Base	| 'mariadb-server mariadb-client'|	Base |

