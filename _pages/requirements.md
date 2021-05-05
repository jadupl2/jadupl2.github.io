---
title:          SADMIN Required Packages
desc:           List of packages required by SADMIN
version:        2.2
updated:        2021-05-05
os:             Linux, Aix, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           requirements 
categories:     requirements
#
layout:         single
search:         true
author_profile: false
toc:            false
classes:        wide
sidebar:
  title:        "Documentation"
  nav:          sidebar-manpage
---

{% include sadm/sadm_page_info.md %}  

<br>
Below is a list of all the packages needed by the SADMIN client and server. If you want to see what 
packages will be installed by the setup script before running it, you can run the command below. 

```bash
$SADMIN/bin/sadm_requirements.sh   
```

It will verify each package needed and will tell you which one will have to installed. For more 
info on this script [view the man page of sadm-requirements.sh]({% post_url 2019-03-21-sadm-requirements %})
{: .text-justify}

<br>

<a name="clientreq"></a> 
## SADMIN client packages

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
## SADMIN server packages


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

