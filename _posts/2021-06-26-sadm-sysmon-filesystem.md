---
title:          Filesystem monitoring 
permalink:      /sysmon-filesystem/
desc:           How-to monitor filesystem usage with SysMon
version:        2.44
summary: |         
    On this page we will demonstrate how you can monitor filesystem utilization on a system.
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



<a id="filesystem"></a>
### Filesystem monitoring (Line beginning with 'FS')

SysMon automatically detect new filesystem on the system and add them to the [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) and can check a filesystem usage and . By default,it will set 
the "Warning" usage level to 85% and the "Error" at 90%. If the file system usage is greater or 
equal to 85% and less than 90% it will shows up in the System Monitor web page as a "Warning". 
If the usage is equal or greater than 90%, it will appear an an "Error" is the System Monitor 
web page and an alert is generated. In the example below, I have change the warning threshold from 
85% to 80% in the fourth column to raise a warning.

Every time Sysmon is run the system [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) is loaded in memory,
updated in memory during execution and then unloaded to disk when terminated.
So SysMon is able to know when a new filesystem is created on the system and it is
added automatically to his configuration file. 
The warning threshold is set to 80% and the error to 90%.
These are initial value, you can change them and they will remain to your setting.

```
# COLUMN 1    2  3   4   5   6  7    8   9 A B C D E F G     H     I      J        K   L
FS/wsadmin   82 >=  80  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
```
If a line in the [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) begin
with "FS", this indicate that this line is used to test the filesystem usage. In the example above
we are evaluating the "/wsadmin" filesystem usage. It is currently using 82% and we've set the
warning level at 80% and the error level at 90%. Since we are above the warning level (and below the
error level), this have trigger an warning alert. 

![Sysmon Warning on Web](/assets/img/sadm_sysmon/sadm_sysmon_filesystem_warning.png){: .align-center} 

The warning will always appear on the system monitor web page, like the example below. 

![Sysmon Warning on Web](/assets/img/sadm_sysmon/sadm_sysmon_warning_email.png){: .align-center} 

```bash
# ----- Filesystem Monitoring
# Can increase it by 10%, two times within 24hours maximum, if script 
# "sadm_fs_incr.sh" in Column L.
# FS/usr 23 >= 25 90 001 0000 0000 Y Y Y Y Y Y Y Y 20180615 0824 wargrp errgrp sadm_fs_incr.sh
#----------------------------------------------------------------------------------------
# ID COLUMN 1  2  3   4   5  6   7    8   9 A B C D E F G     H     I     J       K     L
#----------------------------------------------------------------------------------------
#
#SADMSTAT 2.5 holmes - Sat Feb  4 09:56:10 2017 - Execution Time 5.00 seconds
FS/           39 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/usr        72 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/boot       53 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/wiki        5 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/wsadmin    82 >=  80  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/backups    64 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/psadmin     4 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/storix     12 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/opt        71 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/tmp         1 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/sysadmin    9 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/linternux   4 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/var        27 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/sadmin     38 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/home       55 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/install     6 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/gitrepos   10 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
FS/history     1 >=  85  90 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 default default -
#SYSMON 2.43 holmes - Last Boot: 2021-05-28 07:16:27 - Mon Jun 14 11:07:04 2021 - Execution Time 2.00 seconds
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

