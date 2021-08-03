---
title:          Monitoring Multipath
permalink:      /sysmon-multipath/
desc:           How-to monitor Multipath with SysMon
version:        2.44
summary: |         
    On this page we will demonstrate how you can monitor the health of multipathed disk.
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


<a id="multipath"></a>
### Multipath test

- Again if the [minimum conditions](#sysmon_conditions) are met, then multipath state is evaluated. 
If not we proceed with the next line of Sysmon configuration file.
- Multipath line are only evaluated on Linux.
- Line will only be evaluated if the command 'multipathd' is present on system.
- SysMon check each path of the multipath 
  - If all multipath are active or ready then a "1" is returned (place in column 2).
  - If one one them is not "active" or "ready", a value of 0 is returned.

```bash
# ----- Check Linux Multipath Status (0=Error 1=All path(s) are Online/Ready)
# ID COLUMN 1    2  3   4   5  6    7    8  9 A B C D E F G     H      I     J      K    L
check_multipath  0 !=  00  01 000 0000 0000 Y Y Y Y Y Y Y Y 00000000 0000 warngrp errgrp -
```

In the example above, the multipath test returned a problem ("0" in column 2), since "0" is
not equal (!=) to "1" (Column 5) then an error is generated (Remember that when column 4 or 5 is 
"0" they are ignored). The alert will sent to the error group "errgrp" specify in column
"K". This error group got to be part of the [Alert Group File]({% post_url 2021-06-19-alert-group-cfg %}) 
($SADMIN/cfg/alert_group.cfg).
{: .text-justify}

Example on the command use to verify that multipath are all active/ready :

```bash
# echo 'show paths' | multipathd -k | grep -vi multipath
   0:0:0:0 sda 8:0   1   [active][ready] XX........ 4/20
   0:0:0:1 sdb 8:16  1   [active][ready] XX........ 4/20
   1:0:0:0 sdc 8:32  1   [active][ready] XXXX...... 8/20
   1:0:0:1 sdd 8:48  1   [active][ready] XXXX...... 8/20
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

