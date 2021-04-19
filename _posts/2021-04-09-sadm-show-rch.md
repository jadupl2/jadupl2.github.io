---
title:              sadm_show_rch.sh
layout:             single
date_created:       2021-04-09
date_updated:       2021-04-09 
show_excerpts:      false
entries_layout:     list
tags:               [ Tools ]
categories:         [ Server_Scripts, Utilities ]  
sadm_section_sh:    sadm/sadm_section_sh.md
author_profile: false
toc:            false
classes:        wide
coll_name:      srch.sh
coll_desc:      SADMIN Show All Systems Script History
coll_cat:       "SADMIN Utilities" 
---

Under construction, will be here soon.
srch
Updated: 2020/04/06
O/S : Aix, Linux, MacOS
 
NAME

srch (link to sadm_rch_scr_summary.sh)   -   [S]how the [R]esult [C]ode [H]istory file (*.rch) summary from all systems on terminal.
 
SYNOPSIS

srch     [ -v -h -p -w -m  ]    [ -s   ServerName  ]    [ -d   0-9  ]   
 
DESCRIPTION

    Show the last known status of every scripts of all your systems.
    The information presented by this scripts, is collected from all your servers every 5 minutes by the "sadm_fetch_clients.sh" script.
    The running script (if any) are presented first, followed by the script(s) that ended with error and finally the script that ended with success, sorted by descending date and time.
    This command can be executed only on the SADMIN server.

    Example of the RCH Summary Report on the terminal

    # srch


    Example of the RCH Summary Report for a specific server
    # srch -s raspi6


    Example to watch the RCH Summary Report first page in real time (Refresh every 60 seconds)
    # srch -w


    View the RCH Summary Report without stopping at each page.
    # srch -p


    Send a mail of the RCH Summary Report so to email address specify in $SADMIN/cfg/sadmin.cfg.
    # srch -m


    Example of email sent.


 
OPTIONS

-d [0-9]
    Specify debug level (0-9).
    Value of 0 indicate that no debug information is to be displayed.
-s [ServerName]
    Show the RCH Summary Report for the server specified.
-m
    Send RCH Summary Report to SysAdmin email (Enhance format coming soon).
-w
    Watch the RCH Summary Report in real time (Updated every 60 Sec.).
-p
    List the RCH Summary Report without stopping after each page.
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
sadm_fetch_clients.sh   (Rsync all *.rch *.log *.rpt files from all active SADMIN client to SADMIN Server)
smon (link to sadm_sysmon_cli.sh)   (Run System Monitor and show results) 