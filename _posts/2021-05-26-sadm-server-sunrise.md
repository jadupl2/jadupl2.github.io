---
title:          sadm_server_sunrise.sh
desc:           Collect & process data produced by all actives clients
version:        2.8
updated:        2021-06-03
os:             Linux
type:           S  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ server-scripts ] 
categories:     [ server-scripts ] 
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
This script have multiple functions :  
1- First, it make sure that your $SADMIN directories permissions and [ownerships]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_user) are inline with the one you specified in the [SADMIN configuration file]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_user).
This is the responsibility of the [sadm_server_housekeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %}) script. 

2- Secondly, it collect all the latest performance data and configuration of all your actives clients. 
This is the responsibility of the [sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %}) script.   

3- It then update the SADMIN database with the latest [system information files]({% post_url 2021-05-30-sysinfo-file %}) just collected.    
This is the responsibility of the [sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %}) script.   

4- It is responsible to update the rrd database (Round Robin Database) that allow you to view the performance 
graph of your systems.  
This is done by the [sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %}) script.  

5- The next step is to scan the network subnet you selected to give you an exact picture of your 
IP usage and take a backup of your SADMIN database.  
This step is done by the [sadm_subnet-lookup.py]({% post_url 2021-05-29-sadm-subnet-lookup %}) script.  

6- Finally, a backup of the SADMIN database is taken by the [sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %})
  script.  
{: .text-justify}

This script does a lot of things but actually all it does is to start the six scripts that will do
each a different job. It has to run early in the morning, so when you wake up or arrive to work you
have the latest information about your systems. You may change the execution time if you want in 
"/etc/cron.d/sadm_server" but it as to run early in the morning and after the "[sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %})" script on the clients. The "[sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %})" script is the one that generate the latest data that this script is collecting and processing.
{: .text-justify}

## Portion of server crontab that execute this script
```bash
# cat /etc/cron.d/sadm_server 
...
# Early every morning - Collect Perf data, Update & backup DB, Network scan, Housekeeping
05 05 * * * sadmin sudo ${SADMIN}/bin/sadm_server_sunrise.sh >/dev/null 2>&1
...
```


## This script is responsible to run these six scripts once a day

[sadm_server_housekeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %}) (1)

- Make sure all the server files in "$SADMIN" have proper owner, group and permission  
- Remove files older than 7 days in "$SADMIN/tmp" directory  
- Remove pid files (once a day) in “$SADMIN/tmp” directory 
- Archive alert older than 30 days to $SADMIN/cfg/alert_archive.txt 
- Remove \*.rch files in "${SADMIN}/dat/rch" older than "[${SADM_RCH_KEEPDAYS}]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_rch_keepdays)"
- Remove \*.log files in "${SADMIN}/log" older than "[${SADM_LOG_KEEPDAYS}]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_log_keepdays)"
- Remove \*.nmon files in "${SADMIN}/dat/nmon" older than "[${SADM_NMON_KEEPDAYS}]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_nmon_keepdays)"
- Check existence on the server of "[$SADMIN_USER" and "$SADMIN_GROUP]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_user)"
- Verify if "$SADMIN_USER" is not lock or the password is expired  


[sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %}) (2)  
- Sync clients disaster recovery directory "$SADMIN/dat/dr" to local "$SADMIN/www/dat/$server/dr"  
- Sync clients performance data files "$SADMIN/dat/nmon" to local "$SADMIN/www/dat/$server/nmon"  


[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %}) (3) 
- Update the SADMIN server database with information collected the Daily Farm Fetch    


[sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %}) (4)
- Update the performance statistics database (rrd) with the data that was just collected  


[sadm_subnet-lookup.py]({% post_url 2021-05-29-sadm-subnet-lookup %}) (5)  
- Scan the [network subnet]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_network) specified in sadmin.cfg and update the sadmin database      


[sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %}) (6) 
- Do a backup of all MySQL Databases
  

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
================================================================================
Thu May 27 05:05:05 EDT 2021 - sadm_server_sunrise.sh V2.8 - SADM Lib. V3.70
Server Name: holmes.maison.ca - Type: LINUX
CENTOS 7.9.2009 Kernel 3.10.0-1160.25.1.el7.x86_64
==================================================
 
Running /sadmin/bin/sadm_server_housekeeping.sh ...
[ SUCCESS ] Running /sadmin/bin/sadm_server_housekeeping.sh
Running /sadmin/bin/sadm_daily_farm_fetch.sh ...
[ SUCCESS ] Running /sadmin/bin/sadm_daily_farm_fetch.sh
Running /sadmin/bin/sadm_database_update.py ...
[ SUCCESS ] Running /sadmin/bin/sadm_database_update.py
Running /sadmin/bin/sadm_nmon_rrd_update.sh ...
[ SUCCESS ] Running /sadmin/bin/sadm_nmon_rrd_update.sh
Running /sadmin/bin/sadm_subnet_lookup.py ...
[ SUCCESS ] Running /sadmin/bin/sadm_subnet_lookup.py
Running /sadmin/bin/sadm_backupdb.sh ...
[ SUCCESS ] Running /sadmin/bin/sadm_backupdb.sh

==================================================
Script exit code is 0 (Success) and execution time is 00:33:21
History (/sadmin/dat/rch/holmes_sadm_server_sunrise.rch) trim to 35 lines.
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/sadmin/log/holmes_sadm_server_sunrise.log) created ($SADM_LOG_APPEND='N').
End of sadm_server_sunrise.sh - Thu May 27 05:38:23 EDT 2021
================================================================================
```
<!-- ![Daily Script Report Example](/assets/img/man/sadm_daily_report_script.png){: .align-center} -->

[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

[sadm_server_housekeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %}) - Purge old log,rch,nmon files and check $SADMIN permission   
[sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %}) - Collect Hardware/Software/Performance data from actives servers   
[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %}) - Take data collected from clients and update database    
[sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %}) - Daily performance database update   
[sadm_subnet-lookup.py]({% post_url 2021-05-29-sadm-subnet-lookup %}) - Scan network selected subnet & store info in database  
[sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %}) - Backup one or all MySQL/MariaDB databases on the system  
[sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}) - SADMIN main configuration file  
[System Information File]({% post_url 2021-05-30-sysinfo-file %}) - Documentation about the system information file  
[sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %}) - Clients end of day housekeeping and producing system information files  
