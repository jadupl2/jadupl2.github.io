---
title:          sadm_sysmon.pl
desc:           Perform selected monitoring test defined in SysMon configuration file
summary: |         
    The SADMIN System Monitor (SysMon) is executed at regular interval from the SADMIN client 
    crontab (/etc/cron.d/sadm_client). It monitor everything specified in the configuration
    file and generate a new SysMon report file ($SADMIN/data/rpt/hostname.rpt).
    {: .text-justify}
version:        2.43
updated:        2021-06-25
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
# {{ page.title }} 
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

<br>
**Summary of what step the System Monitor go through when it is started**

- First it check if the System Monitor lock file exist ($SADMIN/sysmon.lock).
    - If it doesn't, it's created and we proceed with the next step.  
    - If it already exist, SysMon check when it was created. If it was more than 30 minutes ago it 
is recreated and execution continue. If it was created less than 30 minutes, a warning message is 
issued and the monitor execution is stop. 
- Next the [SADMIN configuration file]({% post_url 2021-04-26-sadmin-cfg %}) is read (get company 
name and email address of sysadmin).  
- Then it try to open the configuration file ("$SADMIN/cfg/${HOSTNAME}.smon").
  - If the file exist, then the [System Monitor configuration file]({% post_url 2021-06-11-sadm-sysmon-config %}) is loaded in memory and processing begin. 
  - If the file doesn't exist, it copy the 
template named "$SADMIN/cfg/.template.smon" to "$SADMIN/cfg/${HOSTNAME}.smon" and processing begin. 
  - If the sysmon template file can't be found, then execution is aborted after the user is 
advise with an error message. 
- The 'df' command is run and the result is store in memory. Any filesystem that is not in SysMon 
configuration is added with 'Warning' threshold set to 85% and 'Error' at 90%.
- An empty System Monitor report file is created (${SADMIN}/dat/rpt/${HOSTNAME}.rpt).  
- Now each line of SysMon configuration are tested and update the SysMon array in memory.  
  - Error or Warning found are written to the [System Monitor report file]({% post_url 2021-06-20-sysmon-report-file %}).
- Last step is to unload the updated SysMon array into the SysMon configuration file and to remove 
the lock file ($SADMIN/sysmon.lock).
  
Before the System Monitor exit, it write what we call a report file, which contain any error or 
warning detected while processing each line. This [System Monitor report file]({% post_url 2021-06-20-sysmon-report-file %}) is named "hostname.rpt" and it
is created in the "$SADMIN/dat/rpt" directory. This file will then get transferred to the SADMIN 
server by the [sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %}) for analysis and 
trigger an alert if needed.
{: .text-justify}

Each test performed by Sysmon represent a line in the configuration file, for more information see
the [SysMon configuration file page]({% post_url 2021-06-11-sadm-sysmon-config %}).

<br>
**Here is a list of all the type of test that Sysmon can perform:**

- Verify the **[system multipath state]({% post_url 2021-06-11-sadm-sysmon-config %}#multipath)**
- Check the system **[load average]({% post_url 2021-06-11-sadm-sysmon-config %}#loadaverage)** and 
  notify you, if warning or error threshold is sustained of certain period of time. 
- Monitor **[CPU usage]({% post_url 2021-06-11-sadm-sysmon-config %}#cpuusage)** and notify you if warning or error threshold is sustained of certain period of time.
- Verify **[Swap space utilization]({% post_url 2021-06-11-sadm-sysmon-config %}#swapspace)** and alert if warning or error threshold is exceeded.
- Monitor **[filesystem usage]({% post_url 2021-06-11-sadm-sysmon-config %}#filesystem)** and alert if warning or error threshold is reached.
- Can **[ping an IP or a hostname]({% post_url 2021-06-11-sadm-sysmon-config %}#pingtest)** and issue 
an alert if doesn't respond after 3 attempts.
- Verify that a particular **[service]({% post_url 2021-06-11-sadm-sysmon-config %}#service)** is running and advise you if it isn't, it can even restart it if you want.
- Can check if a **[deamon]({% post_url 2021-06-11-sadm-sysmon-config %}#daemon)** of your choice is running
- Can check if we have an **[http response]({% post_url 2021-06-11-sadm-sysmon-config %}#http)** of a particular web site.
- Can run **[your own script]({% post_url 2021-06-11-sadm-sysmon-config %}#script)** and advise you if it terminate with a non zero exit code.
 
[Back to the top](#top_of_page)



<a id="examples"></a>
## EXAMPLE

- You can manually run the System Monitor by entering the command "sadm_sysmon.pl". You can also run 
it by entering the command "[smon](/assets/img/sadm_sysmon_cli/sadm_sysmon_cli_output_2.png)" that will run the system monitor and show you the content of the 
sysmon report file and finally a list of the script(s) that terminated with error on current system. 
- Remember that you can always view the current of all your systems scripts and problems 
(Error/Warning) at the [system monitor web page](/assets/img/sadm_sysmon/sadm_view_sysmon.png) or 
on the command line by using the "[sview](assets/img/sadm_sysmon/sadm_sysmon_tui.png)" command.


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
| [sadm_fetch_clients.sh]({% post_url 2021-03-16-sadm-fetch-clients %})               | rsync all .rch/.log/.rpt from actives clients to the SADMIN server  
| [SysMon configuration file]({% post_url 2021-06-11-sadm-sysmon-config %})         | Client System Monitor configuration file   
| [sadmin.cfg]({% post_url 2021-04-26-sadmin-cfg %})                                | SADMIN main configuration file   
| [System Monitor report file]({% post_url 2021-06-20-sysmon-report-file %})        | Output file generated by System Monitor |   

