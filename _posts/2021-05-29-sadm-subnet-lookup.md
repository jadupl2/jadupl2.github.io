---
title:          sadm_subnet_lookup.py 
permalink:      /sadm-subnet-lookup/
desc:           Scan selected network subnet and store results in database
version:        3.4
updated:        2021-05-31
os:             Linux
type:           S  # [D]oc [S]=Server only [C]=Client [B]oth
tags:           [ server-scripts, network ] 
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
The purpose of this script is to scan the network subnet you specified and check the following things :   
- Did the IP respond to a ping request   
- Is there a hostname assigned to the IP   
- What is the Mac address of the IP   
- Did the Mac address or the hostname change since the last scan   

With this information on hand, you can view what IP are in use, what IP have a DNS entry and what IP
are free to use, useful no ?   

This is an example of the kind of results you can expect when clicking on "Network" in the heading
of the page.
![Subnet Scan Web Results](/assets/img/sadm_subnet_lookup/sadm_subnet_network_lookup_web.png){: .align-center}

You specify the network subnet you want to scan in the [SADMIN configuration file]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_network).
![Subnet to scan](/assets/img/sadm_subnet_lookup/sadm_subnet_lookup_to_scan.png){: .align-center}
In this example, we are scanning one subnet (192.168.1.0/24), but we can specify up to four subnets.  
 
[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
$ sudo sadm_subnet_lookup.py 
================================================================================
Starting sadm_subnet_lookup.py V3.4 - SADM Lib. V3.18
Server Name: holmes.maison.ca - Type: Linux
O/S: Centos  7.9.2009 - Code Name: Core
==================================================
 
Current host interface name     : em1
Possible IP on 192.168.1.0/24   : 256 
Network netmask                 : 255.255.255.0

Running fping and output to /sadmin/dat/net/fping.txt
The fping finished with success.

192.168.1.1      Ping worked, update ping date from 2021-05-31 13:31:30 to 2021-05-31 14:08:13
192.168.1.1      No MAC address changed ('84:16:f9:21:31:cc')
192.168.1.1      [ OK ] Database updated
192.168.1.2      Ping worked, update ping date from 2021-05-31 13:31:30 to 2021-05-31 14:08:13
192.168.1.2      No MAC address changed ('98:10:e8:f4:00:c5')
192.168.1.2      [ OK ] Database updated
192.168.1.3      Ping worked, update ping date from 2021-05-31 13:31:30 to 2021-05-31 14:08:13
192.168.1.3      No MAC address changed ('a0:99:9b:08:f5:11')
192.168.1.3      [ OK ] Database updated
...
...
192.168.1.253    Ping didn't worked, leave last ping date as it is.
192.168.1.253    No MAC address changed ('')
192.168.1.253    [ OK ] Database updated
192.168.1.254    Ping didn't worked, leave last ping date as it is.
192.168.1.254    No MAC address changed ('')
192.168.1.254    [ OK ] Database updated
 
==================================================
Script return code: 0
Script execution time is 00:00:25
Trim /sadmin/dat/rch/holmes_sadm_subnet_lookup.rch to 35 lines.
Alert requested if script fail.
Trim /sadmin/log/holmes_sadm_subnet_lookup.log to 500 lines.
Mon May 31 14:08:26 2021 - End of sadm_subnet_lookup.py
================================================================================
```

[Back to the top](#top_of_page)


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