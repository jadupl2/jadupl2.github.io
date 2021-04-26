---
title:              sadm_support_request.sh
layout:             single
date_created:       2021-04-22
date_updated:       2021-04-22
show_excerpts:      false
entries_layout:     list
tags:               [ utilities ] 
categories:         [ utilities ] 
author_profile: false
toc:            false
classes:        wide
tags:                   utilities
categories:             utilities
sidebar:
  title: "Documentation"
  nav: sidebar-manpage
---

<font size="3">
<div>$SADMIN/bin/sadm_support_request.sh</div>
<div>Updated 2018/11/15</div>
<div>Run on Aix, Linux, MacOS</div>
</font>

### NAME


sadm_support_request.sh   
This script create a file that contain information that will help us, when you submit a problem.
 
### SYNOPSIS

sadm_support_request.sh     [ -v ] [ -h ]    [ -d  [0-9] ]   
 
DESCRIPTION

This script is use to create a file that contain information that will help us, when you submit a problem.
When you submit a problem or request support it is important to attach the file produced by this script to your email.

```bash
root@borg:/etc/cron.d  # sadm_support_request.sh 
================================================================================
Mon 26 Apr 2021 08:55:49 AM EDT - sadm_support_request.sh V2.2 - SADM Lib. V3.69
Server Name: borg.maison.ca - Type: LINUX
UBUNTU 20.04 Kernel 5.8.0-50-generic
==================================================
 
Adding /etc/environment to support request log ...
Adding /etc/profile.d/sadmin.sh to support request log ...
Adding /opt/sadmin/cfg/sadmin.cfg to support request log ...
Adding /etc/sudoers.d/033_sadmin-nopasswd to support request log ...
Adding /etc/cron.d/sadm_client to support request log ...
Adding /etc/postfix/main.cf to support request log ...
Adding /etc/hosts to support request log ...
Adding /opt/sadmin/dat/dr/borg_sysinfo.txt to support request log ...

Running /opt/sadmin/bin/sadmlib_std_demo.sh ...
[SUCCESS] Script sadmlib_std_demo.sh terminated.
Adding /opt/sadmin/tmp/borg_sadmlib_std_demo.log to support request log ...

Running /opt/sadmin/bin/sadmlib_std_demo.py ...
[SUCCESS] Script sadmlib_std_demo.py terminated.
Adding /opt/sadmin/tmp/borg_sadmlib_std_demo.log to support request log ...

Running /opt/sadmin/bin/sadm_check_requirements.sh ...
[SUCCESS] Script sadm_check_requirements.sh terminated.
Adding /opt/sadmin/tmp/borg_sadm_check_requirements.sh.log to support request log ...

Running chage -l sadmin ...
Adding /opt/sadmin/tmp/borg_chage.log to support request log ...
Recording /opt/sadmin tree structure list in /opt/sadmin/log/borg_sadm_support_tree.log ...
Creating a listing of all files in /opt/sadmin to /opt/sadmin/log/borg_sadm_support_files_list.log ...

==================================================
Script exit code is 0 (Success) and execution time is 00:00:21
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/borg_sadm_support_request.log) created ($SADM_LOG_APPEND='N').
End of sadm_support_request.sh - Mon 26 Apr 2021 08:56:04 AM EDT
================================================================================

Please send the file '/opt/sadmin/tmp/borg_sadm_support_request.tgz' to support@sadmin.ca.
We will get back to you as soon as possible.
```




 
OPTIONS

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

 