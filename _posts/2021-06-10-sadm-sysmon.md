---
title:          sadm_sysmon.pl
desc:           Perform selected monitoring test defined in SysMon configuration file
summary: |         
    The SADMIN System Monitor (SysMon) is executed at regular interval from the SADMIN client 
    crontab (/etc/cron.d/sadm_client). When the script begin it try to open is configuration file, 
    name "$SADMIN/cfg/${HOSTNAME}.smon", so for a host named "server1" it would try to open the file 
    "$SADMIN/cfg/server1.smon". If the file exist, it's loaded in memory and processing begin. 
    If the file doesn't exist, it copy the template named "$SADMIN/cfg/.template.smon" to 
    "$SADMIN/cfg/server1.smon" and execution begin. If the sysmon template file can't be found, 
    then script execution is aborted after the user is advise with an error message.
    {: .text-justify}
version:        2.43
updated:        2021-06-10
os:             Linux, Aix, MacOS
type:           C  # [D]oc [S]=Server only [C]=Client [B]oth
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


**File format**
- Blank lines and lines that begin with a "#" are ignored by the System Monitor.
- Each time the system monitor run, the last line of the configuration file is updated. We can see 
the System Monitor version number, the server name, the last boot date, the current date and finally 
the time it took to process all the requested tests.  
Before the System Monitor exit, it write what we call a report file, which contain any error or 
warning detected while processing each line. This SysMon report file is named "hostname.rpt" and 
is created in the "$SADMIN/dat/rpt" directory. This file will then get transferred to the SADMIN 
server by the [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %}) for analysis and 
trigger an alert if needed.

SysMon automatically detect new filesystem on the system and add them to the [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) and can check a filesystem usage and . By default,it will set 
the "Warning" usage level to 85% and the "Error" at 90%. If the file system usage is greater or 
equal to 85% and less than 90% it will shows up in the System Monitor web page as a "Warning". 
If the usage is equal or greater than 90%, it will appear an an "Error" is the System Monitor 
web page and an alert is generated. In the example below, I have change the warning threshold from 
85% to 80% in the fourth column to raise a warning.

```
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

  
Example of the last line :

```perl
#SYSMON 2.43 holmes - LastBoot 2021-05-28 07:16:27 - Sat Jun 12 10:47:03 2021 - Execution Time 1.00 seconds
```

<br>
**Summary of what step the System Monitor go through when it is started**

- First it check if the System Monitor lock file exist (${SADMIN}/sysmon.lock).
    - If it doesn't, it's created and we proceed with the next step.  
    - If it already exist, SysMon check when it was created. If it was more than 30 minutes ago it 
is recreated and execution continue. If it was created less than 30 minutes, a warning message is 
issued and the monitor execution is stop.  
- Next the [SADMIN configuration file]({% post_url 2021-04-26-sadmin-cfg %}) is read (get company 
name and email address of sysadmin).  
- The [System Monitor configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) is then loaded in memory.   
- The 'df' command is run and the result is loaded in memory to determine later on, if there are new filesystem.  
- An empty System Monitor Report File is created (${SADMIN}/dat/rpt/${HOSTNAME}.rpt).  
- The 'df' array is scan and every filesystem not already in the actual System Monitor configuration 
file are added to it.  
- Now each line of SysMon configuration are tested and updated in memory.  
  - If an error or a warning if found it's written to the Sysmon Report File (${HOSTNAME}.rpt).
- Last step is the unload the updated SysMon array into the new configuration file and the lock 
file is removed.   

<dl>
<dt><b>Activate O/S Update Schedule</b></dt>
<dd>If you don't want to schedule an operating system update, make sure the field "Activate O/S Update Schedule" 
is set to "No". This is the default when you create a new server is "No". </dd>
<dd>If you want to schedule an automatic operating system update set this field to "Yes".</dd>
</dl>


{: .text-justify}
 
[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

```bash
# sadm_sysmon.pl

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
Uptime line:  10:57:23 up 15 days,  3:40,  1 user,  load average: 0.18, 0.22, 0.38
Load Average is at 0 - W: 20 E: 35

Checking CPU Usage ...
CPU Usage line:   0  0 279432 3501528  15148 852272    0    0     0     0  629 1477  1  0 99  0  0

CPU User:   1 - System:   0  - Total:   1
 - Warning Level: 85 - Error Level: 95

Checking Swap Space ...
Swap Info Line: Swap:       7340024      279432     7060592
Swap size: 7340024 - Usage: 279432 - Percentage use: 3 %

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
[OK] Filesystem /boot at 56% ... Warning: 85 - Error: 90
[OK] Filesystem /wiki at 5% ... Warning: 85 - Error: 90
[OK] Filesystem /wsadmin at 82% ... Warning: 85 - Error: 90
[OK] Filesystem /backups at 63% ... Warning: 85 - Error: 90
[OK] Filesystem /psadmin at 4% ... Warning: 85 - Error: 90
[OK] Filesystem /storix at 12% ... Warning: 85 - Error: 90
[OK] Filesystem /opt at 71% ... Warning: 85 - Error: 90
[OK] Filesystem /tmp at 1% ... Warning: 85 - Error: 90
[OK] Filesystem /sysadmin at 9% ... Warning: 85 - Error: 90
[OK] Filesystem /linternux at 5% ... Warning: 85 - Error: 90
[OK] Filesystem /var at 31% ... Warning: 85 - Error: 90
[OK] Filesystem /sadmin at 38% ... Warning: 85 - Error: 90
[OK] Filesystem /home at 55% ... Warning: 85 - Error: 90
[OK] Filesystem /install at 6% ... Warning: 85 - Error: 90
[OK] Filesystem /gitrepos at 10% ... Warning: 85 - Error: 90
[OK] Filesystem /history at 1% ... Warning: 85 - Error: 90

-----
Updating SADM Sysmon configuration file (/sadmin/cfg/holmes.smon)
Deleting SYStem MONitor lock file /sadmin/sysmon.lock
#SYSMON 2.43 holmes - Last Boot: 2021-05-28 07:16:27 - Sat Jun 12 10:57:24 2021 - Execution Time 1.00 seconds
```


[Back to the top](#top_of_page)


{% include {{ site.section_options     }} %}
| **-i** | option -i | 

{% include {{ site.section_environment }} %}

{% include {{ site.section_exitcode    }} %}

{% include {{ site.section_author      }} %}

{% include {{ site.section_copyright   }} %}


<a id="seealso"></a>
## SEE ALSO

| Link to ...| Description |  
| :--- | :--- |  
| [sadm_sysmon_tui.pl]({% post_url 2021-05-18-sadm-sysmon-tui %})                   | Command line summary of alerts and failed scripts of all your servers.  
| [sadm_sysmon.pl]({% post_url 2021-06-10-sadm-sysmon %})                           | Client system monitor   
| [sadm_fetch_client.sh]({% post_url 2021-03-16-sadm-fetch-client %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   

