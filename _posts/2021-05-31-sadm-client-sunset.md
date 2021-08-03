---
title:          sadm_client_sunset.sh
permalink:      /sadm-client-sunset/
desc:           Clients end of day housekeeping and producing system information files
version:        2.10
updated:        2021-06-03
os:             Linux, Aix, MacOS
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
The main function of this script is to execute various housekeeping on a SADMIN client. Remember,
the SADMIN server is also consider a client. This script is run daily near the end of the day, 
by default it run around 23:23. All it's doing actually, is execute the four scripts listed below ;   
{: .text-justify}

1- **[sadm_client_housekeeping.sh]({% post_url 2021-05-29-sadm-client-housekeeping %})**   
The function of this script is to perform various housekeeping, such as 
[deleting old logs]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_log_keepdays) and 
[history files]({% post_url 2021-04-26-sadmin-cfg %}/#sadm_rch_keepdays) not used for a number 
of days specified in the [SADMIN configuration file]({% post_url 2021-04-26-sadmin-cfg %}).  

2- **[sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %})**   
Save system filesystems information in order to recreate them from scratch in a LVM environment. 

3- **[sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %})**   
This script is use to collect different software and hardware about the system you are running 
it and record this information in the [System Information File]({% post_url 2021-05-30-sysinfo-file %}). 

4- **[sadm_cfg2html.sh]({% post_url 2021-06-01-sadm-cfg2html %})** 
This script use [cfg2html](https://www.cfg2html.com/) is a little utility to collect the necessary 
system configuration files and system set-up to an ASCII file and HTML file.


**Portion of the SADMIN client crontab**
```bash
# SADMIN Client Crontab File 
# Please don't edit manually, SADMIN Tools generated file
SADMIN=/sadmin
# 
# Run Daily before midnight
# Housekeeping, Save Filesystem Info, Create SysInfo & run cfg2html
23 23 * * *  sadmin sudo ${SADMIN}/bin/sadm_client_sunset.sh > /dev/null 2>&1
```

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
# sadm_client_sunset.sh 
================================================================================
Thu 03 Jun 2021 12:20:07 PM EDT - sadm_client_sunset.sh V2.10 - SADM Lib. V3.70
Server Name: ubuntu2004.maison.ca - Type: LINUX
UBUNTU 20.04 Kernel 5.8.0-53-generic
==================================================
 
[ OK ] /opt/sadmin/bin/sadm_client_housekeeping.sh 
[ OK ] /opt/sadmin/bin/sadm_dr_savefs.sh 
[ OK ] /opt/sadmin/bin/sadm_create_sysinfo.sh 
[ OK ] /opt/sadmin/bin/sadm_cfg2html.sh 

==================================================
Script exit code is 0 (Success) and execution time is 00:01:29
History (/opt/sadmin/dat/rch/ubuntu2004_sadm_client_sunset.rch) trim to 35 lines.
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
New log (/opt/sadmin/log/ubuntu2004_sadm_client_sunset.log) created ($SADM_LOG_APPEND='N').
End of sadm_client_sunset.sh - Thu 03 Jun 2021 12:21:29 PM EDT
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

[sadm_client_sunset.sh]({% post_url 2021-05-31-sadm-client-sunset %}) - Clients end of day housekeeping and producing system information files  
[sadm_client_housekeeping.sh]({% post_url 2021-05-29-sadm-client-housekeeping %}) - Purge old log,rch,nmon files and check $SADMIN permission   
[sadm_create_sysinfo.sh]({% post_url 2021-04-22-sadm-create-sysinfo %}) - Collect hardware & software information about the system   
[System Information File]({% post_url 2021-05-30-sysinfo-file %}) - Documentation about the system information file  
[sadm_dr_savefs.sh]({% post_url 2021-06-02-sadm-dr-savefs %}) - Save system filesystems information in order to recreate them from scratch.  
[sadm_cfg2html.sh]({% post_url 2021-06-01-sadm-cfg2html %}) - Get System information and creates a HTML web page of it.  
