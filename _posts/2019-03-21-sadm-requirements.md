---
layout: single
title: sadm_requirements.sh
show_excerpts: false
entries_layout: list
tags:               utilities
categories:         utilities
author_profile: false
toc:            false
classes:        wide
sidebar:
  title:        "Documentation"
  nav:          sidebar-manpage
---

sadm_requirements.sh
Updated: 2019/03/21
O/S : Linux
 
NAME

sadm_requirements.sh   -   Permit to identify missing 'SADMIN' requirements (if any) and install missing package (option -i).
 
SYNOPSIS

sadm_requirements.sh     [ -v -h  ]    [ -i  ]    [ -d   0-9  ]   
 
DESCRIPTION

    Permit to identify missing 'SADMIN' package requirement (if any) and to install missing package (option -i).



### Verify 'SADMIN' requirements
Check, but do not install missing package(s).
```
# $SADMIN/bin/sadm_requirements.sh 
================================================================================
Starting sadm_requirements.sh V1.1 - SADM Lib. V2.66
Server Name: ubuntu1604.maison.ca - Type: LINUX
UBUNTU 16.04 Kernel 4.4.0-66-generic
==================================================

SADMIN client requirements
Checking availability of command lsb_release ... /usr/bin/lsb_release [OK]
Checking availability of command dmidecode ... /usr/sbin/dmidecode [OK]
Checking availability of command nmon ... /usr/bin/nmon [OK]
Checking availability of command ethtool ... /sbin/ethtool [OK]
Checking availability of command sudo ... /usr/bin/sudo [OK]
Checking availability of command lshw ... Command missing [Warning]
Checking availability of command ifconfig ... /sbin/ifconfig [OK]
Checking availability of command iostat ... Command missing [Warning]
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
Checking availability of command facter ... /usr/bin/facter [OK]
Checking availability of command python3 ... /usr/bin/python3 [OK]

==================================================
Script return code is 0
Script execution time is 00:00:00
Trim History /sadmin/dat/rch/ubuntu1604_sadm_check_requirements.rch to 125 lines
Requested alert only if script fail (Won't send alert)
Trim log /sadmin/log/ubuntu1604_sadm_check_requirements.log to 1000 lines
Wed Mar 20 11:34:25 EDT 2019 - End of sadm_requirements.sh
================================================================================
```


### Verify and install missing package(s) to meet 'SADMIN' requirements.
        
```
$SADMIN/bin/sadm_requirements.sh -i 
================================================================================
Starting sadm_requirements.sh V1.1 - SADM Lib. V2.66
Server Name: ubuntu1604.maison.ca - Type: LINUX
UBUNTU 16.04 Kernel 4.4.0-66-generic
==================================================

SADMIN client requirements
Checking availability of command lsb_release ... /usr/bin/lsb_release [OK]
Checking availability of command dmidecode ... /usr/sbin/dmidecode [OK]
Checking availability of command nmon ... /usr/bin/nmon [OK]
Checking availability of command ethtool ... /sbin/ethtool [OK]
Checking availability of command sudo ... /usr/bin/sudo [OK]
Checking availability of command lshw ... Command missing [Warning]
Synchronize package index files
Running "apt-get update"
Return Code after apt-get update is 0
Installing the Package lshw now
apt-get -y install lshw
Return Code after installation of lshw is 0
Checking availability of command lshw ... /usr/bin/lshw [OK]

Checking availability of command ifconfig ... /sbin/ifconfig [OK]
Checking availability of command iostat ... Command missing [Warning]
Synchronize package index files
Running "apt-get update"
Return Code after apt-get update is 0
Installing the Package sysstat now
apt-get -y install sysstat
Return Code after installation of sysstat is 0
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
Checking availability of command facter ... /usr/bin/facter [OK]
Checking availability of command python3 ... /usr/bin/python3 [OK]

==================================================
Script return code is 0
Script execution time is 00:00:21
Trim History /sadmin/dat/rch/ubuntu1604_sadm_check_requirements.rch to 125 lines
Requested alert only if script fail (Won't send alert)
Trim log /sadmin/log/ubuntu1604_sadm_check_requirements.log to 1000 lines
Wed Mar 20 11:35:49 EDT 2019 - End of sadm_check_requirements.sh
================================================================================
root@ubuntu1604/sadmin# 
```        



 
OPTIONS

-i
    Check and install missing package(s) to meet 'SADMIN' requirements.
-d
    Specify debug level (0-9).
    Value of 0 indicate that no debug information is to be displayed.
-h
    Display this help and exit.
-v
    Output version information and exit.



REQUIREMENTS

    Environment variable 'SADMIN', specify the root directory of the SADMIN tools.
    Define by setup script in /etc/profile.d/sadmin.sh and in /etc/environment .
    SADMIN main configuration file, "$SADMIN/cfg/sadmin.cfg"
    SADMIN Tools Shell Library, "$SADMIN/lib/sadmlib.sh".


 
EXIT STATUS
[0]    An exit status of zero indicates success
[1]    Failure is indicated by a nonzero value, typically ‘1’.

 
AUTHOR
Jacques Duplessis (jacques.duplessis@sadmin.ca.).
Any suggestions or bug report can be sent at http://www.sadmin.ca/support.php

 
COPYRIGHT
Copyright © 2020 Free Software Foundation, Inc. License GPLv3+:
    - GNU GPL version 3 or later http://gnu.org/licenses/gpl.html.
This is free software, you are free to change and redistribute it.
There is NO WARRANTY to the extent permitted by law.

 
SEE ALSO
Installation guide    - Installation Guide, running the setup.sh script.
sadmlib_std_demo.sh    - Show with examples all global variables and functions you can use within your shell script.
sadmlib_std_demo.py    - Show with examples all global variables and functions/modules you can use within your Python script.
