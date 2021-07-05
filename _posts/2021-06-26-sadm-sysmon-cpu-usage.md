---
title:          Monitoring system cpu utilization
desc:           How-to monitor the cpu utilization with SysMon
version:        2.44
summary: |         
    On this page we will demonstrate how you can monitor the system cpu utilization with the System Monitor.
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
<a id="cpuusage"></a>
### Monitoring the CPU utilization

- You can be alerted if the usage percentage of your CPU reach a certain threshold for a certain number  
of minutes, specified in column 6. 
- Every time a "cpu_level" line is process by the System Monitor, it used the "vmstat" (iostat 
on MacOS) command to get a snapshot of the cpu utilization (user + system). The resultant value is
then compare with the warning and error threshold specified respectively in column 4 and 5. 
- If the value is under the warning and error level, then the event starting date ('YYYYMMDD') 
and time ('HHMM') (Column H' and 'I') is set to zeroes ('00000000 0000').
- If the value is over or equal, depending of the test you have put in column 3, then two things 
can happen.
  - If the event starting date and time *(Column H' and 'I') are all zeroes*, then this is the 
first time the cpu usage exceed the warning or error level. Then the System Monitor set the event 
starting date and time to the current date and time of the system and processing continue to
the next line. 
  - If the event starting date and time *(Column H' and 'I') are not all zeroes*, then this is not
the first time the cpu usage exceed the warning or error level. Then the System Monitor calculate 
the number of minutes since the event start date and time. 
    - If the number of minutes is less the number of minutes specify on column 6, then processing 
continue with the next line.
    - If the number of minutes is greater or equal (test in column 3) than the warning or error 
threshold value, then the warning (Column J) or error group (Column K) will get alerted depending 
on which value is exceeded and then the event starting date and time (Column H' and 'I') is set 
back to zeroes ('00000000 0000').
{: .text-justify}


```bash
# ID COLUMN 1  2  3    4   5  6   7    8   9 A B C D E F G     H     I     J      K    L
cpu_level      80 >=  85  95 120 0700 2100 Y Y Y Y Y Y Y Y 20210601 1445 wargrp errgrp -
```

In the example above, the current cpu usage is 80%, the warning threshold is set to 85% and error
at 95%. If the percentage of utilization is greater or equal than one of these value for more than 
"120" minutes (column 6), then the warning group "wargrp" or the "errgrp" will get alerted.
{: .text-justify}


<br>
**Example of SysMon output**
In this example, the CPU usage have reach 100%. Sysmon have calculated that it has been over the
error level (95%) for 36 seconds, so if it reach 1800 seconds (30 minutes) an alert will be 
automatically generated.
{: .text-justify}


```bash
# sudo sadm_sysmon.pl
Checking CPU Usage ...
CPU Usage line:   6  0 211712 311712 588488 1526080    0    0     1   134 6373 13407  5 95  1  0  0

CPU User:   5 - System:  95  - Total: 100
 - Warning Level: 85 - Error Level: 95
Actual Time is 2021 07 05 09 00 36
Actual epoch time is 1625490036
Load on cpu started at 2021 07 05 09 00 00 - 1625490000
So 1625490036 - 1625490000 = 36 seconds
You asked to wait 1800 seconds before report an error

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

