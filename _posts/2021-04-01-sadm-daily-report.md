---
title:          sadm_daily_report.sh
permalink:      /sadm-daily-report/
desc:           Produce and email monitoring daily reports
version:        1.24
updated:        2021-05-05
os:             Linux, Aix, MacOS
type:           S  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ report ] 
categories:     [ system_monitor ] 
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

<a id="name"></a>
## NAME
**{{ page.title }}** - *{{ page.desc }}*   



<a id="synopsis"></a>
## SYNOPSIS

```bash
{{ page.title }} [-b] [-d 0-9] [-h] [-r] [-s] [-v]
```
{% if page.type == "S" %}
<font size="3">Can only be run on SADMIN Server.</font>
{% endif %}


<a id="description"></a>
## DESCRIPTION

The script produce three reports, each of them is sent to the email(s) defined by the field 
'[SADM_MAIL_ADDR]({% post_url 2021-04-26-sadmin-cfg %}#sadm_mail_addr)' in the SADMIN configuration 
file ($SADMIN/cfg/sadmin.cfg). It can only be run on the SADMIN server (Not on a SADMIN client). 
The reports are also accessible via the web interface. It run automatically early every morning 
from the SADMIN server crontab (/etc/cron.d/sadm_server), but you can also be run it manually 
when desired. It can only be run on the SADMIN server.
{: .text-justify}


{: .text-justify}

If one of the three report is not desired, you can use the '-r', '-b' or the '-s' command line 
switch to disable the desired report (email). Note that only the actives systems will appear on 
these reports.  
{: .text-justify}


### The scripts report:
![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center}
  - The running scripts are listed first, then the scripts that terminated with an error and finally all the scripts grouped by system. So it give you view of the statistics of each script (start time, end time, elapse time,...) of each systems sorted and grouped by name. When something look different than the normal, like the alert group used is different than the default group or the last execution date of a script is more than thirty days, it will be shown with a yellow background. 
  {: .text-justify}
  - You can also view the log of each script just by clicking on the script name. 
  - The same report is also accessible in the heading of any of the "Scripts Status" web pages.  

### The daily backup report:
![Daily Backup Report Example](/assets/img/man/sadm_daily_report_backup.png){: .align-center}
  - This report present the last execution statistics of all the daily backup script (sadm_backup.sh) for each systems. Since the daily backup should have been taken during the night, they should all have the same execution date. If this is not the case, then the execution date cell will have a yellow background, to advise you that there may be a problem with the backup on that system.
  {: .text-justify} 
  - The daily backup report is also accessible in the heading of the "Daily Backup Status" web page.  
  - If you want to change the backup schedule of a particular system, just click on the "Schedule Activated" cell of the desired system.
  - If you want to see the log of the backup, click on the "Status" cell of the desired system.


### The [ReaR](https://relax-and-recover.org/) system image backup:
![Daily ReaR Image Backup Report Example](/assets/img/man/sadm_daily_report_rear.png){: .align-center}
  - The [ReaR](https://relax-and-recover.org/) report, show you the last ReaR backup execution result of each systems.
  - If a backup last execution date is older than 7 days, the date cell of that backup will have a yellow background. If the current backup size and the  previous backup differ than more than 50% they will have a yellow background as well. This may tell you that your backup have greater than expected and you may want to take a look at it.
  {: .text-justify} 
  - If you want to change the backup schedule of a particular system just click on the "Schedule Activated" cell of the desired system.  
  - The ReaR daily report is also accessible in the heading of the "ReaR Backup Schedule Status" web page.
  - If you want to see the log of the backup, just click on the "Status" cell of the desired system.  
<br>
- **Excluding Servers or/and Scripts from the reports:**
    - At the beginning of the script you will find a section defining two variables named "**SCRIPTS**" and "**SERVERS**". You can used them to exclude some scripts from the "Daily Scripts Report" by specifying them in the "SCRIPTS" variable.
    - To exclude server(s) from ALL the reports, you can specify them in the "SERVERS" variable. Server name used MUST not include the domain name.
  
```bash
# Exclude template scripts and demo scripts.
SCRIPTS="sadm_template sadmlib_std_demo"
    
# Exclude System Startup/Shutdown Script for Daily scripts report
SCRIPTS="$SCRIPTS sadm_startup sadm_shutdown"

# Server excluded from ALL Daily Report (Backup, Rear and Scripts)
SERVERS="server1 server2"
```



## EXECUTION EXAMPLE

```bash
# sadm_daily_report.sh

Sun Jan 17 14:39:39 EST 2021 - sadm_daily_report.sh V1.20 - SADM Lib. V3.64
Server Name: robin.batcave.com - Type: LINUX
CENTOS 7.9.2009 Kernel 3.10.0-1160.11.1.el7.x86_64
==================================================

Creating the Daily Backup Report
[ OK ] Mount batnas.batcave.com:/volume1/backup_linux /mnt/daily_report
[ OK ] Create Backup Web Page.
[ OK ] Unmount directory /mnt/daily_report
[ OK ] Daily Backup Report sent to batman@batcave.com
End of Daily Backup Report ...

Creating the ReaR Backup Report
[ OK ] Mount batnas.batcave.com:/volume1/backup_rear /mnt/daily_report
[ OK ] Unmount directory /mnt/daily_report
[ OK ] ReaR Backup Report sent to batman@batcave.com
End of the ReaR Backup Report ...

Creating the Daily Script Report
[ OK ] Create Script Web Page.
[ OK ] No script actually running.
[ OK ] No script terminated with error
[ OK ] Scripts grouped by server page generated
[ OK ] Script report sent to batman@batcave.com
End of the Script Report ...

==================================================
Script exit code is 0 (Success) and execution time is 00:00:27
History (/sadmin/dat/rch/robin_sadm_daily_report.rch) trim to 35 lines ($SADM_MAX_RCLINE=35).
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/sadmin/log/robin_sadm_daily_report.log) created ($SADM_LOG_APPEND='N').
End of sadm_daily_report.sh - Sun Jan 17 14:40:02 EST 2021
==========================================================================
```


{% include {{ site.section_options     }} %}
| **-r**  | Don't produce the ReaR backup report       |
| **-b**  | Don't produce the Daily backup report      |
| **-s**  | Don't produce the Scripts report           |

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_wrapper.sh]({% post_url 2018-02-11-sadm-wrapper %}) - Use to run your existing scripts & benefit of SADMIN tools  

