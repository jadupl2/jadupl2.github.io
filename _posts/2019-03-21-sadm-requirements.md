---
title:          sadm_requirements.sh
desc:           List and install required SADMIN Tools packages
version:        1.10
updated:        2021-05-04
os:             Linux, Aix, MacOS
type:           B  # [S]=Run on Server only, [C]=Client Only, [B]=Run on Both
tags:           [ utilities ] 
categories:     [ utilities ] 
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
{% if page.type == "S" %}
<font size="3">Can only be run on SADMIN Server.</font>
{% endif %}



<a id="description"></a>

## DESCRIPTION

The script allow you to check if any SADMIN required packages are missing. Running the script 
with the option '-i', will install any missing package (not available on MacOS).



<a id="examples"></a>

## EXAMPLE
List missing required packages, but don't install any of them.

```
root@raspi3/opt/sadmin/bin # ./sadm_requirements.sh 
================================================================================
Sun May  2 13:54:48 EDT 2021 - sadm_requirements.sh V1.9 - SADM Lib. V3.69
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
Checking availability of command curl ... Missing [Warning]     <<--
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
Script exit code is 0 (Success) and execution time is 00:00:50
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/raspi3_sadm_requirements.log) created ($SADM_LOG_APPEND='N').
End of sadm_requirements.sh - Sun May  2 13:54:52 EDT 2021
================================================================================
```


### Verify and install missing package(s) to meet 'SADMIN' requirements.
List and install missing required packages.
        
```
root@raspi3/opt/sadmin/bin # ./sadm_requirements.sh -i
================================================================================
Sun May  2 14:09:13 EDT 2021 - sadm_requirements.sh V1.10 - SADM Lib. V3.69
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
Checking availability of command curl ... Missing [Warning]     <<--
Synchronize package index files.
Running "apt-get update"
Return Code after apt-get update is 0.
Installing the Package curl now.
apt-get -y install curl.
Return Code after installation of curl is 0 

Checking availability of command curl ... /usr/bin/curl [OK]    <<--
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
Script exit code is 0 (Success) and execution time is 00:01:26
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/raspi3_sadm_requirements.log) created ($SADM_LOG_APPEND='N').
End of sadm_requirements.sh - Sun May  2 14:09:52 EDT 2021
================================================================================
root@raspi3/opt/sadmin/bin # 
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


