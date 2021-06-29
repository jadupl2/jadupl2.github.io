---
title:          sadm_server crontab
desc:           SADMIN server crontab file (/etc/cron.d/sadm_server)
version:        2.2
summary: |         
    This is SADMIN server crontab file, it execute everything that keep SADMIN running smoothly.
    {: .text-justify}
updated:        2021-06-25
os:             Linux
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ configuration-files ] 
tags:           [ configuration-files ] 
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
{{ page.summary }} 
 
- [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %}), that rsync all .rch/.log/.rpt from actives clients to SADMIN server.  
- [sadm_server_sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %}), that collect & process data produced by all actives clients.   
- [sadm_daily_report]({% post_url 2021-04-01-sadm-daily-report %}), that produce and email monitoring daily reports.   
- [sadm_push_sadmin.sh]({% post_url 2021-05-22-sadm-push-sadmin %}), that push SADMIN version to one or all actives clients (optional).


```bash
# SADMIN Server Crontab File 
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/sadmin/bin:/opt/sadmin/usr/bin
SADMIN=/opt/sadmin
# 
# 
# Min, Hrs, Date, Mth, Day, User, Script
# 0=Sun 1=Mon 2=Tue 3=Wed 4=Thu 5=Fri 6=Sat
# 
# Rsync all *.rch,*.log,*.rpt files from all actives clients.
*/5 * * * * sadmin sudo ${SADMIN}/bin/sadm_fetch_clients.sh >/dev/null 2>&1
#
# Early morning daily run, Collect Perf data - Update Database, Housekeeping
08 05 * * * sadmin sudo ${SADMIN}/bin/sadm_server_sunrise.sh >/dev/null 2>&1
#
# Daily SADMIN Report by Email
07 07 * * * sadmin sudo ${SADMIN}/bin/sadm_daily_report.sh >/dev/null 2>&1
#
#
# Daily push of /opt/sadmin/(lib,bin,cfg/.*) to all active servers (Optional)
#   -s To include push of /opt/sadmin/sys
#   -u To include push of /opt/sadmin/(usr/bin usr/lib usr/cfg)
#30 15 * * * sadmin sudo ${SADMIN}/bin/sadm_push_sadmin.sh > /dev/null 2>&1
#
```

[Back to the top](#top_of_page)

<a id="seealso"></a>
## SEE ALSO

| Link to ...| Description |  
| :--- | :--- |  
| [SADMIN installation](/_pages/install)  | SADMIN installation page |   
| [How-to update SADMIN]({% post_url 2021-03-14-sadm-update %})             | How-to update to latest version of SADMIN   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                        | SADMIN main configuration file   
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                   | Client system monitor   
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) | Client System Monitor configuration file     
| [smon]({% post_url 2021-06-15-sadm-sysmon-cli %})|   Allow you run SysMon and see the report file |   

