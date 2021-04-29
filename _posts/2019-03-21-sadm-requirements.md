---
title:          sadm_requirements.sh
desc:           List/Install required SADMIN Tools packages
version:        1.9
date:           2019-03-21
updated:        2021-04-22
os:             Linux, Aix, MacOS
tags:           [ utilities ] 
categories:     [ utilities ] 
#
layout:         single
search:         true
author_profile: false
toc:            false
classes:        wide
sidebar:
  title: "Documentation"
  nav: sidebar-manpage
---


<font size="3">
<div>$SADMIN/bin/{{ page.title }}</div>
<div>Version v{{ page.version }} - Updated {{ page.updated }}</div>
<div>Run on {{ page.os }}</div>
</font>


<a id="name"></a>

## NAME
**{{ page.title }}** - *{{ page.desc }}*   


<a id="synopsis"></a>

## SYNOPSIS

```bash
{{ page.title }} [-d 0-9] [-h] [-i] [-v]
```


<a id="description"></a>

## DESCRIPTION

The script allow you to check if any SADMIN required packages are missing. Running the script with the option '-i', will install any missing package.



<a id="examples"></a>

## EXAMPLE
List missing required packages, but don't install any of them.

```
# sadm_requirements.sh 
================================================================================
Thu Apr 29 09:28:05 EDT 2021 - sadm_requirements.sh V1.9 - SADM Lib. V3.69
Server Name: holmes.maison.ca - Type: LINUX
CENTOS 7.9.2009 Kernel 3.10.0-1160.24.1.el7.x86_64
==================================================
 
SADMIN client requirements
Checking availability of command lsb_release ... /bin/lsb_release [OK]
Checking availability of command dmidecode ... /sbin/dmidecode [OK]
Checking availability of command nmon ... /bin/nmon [OK]
Checking availability of command ethtool ... /sbin/ethtool [OK]
Checking availability of command sudo ... /bin/sudo [OK]
Checking availability of command lshw ... /sbin/lshw [OK]
Checking availability of command ifconfig ... /sbin/ifconfig [OK]
Checking availability of command iostat ... /bin/iostat [OK]
Checking availability of command parted ... /sbin/parted [OK]
Checking availability of command mutt ... /bin/mutt [OK]
Checking availability of command gawk ... /bin/gawk [OK]
Checking availability of command curl ... /bin/curl [OK]
Checking availability of command lscpu ... /bin/lscpu [OK]
Checking availability of command fdisk ... /sbin/fdisk [OK]
Checking availability of rpm package perl-libwww-perl ... [OK]
Checking availability of command perl ... /bin/perl [OK]
Checking availability of command ssh ... /bin/ssh [OK]
Checking availability of command mail ... /bin/mail [OK]
Checking availability of command bc ... /bin/bc [OK]
Checking availability of command python3 ... /bin/python3 [OK]

SADMIN server requirements.
Checking availability of command mysql ... /bin/mysql [OK]
Checking availability of command rrdtool ... /bin/rrdtool [OK]
Checking availability of command fping ... /sbin/fping [OK]
Checking availability of command pip3 ... /bin/pip3 [OK]
Checking availability of command wkhtmltopdf ... /usr/local/bin/wkhtmltopdf [OK]
Checking availability of command php ... /bin/php [OK]
Checking availability of command httpd ... /sbin/httpd [OK]

==================================================
Script exit code is 0 (Success) and execution time is 00:00:04
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/sadmin/log/holmes_sadm_requirements.log) created ($SADM_LOG_APPEND='N').
End of sadm_requirements.sh - Thu Apr 29 09:28:05 EDT 2021
================================================================================
# 
```


### Verify and install missing package(s) to meet 'SADMIN' requirements.
List and install missing required packages.
        
```
# sadm_requirements.sh -i
================================================================================
Thu Apr 29 09:37:26 EDT 2021 - sadm_requirements.sh V1.9 - SADM Lib. V3.69
Server Name: raspi3.maison.ca - Type: LINUX
RASPBIAN 10 Kernel 5.10.17-v7+
==================================================
 
SADMIN client requirements
Checking availability of command lsb_release ... /usr/bin/lsb_release [OK]
Checking availability of command dmidecode ... /usr/sbin/dmidecode [OK]
Checking availability of command nmon ... /usr/bin/nmon [OK]
Checking availability of command ethtool ... /sbin/ethtool [OK]
Checking availability of command sudo ... /usr/bin/sudo [OK]
Checking availability of command lshw ... /usr/bin/lshw [OK]
Checking availability of command ifconfig ... /sbin/ifconfig [OK]
Checking availability of command iostat ... /usr/bin/iostat [OK]
Checking availability of command parted ... /sbin/parted [OK]
Checking availability of command mutt ... /usr/bin/mutt [OK]
Checking availability of command gawk ... /usr/bin/gawk [OK]
Checking availability of command curl ... /usr/bin/curl [OK]
Checking availability of command lscpu ... /usr/bin/lscpu [OK]
Checking availability of command fdisk ... /sbin/fdisk [OK]
Checking availability of deb package libwww-perl ... [OK]
Checking availability of command perl ... /usr/bin/perl [OK]
Checking availability of command ssh ... /usr/bin/ssh [OK]
Checking availability of command mail ... /usr/bin/mail [OK]
Checking availability of command bc ... /usr/bin/bc [OK]
Checking availability of command python3 ... /usr/bin/python3 [OK]

SADMIN server requirements.
Checking availability of command mysql ... /usr/bin/mysql [OK]
Checking availability of command rrdtool ... /usr/bin/rrdtool [OK]
Checking availability of command fping ... /usr/bin/fping [OK]
Checking availability of command pip3 ... /usr/bin/pip3 [OK]
Checking availability of command wkhtmltopdf ... /usr/bin/wkhtmltopdf [OK]
Checking availability of command php ... /usr/bin/php [OK]
Checking availability of command apache2 ... /usr/sbin/apache2 [OK]

==================================================
Script exit code is 0 (Success) and execution time is 00:00:52
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/raspi3_sadm_requirements.log) created ($SADM_LOG_APPEND='N').
End of sadm_requirements.sh - Thu Apr 29 09:37:31 EDT 2021
================================================================================
# 
```        


{% include {{ site.section_options     }} %}
| **-i** | Install missing packages |   

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>

## SEE ALSO
[setup.sh](/_pages/install/#the-setup-script) - SADMIN Setup script.


