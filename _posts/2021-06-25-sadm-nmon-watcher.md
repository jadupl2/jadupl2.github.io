---
title:          sadm_nmon_watcher.sh
desc:           Check if performance collector (nmon) is running, if it is not start it.
version:        2.7
summary: |         
    This script is automatically run from the client crontab every 45 minute. It check if the 
    performance collector 'nmon' is running, it it isn't it will start it.
    {: .text-justify}
updated:        2021-06-30
os:             Linux, Aix
type:           C  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ test ] 
#categories:     [ how-to, web_interface, backup, configuration-files, system_monitor, server-scripts, client-scripts, command_line,  utilities, libraries, templates, test ] 
tags:           [ test ] 
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

{{ page.summary }} 

{: .text-justify}
 

[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
# sadm_nmon_watcher.sh 
================================================================================
Tue 29 Jun 2021 10:35:10 AM EDT - sadm_nmon_watcher.sh V2.7 - SADM Lib. V3.70
Server Name: ubuntu2104.maison.ca - Type: LINUX
UBUNTU 21.04 Kernel 5.11.0-22-generic
==================================================
 
[OK] Yes, 'nmon' is available (/usr/bin/nmon)
 
There is 1 nmon process actually running
     1	root     4005672       1  0 00:00 ?        00:00:04 /usr/bin/nmon -f -s120 -c719 -t -m /opt/sadmin/dat/nmon
 
Nmon already Running ... Nothing to Do.
 
Last nmon files created
-rw-rw-r-- 1 sadmin sadmin 649832 Jun 28 23:56 ubuntu2104_210628_0000.nmon
-rw-r--r-- 1 root   root   318130 Jun 29 10:34 ubuntu2104_210629_0000.nmon
 

==================================================
Script exit code is 0 (Success) and execution time is 00:00:10
History (/opt/sadmin/dat/rch/ubuntu2104_sadm_nmon_watcher.rch) trim to 35 lines ($SADM_MAX_RCLINE=35).
Script will send an alert only when it terminate with error ($SADM_ALERT_TYPE=1).
Script succeeded, no alert will be send to 'default' alert group.
Log /opt/sadmin/log/ubuntu2104_sadm_nmon_watcher.log trim to 500 lines ($SADM_MAX_LOGLINE=500).
End of sadm_nmon_watcher.sh - Tue 29 Jun 2021 10:35:11 AM EDT
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

| Link to ...| Description |  
| :--- | :--- |  
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   
| [sadm_nmon_rrd_update.sh]({% post_url 2021-05-29-sadm-nmon-rrd-update %})         | Daily performance database update   
| [sadm_server crontab]({% post_url 2021-06-25-etc-crond-sadm-server %})            | It execute everything that keep SADMIN running smoothly |   
| [sadm_client crontab]({% post_url 2021-06-25-etc-crond-sadm-client %})            | Collect perf. & system information, run system monitor and housekeeping |   
| [sadm_nmon_watcher.sh]({% post_url 2021-06-25-sadm-nmon-watcher %})               | If performance collector (nmon) is not running, start it. |    