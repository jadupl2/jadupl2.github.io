---
title:              sadm_create_sysinfo.sh
layout:             single
date_created:       2021-04-09
date_updated:       2021-04-09 
show_excerpts:      false
entries_layout:     list
tags:               [ tools ]
categories:         [ client_scripts ] 
author_profile:     false
toc:                false
classes:            wide
sidebar:
  title: "Documentation"
  nav: sidebar-manpage
---


sadm_create_sysinfo.sh
Updated: 2018/11/22
O/S : Aix, Linux, MacOS
 
NAME

sadm_create_sysinfo.sh   -   Run automatically every day to collect hardware & software information about the system.
 
SYNOPSIS

sadm_create_sysinfo.sh     [ -v -h  ]    [ -d   0-9  ]   
 
DESCRIPTION

    When you run this script, no question is asked and files in the disaster recovery directory are updated.
    This script is part of the 'Client Sunset script' (${SADMIN}/bin/sadm_client_sunset.sh).
    The 'Client Sunset script' is scheduled to run daily from the client crontab (/etc/cron.d/sadm_client).



        Information in the Disaster Recovery directory, will be useful in case of complete system rebuild.
        Files in this directory ($SADMIN/dat/dr) are updated daily.




    To view information generated from this script, choose the server to want and click on the buttons on the top of the page..


    This is an example of what you would get by pressing the 'Server Summary' button.


 
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

 
SEE ALSO
sadm_client_sunset.sh   (Daily end of the day script) 