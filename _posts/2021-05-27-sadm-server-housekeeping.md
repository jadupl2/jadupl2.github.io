---
title:          sadm_server_housekeeping.sh
desc:           Enforce security SADMIN Web interface & crontab files
version:        1.48
updated:        2021-05-27
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

The function of this script is to perform various housekeeping, such as making sure permission and
owner/group are correctly set on the SADMIN web site. It also make sure the SADMIN various 
crontab in "/etc/cron.d" are set to the proper permission. Finally, alerts older than 7 days 
are move to the alert archive file.
{: .text-justify}

**Here is a list of the various functions executed by this script**

- Make sure all the Web directories and files have proper owner, group and permission  
- Archive alert older than 7 days to $SADMIN/cfg/alert_archive.txt   
- Remove temporary performance graphics files.

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
# sadm_server_housekeeping.sh 
================================================================================
Sat May 29 11:02:37 EDT 2021 - sadm_server_housekeeping.sh V2.8 - SADM Lib. V3.70
Server Name: holmes.maison.ca - Type: LINUX
CENTOS 7.9.2009 Kernel 3.10.0-1160.25.1.el7.x86_64
==================================================
 
Move Alert older than 7 days to the alert history file.
They are move from /sadmin/cfg/alert_history.txt to /sadmin/cfg/alert_archive.txt file.
Archiving Alert: 2021.05.22 08:10 holmes Success of 'sa_rsync_ds410_to_ds409' on holmes. 
[ OK ] Alert archiving done.

Server Directories HouseKeeping.
[ OK ] find /sadmin/www -type d -exec chmod -R 775 {} \;
[ OK ] find /sadmin/www -exec chown -R apache:apache {} \;

Server Files HouseKeeping.
Make sure SADMIN crontab file have proper permission and owner
[ OK ] running chmod 0644 /etc/cron.d/sadm_server && chown root:root /etc/cron.d/sadm_server
[ OK ] running chmod 0644 /etc/cron.d/sadm_osupdate && chown root:root /etc/cron.d/sadm_osupdate
[ OK ] running chmod 0644 /etc/cron.d/sadm_backup && chown root:root /etc/cron.d/sadm_backup

Setting permissions in the website directories.
[ OK ] running find /sadmin/www/images -type f -exec chmod 664 {} \;
[ OK ] running find /sadmin/www -type f -name *.php -exec chmod 664 {} \;
[ OK ] running find /sadmin/www -type f -name *.css -exec chmod 664 {} \;
[ OK ] running find /sadmin/www -type f -name *.js -exec chmod 664 {} \; 
[ OK ] running find /sadmin/www -type f -name *.rrd -exec chmod 664 {} \; 
[ OK ] running find /sadmin/www -type f -name *.pdf -exec chmod 664 {} \;
[ OK ] running find /sadmin/www/dat -type f -exec chmod 664 {} \;

Delete any *.png files older than 5 days in /sadmin/www/tmp/perf.
[ OK ] running find /sadmin/www/tmp/perf -type f -mtime +5 -name '*.png' -exec rm -f {} \;

==================================================
Script exit code is 0 (Success) and execution time is 00:00:09
History (/sadmin/dat/rch/holmes_sadm_server_housekeeping.rch) trim to 35 lines.
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/sadmin/log/holmes_sadm_server_housekeeping.log) created ($SADM_LOG_APPEND='N').
End of sadm_server_housekeeping.sh - Sat May 29 11:02:43 EDT 2021
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

[sadm_client_housekeeping.sh]({% post_url 2021-05-29-sadm-client-housekeeping %}) - Purge old log,rch,nmon files and check $SADMIN permission   
[sadm_server_housekeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %}) - Enforce security SADMIN Web interface & crontab files
[sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %}) - Collect Hardware/Software/Performance data from actives servers   
[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %}) - Take data collected from clients and update database    
[sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %}) - Daily performance database update   
[sadm_subnet-lookup.py]({% post_url 2021-05-29-sadm-subnet-lookup %}) - Scan network selected subnet & store info in database  
[sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %}) - Backup one or all MySQL/MariaDB databases on the system  
[sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}) - SADMIN main configuration file   
[System Information File]({% post_url 2021-05-30-sysinfo-file %}) - Documentation about the system information file  

