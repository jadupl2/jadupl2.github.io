---
title:          sadm_client crontab
permalink:      /sadm-client-crontab/
desc:           SADMIN client crontab file (/etc/cron.d/sadm_client)
version:        2.2
summary: |         
    This is SADMIN client crontab file, it collect performance and system information data, it also
    run system monitor and perform some housekeeping in the $SADMIN directories.
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

<br>
**The three entries in SADMIN client crontab**

- [sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %}), perform the client end of day housekeeping.  
- [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %}), the client system monitor run every 5 minutes.   
- [sadm_nmon_watcher.sh]({% post_url 2021-06-25-sadm-nmon-watcher %}), it check if the performance collector (nmon) is running, if it is not it will start it.

```bash
# SADMIN Client Crontab File 
# 
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
SADMIN=/opt/sadmin
# 
# Run these four scripts in sequence, just before midnight every day:
# (1) sadm_housekeeping_client.sh (Make sure files in $SADMIN have proper owner:group & permission)
# (2) sadm_dr_savefs.sh (Save lvm filesystems metadata to recreate them easily in Disaster Recovery)
# (3) sadm_create_cfg2html.sh (Run cfg2html tool - Produce system configuration web page).
# (4) sadm_create_sysinfo.sh (Collect Hardware & Software info of system to update Database).
23 23 * * *  sadmin sudo ${SADMIN}/bin/sadm_client_sunset.sh > /dev/null 2>&1
# 
# Run SADMIN System Monitoring every 5 minutes
*/5 * * * * sadmin sudo ${SADMIN}/bin/sadm_sysmon.pl >${SADMIN}/log/$(hostname -s)_sadm_sysmon.log 2>&1
#
# 
# Every 45 Min, make sure 'nmon' performance collector is running.
*/45 * * * *  sadmin sudo ${SADMIN}/bin/sadm_nmon_watcher.sh >/dev/null 2>&1
# 
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

