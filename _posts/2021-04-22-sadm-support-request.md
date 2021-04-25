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

        # sadm_support_request.sh 
        ================================================================================
        Starting sadm_support_request.sh V1.4 - SADM Lib. V2.52
        Server Name: holmes.maison.ca - Type: LINUX
        CENTOS 7.5.1804 Kernel 3.10.0-862.14.4.el7.x86_64
        ==================================================
     
        Adding /etc/environment to support request log ...
        Adding /etc/profile.d/sadmin.sh to support request log ...
        Adding /sadmin/cfg/sadmin.cfg to support request log ...
        Adding /etc/sudoers.d/033_sadmin-nopasswd to support request log ...
        Adding /etc/cron.d/sadm_server to support request log ...
        Adding /etc/cron.d/sadm_client to support request log ...
        Adding /etc/cron.d/sadm_osupdate to support request log ...
        Adding /etc/selinux/config to support request log ...
        Adding /etc/hosts to support request log ...
        Adding /etc/httpd/conf.d/sadmin.conf to support request log ...
        Adding /sadmin/setup/log/sadm_setup.log to support request log ...
        
        ==================================================
        Script return code is 0
        Script execution time is 00:00:00
        Trim History /sadmin/dat/rch/holmes_sadm_support_request.rch to 125 lines
        Requested alert only if script fail (Won't send alert)
        Trim log /sadmin/log/holmes_sadm_support_request.log to 2000 lines
        Sat Nov 17 11:48:37 EST 2018 - End of sadm_support_request.sh
        ================================================================================
        
        Attach this file in the support email request : /sadmin/tmp/sadm_support_request.tgz
        
        # 
        



 
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

 