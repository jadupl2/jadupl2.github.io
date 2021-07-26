---
title:          Monitoring system load average
desc:           How-to monitor the load average with SysMon
version:        2.44
summary: |         
    On this page we will demonstrate how you can monitor the system load average with the System Monitor.
    We demonstrate with a practical example how to do it.
    {: .text-justify}
updated:        2021-07-04
os:             Linux, Aix, MacOS
type:           D  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ system_monitor ] 
tags:           [ system_monitor ] 
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

{% include sadm/sadm_page_info.md %}
{% if page.type == "S" %}
<font size="3"><strong>Can only be run on SADMIN Server.</strong></font>
{% endif %}
{% if page.type == "B" %}
<font size="3"><strong>Can be executed on a client and on the SADMIN Server.</strong></font>
{% endif %}
<br>
{{ page.summary }} 



<br>
<a id="loadaverage"></a>
### Load average

- The "load average" test line, must have the literal "load_average" starting in column one to be valid.
- The system load average of the past 5 minutes, returned by the 'uptime' command is used as the load average value (Linux,Aix,MacOS).  



```bash
# Aix/Linux/MacOS System Load Average Monitoring
# ID - COLUMN 1  2 3   4   5  6   7    8   9 A B C D E F G     H      I     J       K     L
load_average     1 >  20  35 120 0700 2100 Y Y Y Y Y Y Y Y 20210705 1445 default sysadmin -
```

### What we can say about the load average test line above
- The current load average on the system is '1' (column 2).     
- We want to test if the current load average is greater '>' (column 3) the warning (column 4) or error (column 5) threshold.     
- Column 6 tell SysMon the number of continuous minutes that the load average must exceed the "warning" or "Error" threshold before any alert is issued. In our example, the load average must be exceeded for at least 120 minutes, before any alert are issued.     
- We want SysMon to issue a "Warning" alert to the alert group name "default" (column J), if the load average is greater than "20" for more than "120" minutes (column 6).     
- We want SysMon to issue a "Error" alert to the alert group name "sysadmin" (column K), if the load average is greater than "35" for more than "120" minutes (column 6).   
- Within the example above, we can see that we began exceeding the "Warning" or "Error" on July the 5th 2021 (column H) at 14:45 (column I).   
- Sysmon calculate the difference between the actual date & time and the event date (column H) and time (column I), if it's greater than 120 minutes, an alert is issued the "Warning" group (Column J) or to the "Error" group (column K) depending on which value is exceeded.   
- As soon as the "load average" value get under the "Warning" level, the event date (column H) and time (column I) are set back to "000000 0000".   
- Also note that the line is evaluated only from 07:00 (column 7) to 21:00 (column 8) from Sunday to Saturday (column 9 to F).   



<br>
**Example of SysMon output**

```bash
$ sudo sadm_sysmon.pl

Creating lock file /opt/sadmin/sysmon.lock
Loading SADMIN configuration file /opt/sadmin/cfg/sadmin.cfg
------------------------------------------------------------------------------
SADMIN SYStem MONitor Tools - Version 2.44
------------------------------------------------------------------------------
O/S Name                 = linux
Debugging Level          = 5
SADM_BASE_DIR            = /opt/sadmin
Hostname                 = borg
Virtual Server           = N
CMD_SSH                  = /usr/bin/ssh
------------------------------------------------------------------------------

Loading SysMon configuration file /opt/sadmin/cfg/borg.smon
File /opt/sadmin/cfg/borg.smon loaded in sysmon_array (248 lines loaded)

Checking for new filesystems ...
  - New filesystem Found - /vm2
  - New filesystem Found - /vm
2 new filesystem(s) monitored

Checking CPU Load Average ...
Uptime line:  09:11:43 up 4 days, 16 min,  1 user,  load average: 1.79, 1.56, 1.59
Load Average is at 1 - W: 20 E: 35
...
...
```

[Back to the top](#top_of_page)





<a id="seealso"></a>
## See also

| Link to ...| Description |  
| :--- | :--- |  
| [sadm_sysmon_tui.pl]({% post_url 2021-05-18-sadm-sysmon-tui %})                   |  Command line summary of alerts and failed scripts of all your servers.  
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                           | Client system monitor   
| [sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   

