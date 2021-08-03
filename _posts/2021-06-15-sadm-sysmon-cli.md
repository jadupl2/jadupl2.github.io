---
title:          smon (sadm_sysmon_cli.sh)
permalink:      /sadm-sysmon-cli/
desc:           Allow you run SysMon and see the report file
version:        2.3
summary: |         
    This command line tool (smon), will run the System Monitor on then current system and show the 
    content of the SysMon report file. It will also show any script error or warning your have on 
    the current system. So by running this command, you have a pretty good status of any pending
    status on the current system. 
    {: .text-justify}
updated:        2021-06-15
os:             Linux, Aix, MacOS
type:           B  # [D]oc [S]=Server only [C]=Client [B]oth
categories:     [ command_line ] 
tags:           [ command_line ] 
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
~ # smon
Creating lock file /sadmin/sysmon.lock
Loading SADMIN configuration file /sadmin/cfg/sadmin.cfg
------------------------------------------------------------------------------
SADMIN SYStem MONitor Tools - Version 2.43
------------------------------------------------------------------------------
O/S Name                 = linux
Debugging Level          = 5
SADM_BASE_DIR            = /sadmin
Hostname                 = holmes
Virtual Server           = N
CMD_SSH                  = /bin/ssh
------------------------------------------------------------------------------

Loading SysMon configuration file /sadmin/cfg/holmes.smon
File /sadmin/cfg/holmes.smon loaded in sysmon_array (274 lines loaded)

Checking for new filesystems ...
No new filesystem detected

Checking CPU Load Average ...
Uptime line:  10:09:42 up 22 days,  2:53,  2 users,  load average: 0.14, 0.16, 0.17
Load Average is at 0 - W: 20 E: 35

Checking CPU Usage ...
CPU Usage line:   0  0 325888 2774076  15272 2664484    0    0     0     4  424  781  0  0 100  0  0

CPU User:   0 - System:   0  - Total:   0
 - Warning Level: 85 - Error Level: 95

Checking Swap Space ...
Swap Info Line: Swap:       7340024      325888     7014136
Swap size: 7340024 - Usage: 325888 - Percentage use: 4 %

Checking service crond,cron
  - service crond status ... [RUNNING]
[OK] Service is running - Total returned (1)

Checking service chronyd
  - service chronyd status ... [RUNNING]
[OK] Service is running - Total returned (1)

Checking service ssh,sshd
  - service sshd status ... [RUNNING]
[OK] Service is running - Total returned (1)

Checking service postfix
  - service postfix status ... [RUNNING]
[OK] Service is running - Total returned (1)

Checking service at,atd
  - service atd status ... [RUNNING]
[OK] Service is running - Total returned (1)

Checking Multipath ...Status of Multipath skipped - Command multipathd not present on system
Multipath status is not in use - Code = (1) (1=ok 0=Error)
[OK] Filesystem / at 39% ... Warning: 85 - Error: 90
[OK] Filesystem /usr at 72% ... Warning: 85 - Error: 90
[OK] Filesystem /boot at 53% ... Warning: 85 - Error: 90
[OK] Filesystem /wiki at 5% ... Warning: 85 - Error: 90
[WARNING] Filesystem /wsadmin at 82% ... Warning: 80 - Error: 90
Automatic filesystem increase script 'sadm_fs_incr.sh' not specified in /sadmin/cfg/holmes.smon.
Therefore filesystem increase will not be performed.
[OK] Filesystem /backups at 64% ... Warning: 85 - Error: 90
[OK] Filesystem /psadmin at 4% ... Warning: 85 - Error: 90
[OK] Filesystem /storix at 12% ... Warning: 85 - Error: 90
[OK] Filesystem /opt at 71% ... Warning: 85 - Error: 90
[OK] Filesystem /tmp at 1% ... Warning: 85 - Error: 90
[OK] Filesystem /sysadmin at 9% ... Warning: 85 - Error: 90
[OK] Filesystem /linternux at 4% ... Warning: 85 - Error: 90
[OK] Filesystem /var at 27% ... Warning: 85 - Error: 90
[OK] Filesystem /sadmin at 39% ... Warning: 85 - Error: 90
[OK] Filesystem /home at 55% ... Warning: 85 - Error: 90
[OK] Filesystem /install at 6% ... Warning: 85 - Error: 90
[OK] Filesystem /gitrepos at 10% ... Warning: 85 - Error: 90
[OK] Filesystem /history at 1% ... Warning: 85 - Error: 90

-----
Updating SADM Sysmon configuration file (/sadmin/cfg/holmes.smon)
Deleting SYStem MONitor lock file /sadmin/sysmon.lock
#SYSMON 2.43 holmes - Last Boot: 2021-05-28 07:16:27 - Sat Jun 19 10:09:43 2021 - Execution Time 1.00 seconds
```

![SysMon Command line output](/assets/img/sadm_sysmon_cli/sadm_sysmon_cli_output_2.png){: .align-center} 


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
| [sview]({% post_url 2021-05-18-sadm-sysmon-tui %})                        | View summary of alerts & failed scripts of all your servers|  
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                        | SADMIN main configuration file|   
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                   | Client system monitor|   
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) | Client System Monitor configuration file|   
| [sdf]({% post_url 2021-06-13-sadm-df %})                                  | sadmin version of the 'df' command |  
| [sadm]({% post_url 2021-06-14-sadm-ui %})                                 | System Administration Tools Menu |  
| [smon]({% post_url 2021-06-15-sadm-sysmon-cli %})                         | Allow you run SysMon and see the report file |  

