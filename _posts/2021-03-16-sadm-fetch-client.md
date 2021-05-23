---
title:          sadm_fetch_client.sh
desc:           Collect latest scripts results and monitoring status
version:        3.25
updated:        2021-05-05
os:             Linux
type:           S  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ system_monitor ] 
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
{{ page.title }} [-d 0-9] [-h] [-v]
```
{% if page.type == "S" %}
<font size="3">Can only be run on SADMIN Server.</font>
{% endif %}



<a id="description"></a>
## DESCRIPTION
The main function of this script is to collect logs and history files of every *actives clients*. It 
then analyse this information and issue alert by ['SMS/Texto'](/assets/img/sms/textbelt_step10_sms_receive.png), ['Slack'](/assets/img/slack/slack_warning.png) or by [email](/assets/img/mail/sysmon_mail_notification.png) when needed. Finally, it generate 
various crontab files (Daily backup, ReaR backup and O/S update) when user modify some schedule.  
{: .text-justify}

- Only clients having an ‘active’ status are fetched.   
- After making sure it can SSH to clients ;    
    - Only new or modified files with extensions '*.rch', '*.log' and '*.rpt' on clients are
synchronize (rsync) with the SADMIN server.  
    - Then each script history ('*rch') and system monitor ('*.rpt') files are examined and alert
are issue if needed.  
- Finally, if any schedule (Backup, Rear backup, O/S update) have been modified the proper
crontab file is updated accordingly in /etc/cron.d directory.  

```bash
    /etc/cron.d $ ls -l 
    -rw-r--r-- 1 root root 2319 May  5 16:36 sadm_backup
    -rw-r--r-- 1 root root 1998 May  5 16:36 sadm_osupdate
    -rw-r--r-- 1 root root 1389 May  5 16:36 sadm_rear_backup
```


<a id="examples"></a>
## EXAMPLE

```bash
root@holmes:~ # sadm_fetch_clients.sh
================================================================================
Wed May  5 21:21:52 EDT 2021 - sadm_fetch_clients.sh V3.25 - SADM Lib. V3.69
Server Name: holmes.maison.ca - Type: LINUX
CENTOS 7.9.2009 Kernel 3.10.0-1160.24.1.el7.x86_64
==================================================

Processing active 'linux' server(s)

Processing [1] borg.maison.ca
[ OK ] rsync /sadmin/cfg/alert_group.cfg borg.maison.ca:/opt/sadmin/cfg/alert_group.cfg
[ OK ] rsync /sadmin/cfg/alert_slack.cfg borg.maison.ca:/opt/sadmin/cfg/alert_slack.cfg
[ OK ] rsync -var --delete borg.maison.ca:/opt/sadmin/cfg/ /sadmin/www/dat/borg/cfg/
[ OK ] rsync -var --delete borg.maison.ca:/opt/sadmin/log/ /sadmin/www/dat/borg/log/
[ OK ] rsync -var --delete borg.maison.ca:/opt/sadmin/dat/rch/ /sadmin/www/dat/borg/rch/
[ OK ] rsync -var --delete borg.maison.ca:/opt/sadmin/dat/rpt/ /sadmin/www/dat/borg/rpt/
...
Processing [6] debian9.maison.ca
[ WARNING ]  Can't SSH to debian9.maison.ca (Sporadic System).
...
----------
No Active 'aix' system found.

==================================================
Processing active 'darwin' server(s)

Processing [1] imac.maison.ca
[ OK ] rsync /sadmin/cfg/alert_group.cfg imac.maison.ca:/Users/jacques/Documents/Prod/sadmin/cfg/alert_group.cfg
[ OK ] rsync /sadmin/cfg/alert_slack.cfg imac.maison.ca:/Users/jacques/Documents/Prod/sadmin/cfg/alert_slack.cfg
[ OK ] rsync -var --delete imac.maison.ca:/Users/jacques/Documents/Prod/sadmin/cfg/ /sadmin/www/dat/imac/cfg/
[ OK ] rsync -var --delete imac.maison.ca:/Users/jacques/Documents/Prod/sadmin/log/ /sadmin/www/dat/imac/log/
[ OK ] rsync -var --delete imac.maison.ca:/Users/jacques/Documents/Prod/sadmin/dat/rch/ /sadmin/www/dat/imac/rch/
[ OK ] rsync -var --delete imac.maison.ca:/Users/jacques/Documents/Prod/sadmin/dat/rpt/ /sadmin/www/dat/imac/rpt/

Systems Rsync Summary
 - Total Linux error(s)  : 0
 - Total Aix error(s)    : 0
 - Total Mac error(s)    : 0
Rsync Total Error(s)     : 0
----------

Crontab Update Summary
  - No need to update the O/S update schedule crontab (/etc/cron.d/sadm_osupdate).
  - No need to update the backup crontab (/etc/cron.d/sadm_backup).
  - No need to update the ReaR backup crontab (/etc/cron.d/sadm_rear_backup).
----------

Verifying all Systems Monitors reports files (*.rpt) :
No error reported by any 'SysMon report files' (*.rpt).

No System Monitor Alert(s) submitted
   - New alert sent successfully : 0
   - Alert error trying to send  : 0
   - Alert older than 24 Hrs     : 0
   - Alert already sent          : 0
----------

Verifying all systems scripts results files (*.rch) :
1) 2021.04.15 09:15 alert (S) for sa_rsync_ds410_to_rasnas on holmes: Alert is older than 24 hrs.
2) 2021.05.05 18:30 alert (S) for sa_rsync_pictures on borg: Alert already sent.
3) 2021.05.05 15:30 alert (S) for sadm_vm_backup on borg: Alert already sent.

3 Script(s) Alert(s) submitted
   - New alert sent successfully : 0
   - Alert error trying to send  : 0
   - Alert older than 24 Hrs     : 1
   - Alert already sent          : 2
----------

==================================================
Script exit code is 0 (Success) and execution time is 00:01:26
History (/sadmin/dat/rch/holmes_sadm_fetch_clients.rch) trim to 150 lines ($SADM_MAX_RCLINE=150).
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
Log /sadmin/log/holmes_sadm_fetch_clients.log trim to 25000 lines ($SADM_MAX_LOGLINE=25000).
End of sadm_fetch_clients.sh - Wed May  5 21:23:14 EDT 2021
================================================================================

```
<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->


{% include {{ site.section_options     }} %}

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_requirements.sh]({% post_url 2019-03-21-sadm-requirements %}) - List/Install required SADMIN Tools packages  
