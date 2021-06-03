---
title:          sadm_daily_farm_fetch.sh
desc:           Collect Hardware/Software/Performance data from actives servers
version:        2.2
updated:        2021-05-28
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
This script is run automatically every morning by the [sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %}) script. The function of this script is to transfer the disaster 
recovery directory and the system performance monitor files (*.nmon) produced by each client to 
the SADMIN server.   
{: .text-justify}

- The disaster recovery directories will then become the input for the "[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %})" script, that is again run as part of the [sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %}).
{: .text-justify}
        rsync -ar --delete $HOSTNAME:/sadmin/dat/dr/ /sadmin/www/dat/$HOSTNAME/dr/ 

- The performance data files will be processed by the "[sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %})" that execution 
usually follow this script in the execution sequence in [sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %}).   
{: .text-justify}
        rsync -ar --delete $HOSTNAME:/sadmin/dat/nmon/ /sadmin/www/dat/$HOSTNAME/nmon/ 

 
[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
# sadm_daily_farm_fetch.sh 
================================================================================
Sat May 29 12:21:14 EDT 2021 - sadm_daily_farm_fetch.sh V4.5 - SADM Lib. V3.70
Server Name: holmes.maison.ca - Type: LINUX
CENTOS 7.9.2009 Kernel 3.10.0-1160.25.1.el7.x86_64
==================================================
 
Processing All Actives Server(s)

Processing (1) borg.maison.ca
SADMIN installed in /opt/sadmin on borg.
[ OK ] rsync -ar --delete borg:/opt/sadmin/dat/dr/ /sadmin/www/dat/borg/dr/ 
[ OK ] rsync -ar --delete borg:/opt/sadmin/dat/nmon/ /sadmin/www/dat/borg/nmon/ 

Processing (2) centos6.maison.ca
[ WARNING ]  Can't SSH to centos6.maison.ca (Sporadic System).

Processing (3) centos7.maison.ca
SADMIN installed in /sadmin on centos7.
[ OK ] rsync -ar --delete centos7:/sadmin/dat/dr/ /sadmin/www/dat/centos7/dr/ 
[ OK ] rsync -ar --delete centos7:/sadmin/dat/nmon/ /sadmin/www/dat/centos7/nmon/ 

Processing (4) centos8.maison.ca
SADMIN installed in /opt/sadmin on centos8.
[ OK ] rsync -ar --delete centos8:/opt/sadmin/dat/dr/ /sadmin/www/dat/centos8/dr/ 
[ OK ] rsync -ar --delete centos8:/opt/sadmin/dat
...
...
----------
FINAL number of Error(s) detected is 0 

==================================================
Script exit code is 0 (Success) and execution time is 00:00:57
History (/sadmin/dat/rch/holmes_sadm_daily_farm_fetch.rch) trim to 35 lines.
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/sadmin/log/holmes_sadm_daily_farm_fetch.log) created ($SADM_LOG_APPEND='N').
End of sadm_daily_farm_fetch.sh - Sat May 29 12:22:07 EDT 2021

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

[sadm_server-sunrise.sh]({% post_url 2021-05-26-sadm-server-sunrise %}) - Collect & process data produced by all actives clients  
[sadm_server_housekeeping.sh]({% post_url 2021-05-27-sadm-server-housekeeping %}) - Enforce security SADMIN Web interface & crontab files
[sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %}) - Collect Hardware/Software/Performance data from actives servers   
[sadm_database_update.py]({% post_url 2021-05-29-sadm-database-update %}) - Take data collected from clients and update database    
[sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %}) - Daily performance database update   
[sadm_subnet-lookup.py]({% post_url 2021-05-29-sadm-subnet-lookup %}) - Scan network selected subnet & store info in database  
[sadm_backupdb.sh]({% post_url 2021-05-26-sadm-backupdb %}) - Backup one or all MySQL/MariaDB databases on the system
[sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %}) - SADMIN main configuration file   


