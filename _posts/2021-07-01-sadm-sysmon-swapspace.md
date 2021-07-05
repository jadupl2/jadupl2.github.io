---
title:          Monitoring system swap space
desc:           How-to monitor system swap space with SysMon
version:        2.44
summary: |         
    On this page we will demonstrate how you can monitor the swap space utilization of a system.
    {: .text-justify}
updated:        2021-07-05
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


<a id="swapspace"></a>
### Monitoring the Swap Space

To monitor a system swap space with SysMon, you must insert a line in SysMon configuration file 
($SADMIN/cfg/`hostname-s`.smon) like the one below. The line MUST begin with the string "swap_space".  
In the example below, the current swap usage is at 3%, the "Warning" threshold is set to 85% and 
"Error" at 90%. If the percentage of utilization is greater or equal than one of these value then 
the ["Warning" alert group]({% post_url 2021-06-11-sadm-sysmon-config %}#sysmon_warning_group) 
"wargrp" or the ["Error" alert group]({% post_url 2021-06-11-sadm-sysmon-config %}#sysmon_error_group) 
"errgrp" will get alerted.
{: .text-justify}sysmon_warning_group

```bash
# ID COLUMN 1  2  3   4   5   6  7    8   9 A B C D E F G     H     I     J       K   L
swap_space     3  >  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 wargrp errgrp -
```

- Every time a "swap_space" line is process by the System Monitor, it used the "free | grep -i swap" 
command (on MacOS 'sysctl vm.swapusage') to get a snapshot of the swap space utilization. The 
resultant value is then compare with the "Warning" and "Error" threshold specified respectively 
in column 4 and 5.  
- If the usage percentage is greater or equal (test in column 3) than the "Warning" or "Error" 
threshold value, then the 
["Warning" alert group]({% post_url 2021-06-11-sadm-sysmon-config %}#sysmon_warning_group) (Column J) 
or ["Error" alert group]({% post_url 2021-06-11-sadm-sysmon-config %}#sysmon_error_group) (Column K) 
will get alerted depending on which value is exceeded.
{: .text-justify}


<br>
**Example of SysMon output**  

In the example below the Swap Space utilization percentage is at 1%, no need to trigger an alert.

```bash
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
File /opt/sadmin/cfg/borg.smon loaded in sysmon_array (252 lines loaded)

Checking for new filesystems ...
No new filesystem detected

Checking CPU Load Average ...
Uptime line:  09:08:03 up 21:47,  1 user,  load average: 0.60, 1.34, 1.63
Load Average is at 0 - W: 20 E: 35

Checking CPU Usage ...
CPU Usage line: 0 0 211712 275768 593136 1527376 0 0 0 300 6148 10373 3 11 85 0 0

CPU User:   3 - System:  11  - Total:  14
 - Warning Level: 85 - Error Level: 95

Checking Swap Space ...
Swap Info Line: Swap:      16777204      211712    16565492
Swap size: 16777204 - Usage: 211712 - Percentage use: 1 %
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
| [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   

