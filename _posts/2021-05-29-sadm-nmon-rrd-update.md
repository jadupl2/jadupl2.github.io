---
title:          sadm_nmon_rrd_update.sh
permalink:      /sadm-nmon-rrd-update/
desc:           Daily update of the performance database (.rrd)
version:        2.2
updated:        2021-05-30
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
First this script, produce a list of all 'nmon' ([Linux nmon](http://nmon.sourceforge.net/pmwiki.php),
[Aix nmon](https://www.ibm.com/support/knowledgecenter/en/ssw_aix_72/com.ibm.aix.cmds4/nmon.htm)) files 
collected by the [sadm_daily_farm_fetch.sh]({% post_url 2021-05-28-sadm-daily-farm-fetch %}) script
and that were produced yesterday.  
Next it read each of these files and update the associated server rrd ([[R]ound [R]obin [D]atabase](https://oss.oetiker.ch/rrdtool/)) database.
The updated performance database files (hostname.rrd) file are located in ${SADMIN}/www/rrd/${hostname} 
directory. To update all the servers performance database can take some time depending on your CPU
and the number of clients you have. The performance graph (click on the "Performance" in the SADMIN
site heading) you see on the web interface come from these databases (.rrd).   


**Example of the rrd directory for system 'raspi5'**  


    $ ls -l $SADMIN/www/rrd/raspi5
    total 49292
    -rw-rw-r-- 1 apache apache       11 Nov 30 05:46 netdev.txt
    -rw-rw-r-- 1 apache apache 50467232 Nov 30 05:46 raspi5.rrd
    
    $ cat $SADMIN/www/rrd/raspi5/netdev.txt
    eth0
    wlan0
    $ 
    

The 'netdev.txt' file, contain the network interface name on the system.
They are used in the network interface performance graph.

{: .text-justify}
 

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
2018.11.30 05:06:18 ================================================================================
2018.11.30 05:06:18 Starting sadm_nmon_rrd_update.sh V2.3 - SADM Lib. V2.52
2018.11.30 05:06:18 Server Name: holmes.maison.ca - Type: LINUX
2018.11.30 05:06:19 CENTOS 7.5.1804 Kernel 3.10.0-862.14.4.el7.x86_64
2018.11.30 05:06:19 ==================================================
2018.11.30 05:06:19  
2018.11.30 05:06:19 List of nmon files we are about to process :
2018.11.30 05:06:19 find /sadmin/www/dat -type f -name "*_181129_*.nmon"
2018.11.30 05:06:19  1)  There is 718 snapshots in /sadmin/www/dat/centos6/nmon/centos6_181129_0002.nmon
2018.11.30 05:06:19  2)  There is 718 snapshots in /sadmin/www/dat/centos7/nmon/centos7_181129_0002.nmon
...
2018.11.30 05:06:19  22)  There is 2 snapshots in /sadmin/www/dat/yoda/nmon/yoda_181129_1006.nmon
2018.11.30 05:06:19  23)  There is 413 snapshots in /sadmin/www/dat/yoda/nmon/yoda_181129_1012.nmon
2018.11.30 05:06:19  
2018.11.30 05:06:19 ----------
2018.11.30 05:06:19 [1] Processing /sadmin/www/dat/centos6/nmon/centos6_181129_0002.nmon
2018.11.30 05:06:19 Processing centos6 '^ZZZZ' Time Lines (718 elements).
2018.11.30 05:06:36 Processing centos6 '^CPU_ALL' Lines (718 elements).
2018.11.30 05:06:42 Processing centos6 '^PROC,T' Lines (718 elements).
2018.11.30 05:06:44 Processing centos6 '^DISKREAD' Lines (718 elements).
2018.11.30 05:07:17 Processing centos6 '^DISKWRITE' Lines (718 elements).
2018.11.30 05:07:50 Processing LINUX - centos6 '^MEM,T' Lines (718 elements).
2018.11.30 05:07:57 Processing LINUX Paging Activity '^VM,T'  Lines (718 elements)
2018.11.30 05:08:01 Processing Network of centos6 (LINUX) '^NET,' Lines (718 elements).
2018.11.30 05:08:01 System centos6 have 1 network interface(s)
2018.11.30 05:08:01 Chosen Network Devices (Up to 4)
2018.11.30 05:08:01   1) eth0
2018.11.30 05:08:04 Updating RRD Database /sadmin/www/rrd/centos6/centos6.rrd
2018.11.30 05:08:39 [SUCCESS] Updating centos6 RRD Database (718)
2018.11.30 05:08:39  
...
2018.11.30 05:53:04 ----------
2018.11.30 05:53:04 [23] Processing /sadmin/www/dat/yoda/nmon/yoda_181129_1012.nmon
2018.11.30 05:53:04 Processing yoda '^ZZZZ' Time Lines (413 elements).
2018.11.30 05:53:15 Processing yoda '^CPU_ALL' Lines (413 elements).
2018.11.30 05:53:19 Processing yoda '^PROC,T' Lines (413 elements).
2018.11.30 05:53:21 Processing yoda '^DISKREAD' Lines (413 elements).
2018.11.30 05:53:36 Processing yoda '^DISKWRITE' Lines (413 elements).
2018.11.30 05:53:51 Processing LINUX - yoda '^MEM,T' Lines (413 elements).
2018.11.30 05:53:56 Processing LINUX Paging Activity '^VM,T'  Lines (413 elements)
2018.11.30 05:53:58 Processing Network of yoda (LINUX) '^NET,' Lines (413 elements).
2018.11.30 05:53:58 System yoda have 2 network interface(s)
2018.11.30 05:53:58 Chosen Network Devices (Up to 4)
2018.11.30 05:53:58   1) eth0
2018.11.30 05:53:58   2) wlx000f6002a8f0
2018.11.30 05:54:01 Updating RRD Database /sadmin/www/rrd/yoda/yoda.rrd
2018.11.30 05:54:21 [SUCCESS] Updating yoda RRD Database (413)
2018.11.30 05:54:21  
2018.11.30 05:54:21 ==================================================
2018.11.30 05:54:21 Script return code is 0
2018.11.30 05:54:21 Script execution time is 00:48:02
2018.11.30 05:54:21 Trim History /sadmin/dat/rch/holmes_sadm_nmon_rrd_update.rch to 125 lines
2018.11.30 05:54:21 Requested alert only if script fail (Won't send alert)
2018.11.30 05:54:21 Trim log /sadmin/log/holmes_sadm_nmon_rrd_update.log to 2000 lines
2018.11.30 05:54:21 Fri Nov 30 05:54:21 EST 2018 - End of sadm_nmon_rrd_update.sh
2018.11.30 05:54:21 ================================================================================
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