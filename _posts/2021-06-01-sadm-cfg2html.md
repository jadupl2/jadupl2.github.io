---
title:          cfg2html.sh
desc:           Get System information and creates a HTML web page of it
version:        3.6
updated:        2021-06-03
os:             Linux, Aix
type:           B  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ client-scripts ] 
tags:           [ client-scripts ] 
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
<a id="top_of_page"></a>



<a id="name"></a>
## NAME
**{{ page.title }}**  
*{{ page.desc }}*   



<a id="synopsis"></a>
## SYNOPSIS

```bash
{{ page.title }} [-d 0-9] [-h] [-v]
```

{% include sadm/sadm_page_info.md %}
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}




<a id="description"></a>
## DESCRIPTION
This script is use to generate a system information web page that is accessible via the SADMIN
web interface. To generate this web page, we use 
the open source project "[cfg2html](https://www.cfg2html.com/)". 
The HTML page produced, include the collection of Cron and At, 
installed Hardware, installed Software, Filesystems, Dump- and Swap-configuration, LVM, 
Network Settings, Kernel, System enhancements and Applications, Subsystems. As of now, this script 
doesn't support MacOS operating system.
{: .text-justify}
 
 
**Files produced by the script** 
```bash
root@raspi8:~  # cd $SADMIN/dat/dr
root@raspi8:/opt/sadmin/dat/dr  # ls -l cfg2html*
-rw-rw-r-- 1 sadmin sadmin   2846 Jun  3 14:54 cfg2html_raspi8.err
-rw-rw-r-- 1 sadmin sadmin 752477 Jun  3 14:54 cfg2html_raspi8.html
-rw-rw-r-- 1 sadmin sadmin      0 Jun  3 14:54 cfg2html_raspi8.partitions.save
-rw-rw-r-- 1 sadmin sadmin 724874 Jun  3 14:54 cfg2html_raspi8.txt
root@raspi8:/opt/sadmin/dat/dr  # 
```

**To view cfg2html page, choose the server you want and click on "cfg2html" button**
![sadm_cfg2html_button](/assets/img/sadm_cfg2html/sadm_cfg2html_viewing.png){: .align-center}

Here is an [example of report](/assets/img/sadm_cfg2html/man_sadm_cfg2html_example.html) that was generated for a raspberry pi.


[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
# sadm_cfg2html.sh 
================================================================================
Thu Jun  3 14:54:22 EDT 2021 - sadm_cfg2html.sh V3.6 - SADM Lib. V3.70
Server Name: raspi8.maison.ca - Type: LINUX
RASPBIAN 10 Kernel 5.10.17-v7l+
==================================================
 
cfg2html-linux version 2.94-2014/05/07 // Linux 5.10.17-v7l+ armv7l
Running : /usr/bin/cfg2html -H -o /opt/sadmin/dat/dr.
Return code of the command is 0.

==================================================
Script exit code is 0 (Success) and execution time is 00:00:59
History (/opt/sadmin/dat/rch/raspi8_sadm_cfg2html.rch) trim to 35 lines.
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/raspi8_sadm_cfg2html.log) created ($SADM_LOG_APPEND='N').
End of sadm_cfg2html.sh - Thu Jun  3 14:54:54 EDT 2021
================================================================================
```

[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %}) - rsync all .rch/.log/.rpt from actives clients to the SADMIN server.  
[sadm_requirements.sh]({% post_url 2019-03-21-sadm-requirements %}) - List/install required SADMIN tools packages  
[sadm_sysmon_tui.pl]({% post_url 2021-05-18-sadm-sysmon-tui %}) -  Command line summary of alerts and failed scripts of all your servers.  
[sadm_daily_report]({% post_url 2021-04-01-sadm-daily-report %}) - Produce and email monitoring daily reports
[sadm_template.sh]({% post_url 2021-03-16-sadm-template-sh %}) - Using SADMIN shell script template   
[sadm_template.py]({% post_url 2021-03-16-sadm-template-py %}) - Using SADMIN python script template    
[sadm_template_menu.sh]({% post_url 2021-04-30-sadm-template-menu %}) - Using SADMIN shell menu template   
[sadm_wrapper.sh]({% post_url 2018-02-11-sadm-wrapper %}) - Use to run your existing scripts & benefit of SADMIN tools  
[sadmlib_std.sh]({% post_url 2021-04-07-sadmlib-std-sh %}) - SADMIN standard shell library  
[sadmlib_std.py]({% post_url 2021-04-07-sadmlib-std-py %}) - SADMIN standard python library  
[sadmlib_screen.sh]({% post_url 2019-10-12-sadmlib-screen-sh %}) - SADMIN screen oriented library  
[sadmlib_std_demo.sh]({% post_url 2019-10-12-sadmlib-std-demo-sh %}) - SADMIN shell library functions demo   
[sadmlib_std_demo.py]({% post_url 2019-10-12-sadmlib-std-demo-py %}) - SADMIN python library functions demo  
[SADMIN installation](/_pages/install) - SADMIN installation page  
[How-to Add a client]({% post_url 2021-04-11-web-add-client %}) - How-to add a client to SADMIN inventory  
[How-to Remove a client]({% post_url 2021-05-19-how-to-remove-a-client %}) - How-to remove a client from SADMIN inventory  
[sadm_uninstall.sh]({% post_url 2021-05-21-sadm-uninstall %}) - Uninstall the SADMIN tools  
[sadm_push_sadmin.sh]({% post_url 2021-05-22-sadm-push-sadmin %}) - Push SADMIN version to one or all actives clients  
[How-to update SADMIN]({% post_url 2021-03-14-sadm-update %}) - How-to update to latest version of SADMIN   
[sadm_service_ctrl.sh]({% post_url 2021-05-23-sadm-service-ctrl %}) - Enable, Disable and get status of system startup and shutdown script  
[sadm_backup.sh]({% post_url 2021-05-24-sadm-backup %}) - Backup based on the content of the backup list & exclude file  
[sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}) - SADMIN main configuration file   
[sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %}) - Collect & process data produced by all actives clients  
[sadm_server_housekeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %}) - Enforce security SADMIN Web interface & crontab files
[sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %}) - Collect Hardware/Software/Performance data from actives servers   
[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %}) - Take data collected from clients and update database    
[sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %}) - Daily performance database update   
[sadm_subnet-lookup.py]({% post_url 2021-05-29-sadm-subnet-lookup %}) - Scan network selected subnet & store info in database  
[sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %}) - Backup one or all MySQL/MariaDB databases on the system  
[sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %}) - Clients end of day housekeeping and producing system information files  
[sadm_client_housekeeping.sh]({% post_url 2021-05-29-sadm-client-housekeeping %}) - Purge old log,rch,nmon files and check $SADMIN permission   
[sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %}) - Collect hardware & software information about the system   
[System Information File]({% post_url 2021-05-30-sysinfo-file %}) - Documentation about the system information file  
[sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %}) - Save system filesystems information in order to recreate them from scratch.
[sadm_cfg2html.sh]({% post_url 2021-06-01-sadm-cfg2html %}) - Get System information and creates a HTML web page of it.